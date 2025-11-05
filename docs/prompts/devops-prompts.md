# DevOps Prompts

A collection of prompt templates for CI/CD, deployment, infrastructure, and DevOps automation tasks.

---

## CI/CD

### 1. Generate CI/CD Pipeline

**Purpose:** Create CI/CD pipeline configuration.

**Prompt:**
```
Create a CI/CD pipeline for [PROJECT]:

Project details:
- Type: [WEB_APP/API/LIBRARY/MOBILE]
- Tech stack: [LANGUAGES/FRAMEWORKS]
- Repository: [GITHUB/GITLAB/BITBUCKET]
- CI/CD platform: [GITHUB_ACTIONS/JENKINS/GITLAB_CI/CIRCLE_CI]

Pipeline stages:
- Build: [BUILD_STEPS]
- Test: [TEST_TYPES]
- Security: [SECURITY_SCANS]
- Deploy: [ENVIRONMENTS]
- Notifications: [SLACK/EMAIL/ETC]

Requirements:
- Trigger on: [PUSH/PR/TAG/SCHEDULE]
- Environment variables: [SECRETS_NEEDED]
- Caching: [DEPENDENCIES/BUILD_ARTIFACTS]
- Parallel jobs: [WHICH_STAGES]
- Deployment strategy: [BLUE_GREEN/ROLLING/CANARY]

Provide complete pipeline configuration file with comments.
```

**Example:**
```
Create GitHub Actions pipeline for Node.js REST API:

Project:
- Type: REST API microservice
- Stack: Node.js 18, TypeScript, Express, PostgreSQL
- Repository: GitHub
- Platform: GitHub Actions

Stages:
- Build: Install deps, compile TypeScript, build Docker image
- Test: Unit tests (Jest), integration tests, E2E tests
- Security: Dependency audit, SAST (CodeQL), container scan
- Deploy: Staging on PR, Production on main merge
- Notifications: Slack on failure, success

Requirements:
- Trigger: Push to main, Pull requests, manual workflow
- Secrets: DB credentials, AWS keys, Docker Hub token
- Caching: npm modules, Docker layers
- Parallel: Test jobs run in parallel
- Strategy: Rolling deployment with health checks

Pipeline (.github/workflows/ci-cd.yml):

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]
  workflow_dispatch:  # Manual trigger

env:
  NODE_VERSION: '18'
  DOCKER_IMAGE: 'mycompany/api'

jobs:
  # Job 1: Build and test
  build-and-test:
    runs-on: ubuntu-latest

    services:
      # PostgreSQL for integration tests
      postgres:
        image: postgres:14
        env:
          POSTGRES_USER: test
          POSTGRES_PASSWORD: test
          POSTGRES_DB: testdb
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          cache: 'npm'  # Cache npm modules

      - name: Install dependencies
        run: npm ci  # Clean install (faster, deterministic)

      - name: Lint code
        run: npm run lint

      - name: Type check
        run: npm run type-check

      - name: Build TypeScript
        run: npm run build

      - name: Run unit tests
        run: npm run test:unit -- --coverage

      - name: Run integration tests
        env:
          DATABASE_URL: postgresql://test:test@localhost:5432/testdb
        run: npm run test:integration

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info
          flags: unittests

      - name: Upload build artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-output
          path: dist/

  # Job 2: Security scanning (runs in parallel with build)
  security-scan:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run npm audit
        run: npm audit --audit-level=moderate
        continue-on-error: true  # Don't fail build, but report

      - name: Initialize CodeQL
        uses: github/codeql-action/init@v2
        with:
          languages: javascript

      - name: Perform CodeQL Analysis
        uses: github/codeql-action/analyze@v2

      - name: Run Snyk vulnerability scan
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
        with:
          args: --severity-threshold=high

  # Job 3: Build Docker image
  build-docker:
    runs-on: ubuntu-latest
    needs: [build-and-test, security-scan]  # Wait for tests to pass

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Download build artifacts
        uses: actions/download-artifact@v3
        with:
          name: build-output
          path: dist/

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2

      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Extract metadata
        id: meta
        uses: docker/metadata-action@v4
        with:
          images: ${{ env.DOCKER_IMAGE }}
          tags: |
            type=ref,event=branch
            type=ref,event=pr
            type=sha,prefix={{branch}}-
            type=semver,pattern={{version}}

      - name: Build and push Docker image
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          cache-from: type=registry,ref=${{ env.DOCKER_IMAGE }}:buildcache
          cache-to: type=registry,ref=${{ env.DOCKER_IMAGE }}:buildcache,mode=max

      - name: Scan Docker image with Trivy
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: ${{ env.DOCKER_IMAGE }}:${{ github.sha }}
          format: 'sarif'
          output: 'trivy-results.sarif'

      - name: Upload Trivy results to GitHub Security
        uses: github/codeql-action/upload-sarif@v2
        with:
          sarif_file: 'trivy-results.sarif'

  # Job 4: Deploy to staging (on PR)
  deploy-staging:
    runs-on: ubuntu-latest
    needs: build-docker
    if: github.event_name == 'pull_request'
    environment:
      name: staging
      url: https://staging-api.example.com

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Deploy to ECS
        run: |
          # Update ECS task definition with new image
          aws ecs update-service \
            --cluster staging-cluster \
            --service api-service \
            --force-new-deployment \
            --task-definition api-task:staging

      - name: Wait for deployment
        run: |
          aws ecs wait services-stable \
            --cluster staging-cluster \
            --services api-service

      - name: Run smoke tests
        run: |
          curl -f https://staging-api.example.com/health || exit 1

      - name: Comment on PR
        uses: actions/github-script@v6
        with:
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: '✅ Deployed to staging: https://staging-api.example.com'
            })

  # Job 5: Deploy to production (on main merge)
  deploy-production:
    runs-on: ubuntu-latest
    needs: build-docker
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    environment:
      name: production
      url: https://api.example.com

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Deploy to ECS (Rolling Update)
        run: |
          # Rolling deployment with health checks
          aws ecs update-service \
            --cluster prod-cluster \
            --service api-service \
            --force-new-deployment \
            --deployment-configuration "maximumPercent=200,minimumHealthyPercent=100" \
            --task-definition api-task:prod

      - name: Wait for deployment
        run: |
          aws ecs wait services-stable \
            --cluster prod-cluster \
            --services api-service

      - name: Run smoke tests
        run: |
          curl -f https://api.example.com/health || exit 1

      - name: Send Slack notification
        if: always()  # Run even if previous steps failed
        uses: 8398a7/action-slack@v3
        with:
          status: ${{ job.status }}
          text: 'Production deployment ${{ job.status }}'
          webhook_url: ${{ secrets.SLACK_WEBHOOK }}

  # Job 6: Rollback (manual trigger)
  rollback-production:
    runs-on: ubuntu-latest
    if: github.event_name == 'workflow_dispatch'
    environment:
      name: production

    steps:
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Rollback to previous version
        run: |
          # Get previous task definition
          PREVIOUS_TASK_DEF=$(aws ecs describe-services \
            --cluster prod-cluster \
            --services api-service \
            --query 'services[0].deployments[1].taskDefinition' \
            --output text)

          # Update to previous version
          aws ecs update-service \
            --cluster prod-cluster \
            --service api-service \
            --task-definition $PREVIOUS_TASK_DEF

      - name: Send Slack notification
        uses: 8398a7/action-slack@v3
        with:
          status: custom
          custom_payload: |
            {
              text: '🔄 Production rollback initiated by ${{ github.actor }}'
            }
          webhook_url: ${{ secrets.SLACK_WEBHOOK }}
```

