# commands.md (Execution Log)

## 0) Environment and Preflight
```bash
aws sts get-caller-identity
aws configure get region
date
```
- Key output: "UserId": "AROAVRSF25B2D725DU562:user4886936=Sanay_Manish_Mutha_Mutha",
    "Account": "381324814452",
    "Arn": "arn:aws:sts::381324814452:assumed-role/voclabs/user4886936=Sanay_Manish_Mutha_Mutha"
  us-east-1
  Sat Mar 28 23:30:10 KST 2026
- Interpretation:AWS CLI is correctly configured with the intended AWS account

## 1) Build Artifact
```bash
cd toy-example
bash scripts/build.sh
ls -la dist
```
- Key output:Build completed successfully.
- Interpretation: the files are ready for upload

## 2) Runtime Variables
```bash
export AWS_REGION="us-east-1"
export BUCKET_NAME="ccaws-a1-<student-id>-$(date +%s)"
echo "$AWS_REGION"
echo "$BUCKET_NAME"
```
- Key output:us-east-1
dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an
- Interpretation: the output is matching with the intended service

## 3) Deploy
```bash
bash scripts/deploy-s3.sh
```
- Key output:make_bucket: dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an
upload: dist/index.html to s3://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an/index.html
upload: dist/error.html to s3://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an/error.html
Website endpoint: http://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an.s3-website-us-east-1.amazonaws.com/
- Interpretation:The s3 has been created and files regarding the bucket have been successfully been installed.

## 4) Verify
```bash
bash scripts/verify-s3.sh
```
- Key output:Bucket exists: PASS
Website configuration: PASS
Public access block: DISABLED
Bucket policy: PRESENT
Versioning: ENABLED
Objects accessible: PASS
- Interpretation: all the factors of the s3 are working properly

## 5) Browser Test
- Endpoint URL:http://dku-cloudcomputing-sanay-bucket-1-381324814452-us-east-1-an.s3-website-us-east-1.amazonaws.com/
- Test timestamp (KST):Sat Mar 29 00:47:30 KST 2026
- Result:index.html is shown as the main webpage


- Final status: Web page is working as intended.
