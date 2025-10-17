# LLM Code Deployment System

An automated system that builds, deploys, and evaluates web applications using LLMs.

## Overview
This project automates the process of:
1. Receiving a project brief
2. Generating app code using an LLM
3. Deploying the app to GitHub Pages
4. Notifying an evaluation API

## Features
- LLM-based code generation (Gemini / OpenAI compatible)
- Automated GitHub repository creation and deployment
- Evaluation API notification with retry logic
- Secret-based authentication for security

## Setup
### Prerequisites
- Python 3.13+
- GitHub account with a Personal Access Token
- OpenAI or Gemini API key

### Installation
```bash
pip install -r requirements.txt
```

### Environment Variables
Create a `.env` file with:
```
GITHUB_TOKEN=your_github_token
GITHUB_USERNAME=your_username
OPENAI_API_KEY=your_api_key
SECRET=your_secret
PORT=5000
```

## Running Locally
```bash
python main.py
```
Server will run at: `http://localhost:5000`

## API Endpoints

### POST `/api-endpoint`
Handles build and revise requests.

Example:
```bash
curl http://localhost:5000/api-endpoint   -H "Content-Type: application/json"   -d '{
    "email": "test@example.com",
    "secret": "your_secret_key",
    "task": "test-app",
    "round": 1,
    "brief": "Create a simple calculator app",
    "evaluation_url": "https://httpbin.org/post"
  }'
```

### GET `/health`
Health check endpoint. Returns:
```json
{"status": "healthy"}
```

## Evaluation API
After deployment, your system automatically sends a POST request with:
- repo URL
- pages URL
- commit SHA

to the `evaluation_url` provided in the input.

## Troubleshooting
- Ensure `.env` is correctly configured
- Verify GitHub token and API key are valid
- GitHub Pages may take 1–2 minutes to deploy

## License
MIT License