Secrets to configure in GitHub:
- DOCKER_USERNAME
- DOCKER_PASSWORD
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- SNYK_TOKEN
- SLACK_WEBHOOK

Features:
- Parallel execution of tests and security scans
- Docker layer caching for faster builds
- Automatic staging deployment on PRs
- Production deployment with rolling updates
- Manual rollback capability
- Comprehensive security scanning
- Slack notifications
- PR comments with deployment status

Estimated pipeline time:
- Build + Test: 5-7 minutes
- Security scan: 3-4 minutes (parallel)
- Docker build: 3-5 minutes
- Deploy: 2-3 minutes
- Total: ~10-12 minutes for full pipeline
```

---

### 2. Configure Deployment Strategy

**Purpose:** Design and configure deployment strategy.

**Prompt:**
```
Design a deployment strategy for [APPLICATION]:

Application context:
- Type: [WEB/API/MICROSERVICE]
- Traffic: [REQUESTS_PER_SECOND]
- Availability requirement: [SLA]
- Deployment frequency: [DAILY/WEEKLY/ON_DEMAND]
- Rollback time requirement: [MINUTES]
- User impact tolerance: [ZERO_DOWNTIME/MINIMAL/SCHEDULED]

Deployment options:
[BLUE_GREEN/CANARY/ROLLING/RECREATE]

Provide:
- Strategy recommendation with rationale
- Step-by-step deployment process
- Health check configuration
- Rollback procedure
- Monitoring and alerts
- Configuration examples (Kubernetes, AWS, etc.)
- Testing strategy before production
```

**Example:**
```
Deployment strategy for high-traffic e-commerce API:

Context:
- Type: REST API microservice
- Traffic: 10k requests/second peak
- Availability: 99.99% SLA (52 minutes downtime/year)
- Frequency: Multiple deploys per day
- Rollback: < 2 minutes
- User impact: Zero downtime required

Recommendation: Canary Deployment with automatic rollback

Rationale:
- Zero downtime: New version runs alongside old
- Risk mitigation: Gradual traffic shift detects issues early
- Quick rollback: Route traffic back to old version instantly
- Frequent deploys: Supports multiple daily deployments
- Monitoring: Detect issues before affecting all users

Deployment Process:

Phase 1: Pre-deployment (5 minutes)
1. Run full test suite in CI
2. Build and scan Docker image
3. Deploy to staging, run smoke tests
4. Get approval (auto or manual based on confidence)

Phase 2: Canary deployment (15-30 minutes)
1. Deploy new version (canary) alongside current (baseline)
   - Canary: 10% of pods
   - Baseline: 90% of pods
2. Route 5% traffic to canary
3. Monitor for 5 minutes:
   - Error rate < 1%
   - Latency p99 < 500ms
   - No increase in 5xx errors
4. If healthy, increase to 25% traffic, monitor 5 min
5. If healthy, increase to 50% traffic, monitor 5 min
6. If healthy, increase to 100% traffic
7. Monitor for 10 minutes at 100%
8. If still healthy, terminate baseline pods

