# Assignment 1 Report: S3 Static Website Hosting

## 1) Student Info
- Name: Sanay Manish Mutha Mutha
- Student ID: 32249369
- Date (KST): 23-03-2026
- AWS Account ID: 381324814452
- AWS Region: United States(N. Virginia)

## 2) Objective and Scope
- Objective: To deploy a static website using Amazon S3 via AWS CLI and configure it for public access.
- Scope (what was implemented):
Created an S3 bucket
Enabled static website hosting
Configured public access settings
Applied bucket policy for public read access
Uploaded static website files (index.html, error.html)
- Out of scope: Using AWS as a front for the cli commands

## 3) Architecture Summary
- Bucket name: dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an
- Endpoint URL: http://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an.s3-website-us-east-1.amazonaws.com/
- Static files deployed:index.html and error.html
- Access model (public website read policy):s3:GetObject

## 4) Implementation Steps (What and Why)
1. Bucket creation/check
- Command evidence reference:aws s3 mb s3://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an --region us-east-1
- Why this step is required:It is the storage container

2. Static website configuration (`index.html`, `error.html`)
- Command evidence reference:aws s3 website s3://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an --index-document index.html --error-document error.html
- Why this step is required:It is for the default pages

3. Public access block configuration
- Command evidence reference:aws s3api put-public-access-block --bucket dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an --public-access-block-configuration BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false
- Why this step is required for website mode:This makes the website public and ready to view for everyone

4. Bucket policy application (`s3:GetObject`)
- Command evidence reference:aws s3api put-bucket-policy --bucket dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an --policy file://policy.json
- Policy scope justification (least privilege):The policy allows only s3:GetObject on objects within the bucket, ensuring read-only access without exposing write or delete permissions.

5. Versioning enablement
- Command evidence reference:aws s3api put-bucket-versioning --bucket dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an --versioning-configuration Status=Enabled
- Why this step is required: To check the changes in versions

6. Upload/sync
- Command evidence reference:aws s3 sync ./website s3://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an
- Validation summary:to ensure that the files were uploaded successfully

## 5) Validation Results
- Website reachable: Yes 
- Website config verified: Yes
- Policy verified: Yes 
- Versioning/object versions verified: Yes
- Public access block state recorded: Yes 

## 6) Failure and Recovery (At least one)
- Symptom:Website returned “Access Denied” error when accessed via browser
- Error message:AccessDenied
- Root cause:Public access block settings were enabled, preventing public access
- Fix:Disabled public access block and applied correct bucket policy
- Re-verification:Website successfully loaded after changes

## 7) Reproducibility Checklist
- [x] `commands.md` includes command + key output + interpretation
- [x] Endpoint is tested from browser
- [x] Evidence is aligned with rubric items
- [x] Final resources/state are documented
