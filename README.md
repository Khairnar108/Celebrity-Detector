<img width="1361" height="262" alt="Screenshot 2026-07-16 204423" src="https://github.com/user-attachments/assets/8877c7b3-6b99-46c5-af2c-08b81daa3828" />
# Celebrity-Detector

Celebrity Recognition System using AWS
Project Overview

The Celebrity Recognition System is a serverless cloud application built on AWS that identifies celebrities from uploaded images using Amazon Rekognition. Users upload an image through a web application, and the system detects one or more celebrities present in the image along with their confidence scores. The recognition results are stored in Amazon DynamoDB to reduce repeated API calls and maintain request history. The application is exposed through Amazon API Gateway, making it accessible via REST APIs.

The project follows a serverless architecture, making it scalable, cost-effective, and easy to maintain without managing servers.

Project Architecture
User
   │
   ▼
Frontend Website (HTML/CSS/JavaScript)
   │
   ▼
Amazon API Gateway
   │
   ▼
AWS Lambda
   │
   ├────────► Amazon S3
   │            (Read uploaded image)
   │
   ├────────► Amazon Rekognition
   │            (Detect celebrity)
   │
   └────────► Amazon DynamoDB
                (Store results & request history)
AWS Services Used
Service	Purpose
Amazon S3	Store uploaded celebrity images
AWS Lambda	Process API requests and call Rekognition
Amazon Rekognition	Identify celebrities in images
Amazon DynamoDB	Store recognition results and history
API Gateway	Create REST APIs
IAM	Manage permissions
CloudWatch	Store logs and monitor Lambda
Project Workflow
User uploads an image.
Image is stored in Amazon S3.
User sends the image name to API Gateway.
API Gateway invokes Lambda.
Lambda checks DynamoDB for existing results.
If results exist, they are returned immediately.
Otherwise, Lambda calls Amazon Rekognition.
Rekognition detects celebrity names and confidence.
Lambda stores results in DynamoDB.
Results are returned to the website.
Step-by-Step Implementation (Short)
Step 1: Create an S3 Bucket
Create an S3 bucket.
Upload celebrity images.
Enable CORS for browser uploads.
Step 2: Create DynamoDB Tables

Create two tables.

CelebrityResults

Stores recognized celebrity information.

Primary Key

imageKey
RequestHistory

Stores every API request.

Primary Key

requestId

Sort Key

timestamp
Step 3: Create IAM Role

Give Lambda permission to access

Amazon S3
Amazon Rekognition
DynamoDB
CloudWatch Logs
Step 4: Create Lambda Function

Develop the Lambda function in Python using boto3.

The function performs the following:

Receives image name
Checks DynamoDB cache
Reads image from S3
Calls Rekognition
Stores results in DynamoDB
Returns JSON response
Step 5: Deploy Lambda
Zip the Python code.
Upload it to Lambda.
Configure:
Python Runtime
IAM Role
Handler
Memory
Timeout
Step 6: Create API Gateway

Create REST APIs.

GET /celebrity

Input

imageKey=photo.jpg

Output

{
  "celebrity":"Virat Kohli",
  "confidence":99.3
}
Step 7: Create Frontend Website

Develop a simple webpage using

HTML
CSS
JavaScript

Features

Upload Image
Detect Celebrity
Display Name
Show Confidence Score
Step 8: Upload Image

Upload an image to the S3 bucket.

Example

virat.jpg
Step 9: Test API

Call the API

GET /celebrity?imageKey=virat.jpg

Lambda processes the request and returns the detected celebrity.

Step 10: Monitor

Use CloudWatch Logs to

View Lambda execution
Debug errors
Monitor API performance
Features
Serverless architecture
Fast celebrity recognition
Multiple celebrity detection
DynamoDB caching
REST API integration
Scalable and cost-efficient
CloudWatch monitoring
Responsive web interface
Project Advantages
No server management required
Automatically scales with user requests
Reduces Rekognition cost using cache
High availability
Easy deployment
Secure AWS IAM permissions
Technologies Used
Python
HTML
CSS
JavaScript
AWS Lambda
Amazon S3
Amazon Rekognition
Amazon DynamoDB
API Gateway
IAM
CloudWatch
Boto3
Expected Output
User uploads a celebrity image.
The application detects the celebrity.
Celebrity name and confidence score are displayed.
Results are stored in DynamoDB.
Future requests for the same image are served from the cache instead of calling Rekognition again.

<img width="1365" height="763" alt="Screenshot 2026-07-16 224243" src="https://github.com/user-attachments/assets/d9506fdf-cc84-4f2d-892a-c245618bb619" />
<img width="682" height="765" alt="Screenshot 2026-07-16 224218" src="https://github.com/user-attachments/assets/c64bc986-31de-4851-a14d-3ecf1927b5ed" />
<img width="680" height="766" alt="Screenshot 2026-07-16 224149" src="https://github.com/user-attachments/assets/81c80951-ffc5-411f-97a2-7a1173f3f9e6" />
<img width="679" height="766" alt="Screenshot 2026-07-16 224133" src="https://github.com/user-attachments/assets/842c718f-d570-478f-9e46-bb6a03c657c7" />
<img width="679" height="766" alt="Screenshot 2026-07-16 224133" src="https://github.com/user-attachments/assets/b97383db-f9f2-4033-a5fd-ec606072b8e4" />
<img width="681" height="759" alt="Screenshot 2026-07-16 224044" src="https://github.com/user-attachments/assets/23644893-e0c3-4263-806d-ff5de534b7ac" />
