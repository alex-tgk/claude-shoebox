# Security Vulnerability Analysis

You are tasked with analyzing code for security vulnerabilities and providing recommendations or fixes to improve security posture.

## Instructions

1. **Identify Scope**
   - Ask which file(s), directory, or entire codebase to scan
   - Determine tech stack to focus on relevant vulnerabilities
   - Check if security tools are already in use
   - Understand the application's security requirements

2. **Automated Security Scanning**

   Run appropriate security scanning tools:

   **Node.js/JavaScript/TypeScript:**
   - `npm audit` or `pnpm audit` for dependency vulnerabilities
   - ESLint with security plugins (eslint-plugin-security)
   - Snyk or Socket.dev for dependency scanning
   - OWASP Dependency-Check

   **Go:**
   - `go list -json -m all | nancy sleuth` (Nancy)
   - `gosec` for code security scanning
   - `govulncheck` for vulnerability checking

   **Docker:**
   - `docker scan` or Trivy for container scanning
   - Check base image vulnerabilities

   **General:**
   - GitLeaks for secrets scanning
   - TruffleHog for finding secrets in git history

3. **Manual Code Security Review**

   **Injection Vulnerabilities:**
   - SQL Injection
     - Check for string concatenation in SQL queries
     - Ensure parameterized queries/prepared statements
     - Validate all user inputs
   - NoSQL Injection
     - Sanitize inputs for MongoDB, etc.
     - Avoid eval-like operations
   - Command Injection
     - Avoid exec/spawn with user input
     - Sanitize file paths
   - XSS (Cross-Site Scripting)
     - Check for unescaped user input in HTML
     - Validate React's dangerouslySetInnerHTML usage
     - Sanitize user-generated content
   - LDAP Injection
   - XML Injection

   **Authentication & Authorization:**
   - Check password storage (hashing with bcrypt/argon2)
   - Verify JWT implementation
     - Secret key strength
     - Token expiration
     - Signature verification
   - Check session management
   - Verify authorization checks on all protected routes
   - Check for broken access control
   - Verify multi-factor authentication implementation
   - Check for authentication bypass vulnerabilities

   **Sensitive Data Exposure:**
   - Secrets in code (API keys, passwords)
   - Secrets in environment variables (use .env)
   - Secrets in git history
   - Sensitive data in logs
   - Sensitive data in error messages
   - Unencrypted data transmission (enforce HTTPS)
   - Missing encryption at rest
   - Weak encryption algorithms

   **Security Misconfiguration:**
   - Default passwords/credentials
   - Unnecessary features enabled
   - Directory listing enabled
   - Verbose error messages in production
   - Missing security headers
     - Content-Security-Policy
     - X-Content-Type-Options
     - X-Frame-Options
     - Strict-Transport-Security
   - CORS misconfiguration
   - Insecure cookie settings (httpOnly, secure, sameSite)

   **Vulnerable Dependencies:**
   - Outdated packages with known vulnerabilities
   - Unmaintained dependencies
   - Transitive dependency vulnerabilities
   - Supply chain attacks risks

   **Input Validation:**
   - Missing input validation
   - Type confusion vulnerabilities
   - Buffer overflow risks
   - File upload vulnerabilities
     - File type validation
     - File size limits
     - Malicious file scanning
   - Regex DoS (ReDoS)
   - Path traversal vulnerabilities

   **Cryptography Issues:**
   - Weak hashing algorithms (MD5, SHA1)
   - Weak encryption (DES, 3DES)
   - Hardcoded cryptographic keys
   - Insufficient key length
   - Improper random number generation
   - Missing certificate validation

   **API Security:**
   - Missing rate limiting
   - Lack of input validation
   - Insufficient logging
   - Missing authentication
   - Insecure direct object references (IDOR)
   - Mass assignment vulnerabilities
   - API key exposure

   **Code Quality Issues:**
   - Use of eval() or similar dangerous functions
   - Use of `innerHTML` in JavaScript
   - Deserialization of untrusted data
   - Race conditions
   - Memory leaks
   - Integer overflow
   - Use of `any` type (TypeScript) bypassing type safety

   **Frontend-Specific:**
   - Local storage of sensitive data
   - Exposed API endpoints in client code
   - Client-side validation only (no server-side)
   - Missing CSRF protection
   - Clickjacking vulnerabilities
   - Open redirects

   **Backend-Specific:**
   - Missing request size limits
   - Lack of timeout configuration
   - Insufficient logging and monitoring
   - Missing backup and recovery procedures
   - Insecure deserialization

4. **Docker/Container Security**
   - Running as root user
   - Using latest tag instead of specific versions
   - Unnecessary packages in container
   - Exposed ports
   - Secrets in Dockerfile
   - Vulnerable base images

5. **Infrastructure as Code (Terraform/K8s)**
   - Overly permissive IAM roles
   - Unencrypted storage
   - Public S3 buckets
   - Missing network segmentation
   - Exposed secrets in config files

6. **Git Security**
   - Secrets in commit history
   - Sensitive files not in .gitignore
   - Unprotected branches
   - Missing branch protection rules

7. **Security Recommendations**

   For each vulnerability found, provide:
   - Severity level (Critical, High, Medium, Low)
   - Description of the vulnerability
   - Potential impact
   - Location in code
   - Code example showing the issue
   - Recommended fix with code example
   - References to security standards (OWASP, CWE)

8. **Implementation of Fixes**

   If user requests implementation:
   - Fix critical vulnerabilities first
   - Make one security improvement at a time
   - Test after each fix
   - Ensure fixes don't break functionality
   - Run security tests

9. **Security Best Practices**

   Recommend implementing:
   - Dependency scanning in CI/CD
   - Pre-commit hooks for secret scanning
   - Security linting in CI/CD
   - Regular security audits
   - Security headers middleware
   - Input validation libraries
   - Content Security Policy
   - Rate limiting
   - Logging and monitoring
   - Incident response plan

10. **Documentation**
    - Document security measures implemented
    - Create security guidelines for team
    - Document secure coding practices
    - Add security section to README
    - Document authentication/authorization flow

11. **Security Testing**
    - Add security test cases
    - Test authentication/authorization
    - Test input validation
    - Test error handling
    - Perform penetration testing if applicable

12. **Final Security Report**

    Provide comprehensive report including:
    - Executive summary
    - Total vulnerabilities found by severity
    - Detailed findings with locations
    - Automated scan results
    - Dependencies with vulnerabilities
    - Recommendations prioritized by risk
    - Fixes implemented (if applicable)
    - Remediation timeline for remaining issues
    - Security best practices to adopt

Complete the security analysis and provide actionable recommendations to improve security posture.
