# AI Blog Generation

This project is an AWS Lambda-based application that generates blogs using Amazon Bedrock and saves the output to an S3 bucket. The application is triggered via an API Gateway endpoint and tested using Postman. It leverages the `boto3` library, included as a Lambda layer, to interact with AWS services.

## Tech Stack
- **Language**: Python
- **AWS Services**: Lambda, Bedrock, S3, API Gateway, CloudWatch
- **Libraries**: boto3 (Lambda layer), botocore
- **Tools**: Postman, GitHub
- **Model**: Meta LLaMA 2 (via Bedrock)

## Project Overview

- **Purpose**: Generate a 200-word blog based on a user-provided topic using the Meta LLaMA 2 model via Amazon Bedrock.
- **AWS Services Used**:
  - **AWS Lambda**: Hosts the application logic.
  - **Amazon Bedrock**: Generates blog content using the LLaMA 2 model.
  - **Amazon S3**: Stores generated blog content.
  - **API Gateway**: Provides an HTTP endpoint to trigger the Lambda function.
  - **CloudWatch**: Monitors logs for debugging and performance tracking.
- **Testing**: Postman is used to send HTTP requests to the API Gateway endpoint.

## Prerequisites

- AWS account with access to Lambda, Bedrock, S3, API Gateway, and CloudWatch.
- Python 3.8+ for local development.
- `boto3` library included as an AWS Lambda layer.
- Postman for testing API endpoints.
- GitHub repository: [Ai_Blog_generation](https://github.com/Monish-Nallagondalla/Ai_Blog_generation.git)

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Monish-Nallagondalla/Ai_Blog_generation.git
   cd Ai_Blog_generation
   ```

2. **Install Dependencies**:
   Ensure you have the required packages listed in `requirements.txt` for local testing:
   ```bash
   pip install -r requirements.txt
   ```

3. **AWS Lambda Layer Setup**:
   - The `boto3` library is zipped and added as a Lambda layer to avoid including it in the function package.
   - Follow AWS documentation to create and attach the layer to the Lambda function.

## Project Structure

```
Ai_Blog_generation/
├── lambda_function.py  # Main Lambda handler and logic
├── requirements.txt    # Python dependencies for local development
└── README.md          # Project documentation
```

## Usage

1. **Deploy the Lambda Function**:
   - Zip the `lambda_function.py` file.
   - Upload it to AWS Lambda.
   - Attach the `boto3` layer to the Lambda function.
   - Configure the function with the following environment details:
     - Region: `us-east-1`
     - S3 Bucket: `aws_bedrock_course1`
     - Model ID: `meta.llama2-13b-chat-v1`

2. **Set Up API Gateway**:
   - Create a REST API in API Gateway.
   - Configure a POST method to trigger the Lambda function.
   - Deploy the API and note the endpoint URL.

3. **Test with Postman**:
   - Send a POST request to the API Gateway endpoint with the following JSON body:
     ```json
     {
       "blog_topic": "Your blog topic here"
     }
     ```
   - Verify the response status code (200) and check the S3 bucket for the generated blog.

4. **Monitor Logs**:
   - Use CloudWatch to view Lambda function logs for debugging and performance monitoring.

## Lambda Function Details

- **File**: `lambda_function.py`
- **Handler**: `lambda_handler`
- **Functionality**:
  - Accepts a JSON payload with a `blog_topic` field.
  - Calls Amazon Bedrock to generate a 200-word blog using the LLaMA 2 model.
  - Saves the generated blog to an S3 bucket (`aws_bedrock_course1`) with a timestamped key (`blog-output/{timestamp}.txt`).
  - Returns a JSON response with status code 200 upon completion.

## Testing

- **Local Testing**:
  - Install dependencies from `requirements.txt`.
  - Mock AWS services using tools like `moto` for local testing.
- **Postman Testing**:
  - Use the API Gateway endpoint to send POST requests.
  - Ensure the `blog_topic` field is included in the request body.
- **S3 Verification**:
  - Check the `aws_bedrock_course1` bucket for generated blog files under the `blog-output/` prefix.

## Monitoring

- **CloudWatch Logs**:
  - Lambda function logs are automatically sent to CloudWatch.
  - Monitor for errors, timeouts, or successful blog generation.
- **API Gateway Logs**:
  - Enable logging in API Gateway to track request/response details.

## Dependencies

- `boto3`: Included as a Lambda layer.
- `botocore`: Used for AWS service configurations.
- Local development dependencies listed in `requirements.txt`.

## Notes

- Ensure IAM roles for the Lambda function have permissions for Bedrock, S3, and CloudWatch.
- The Bedrock model (`meta.llama2-13b-chat-v1`) requires access in the `us-east-1` region.
- The S3 bucket (`aws_bedrock_course1`) must exist before deploying the function.
- The application assumes the `boto3` layer is correctly configured in Lambda.

## Contributing

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature-branch`).
3. Commit changes (`git commit -m "Add feature"`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For questions or issues, open a GitHub issue or contact the repository owner at [Monish-Nallagondalla](https://github.com/Monish-Nallagondalla).
