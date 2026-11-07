[README.md](https://github.com/user-attachments/files/34524323/README.md)
![](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_tz9xp5km)

## Introducing Today's Project!

In this project, I am building an AI Security Scanner for Python, a CLI tool to detect security vulnerabilities in Python source code. This tool will give me the chance to learn how to integrate the Google API, how to store and manage API keys securely, and how to engineer effective security prompts that can identify flaws such as SQL injection, weak hashing algorithms, and command injection. I picked this project because it is at the intersection of two relevant fields, artificial intelligence and cybersecurity, and my end goal is to package it into a VS Code extension."

### Key tools and concepts

The key tools I used include  Gemini API , Environment Management and Python , python Key concepts I learnt include Secure API Credential Management , Security-Focused Prompt Engineering  and Common security vulnerabilities such as SQL injection, hardcoded secrets, and weak cryptography

### Challenges and wins

I did this project today to learn how to integrate the Google Gemini API into a Python CLI tool, manage API keys securely, and engineer prompts that detect code vulnerabilities like SQL injection, weak hashing, and command injection. Another skill I want to learn is how to build and package a VS Code extension so I can run this security scanner directly inside my code editor

## Generating the Gemini API Key

In this step, I'm setting up my google AI-API-key , i need to do this to connect to Gemini

![Generating the Gemini API Key](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_h3ymx6kd)

## Setting Up the Python Environment

In this step, I'm setting up a Virtual Environment This is important for this project because It keeps all your project's packages isolated from other projects, so they don't interfere with each other

![Setting Up the Python Environment](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_rb4kj7mz)

### Installing the required packages

Now that I have my virtual environment set up I need to Install Packages  mainly python-dotenv for securely storing our Gemini API Key, and google-genai for recognizing Gemini calls written in Python.

![Setting Up the Python Environment](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_pw6dq3ck)

## Connecting to the Gemini API

In this step, I'm connecting to  Gemini by writing a security scanner.py and test it  . This is important because we cant proceed without connecting to Gemini

![Connecting to the Gemini API](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_yw8dt2jh)

### Securing the API key with a .env file

I got an error! My error was forgetting to put in the api-key in .env file ,Having a .env file is important because  hardcoding API keys directly in your code is dangerous. If someone gets your key, their requests count against YOUR quota, potentially blocking your access or incurring charges.

![Connecting to the Gemini API](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_kn3jm8tb)

### Verifying the connection

I verified the connection by running scanner.py Gemini responded with  printing the response the my prompt  which confirmed that the connection is working!

## Engineering the Security Prompt

In this step, I'm writing a security prompt that tells Gemini to analyze code for vulnerabilities  then we will test it This is important because i need Gemini to verify the security of out code

![Engineering the Security Prompt](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_rk9mb7ys)

## Building the File Scanner

In this step, I'm adding file scanning so my scanner can so it can read real Python files from your computer and send their code to Gemini for a full security analysis This is important because we do not have to copy and paste the code in scanner.py every time

![Building the File Scanner](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_jt7px3na)

## Running the Security Audit

In this step, I'm testing my scanner by giving it actual vulnerable code and see what it catches .I'll start with one vulnerability first because we need to check if it really works , then we ramp it up from there !

![Running the Security Audit](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_ub6ry1wf)

### Analyzing the vulnerability report

My scanner detected 4 vulnerabilities  The most surprising vulnerability was 3. Command Injection in process\_input This shows that AI can help with security by catching vulnerabilities befor shipping

## Adding Color-Coded Severity Ratings

In this project extension, I'm adding color-coded severity ratings  This lets the scanner give us insight on what vulnerabilities we should prioritise  so you always know what to fix first.

![Adding Color-Coded Severity Ratings](https://nextwork.ai/mohamed-zegnanie/uploads/7303f8f5-e0c4-5469-8727-b19d56edf6f5_mj7rc2vy)

### How the color system works

I added colour to my responses by  including  severity ratings and using colorama to add color to terminal output.

## Wrapping Up

This project took me approximately a weekend to build. The most challenging part was ensuring the AI generated consistent, predictable outputs—it required iterative prompt engineering to make sure the model reliably flagged vulnerabilities and followed the same reporting format every time