Phase 3: Post-deployment
1. Monitor metrics for 1 hour
2. Keep previous version image for 24 hours (rollback capability)
3. Update monitoring dashboards
4. Notify team in Slack

Kubernetes Canary Configuration:

```yaml
# baseline-deployment.yaml (current version)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-baseline
  labels:
    app: api
    version: v1.2.3
    track: baseline
spec:
  replicas: 9  # 90% of 10 total pods
  selector:
    matchLabels:
      app: api
      track: baseline
  template:
    metadata:
      labels:
        app: api
        version: v1.2.3
        track: baseline
    spec:
      containers:
      - name: api
        image: mycompany/api:v1.2.3
        ports:
        - containerPort: 3000
        livenessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 5
        resources:
          requests:
            cpu: 500m
            memory: 512Mi
          limits:
            cpu: 1000m
            memory: 1Gi
---
# canary-deployment.yaml (new version)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api-canary
  labels:
    app: api
    version: v1.2.4
    track: canary
spec:
  replicas: 1  # 10% of 10 total pods
  selector:
    matchLabels:
      app: api
      track: canary
  template:
    metadata:
      labels:
        app: api
        version: v1.2.4
        track: canary
    spec:
      containers:
      - name: api
        image: mycompany/api:v1.2.4  # New version
        # ... same as baseline ...
---
# service.yaml (routes traffic to both)
apiVersion: v1
kind: Service
metadata:
  name: api-service
spec:
  selector:
    app: api  # Matches both baseline and canary
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
---
# ingress.yaml (traffic splitting with Nginx)
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: api-ingress
  annotations:
    nginx.ingress.kubernetes.io/canary: "true"
    nginx.ingress.kubernetes.io/canary-weight: "5"  # 5% to canary
spec:
  rules:
  - host: api.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 80
```

Health Checks:

Readiness Probe (determines if pod receives traffic):
```
GET /ready
Expected: 200 OK
Checks:
- Application started
- Database connection pool ready
- Required services reachable
```

Liveness Probe (determines if pod should be restarted):
```
GET /health
Expected: 200 OK
Checks:
- Application responsive
- Not in deadlock/crash loop
- Memory not exhausted
```

Automated Rollback Triggers:

Monitor these metrics (5-minute windows):
1. Error rate > 1% (vs < 0.5% baseline)
2. P99 latency > 500ms (vs < 300ms baseline)
3. 5xx errors > 10/minute (vs < 2/minute baseline)
4. Pod crash loops (> 2 restarts/minute)
5. Failed health checks > 10%

Rollback script:
```bash
#!/bin/bash
# rollback.sh

echo "Rolling back to baseline version..."

# Set canary traffic to 0%
kubectl patch ingress api-ingress -p '
{
  "metadata": {
    "annotations": {
      "nginx.ingress.kubernetes.io/canary-weight": "0"
    }
  }
}'

# Scale down canary
kubectl scale deployment api-canary --replicas=0

# Scale up baseline to full capacity
kubectl scale deployment api-baseline --replicas=10

echo "Rollback complete. Monitoring..."

# Wait and verify
sleep 30
kubectl get pods -l app=api

# Send alert
curl -X POST $SLACK_WEBHOOK -d '{"text":"⚠️ API rolled back to baseline"}'
```

Monitoring & Alerts:

Prometheus queries for monitoring:
```yaml
# Error rate
sum(rate(http_requests_total{status=~"5.."}[5m])) /
sum(rate(http_requests_total[5m]))

# Latency p99
histogram_quantile(0.99,
  sum(rate(http_request_duration_seconds_bucket[5m])) by (le, version)
)

# Requests per second by version
sum(rate(http_requests_total[1m])) by (version)
```

AlertManager rules:
```yaml
groups:
- name: canary-alerts
  interval: 30s
  rules:
  - alert: CanaryHighErrorRate
    expr: |
      (sum(rate(http_requests_total{track="canary",status=~"5.."}[5m]))
      / sum(rate(http_requests_total{track="canary"}[5m]))) > 0.01
    for: 2m
    annotations:
      summary: "Canary error rate > 1% for 2 minutes"
      description: "Automatic rollback triggered"

  - alert: CanaryHighLatency
    expr: |
      histogram_quantile(0.99,
        sum(rate(http_request_duration_seconds_bucket{track="canary"}[5m])) by (le)
      ) > 0.5
    for: 2m
    annotations:
      summary: "Canary p99 latency > 500ms"
```

Gradual Rollout Script:
```bash
#!/bin/bash
# canary-rollout.sh

WEIGHTS=(5 25 50 100)
MONITOR_DURATION=300  # 5 minutes

for WEIGHT in "${WEIGHTS[@]}"; do
  echo "Setting canary weight to $WEIGHT%..."

  kubectl patch ingress api-ingress -p "{
    \"metadata\": {
      \"annotations\": {
        \"nginx.ingress.kubernetes.io/canary-weight\": \"$WEIGHT\"
      }
    }
  }"

  echo "Monitoring for $MONITOR_DURATION seconds..."
  sleep $MONITOR_DURATION

  # Check metrics (simplified - use Prometheus API in reality)
  ERROR_RATE=$(check_error_rate)
  if (( $(echo "$ERROR_RATE > 0.01" | bc -l) )); then
    echo "❌ Error rate too high ($ERROR_RATE). Rolling back..."
    ./rollback.sh
    exit 1
  fi

  echo "✅ Health check passed at $WEIGHT%"
done

echo "🎉 Canary deployment successful! Promoting to 100%..."

# Scale up canary to full capacity
kubectl scale deployment api-canary --replicas=10

# Scale down baseline
kubectl scale deployment api-baseline --replicas=0

echo "Deployment complete."
```

