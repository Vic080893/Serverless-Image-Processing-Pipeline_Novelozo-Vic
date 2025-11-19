# Serverless Image Processing Pipeline - Novelozo Vic
**Capstone Project**

## Image Resizer Application
This application resizes images uploaded to an S3 bucket using **AWS Lambda** and **Step Functions**. You can trigger the workflow either manually via Step Functions or via an API Gateway endpoint.

## Step 1 — Upload Images to S3

### 1.1 For Step Functions Trigger
1. Open AWS Console → **S3** → `novelozo-original-images`.
2. Click **Upload**.
3. Select the image file(s) you want to resize via Step Functions.
4. Click **Upload**.
5. Note the exact filename; you’ll need it in Step 2.

### 1.2 For API Gateway Trigger
1. Open AWS Console → **S3** → `novelozo-original-images`.
2. Click **Upload**.
3. Select the image file(s) you want to resize via API Gateway.
4. Click **Upload**.
5. Note the exact filename; you’ll need it in Step 3.

> You can upload the same image for both triggers or different images. Just make sure you reference the correct filename in each case.

## Step 2 — Trigger Step Functions Manually
1. Go to AWS Console → **Step Functions** → **State Machines**.
2. Select `ImageResizerStateMachine`.
3. Click **Start execution**.
4. Enter JSON input:
   {
    "imageKey": "example-stepfunction.jpg"
    }
6. Click Start execution.
7. Wait for it to complete.
8. Monitor the execution status in Step Functions:
     Succeeded means the workflow completed successfully.
     Failed indicates there was an error; check the logs in CloudWatch.
9. Check the resized image in novelozo-resized-images.
10. Optionally, repeat for additional images by starting a new execution with the corresponding imageKey.

## Step 3 — Trigger via API Gateway (Postman)

1. Open Postman.
2. Create a POST request to your API Gateway endpoint:
   https://<api-id>.execute-api.us-east-1.amazonaws.com/prod/start
3. Set Header
   Content-Type: application/json
4. Set Body (raw JSON):
   {
  "imageKey": "example-apigateway.jpg"
    }
5. Click Send.
6. Wait for the workflow to complete.
7. Check the resized image in novelozo-resized-images.

## SUMMARY

Upload images separately for Step Functions and API Gateway, then trigger the workflow either manually via Step Functions or through API Gateway. The resized images will appear in novelozo-resized-images, and you can monitor workflow execution in Step Functions as well as check CloudWatch logs for troubleshooting if needed.
   
