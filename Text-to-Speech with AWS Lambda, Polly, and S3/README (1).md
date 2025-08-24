
# Text-to-Speech with AWS Lambda, Polly, and S3

This project demonstrates how to automatically convert text files stored in Amazon S3 into speech using Amazon Polly and save the resulting audio file (MP3) into a destination S3 bucket. The process is fully automated with AWS Lambda, which is triggered whenever a new text file is uploaded to the source bucket.

## ⚙️Architecture

1. Upload a .txt file into the Source S3 Bucket.

2. An S3 Event Trigger invokes the Lambda function.

3. The Lambda function:

 * Reads the text file from the source bucket.

 * Sends the content to Amazon Polly for speech synthesis.

 * Stores the resulting .mp3 file in the Destination S3 Bucket.

## 📂 Project Structure

    lambda_function.py   # Main Lambda handler code

    README.md            # Documentation

## 🛠️ Prerequisites

* AWS Account with permissions to use:

  * Lambda

  * S3

   * Polly

* AWS CLI (optional, for testing)

* Python 3.8+ runtime for Lambda
## 🔑 IAM Role Requirements

    
    {
    "Version": "2012-10-17",
    "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::source-bucket-5444/*",
        "arn:aws:s3:::destination-bucket-5444/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": "polly:SynthesizeSpeech",
      "Resource": "*"
    }
    ]
    }

    

























## ⚙️ Environment Variables

Set these environment variables in your Lambda configuration:

    SOURCE_BUCKET → name of your source bucket (e.g., source-bucket-5444)

    DESTINATION_BUCKET → name of your destination bucket (e.g., destination-bucket-5444)
## 🚀 Deployment Steps

**1.** Create two S3 buckets:

    source-bucket-5444
    destination-bucket-5444

**2.** Create a Lambda function (Python 3.8 runtime).

**3.** Upload the lambda_function.py code.

**4.** Set environment variables for bucket names.

**5.** Attach the IAM role with the required policies.

**6.** Add an S3 Event Notification on the source bucket to       trigger the Lambda function when a .txt file is uploaded.
## 🔄 Flow Description

**1.** Upload Text File
* The user/client uploads a .txt file (such as a blog or book) to the Source S3 Bucket.

**2.** Trigger Lambda Function
* An S3 Event Notification triggers the AWS Lambda function (Audio Processor) whenever a new text file is uploaded.

**3.** Text-to-Speech Conversion
* The Lambda function retrieves the file, extracts the text, and sends it to Amazon Polly, which converts the text into an audio stream (MP3).

**4.** Store Audio File
* The generated MP3 file is stored in the Destination S3 Bucket.

**5.** Download & Listen
* The End User can then access the destination bucket to download or stream the generated audio file.


![App Screenshot](https://github.com/vivekshinde25/AWS-PROJECTS/blob/2cb497058a1776ed5499c1bd9d41fac6ec6330a1/Text-to-Speech%20with%20AWS%20Lambda%2C%20Polly%2C%20and%20S3/Screenshot%202025-08-24%20141359.png)

## 🎯 Use Cases


* Content Accessibility – Provides audio versions of written content for visually impaired users.

* Learning – Enables users to listen to educational materials, enhancing learning experiences.

* Content Distribution – Offers an additional medium for content consumption, increasing engagement.

* Convenience – Allows users to listen to articles or books while multitasking, such as during commutes or workouts.
## ✅ Example Flow

* Upload: polly.txt → "Hello, this is a test of AWS Polly."

* Output: polly.mp3 stored in destination bucket.
## 📝 Notes

* Increase Lambda timeout to at least 30 seconds for larger text files.

* Increase Lambda memory to 256 MB or more for faster performance.

* Polly supports multiple voices and languages; adjust VoiceId in code as needed.