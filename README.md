**server.js**

  Main server file.
  
  Starts Express app and loads random users.
  
  Defines /onboarding (uploads data to S3) and /query (runs analytics).
  Errors:
  
  “Failed to fetch random users” → API or internet issue.
  
  “Failed to forward data” → Check AWS credentials or bucket name.

**services/forwardService.js**

  Handles uploading JSON data to AWS S3 using AWS SDK v3.
  Errors:
  
  “Missing credentials” → Add AWS keys to .env.
  
  TypeError (email.replace) → Ensure payload includes email.
  Tip: Log payload before upload.

**utils/logger.js**

  Simple JSON logger for info and error messages with timestamps.
  Tip: Redirect logs to a file with node server.js > logs.json 2>&1.

**.env**

  Stores environment variables for AWS and app config.
  Example:
  
  AWS_ACCESS_KEY_ID=your-key
  AWS_SECRET_ACCESS_KEY=your-secret
  AWS_REGION=us-east-1
  S3_BUCKET_NAME=your-bucket


**Errors:**

  AccessDenied / InvalidAccessKeyId → Check IAM permissions and key values.
  
  “.env not found” → Ensure it’s in the project root and loaded via dotenv.
