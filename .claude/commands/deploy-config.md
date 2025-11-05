# Create Deployment Configurations

You are tasked with creating comprehensive deployment configurations including Docker, Kubernetes, and CI/CD pipelines.

## Instructions

1. **Gather Requirements**
   - Ask about the application type (web app, API, microservice, etc.)
   - Determine deployment platform (Docker, Kubernetes, AWS, GCP, Azure)
   - Understand environment needs (dev, staging, production)
   - Ask about CI/CD platform (GitHub Actions, GitLab CI, CircleCI)
   - Identify dependencies (databases, Redis, external services)
   - Understand scaling requirements
   - Determine monitoring and logging needs

2. **Docker Configuration**

   **Multi-Stage Dockerfile for Node.js/TypeScript:**

   ```dockerfile
   # Build stage
   FROM node:20-alpine AS builder

   # Set working directory
   WORKDIR /app

   # Copy package files
   COPY package*.json ./
   COPY pnpm-lock.yaml ./

   # Install pnpm
   RUN npm install -g pnpm

   # Install dependencies
   RUN pnpm install --frozen-lockfile

   # Copy source code
   COPY . .

   # Build application
   RUN pnpm run build

   # Remove dev dependencies
   RUN pnpm prune --prod

   # Production stage
   FROM node:20-alpine

   # Install dumb-init for proper signal handling
   RUN apk add --no-cache dumb-init

   # Create app user
   RUN addgroup -g 1001 -S nodejs && \
       adduser -S nodejs -u 1001

   # Set working directory
   WORKDIR /app

   # Copy built application from builder
   COPY --from=builder --chown=nodejs:nodejs /app/dist ./dist
   COPY --from=builder --chown=nodejs:nodejs /app/node_modules ./node_modules
   COPY --from=builder --chown=nodejs:nodejs /app/package*.json ./

   # Switch to non-root user
   USER nodejs

   # Expose port
   EXPOSE 3000

   # Health check
   HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
     CMD node -e "require('http').get('http://localhost:3000/health', (r) => {process.exit(r.statusCode === 200 ? 0 : 1)})"

   # Use dumb-init to handle signals properly
   ENTRYPOINT ["dumb-init", "--"]

   # Start application
   CMD ["node", "dist/index.js"]
   ```

   **Dockerfile for Go:**

   ```dockerfile
   # Build stage
   FROM golang:1.21-alpine AS builder

   WORKDIR /app

   # Install dependencies
   RUN apk add --no-cache git

   # Copy go mod files
   COPY go.mod go.sum ./
   RUN go mod download

   # Copy source code
   COPY . .

   # Build binary
   RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ./cmd/server

   # Production stage
   FROM alpine:latest

   RUN apk --no-cache add ca-certificates

   WORKDIR /root/

   # Copy binary from builder
   COPY --from=builder /app/main .

   # Expose port
   EXPOSE 8080

   # Health check
   HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
     CMD wget --no-verbose --tries=1 --spider http://localhost:8080/health || exit 1

   # Run
   CMD ["./main"]
   ```

   **.dockerignore:**

   ```
   # Dependencies
   node_modules
   npm-debug.log
   yarn-error.log
   pnpm-debug.log

   # Build outputs
   dist
   build
   .next
   out

   # Git
   .git
   .gitignore
   .gitattributes

   # Documentation
   README.md
   CHANGELOG.md
   docs

   # Tests
   **/*.test.ts
   **/*.spec.ts
   **/__tests__
   coverage

   # IDE
   .vscode
   .idea
   *.swp
   *.swo

   # Environment
   .env
   .env.local
   .env.*.local

   # CI/CD
   .github
   .gitlab-ci.yml
   .circleci

   # Docker
   Dockerfile
   docker-compose.yml
   .dockerignore
   ```

3. **Docker Compose for Local Development**

   **docker-compose.yml:**

   ```yaml
   version: '3.8'

   services:
     app:
       build:
         context: .
         dockerfile: Dockerfile
         target: builder  # Use builder stage for development
       ports:
         - "3000:3000"
       environment:
         NODE_ENV: development
         DATABASE_URL: postgresql://user:password@postgres:5432/myapp
         REDIS_URL: redis://redis:6379
       volumes:
         - .:/app
         - /app/node_modules
       depends_on:
         postgres:
           condition: service_healthy
         redis:
           condition: service_healthy
       networks:
         - app-network
       command: pnpm run dev

     postgres:
       image: postgres:15-alpine
       environment:
         POSTGRES_USER: user
         POSTGRES_PASSWORD: password
         POSTGRES_DB: myapp
       ports:
         - "5432:5432"
       volumes:
         - postgres_data:/var/lib/postgresql/data
         - ./init-scripts:/docker-entrypoint-initdb.d
       healthcheck:
         test: ["CMD-SHELL", "pg_isready -U user -d myapp"]
         interval: 10s
         timeout: 5s
         retries: 5
       networks:
         - app-network

     redis:
       image: redis:7-alpine
       ports:
         - "6379:6379"
       volumes:
         - redis_data:/data
       healthcheck:
         test: ["CMD", "redis-cli", "ping"]
         interval: 10s
         timeout: 3s
         retries: 5
       networks:
         - app-network

     nginx:
       image: nginx:alpine
       ports:
         - "80:80"
       volumes:
         - ./nginx.conf:/etc/nginx/nginx.conf:ro
       depends_on:
         - app
       networks:
         - app-network

   volumes:
     postgres_data:
     redis_data:

   networks:
     app-network:
       driver: bridge
   ```

