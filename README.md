# Alboost
– An interactive AI-powered marketing workflow platform that automates campaign strategy, execution, and performance tracking.

## 🌟 Features  
- **AI-Generated Campaign Strategies** – AI analyzes user goals & generates optimized marketing plans.  
- **Approval Workflow** – Users approve/refine AI-generated strategies before execution.  
- **Service Integrations** – Connect Google Analytics, Twitter, and Discord for data-driven marketing.  
- **Automated Execution** – AI handles influencer outreach, social media scheduling, and campaign deployment.  
- **Performance Tracking** – Real-time engagement metrics & AI-powered insights for next steps.  

## 🛠️ Tech Stack  
- **Bubble.io** (Frontend & MVP)  
- **n8n** (Backend automation)  
- **Google Cloud Platform** (Optional - API hosting)  

## 🌐 Live MVP  
https://foralindor24.bubbleapps.io/version-test/ai_landing_page_2?debug_mode=true

## 📡 API Documentation  

🧩 Overview
The workflow is designed to:

Receive a POST request.
Process data with a language model.
Send results to a Telegram chat.
Schedule tweets based on the processed data.
🌐 Endpoints
1. Webhook Endpoint
URL
/campaign-request

Method
POST

Description
This endpoint accepts a POST request and triggers the n8n workflow.

Parameters
projectType: The type of the project.
goal: The goal of the project.
Response
The response is set to lastNode, returning the output from the final node in the workflow.

🛠️ Workflow Nodes
1. Webhook
Type: n8n-nodes-base.webhook
ID: 5121e568-dcba-423d-bd7b-c9e2dda633b7
Description: Receives the initial POST request to trigger the workflow.

3. Basic LLM Chain
Type: @n8n/n8n-nodes-langchain.chainLlm
ID: 17e76b0d-2781-4da4-9dc5-731099b7f41a
Description: Processes input data using a language model to generate a marketing strategy.
Parameters:
promptType: define
text: Based on the project type {{ $json.projectType }} and goal {{ $json.goal }}, analyze Web2 & Web3 market trends and suggest a marketing strategy. Keep it short.
messages: Contains the system message.

5. OpenAI Chat Model
Type: @n8n/n8n-nodes-langchain.lmChatOpenAi
ID: d3943c2d-345f-4f83-9ed1-a044dfba186c
Description: Uses OpenAI Chat Model to generate responses.
Credentials: OpenAi account

7. Telegram
Type: n8n-nodes-base.telegram
ID: ddd53c5b-2300-4a42-85aa-4aef0ad9a690
Description: Sends the generated strategy to a Telegram chat.
Parameters:
chatId: 299206419
text: 🔹 AI Strategy Proposal 🔹 \n{{ $json["text"] }}
replyMarkup: inlineKeyboard
inlineKeyboard: Contains "Yes" and "No" buttons.

9. Telegram Trigger
Type: n8n-nodes-base.telegramTrigger
ID: c0ed4a1e-b743-4862-ac0e-6a619fdfb315
Description: Listens for updates from the Telegram chat.
Parameters:
updates: callback_query, inline_query, message

11. Switch
Type: n8n-nodes-base.switch
ID: f0a19b24-acae-4fbc-be8e-d1db30256b54
Description: Switches workflow based on user response ("Yes" or "No").

13. Edit Fields
Type: n8n-nodes-base.set
ID: 315a835c-b728-4522-b933-4a541a6c6b44
Description: Edits the fields for subsequent steps.
Parameters:
assignments: Contains the tweets to be scheduled.

15. Loop Over Items
Type: n8n-nodes-base.splitInBatches
ID: 996c07ed-757a-4795-9aec-43f4f1837063
Description: Loops over items and processes them in batches.

17. Wait
Type: n8n-nodes-base.wait
ID: 427ab84e-7baf-4197-81f8-6bc9fe26aad2
Description: Waits until a specified time before proceeding.
Parameters:
resume: specificTime
dateTime: {{$json["scheduledTime"]}}

19. X (Twitter)
Type: n8n-nodes-base.twitter
ID: c591a8c3-766b-41ca-afc8-f26b41aae9ec
Description: Posts tweets to Twitter.
Credentials: X account

21. Replace Me
Type: n8n-nodes-base.noOp
ID: e9a68b44-d4c9-4f60-9cf7-c658a4d24551
Description: Placeholder node, replace with actual functionality.


🔗 Node Connections
Webhook → Basic LLM Chain
Basic LLM Chain → Telegram
Telegram Trigger → Switch
Switch → Edit Fields
Edit Fields → Loop Over Items
Loop Over Items → Wait
Loop Over Items → Replace Me
Wait → X (Twitter)
Replace Me → Loop Over Items



## 📄 Setup Instructions  
1️⃣ Access the Web App

Go to the Landing Page.
Click on "Explore Now" to proceed.
2️⃣ Navigate to the Dashboard

You’ll be redirected to the AI-powered dashboard.
Start interacting with the AI agent to receive action plans tailored to your campaign goals.
3️⃣ Approve & Automate Campaigns

Review AI-generated action plans.
Click "Approve" to automate social media campaigns across Twitter, Discord, and Google Analytics.
4️⃣ Integrate Social Media Platforms

Connect your Twitter, Discord, and Google Analytics accounts for seamless execution.
View and manage integrations in the dashboard settings.
5️⃣ Schedule Social Media Posts

Click on "Schedule Posts" to automate content distribution.
The AI will handle post timing and audience targeting based on campaign insights.
