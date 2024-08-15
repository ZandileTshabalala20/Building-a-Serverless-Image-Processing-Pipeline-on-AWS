# Building-a-Serverless-Image-Processing-Pipeline-on-AWS

step by step guide to create a POC which will detect for a specific text in the image uploaded to S3 and saves the result to dynamoDb as well as sends the notification to all the subscribers to the SNS topic:”

To create a serverless image processing pipeline that detects specific text in images using AWS services like Lambda, S3, Rekognition, DynamoDB, and SNS. This pipeline will detect text in an image uploaded to an S3 bucket, store the result in DynamoDB, and send notifications to all subscribers of an SNS topic.

Services: Lambda, S3, Rekognition, DynamoDB, and SNS.
______________________________________________________________________________________________________________________________________________________________________________________________
Step 1: Set Up the S3 Bucket
1.	Create an S3 Bucket:
o	Go to the S3 console and create a new bucket ( image-upload-bucket).
o	Enable event notifications to trigger a Lambda function when a new image is uploaded.
![image](https://github.com/user-attachments/assets/65e35578-6a06-4001-be60-1e86e2ce65aa)

Step 2: Set Up the DynamoDB Table
1.	Create a DynamoDB Table:
o	Go to the DynamoDB console and create a new table (ImageTextMetadata).
o	Use ImageID as the partition key (unique identifier for each image).
![dynamodb](https://github.com/user-attachments/assets/11265351-a4da-4bbf-b2b3-18065d4ef82c)

Step 3: Create the SNS Topic
1.	Create an SNS Topic:
o	Go to the SNS console and create a new topic (ImageTextDetectionTopic).
o	Add subscribers to the topic, such as email addresses.
![sns](https://github.com/user-attachments/assets/c7681e4d-9f81-41ac-8882-41ddb59a6d41)
![subscription](https://github.com/user-attachments/assets/d6246c7d-627c-46cf-bb2d-7c6a22d5837a)
![subscription confirmation](https://github.com/user-attachments/assets/b2d6d632-7487-4b16-ad8c-23a8d9fd6e0a)
![subscription1 ](https://github.com/user-attachments/assets/23885fb1-2f7c-43be-856b-285ecbead814)

Step 4: Create the Lambda Function for Image Processing
1.	Create a Lambda Function:
o	Go to the Lambda console and create a new function (TextDetectionLambda).
o	Choose a runtime (Python 3.x).
o	Set up an S3 trigger for the image-upload-bucket bucket.
2.	Install AWS SDK and Rekognition:
o	Include the necessary libraries in your Lambda function, such as boto3 for AWS SDK.
3.	Write the Lambda Function Code:
o	The function should:
	Retrieve the image from the S3 bucket.
	Use AWS Rekognition to detect text in the image.
	Store the detected text and related metadata in the DynamoDB table.
	Publish a notification to the SNS topic with the detection results.
![lambda](https://github.com/user-attachments/assets/e8d9ac3e-aa40-4359-958c-aa84eb382ce2)

Set Up IAM Role for Lambda:
•	Ensure your Lambda function has permissions to access S3, Rekognition, DynamoDB, and SNS.
•	Attach an IAM role with the necessary policies.
![iam](https://github.com/user-attachments/assets/223e6357-5ed4-4cb6-9d88-b8db5f113cb5)

Step 5: Test the Pipeline
1.	Upload an Image:
o	Upload an image with text to the S3 bucket (image-upload-bucket).
2.	Check DynamoDB and SNS:
o	Verify that the detected text and metadata are saved in the DynamoDB table.
o	Check that a notification is sent to SNS subscribers with the detection result.










