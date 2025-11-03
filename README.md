**README
server.js**

  Starts Express app, loads random users via randomuser.me
  .
  
  Uses axios with retry (3 attempts, exponential backoff) for API calls.
  
  Endpoints:
  
  POST /onboarding: Uploads user data to S3.
  
  POST /query: Runs queries on stored data.

**Errors:**

  "Failed to fetch random users" — API/internet issues.
  
  "Failed to forward data" — Check AWS credentials/bucket.

**services/forwardService.js**

  Uploads JSON to AWS S3 (AWS SDK v3).
  
  Supports bulk and single uploads.

**Errors:**

  "Missing credentials" — Configure AWS keys or IAM roles.
  
  TypeError (email.replace) — Payload missing email; log payload before upload.

**utils/logger.js**

  JSON logger with timestamps for info/error.
  
  Tip: Save logs to file with node server.js > logs.json 2>&1.
  
  Configuration & Deployment
**
**Local development:****
  Use .env file for AWS keys, region, bucket name. Loaded via dotenv.
  
**  Production:**
  Use IAM Roles attached to EC2 (or container) instance — do not store AWS keys in .env or code.
  AWS SDK automatically uses the instance role credentials.

**  Axios config:**
  Axios client has a 5-second timeout and retries 3 times on network or 5xx errors with exponential backoff.
