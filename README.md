

# 🤖 EZEGS-AI-ChatBot — Serverless AI Chatbot with Amazon Bedrock, Lambda, API Gateway & S3

![Chatbot Architecture](https://i.postimg.cc/mkRHgr8X/architectural-diagram.png)

Welcome to the **EZEGS-AI-ChatBot** project! This guide will walk you through building a powerful, **serverless** AI chatbot using Amazon Bedrock's **Titan Text G1 - Express** large language model. This project leverages **AWS Lambda**, **API Gateway**, and **Amazon S3** to deliver a real-time conversational experience with no servers to manage.

> 🎓 If you're a **visual learner**, this project is a great start! You’ll get step-by-step guidance to deploy it **100% on the AWS Free Tier**.

---

## 🧠 Features

- Uses **Amazon Bedrock** Titan model to generate AI responses
- Entirely **serverless** architecture
- Deployed on **AWS Free Tier**
- Secure API exposed via **API Gateway**
- Stylish front-end chat interface built with **HTML, CSS, and JavaScript**
- Hosted via **Amazon S3 Static Website**

---

## 🔎 Architecture Overview

1. **Users** interact with the chatbot via a web UI or direct API call.
2. **API Gateway** receives the HTTP POST request and forwards it to Lambda.
3. **Lambda Function** invokes the **Amazon Bedrock** Titan model using a secure **IAM Role**.
4. AI **response** is returned back to the user.
5. Frontend is served via **Amazon S3** static website hosting.

> 📌 [Click to view full-size architecture diagram](https://i.postimg.cc/mkRHgr8X/architectural-diagram.png)

---

## 🛠️ Tech Stack

- 🧠 Amazon Bedrock (Titan Text G1 - Express)
- 🖥️ AWS Lambda (Python 3.12)
- 🌐 Amazon API Gateway (REST API)
- 🗂️ Amazon S3 (Static Website Hosting)
- 💻 HTML + CSS + JavaScript (No frameworks)

---

## 🚀 Project Setup & Deployment Guide

### ➡️ Step 1: Enable Amazon Bedrock Access

1. Open **Amazon Bedrock** in the AWS Console.
2. Request access to: `amazon.titan-text-express-v1`.
3. Bedrock is GA (generally available), but **us-east-1 (N. Virginia)** is recommended for compatibility.

![Bedrock Access UI](https://i.postimg.cc/bwMS2gm2/439894174-d86d2963-1c01-4fe6-a215-12817e17f1e3.png)

---

### ➡️ Step 2: Create IAM Role for Lambda

1. Go to **IAM > Roles > Create Role**
2. **Trusted Entity Type**: AWS Service → Lambda
3. **Permissions**:
   - `AmazonBedrockFullAccess`
   - `CloudWatchLogsFullAccess`
4. Name it: `chatBotLambdaRole`
5. Click **Create Role**

---

### ➡️ Step 3: Create the Lambda Function

1. Go to **Lambda > Create function**
2. **Function name**: `chatbotlambda`
3. **Runtime**: Python 3.12
4. Paste your code into `lambda_function.py`

#### ✅ Lambda Function Responsibilities

- Accepts a user message
- Sends it to the Bedrock Titan model
- Returns the AI-generated response

---

### ➡️ Step 4: Set Up API Gateway

1. Go to **API Gateway > REST API > Build**
2. Name your API: `chatbot-api`
3. Create a **Resource**: `/chat` → Enable **CORS**
4. Add **POST Method**:
   - Integration type: Lambda Function
   - Region: `us-east-1`
   - Enable **Lambda Proxy Integration**
5. Deploy the API:
   - Stage name: `dev`

💡 **Test your endpoint** using Postman or `curl`:

```bash
curl -X POST https://your-api-id.execute-api.us-east-1.amazonaws.com/dev/chat \
-H "Content-Type: application/json" \
-d '{"message": "Hello"}'
````

---

### ➡️ Step 5: Build the Frontend Chat UI

1. Create an `index.html` file using basic HTML/CSS/JavaScript
2. Replace the `fetch` URL or endpoint in your JavaScript with:

```
https://your-api-id.execute-api.us-east-1.amazonaws.com/dev/chat
```

> 💬 Keep it lightweight and framework-free for S3 hosting.

---

### ➡️ Step 6: Deploy Frontend to S3 Static Website

1. Go to **Amazon S3 > Create Bucket**

   * Name it: `myaichatbotdemo` (must be globally unique)
   * Uncheck **Block all public access**
2. Upload `index.html`
3. Go to **Properties > Static Website Hosting**:

   * Enable static hosting
   * Set `index.html` as index document
4. Set **Bucket Policy**:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

> 🔁 Replace `your-bucket-name` with your actual bucket name.

5. Copy the **S3 Object URL** and open it in your browser.

---

## 🧪 Demo & Testing

* Visit your chatbot via the S3 URL
* Ask questions and get real-time responses
* Responses are powered by **Amazon Bedrock**

## 🧪 Demo & Testing

- Visit your chatbot via the S3 URL
- Ask questions and get real-time responses
- Responses are powered by **Amazon Bedrock**

> 🖼️ Live Chatbot Interface  
![EZEGS AI Chatbot Demo](https://i.postimg.cc/PJRvzMdc/Opera-Snapshot-2025-08-05-041055-ezegs-ai-chatbot-s3-us-east-1-amazonaws-com.png)


---

## 🧼 Clean Up Resources

To avoid AWS charges after testing:

* ❌ Delete the S3 bucket
* ❌ Delete the Lambda function
* ❌ Delete the API Gateway
* ❌ Delete the IAM Role
* ❌ Revoke Amazon Bedrock access (optional)

---

## 📚 Learning Resources

* [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
* [AWS Lambda Docs](https://docs.aws.amazon.com/lambda/)
* [API Gateway CORS Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html)
* [S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)

---

## 🏁 Final Result

You now have a fully functional **serverless AI chatbot** powered by **Amazon Bedrock**!

* 🎯 No server management
* 🧠 LLM-powered responses (Titan)
* 💸 Free Tier friendly

---

## 📷 Screenshots

> Add your own screenshots here:

* ✅ Chat UI preview
* ✅ API Gateway test
* ✅ Lambda logs
* ✅ S3 website link

---

## 📩 Contact & Contributions

Have questions, feedback, or want to contribute?

* 🧑‍💻 GitHub: [@BishopDavid7](https://github.com/BishopDavid7)
* 📧 Email: [p.fonjock@gmail.com](mailto:p.fonjock@gmail.com)
* 🌐 Portfolio: Coming Soon

---

> Built with 💙 on AWS by [@BishopDavid7](https://github.com/BishopDavid7)

```

---

✅ You can now:

- Save this as `README.md` in your GitHub repo.
- Add the `lambda_function.py` and `index.html` files alongside it.
- Push everything to GitHub or zip the project for sharing.

