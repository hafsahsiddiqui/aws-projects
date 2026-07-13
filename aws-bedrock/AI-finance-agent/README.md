# AI Finance Agent with Amazon Bedrock
In this project, I built a Bedrock Agent that analyzes my financial data and makes suggestions. I did this project to learn how to use AWS Bedrock Agents.

## Key Services & Concepts

**Tools used:** Amazon Bedrock, Bedrock Agents, Code Interpreter

**Concepts learned:** How AI agents can autonomously write and execute Python code, how to give an agent cross-session memory so it retains context between conversations, and how to iterate on agent instructions to improve its responses over time.

## Challenges & Wins

This project took approximately **1 hour**. The most challenging part was the "secret mission" where I had to teach my agent to remember previous conversations — it didn't work the first time, and I had to go back and redo it. It was most rewarding to see the AI agent write its own Python code and correctly analyze my spending data without me having to write any analysis logic myself.

---

## Step 1: Exploring Amazon Bedrock and Foundation Models

In this step, I navigated to AWS Bedrock, since we're working with Bedrock Agents, and previewed the Bedrock Agents feature.

**Understanding foundation models:** A foundation model is a large AI model trained on a large amount of data. I used Amazon Nova Lite because it's a lightweight, readily available model.

**Discovering Bedrock Agents:** A Bedrock Agent is an AI that can execute tasks based on a foundation model. Unlike a chatbot, it can reason through and execute programmatic tasks.

<img width="2940" height="1912" alt="aws-genai-bedrock-agent_h4t7y1a5" src="https://github.com/user-attachments/assets/3b119932-f44c-4188-958c-1dd68b57a0db" />


## Step 2: Creating the AI Finance Agent

In this step, I created an Amazon Bedrock Agent to act as a personal financial advisor, and enabled it to write and execute Python code.

**Crafting the agent instructions:** I wrote instructions telling the agent to analyze spending data. This matters because the instructions are what the agent bases all of its responses on.

<img width="2940" height="1912" alt="aws-genai-bedrock-agent_q4j6r2m8" src="https://github.com/user-attachments/assets/be124d1b-5d10-40b5-9b46-8829c500ca85" />


## Step 3: Analyzing Spending Data with Code Interpreter

In this step, I uploaded a transactions file and got a spending summary from my agent, along with budget recommendations, then iterated on the agent's instructions for better output.

**How Code Interpreter processed the data:** I uploaded `transactions.csv`. The agent used Code Interpreter to write Python code that analyzed the CSV file, producing an output showing total spending by category.

**Iterating on agent instructions with traces:** I updated the instructions to request a percentage breakdown. The output improved, showing a table with costs displayed to two decimal places along with a percentage breakdown per category.

<img width="2940" height="1912" alt="aws-genai-bedrock-agent_p4r7t9v1" src="https://github.com/user-attachments/assets/46bc8d1e-e598-4471-a281-6fee6a7d972a" />


## Extension: Enabling Cross-Session Agent Memory

In this extension, I enabled memory for my Bedrock Agent. Cross-session memory matters because users might want to ask about content they worked on in a previous session.

**Session summarization vs. full history:** I configured the agent to enable memory. Summarization is useful here because you don't want to pass the entire chat history to the model on every request.

**Testing cross-session recall:** I tested the memory feature, and the agent successfully recalled all three suggestions it had given me in an earlier session.

<img width="2940" height="1912" alt="aws-genai-bedrock-agent_t8h1g5f3" src="https://github.com/user-attachments/assets/728f62c7-6df7-4797-b60e-83ae8812fd8e" />

---

## Wrapping Up

I did this project today to learn how to set up an AI agent in Amazon Bedrock that can write and execute its own Python code, analyze real data autonomously, and retain context across multiple sessions using memory. Another skill I want to learn is how to build a visual AI workflow that classifies and responds to customer emails.