4. **Kubernetes Configuration**

   **Namespace:**

   ```yaml
   # k8s/namespace.yaml
   apiVersion: v1
   kind: Namespace
   metadata:
     name: myapp
     labels:
       name: myapp
       environment: production
   ```

   **ConfigMap:**

   ```yaml
   # k8s/configmap.yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: myapp-config
     namespace: myapp
   data:
     NODE_ENV: "production"
     LOG_LEVEL: "info"
     PORT: "3000"
   ```

   **Secrets:**

   ```yaml
   # k8s/secrets.yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: myapp-secrets
     namespace: myapp
   type: Opaque
   stringData:
     DATABASE_URL: "postgresql://user:password@postgres:5432/myapp"
     JWT_SECRET: "your-secret-key"
     API_KEY: "your-api-key"
   ```

   **Deployment:**

   ```yaml
   # k8s/deployment.yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: myapp
     namespace: myapp
     labels:
       app: myapp
   spec:
     replicas: 3
     revisionHistoryLimit: 3
     selector:
       matchLabels:
         app: myapp
     strategy:
       type: RollingUpdate
       rollingUpdate:
         maxSurge: 1
         maxUnavailable: 0
     template:
       metadata:
         labels:
           app: myapp
           version: v1
       spec:
         serviceAccountName: myapp
         securityContext:
           runAsNonRoot: true
           runAsUser: 1001
           fsGroup: 1001
         containers:
         - name: myapp
           image: myregistry.io/myapp:latest
           imagePullPolicy: Always
           ports:
           - containerPort: 3000
             name: http
             protocol: TCP
           env:
           - name: PORT
             valueFrom:
               configMapKeyRef:
                 name: myapp-config
                 key: PORT
           - name: NODE_ENV
             valueFrom:
               configMapKeyRef:
                 name: myapp-config
                 key: NODE_ENV
           envFrom:
           - secretRef:
               name: myapp-secrets
           resources:
             requests:
               memory: "256Mi"
               cpu: "100m"
             limits:
               memory: "512Mi"
               cpu: "500m"
           livenessProbe:
             httpGet:
               path: /health
               port: 3000
             initialDelaySeconds: 30
             periodSeconds: 10
             timeoutSeconds: 5
             failureThreshold: 3
           readinessProbe:
             httpGet:
               path: /health/ready
               port: 3000
             initialDelaySeconds: 10
             periodSeconds: 5
             timeoutSeconds: 3
             failureThreshold: 3
           volumeMounts:
           - name: tmp
             mountPath: /tmp
         volumes:
         - name: tmp
           emptyDir: {}
   ```

   **Service:**

   ```yaml
   # k8s/service.yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: myapp
     namespace: myapp
     labels:
       app: myapp
   spec:
     type: ClusterIP
     ports:
     - port: 80
       targetPort: 3000
       protocol: TCP
       name: http
     selector:
       app: myapp
   ```

   **Ingress:**

   ```yaml
   # k8s/ingress.yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: myapp
     namespace: myapp
     annotations:
       cert-manager.io/cluster-issuer: "letsencrypt-prod"
       nginx.ingress.kubernetes.io/ssl-redirect: "true"
       nginx.ingress.kubernetes.io/rate-limit: "100"
   spec:
     ingressClassName: nginx
     tls:
     - hosts:
       - api.example.com
       secretName: myapp-tls
     rules:
     - host: api.example.com
       http:
         paths:
         - path: /
           pathType: Prefix
           backend:
             service:
               name: myapp
               port:
                 number: 80
   ```

   **HorizontalPodAutoscaler:**

   ```yaml
   # k8s/hpa.yaml
   apiVersion: autoscaling/v2
   kind: HorizontalPodAutoscaler
   metadata:
     name: myapp
     namespace: myapp
   spec:
     scaleTargetRef:
       apiVersion: apps/v1
       kind: Deployment
       name: myapp
     minReplicas: 3
     maxReplicas: 10
     metrics:
     - type: Resource
       resource:
         name: cpu
         target:
           type: Utilization
           averageUtilization: 70
     - type: Resource
       resource:
         name: memory
         target:
           type: Utilization
           averageUtilization: 80
     behavior:
       scaleDown:
         stabilizationWindowSeconds: 300
         policies:
         - type: Percent
           value: 50
           periodSeconds: 60
       scaleUp:
         stabilizationWindowSeconds: 0
         policies:
         - type: Percent
           value: 100
           periodSeconds: 30
         - type: Pods
           value: 2
           periodSeconds: 30
   ```