Testing Before Production:

1. Staging canary:
   - Deploy to staging environment first
   - Run full test suite + load tests
   - Verify metrics collection works

2. Feature flags:
   - Use feature flags for risky features
   - Enable for internal users first (dogfooding)
   - Gradual enable for external users

3. Synthetic monitoring:
   - Run synthetic transactions during canary
   - Verify critical user flows work

4. Dashboard:
   - Side-by-side comparison of baseline vs canary
   - Real-time error rates, latency, traffic split
   - Historical comparison (vs previous deploys)

Estimated Timeline:
- Canary start to 100%: 15-30 minutes (automated)
- Full confidence: 1 hour post-100%
- Rollback: < 2 minutes (automated)

Success Metrics:
- Deployment frequency: 5-10/day
- Failed deployments: < 1%
- Mean time to recovery: < 2 minutes
- Deployment duration: < 30 minutes
- User-impacting incidents: 0
```

---

## Infrastructure as Code

### 3. Generate Terraform Configuration

**Purpose:** Create Terraform infrastructure code.

**Prompt:**
```
Generate Terraform configuration for [INFRASTRUCTURE]:

Infrastructure requirements:
- Cloud provider: [AWS/GCP/AZURE]
- Resources needed: [COMPUTE/STORAGE/NETWORK/DATABASE]
- Environment: [DEV/STAGING/PRODUCTION]
- Region: [REGION]
- High availability: [YES/NO]
- Estimated cost: [BUDGET]

Include:
- Provider configuration
- VPC/Network setup
- Compute resources (EC2, ECS, Lambda, etc.)
- Storage (S3, EBS, etc.)
- Database (RDS, DynamoDB, etc.)
- Security groups and IAM roles
- Load balancers
- Monitoring and logging
- Variables and outputs
- Backend configuration (state management)

Organize in modules, use variables, follow best practices.
```

**Example:**
```
Terraform for AWS web application infrastructure:

Requirements:
- AWS (us-east-1)
- Resources: VPC, ECS Fargate, RDS PostgreSQL, S3, ALB
- Environment: Production
- HA: Yes (multi-AZ)
- Budget: ~$500/month

Structure:
```
terraform/
├── main.tf
├── variables.tf
├── outputs.tf
├── backend.tf
├── modules/
│   ├── vpc/
│   ├── ecs/
│   ├── rds/
│   ├── alb/
│   └── s3/
└── environments/
    ├── prod/
    │   └── terraform.tfvars
    └── staging/
        └── terraform.tfvars
```

backend.tf (state management):
```hcl
terraform {
  required_version = ">= 1.5"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }

  backend "s3" {
    bucket         = "mycompany-terraform-state"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-state-lock"
  }
}

provider "aws" {
  region = var.aws_region

  default_tags {
    tags = {
      Environment = var.environment
      ManagedBy   = "Terraform"
      Project     = var.project_name
    }
  }
}
```

variables.tf:
```hcl
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "environment" {
  description = "Environment name"
  type        = string
  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Environment must be dev, staging, or prod"
  }
}

variable "project_name" {
  description = "Project name for tagging"
  type        = string
  default     = "webapp"
}

variable "vpc_cidr" {
  description = "CIDR block for VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "db_instance_class" {
  description = "RDS instance class"
  type        = string
  default     = "db.t3.micro"
}

variable "db_password" {
  description = "Database password"
  type        = string
  sensitive   = true
}

variable "ecs_task_cpu" {
  description = "ECS task CPU units"
  type        = number
  default     = 256
}

variable "ecs_task_memory" {
  description = "ECS task memory (MB)"
  type        = number
  default     = 512
}

variable "app_count" {
  description = "Number of ECS tasks"
  type        = number
  default     = 2
}
```

main.tf:
```hcl
# VPC Module
module "vpc" {
  source = "./modules/vpc"

  environment         = var.environment
  vpc_cidr           = var.vpc_cidr
  availability_zones = ["${var.aws_region}a", "${var.aws_region}b"]
}

# Application Load Balancer
module "alb" {
  source = "./modules/alb"

  environment         = var.environment
  vpc_id             = module.vpc.vpc_id
  public_subnet_ids  = module.vpc.public_subnet_ids
  ssl_certificate_arn = aws_acm_certificate.main.arn
}

# ECS Cluster and Service
module "ecs" {
  source = "./modules/ecs"

  environment        = var.environment
  vpc_id            = module.vpc.vpc_id
  private_subnet_ids = module.vpc.private_subnet_ids
  alb_target_group_arn = module.alb.target_group_arn
  alb_security_group_id = module.alb.security_group_id

  task_cpu    = var.ecs_task_cpu
  task_memory = var.ecs_task_memory
  app_count   = var.app_count

  container_image = "mycompany/webapp:latest"
  container_port  = 3000

  environment_variables = {
    NODE_ENV     = var.environment
    DATABASE_URL = "postgresql://${module.rds.endpoint}/${module.rds.database_name}"
    S3_BUCKET    = module.s3.bucket_name
  }

  secrets = {
    DB_PASSWORD = module.rds.password_secret_arn
  }
}

# RDS PostgreSQL
module "rds" {
  source = "./modules/rds"

  environment         = var.environment
  vpc_id             = module.vpc.vpc_id
  subnet_ids         = module.vpc.private_subnet_ids
  allowed_security_group_ids = [module.ecs.security_group_id]

  instance_class     = var.db_instance_class
  database_name      = "webapp"
  master_username    = "admin"
  master_password    = var.db_password

  multi_az           = var.environment == "prod" ? true : false
  backup_retention_period = var.environment == "prod" ? 7 : 1
}

# S3 Bucket for assets
module "s3" {
  source = "./modules/s3"

  environment = var.environment
  bucket_name = "${var.project_name}-${var.environment}-assets"

  versioning_enabled = var.environment == "prod" ? true : false
  lifecycle_rules = [
    {
      id      = "expire-old-versions"
      enabled = true
      noncurrent_version_expiration_days = 90
    }
  ]
}

# ACM Certificate
resource "aws_acm_certificate" "main" {
  domain_name       = var.environment == "prod" ? "example.com" : "${var.environment}.example.com"
  validation_method = "DNS"

  lifecycle {
    create_before_destroy = true
  }
}
```

