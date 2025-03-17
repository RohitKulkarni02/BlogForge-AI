# Blog Generation Using AWS Bedrock

This project is a serverless application that generates a blog using Amazon Bedrock's LLaMA-2 model and stores the generated content in an Amazon S3 bucket. The application is implemented as an AWS Lambda function written in Python.

## Features
- Generates a 200-word blog based on a provided topic.
- Uses the **Meta LLaMA-2 13B Chat** model from Amazon Bedrock for content generation.
- Stores the generated content in an Amazon S3 bucket for easy access and management.

## Prerequisites
Before running the project, ensure you have the following:
- AWS account with necessary permissions for Bedrock and S3.
- Python 3.x installed.
- Required dependencies installed via pip:

```bash
pip install boto3 botocore
```

## Project Structure
- **`lambda_function.py`**: The main Lambda handler that triggers blog generation and uploads the output to S3.
- **`requirements.txt`**: Lists the required dependencies.
- **`README.md`**: Documentation for the project.

## Configuration
1. Update the following values in `lambda_function.py`:
   - **`region_name`** in the Bedrock client (`us-east-1` in this example).
   - **`s3_bucket`**: Specify the target S3 bucket name where blogs will be stored.

## Deployment Steps
1. Package your code:
   ```bash
   zip -r lambda_function.zip lambda_function.py
   ```
2. Deploy the packaged code to AWS Lambda:
   ```bash
   aws lambda create-function \
   --function-name BlogGenerator \
   --runtime python3.x \
   --handler lambda_function.lambda_handler \
   --role <YOUR_AWS_LAMBDA_ROLE_ARN> \
   --zip-file fileb://lambda_function.zip
   ```
3. Add the necessary permissions for Bedrock and S3 to the Lambda role.

## Usage
1. Trigger the Lambda function with a JSON request body like below:

```json
{
    "blog_topic": "AI trends in 2025"
}
```

2. The generated blog will be stored in your specified S3 bucket under the path: `blog-output/{timestamp}.txt`

## Error Handling
- Logs errors encountered during blog generation or S3 upload.
- Uses retry logic for Bedrock API calls to improve reliability.

## Future Improvements
- Add better exception handling for network failures.
- Introduce more customization options for blog length, tone, or style.

## License
This project is licensed under the MIT License.
