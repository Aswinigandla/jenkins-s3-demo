# Jenkins + GitHub + Amazon S3 demo

A small static website deployed to an S3 bucket using a Jenkins Pipeline.

## Files

- `site/index.html` — website markup
- `site/style.css` — styling
- `site/script.js` — button interaction
- `Jenkinsfile` — checkout, validate, and deploy pipeline

## Before running

1. Create an S3 bucket in AWS (example region: `ap-south-1`).
2. Replace `YOUR-BUCKET-NAME` in the `Jenkinsfile` with your bucket name.
3. In Jenkins, create an AWS credential with ID `aws-s3-creds` using the AWS Credentials plugin.
4. Ensure AWS CLI is installed on the Jenkins agent that runs the job.
5. Push these files to a GitHub repository.
6. Create a Jenkins Pipeline job using **Pipeline script from SCM**, Git, your repository URL, branch `*/main`, and script path `Jenkinsfile`.
7. Click **Build Now** and check Console Output and the S3 bucket objects.

## IAM permissions

Grant only the permissions needed for your bucket. For this demo, the pipeline uses `s3:ListBucket` on the bucket ARN and `s3:PutObject` / `s3:GetObject` on its object ARN. Add delete permission only if you intentionally configure a sync command with `--delete`.

## Important notes

- Do not put AWS access keys in this repository or in the Jenkinsfile.
- The pipeline supports Windows agents (`bat`) and Linux agents (`sh`).
- Uploading files does not by itself make the site public. For a simple learning setup, configure S3 static website hosting and understand its public-access implications. For a production-style setup, keep the bucket private and serve it through CloudFront with Origin Access Control.
- The AWS credential binding requires the Jenkins AWS Credentials plugin.