modules/vpc/main.tf:
```hcl
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name = "${var.environment}-vpc"
  }
}

# Public subnets (for ALB)
resource "aws_subnet" "public" {
  count             = length(var.availability_zones)
  vpc_id            = aws_vpc.main.id
  cidr_block        = cidrsubnet(var.vpc_cidr, 8, count.index)
  availability_zone = var.availability_zones[count.index]
  map_public_ip_on_launch = true

  tags = {
    Name = "${var.environment}-public-subnet-${count.index + 1}"
    Type = "Public"
  }
}

# Private subnets (for ECS, RDS)
resource "aws_subnet" "private" {
  count             = length(var.availability_zones)
  vpc_id            = aws_vpc.main.id
  cidr_block        = cidrsubnet(var.vpc_cidr, 8, count.index + 100)
  availability_zone = var.availability_zones[count.index]

  tags = {
    Name = "${var.environment}-private-subnet-${count.index + 1}"
    Type = "Private"
  }
}

# Internet Gateway
resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "${var.environment}-igw"
  }
}

# NAT Gateway (for private subnet internet access)
resource "aws_eip" "nat" {
  count  = length(var.availability_zones)
  domain = "vpc"

  tags = {
    Name = "${var.environment}-nat-eip-${count.index + 1}"
  }
}

resource "aws_nat_gateway" "main" {
  count         = length(var.availability_zones)
  allocation_id = aws_eip.nat[count.index].id
  subnet_id     = aws_subnet.public[count.index].id

  tags = {
    Name = "${var.environment}-nat-${count.index + 1}"
  }
}

# Route tables
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "${var.environment}-public-rt"
  }
}

resource "aws_route_table" "private" {
  count  = length(var.availability_zones)
  vpc_id = aws_vpc.main.id

  route {
    cidr_block     = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.main[count.index].id
  }

  tags = {
    Name = "${var.environment}-private-rt-${count.index + 1}"
  }
}

# Route table associations
resource "aws_route_table_association" "public" {
  count          = length(var.availability_zones)
  subnet_id      = aws_subnet.public[count.index].id
  route_table_id = aws_route_table.public.id
}

resource "aws_route_table_association" "private" {
  count          = length(var.availability_zones)
  subnet_id      = aws_subnet.private[count.index].id
  route_table_id = aws_route_table.private[count.index].id
}
```

modules/ecs/main.tf (abridged):
```hcl
# ECS Cluster
resource "aws_ecs_cluster" "main" {
  name = "${var.environment}-cluster"

  setting {
    name  = "containerInsights"
    value = "enabled"
  }
}

# Task Definition
resource "aws_ecs_task_definition" "app" {
  family                   = "${var.environment}-app"
  network_mode             = "awsvpc"
  requires_compatibilities = ["FARGATE"]
  cpu                      = var.task_cpu
  memory                   = var.task_memory
  execution_role_arn       = aws_iam_role.ecs_execution.arn
  task_role_arn            = aws_iam_role.ecs_task.arn

  container_definitions = jsonencode([{
    name      = "app"
    image     = var.container_image
    essential = true

    portMappings = [{
      containerPort = var.container_port
      protocol      = "tcp"
    }]

    environment = [
      for k, v in var.environment_variables : {
        name  = k
        value = v
      }
    ]

    secrets = [
      for k, v in var.secrets : {
        name      = k
        valueFrom = v
      }
    ]

    logConfiguration = {
      logDriver = "awslogs"
      options = {
        "awslogs-group"         = aws_cloudwatch_log_group.app.name
        "awslogs-region"        = data.aws_region.current.name
        "awslogs-stream-prefix" = "ecs"
      }
    }

    healthCheck = {
      command     = ["CMD-SHELL", "curl -f http://localhost:${var.container_port}/health || exit 1"]
      interval    = 30
      timeout     = 5
      retries     = 3
      startPeriod = 60
    }
  }])
}

# ECS Service
resource "aws_ecs_service" "app" {
  name            = "${var.environment}-app-service"
  cluster         = aws_ecs_cluster.main.id
  task_definition = aws_ecs_task_definition.app.arn
  desired_count   = var.app_count
  launch_type     = "FARGATE"

  network_configuration {
    subnets          = var.private_subnet_ids
    security_groups  = [aws_security_group.ecs_tasks.id]
    assign_public_ip = false
  }

  load_balancer {
    target_group_arn = var.alb_target_group_arn
    container_name   = "app"
    container_port   = var.container_port
  }

  depends_on = [var.alb_target_group_arn]
}

# Auto Scaling
resource "aws_appautoscaling_target" "ecs" {
  max_capacity       = 10
  min_capacity       = 2
  resource_id        = "service/${aws_ecs_cluster.main.name}/${aws_ecs_service.app.name}"
  scalable_dimension = "ecs:service:DesiredCount"
  service_namespace  = "ecs"
}

resource "aws_appautoscaling_policy" "ecs_cpu" {
  name               = "${var.environment}-cpu-autoscaling"
  policy_type        = "TargetTrackingScaling"
  resource_id        = aws_appautoscaling_target.ecs.resource_id
  scalable_dimension = aws_appautoscaling_target.ecs.scalable_dimension
  service_namespace  = aws_appautoscaling_target.ecs.service_namespace

  target_tracking_scaling_policy_configuration {
    predefined_metric_specification {
      predefined_metric_type = "ECSServiceAverageCPUUtilization"
    }
    target_value = 70.0
  }
}
```