5. **GitHub Actions CI/CD**

   **.github/workflows/ci.yml:**

   ```yaml
   name: CI

   on:
     pull_request:
       branches: [main, develop]
     push:
       branches: [main, develop]

   jobs:
     test:
       runs-on: ubuntu-latest

       services:
         postgres:
           image: postgres:15
           env:
             POSTGRES_USER: test
             POSTGRES_PASSWORD: test
             POSTGRES_DB: testdb
           options: >-
             --health-cmd pg_isready
             --health-interval 10s
             --health-timeout 5s
             --health-retries 5
           ports:
             - 5432:5432

       steps:
         - uses: actions/checkout@v4

         - uses: pnpm/action-setup@v2
           with:
             version: 8

         - uses: actions/setup-node@v4
           with:
             node-version: '20'
             cache: 'pnpm'

         - name: Install dependencies
           run: pnpm install --frozen-lockfile

         - name: Lint
           run: pnpm run lint

         - name: Type check
           run: pnpm run type-check

         - name: Run tests
           run: pnpm run test:ci
           env:
             DATABASE_URL: postgresql://test:test@localhost:5432/testdb

         - name: Upload coverage
           uses: codecov/codecov-action@v3
           with:
             files: ./coverage/coverage-final.json

         - name: Build
           run: pnpm run build

     security:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4

         - name: Run security audit
           run: pnpm audit

         - name: Run Trivy vulnerability scanner
           uses: aquasecurity/trivy-action@master
           with:
             scan-type: 'fs'
             scan-ref: '.'
             format: 'sarif'
             output: 'trivy-results.sarif'

         - name: Upload Trivy results to GitHub Security
           uses: github/codeql-action/upload-sarif@v2
           with:
             sarif_file: 'trivy-results.sarif'
   ```

   **.github/workflows/deploy.yml:**

   ```yaml
   name: Deploy

   on:
     push:
       branches: [main]
     workflow_dispatch:

   env:
     REGISTRY: ghcr.io
     IMAGE_NAME: ${{ github.repository }}

   jobs:
     build-and-push:
       runs-on: ubuntu-latest
       permissions:
         contents: read
         packages: write

       steps:
         - uses: actions/checkout@v4

         - name: Set up Docker Buildx
           uses: docker/setup-buildx-action@v3

         - name: Log in to Container Registry
           uses: docker/login-action@v3
           with:
             registry: ${{ env.REGISTRY }}
             username: ${{ github.actor }}
             password: ${{ secrets.GITHUB_TOKEN }}

         - name: Extract metadata
           id: meta
           uses: docker/metadata-action@v5
           with:
             images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
             tags: |
               type=ref,event=branch
               type=sha,prefix={{branch}}-
               type=semver,pattern={{version}}

         - name: Build and push
           uses: docker/build-push-action@v5
           with:
             context: .
             push: true
             tags: ${{ steps.meta.outputs.tags }}
             labels: ${{ steps.meta.outputs.labels }}
             cache-from: type=gha
             cache-to: type=gha,mode=max

     deploy:
       needs: build-and-push
       runs-on: ubuntu-latest
       environment: production

       steps:
         - uses: actions/checkout@v4

         - name: Install kubectl
           uses: azure/setup-kubectl@v3

         - name: Set kubectl context
           uses: azure/k8s-set-context@v3
           with:
             method: kubeconfig
             kubeconfig: ${{ secrets.KUBE_CONFIG }}

         - name: Deploy to Kubernetes
           run: |
             kubectl apply -f k8s/
             kubectl rollout status deployment/myapp -n myapp
             kubectl get pods -n myapp

         - name: Verify deployment
           run: |
             kubectl wait --for=condition=available --timeout=300s deployment/myapp -n myapp
   ```

6. **Helm Chart (Optional)**

   Create Helm chart for more flexible deployments:

   ```yaml
   # helm/values.yaml
   replicaCount: 3

   image:
     repository: myregistry.io/myapp
     tag: latest
     pullPolicy: Always

   service:
     type: ClusterIP
     port: 80

   ingress:
     enabled: true
     className: nginx
     annotations:
       cert-manager.io/cluster-issuer: letsencrypt-prod
     hosts:
       - host: api.example.com
         paths:
           - path: /
             pathType: Prefix
     tls:
       - secretName: myapp-tls
         hosts:
           - api.example.com

   resources:
     requests:
       memory: 256Mi
       cpu: 100m
     limits:
       memory: 512Mi
       cpu: 500m

   autoscaling:
     enabled: true
     minReplicas: 3
     maxReplicas: 10
     targetCPUUtilizationPercentage: 70
   ```

7. **Environment-Specific Configurations**

   Create separate configs for each environment:
   - `k8s/overlays/dev/`
   - `k8s/overlays/staging/`
   - `k8s/overlays/production/`

8. **Final Deliverables**

   Provide:
   - Dockerfile with multi-stage builds
   - docker-compose.yml for local dev
   - Complete Kubernetes manifests
   - CI/CD pipeline configurations
   - Environment-specific configs
   - Deployment documentation
   - Rollback procedures
   - Monitoring setup instructions

Complete deployment configuration ensuring production-ready, scalable infrastructure.
