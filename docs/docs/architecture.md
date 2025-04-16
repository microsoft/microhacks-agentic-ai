# Solution Architecture

In this workshop, you will create the Contoso Sales Assistant: a conversational agent designed to answer questions about sales data, generate charts, and download data files for further analysis.

## Components of the agent

This agent is built on Microsoft Azure services. Your lab instructor may have provisioned these resources for you ahead of time. 

### Generative AI model
 The underlying Large Language Model (LLM) powering this app is the [Azure OpenAI gpt-4o](https://learn.microsoft.com/azure/ai-services/openai/concepts/models?tabs=global-standard%2Cstandard-chat-completions#gpt-4o-and-gpt-4-turbo){:target="_blank"} large language model (LLM). 


### Software Development Kit (SDK)

The app is built in Python using the [Azure AI Agents Service SDK](https://learn.microsoft.com/python/api/overview/azure/ai-projects-readme?view=azure-python-preview&context=%2Fazure%2Fai-services%2Fagents%2Fcontext%2Fcontext){:target="_blank"}. This SDK makes use of the [Code Interpreter](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/code-interpreter?view=azure-python-preview&tabs=python&pivots=overview) and [Function Calling](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/function-calling?view=azure-python-preview&tabs=python&pivots=overview) features of the Azure AI Agents service.

### Database

The app is informed by the Contoso Sales Database, a [SQLite database](https://www.sqlite.org/) containing 40,000 rows of synthetic data. Upon startup, the app reads the sales database schema, product categories, product types, and reporting years, then incorporates this data into the Azure AI Agent Service’s instruction context.

### Vector Store

We will provide the agent with product information as a PDF file to support its queries. The agent will use the "basic agent setup" of the [Azure AI Agent Service file search tool](https://learn.microsoft.com/azure/ai-services/agents/how-to/tools/file-search?tabs=python&pivots=overview) to find relevant portions of the document with vector search and provide them to the agent as context.

### Control Plane

The app and its architectural components are managed and monitored using the [Azure AI Foundry](https://ai.azure.com) portal, accessible via the browser.

## Extending the Workshop Solution

The workshop solution is highly adaptable to various scenarios, such as customer support, by modifying the database and tailoring the Azure AI Agent Service instructions to suit specific use cases. It is intentionally designed to be interface-agnostic, allowing you to focus on the core functionality of the AI Agent Service and apply the foundational concepts to build your own conversational agent.