outputs.tf:
```hcl
output "alb_dns_name" {
  description = "DNS name of the load balancer"
  value       = module.alb.dns_name
}

output "ecs_cluster_name" {
  description = "Name of the ECS cluster"
  value       = module.ecs.cluster_name
}

output "rds_endpoint" {
  description = "RDS endpoint"
  value       = module.rds.endpoint
  sensitive   = true
}

output "s3_bucket_name" {
  description = "S3 bucket name"
  value       = module.s3.bucket_name
}
```

environments/prod/terraform.tfvars:
```hcl
environment       = "prod"
aws_region        = "us-east-1"
project_name      = "webapp"
vpc_cidr          = "10.0.0.0/16"

db_instance_class = "db.t3.small"
# db_password provided via TF_VAR_db_password env var

ecs_task_cpu    = 512
ecs_task_memory = 1024
app_count       = 3  # High availability
```

Usage:
```bash
# Initialize
terraform init

# Plan
terraform plan -var-file=environments/prod/terraform.tfvars

# Apply
terraform apply -var-file=environments/prod/terraform.tfvars

# Destroy
terraform destroy -var-file=environments/prod/terraform.tfvars
```

Best Practices:
1. State management: Remote backend in S3 with DynamoDB locking
2. Modules: Reusable, tested modules
3. Variables: All configurable values as variables
4. Secrets: Use AWS Secrets Manager, not hardcoded
5. Tagging: Consistent tagging for cost tracking
6. Validation: Input validation on variables
7. Outputs: Export important values
8. Multi-environment: Separate tfvars files
9. Version pinning: Lock provider versions
10. Documentation: README in each module
```

---

## Monitoring & Logging

### 4. Configure Monitoring and Alerting

**Purpose:** Set up monitoring, logging, and alerting.

**Prompt:**
```
Configure monitoring and alerting for [APPLICATION]:

Application details:
- Type: [WEB/API/DATABASE/INFRASTRUCTURE]
- Stack: [TECHNOLOGIES]
- Critical metrics: [METRICS_TO_TRACK]
- SLA: [AVAILABILITY_TARGET]
- Monitoring tools: [PROMETHEUS/DATADOG/NEW_RELIC/CLOUDWATCH]

Setup:
- Metrics collection (what and how)
- Log aggregation (sources, format, retention)
- Dashboards (visualizations)
- Alerts (conditions, severity, notifications)
- On-call rotation integration
- Incident response runbooks

Provide configuration files, dashboard JSON, alert rules.
```

**Example:**
```
Monitoring setup for Node.js API (Prometheus + Grafana + AlertManager):

Application:
- REST API microservice
- Node.js, Express, PostgreSQL
- Critical: Response time, error rate, availability
- SLA: 99.9% uptime, p95 < 200ms
- Tools: Prometheus, Grafana, AlertManager, Loki

Architecture:
```
App → prom-client (metrics) → Prometheus (scrape)
    → winston (logs)      → Loki (aggregation)

Prometheus → AlertManager → Slack/PagerDuty
Prometheus → Grafana (dashboards)
```

1. Application Instrumentation (prom-client):

```javascript
// metrics.js
const client = require('prom-client');

// Enable default metrics (CPU, memory, event loop, etc.)
client.collectDefaultMetrics({ timeout: 5000 });

// Custom metrics
const httpRequestDuration = new client.Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duration of HTTP requests in seconds',
  labelNames: ['method', 'route', 'status_code'],
  buckets: [0.001, 0.005, 0.01, 0.05, 0.1, 0.5, 1, 5]
});

const httpRequestTotal = new client.Counter({
  name: 'http_requests_total',
  help: 'Total number of HTTP requests',
  labelNames: ['method', 'route', 'status_code']
});

const activeConnections = new client.Gauge({
  name: 'active_connections',
  help: 'Number of active connections'
});

const dbQueryDuration = new client.Histogram({
  name: 'db_query_duration_seconds',
  help: 'Duration of database queries',
  labelNames: ['operation', 'table'],
  buckets: [0.001, 0.005, 0.01, 0.05, 0.1, 0.5, 1]
});

// Middleware to track requests
function metricsMiddleware(req, res, next) {
  const start = Date.now();

  res.on('finish', () => {
    const duration = (Date.now() - start) / 1000;
    const route = req.route ? req.route.path : req.path;

    httpRequestDuration
      .labels(req.method, route, res.statusCode)
      .observe(duration);

    httpRequestTotal
      .labels(req.method, route, res.statusCode)
      .inc();
  });

  next();
}

// Expose metrics endpoint
function setupMetricsEndpoint(app) {
  app.get('/metrics', async (req, res) => {
    res.set('Content-Type', client.register.contentType);
    res.end(await client.register.metrics());
  });
}

module.exports = {
  metricsMiddleware,
  setupMetricsEndpoint,
  httpRequestDuration,
  activeConnections,
  dbQueryDuration
};
```

