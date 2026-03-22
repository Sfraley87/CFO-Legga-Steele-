# CFO-Legga-Steele-
When called by another workflow, the agent receives a chat input, searches its vector memory for relevant context, generates a response using Claude, and then stores the interaction back into memory. This creates a learning system that builds knowledge over time.

Setup Required:

Configure your Cohere API credentials for the embedding models
Configure your Anthropic API credentials for Claude
The vector store uses an in-memory key called "vector_store_key" - data will persist across executions but will be lost if the workflow is restarted