2. Prometheus Configuration:

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  external_labels:
    cluster: 'prod'
    env: 'production'

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets: ['alertmanager:9093']

# Load alert rules
rule_files:
  - 'alerts/*.yml'

scrape_configs:
  # API service
  - job_name: 'api'
    static_configs:
      - targets: ['api:3000']
        labels:
          app: 'api'
          env: 'production'
    metrics_path: '/metrics'
    scrape_interval: 10s

  # PostgreSQL exporter
  - job_name: 'postgres'
    static_configs:
      - targets: ['postgres-exporter:9187']

  # Node exporter (system metrics)
  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']

  # Cadvisor (container metrics)
  - job_name: 'cadvisor'
    static_configs:
      - targets: ['cadvisor:8080']
```

3. Alert Rules:

```yaml
# alerts/api-alerts.yml
groups:
  - name: api-alerts
    interval: 30s
    rules:
      # High error rate
      - alert: HighErrorRate
        expr: |
          (
            sum(rate(http_requests_total{status_code=~"5.."}[5m]))
            /
            sum(rate(http_requests_total[5m]))
          ) > 0.05
        for: 2m
        labels:
          severity: critical
          team: backend
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value | humanizePercentage }} (threshold: 5%)"
          runbook: "https://wiki.company.com/runbooks/high-error-rate"

      # High latency
      - alert: HighLatency
        expr: |
          histogram_quantile(0.95,
            sum(rate(http_request_duration_seconds_bucket[5m])) by (le)
          ) > 0.2
        for: 5m
        labels:
          severity: warning
          team: backend
        annotations:
          summary: "API latency is high"
          description: "P95 latency is {{ $value }}s (threshold: 0.2s)"

      # Service down
      - alert: ServiceDown
        expr: up{job="api"} == 0
        for: 1m
        labels:
          severity: critical
          team: backend
        annotations:
          summary: "API service is down"
          description: "API service {{ $labels.instance }} is unreachable"

      # High CPU usage
      - alert: HighCPUUsage
        expr: |
          rate(process_cpu_seconds_total{job="api"}[5m]) * 100 > 80
        for: 10m
        labels:
          severity: warning
          team: backend
        annotations:
          summary: "High CPU usage"
          description: "CPU usage is {{ $value }}% (threshold: 80%)"

      # High memory usage
      - alert: HighMemoryUsage
        expr: |
          (process_resident_memory_bytes{job="api"} / 1024 / 1024 / 1024) > 1.5
        for: 5m
        labels:
          severity: warning
          team: backend
        annotations:
          summary: "High memory usage"
          description: "Memory usage is {{ $value }}GB (threshold: 1.5GB)"

      # Database connection pool exhaustion
      - alert: DBConnectionPoolExhausted
        expr: |
          pg_pool_size{job="api"} - pg_pool_available{job="api"} > pg_pool_size * 0.9
        for: 2m
        labels:
          severity: critical
          team: backend
        annotations:
          summary: "Database connection pool nearly exhausted"
          description: "{{ $value }} connections used out of {{ $labels.pool_size }}"

      # Request rate drop (potential outage)
      - alert: RequestRateDrop
        expr: |
          sum(rate(http_requests_total[5m])) < 10
          AND
          sum(rate(http_requests_total[5m] offset 1h)) > 100
        for: 3m
        labels:
          severity: critical
          team: backend
        annotations:
          summary: "Sudden drop in request rate"
          description: "Current: {{ $value }} req/s, was {{ $value offset 1h }} req/s an hour ago"
```

4. AlertManager Configuration:

```yaml
# alertmanager.yml
global:
  resolve_timeout: 5m
  slack_api_url: 'https://hooks.slack.com/services/YOUR/WEBHOOK/URL'

# Routing tree
route:
  group_by: ['alertname', 'cluster', 'severity']
  group_wait: 10s
  group_interval: 10s
  repeat_interval: 12h
  receiver: 'default'

  routes:
    # Critical alerts to PagerDuty
    - match:
        severity: critical
      receiver: 'pagerduty'
      continue: true  # Also send to Slack

    # Warnings to Slack only
    - match:
        severity: warning
      receiver: 'slack-warnings'

    # Team-specific routing
    - match:
        team: backend
      receiver: 'slack-backend'

receivers:
  - name: 'default'
    slack_configs:
      - channel: '#alerts'
        title: '{{ .GroupLabels.alertname }}'
        text: '{{ range .Alerts }}{{ .Annotations.description }}{{ end }}'

  - name: 'pagerduty'
    pagerduty_configs:
      - service_key: 'YOUR_PAGERDUTY_KEY'
        description: '{{ .GroupLabels.alertname }}: {{ .CommonAnnotations.summary }}'

  - name: 'slack-warnings'
    slack_configs:
      - channel: '#warnings'
        title: '⚠️ {{ .GroupLabels.alertname }}'
        text: '{{ range .Alerts }}{{ .Annotations.description }}{{ end }}'
        color: 'warning'

  - name: 'slack-backend'
    slack_configs:
      - channel: '#backend-alerts'
        title: '{{ .GroupLabels.alertname }}'
        text: '{{ range .Alerts }}{{ .Annotations.description }}{{ end }}'

inhibit_rules:
  # Don't alert about high latency if service is down
  - source_match:
      alertname: 'ServiceDown'
    target_match:
      alertname: 'HighLatency'
    equal: ['instance']
```

5. Grafana Dashboard (JSON):

```json
{
  "dashboard": {
    "title": "API Monitoring Dashboard",
    "panels": [
      {
        "title": "Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "sum(rate(http_requests_total[1m])) by (status_code)",
            "legendFormat": "{{ status_code }}"
          }
        ],
        "yaxes": [{ "label": "req/s" }]
      },
      {
        "title": "Latency (P50, P95, P99)",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.50, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))",
            "legendFormat": "P50"
          },
          {
            "expr": "histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))",
            "legendFormat": "P95"
          },
          {
            "expr": "histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))",
            "legendFormat": "P99"
          }
        ]
      },
      {
        "title": "Error Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "(sum(rate(http_requests_total{status_code=~\"5..\"}[5m])) / sum(rate(http_requests_total[5m]))) * 100",
            "legendFormat": "Error %"
          }
        ],
        "thresholds": [
          { "value": 1, "color": "yellow" },
          { "value": 5, "color": "red" }
        ]
      },
      {
        "title": "Active Connections",
        "type": "graph",
        "targets": [
          {
            "expr": "active_connections",
            "legendFormat": "Connections"
          }
        ]
      }
    ]
  }
}
```

6. Logging Configuration (Winston + Loki):

```javascript
// logger.js
const winston = require('winston');
const LokiTransport = require('winston-loki');

const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.json()
  ),
  defaultMeta: {
    service: 'api',
    environment: process.env.NODE_ENV
  },
  transports: [
    // Console (local dev)
    new winston.transports.Console({
      format: winston.format.simple()
    }),

    // Loki (production)
    new LokiTransport({
      host: 'http://loki:3100',
      labels: {
        app: 'api',
        env: process.env.NODE_ENV
      },
      json: true,
      batching: true,
      interval: 5
    })
  ]
});

module.exports = logger;
```

7. Runbook Example:

```markdown
# Runbook: High Error Rate

## Alert
**Name:** HighErrorRate
**Severity:** Critical
**Threshold:** Error rate > 5% for 2 minutes

## Impact
Users experiencing failed requests, potential service degradation.

## Investigation Steps

1. **Check error dashboard:**
   - Grafana: https://grafana.company.com/d/api-errors
   - Look at error breakdown by endpoint and status code

2. **Check recent deployments:**
   ```bash
   kubectl rollout history deployment/api
   ```
   - Was there a recent deploy? Could be related.

3. **Check logs for errors:**
   ```bash
   # Loki query
   {app="api"} |= "error" | json | level="error"
   ```
   - Look for patterns (same error repeated)
   - Check for stack traces

4. **Check dependencies:**
   - Database: Is RDS healthy? Check CloudWatch
   - External APIs: Are they responding?
   - Check network issues

## Resolution

### If recent deployment caused it:
```bash
# Rollback to previous version
kubectl rollout undo deployment/api

# Verify rollback
kubectl rollout status deployment/api

# Check if error rate drops
```

### If database issue:
- Check RDS metrics (CPU, connections, slow queries)
- Consider scaling up instance or adding read replicas

### If external API issue:
- Enable circuit breaker
- Use cached/fallback data if possible

## Post-Incident

1. Create incident report
2. Schedule postmortem meeting
3. Add monitoring/alerts if gaps found
4. Update this runbook with learnings
```

Deployment (docker-compose for local testing):

```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - LOG_LEVEL=info

  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - ./alerts:/etc/prometheus/alerts
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.retention.time=30d'

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3001:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - ./grafana/dashboards:/etc/grafana/provisioning/dashboards

  alertmanager:
    image: prom/alertmanager:latest
    ports:
      - "9093:9093"
    volumes:
      - ./alertmanager.yml:/etc/alertmanager/alertmanager.yml

  loki:
    image: grafana/loki:latest
    ports:
      - "3100:3100"

  postgres-exporter:
    image: prometheuscommunity/postgres-exporter:latest
    environment:
      DATA_SOURCE_NAME: "postgresql://user:pass@postgres:5432/dbname?sslmode=disable"
```

This setup provides:
- Application metrics (request rate, latency, errors)
- System metrics (CPU, memory, disk)
- Database metrics
- Centralized logging
- Real-time dashboards
- Alerting with escalation
- Runbooks for incident response
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for writing effective DevOps prompts
- **Architecture:** See [architecture-prompts.md](./architecture-prompts.md) for infrastructure architecture
- **Testing:** See [testing-prompts.md](./testing-prompts.md) for testing CI/CD pipelines
