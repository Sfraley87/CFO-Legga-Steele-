{
  "name": "Boardroom CFO Financial Planning and Cash Runway Analysis Agent",
  "nodes": [
    {
      "parameters": {},
      "id": "1835e14f-9d27-4bce-b0d0-1f66ed0bb1d4",
      "name": "Execute Workflow Trigger",
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "typeVersion": 1.1,
      "position": [
        0,
        0
      ]
    },
    {
      "parameters": {
        "mode": "retrieve-as-tool",
        "memoryKey": {
          "__rl": true,
          "mode": "list",
          "value": "vector_store_key"
        }
      },
      "id": "e6f7998a-a721-4490-88a6-1221bcce00ec",
      "name": "Memory Retrieve",
      "type": "@n8n/n8n-nodes-langchain.vectorStoreInMemory",
      "typeVersion": 1.3,
      "position": [
        352,
        224
      ]
    },
    {
      "parameters": {},
      "id": "d132b624-32c4-43c3-8d36-44d76fa14d0a",
      "name": "Embeddings Cohere",
      "type": "@n8n/n8n-nodes-langchain.embeddingsCohere",
      "typeVersion": 1,
      "position": [
        432,
        432
      ]
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "claude-sonnet-4-5-20250929",
          "cachedResultName": "Claude Sonnet 4.5"
        },
        "options": {}
      },
      "id": "0fe0e55c-4802-4fb6-906a-b7b8dba96455",
      "name": "Anthropic Chat Model",
      "type": "@n8n/n8n-nodes-langchain.lmChatAnthropic",
      "typeVersion": 1.3,
      "position": [
        224,
        224
      ]
    },
    {
      "parameters": {
        "options": {}
      },
      "id": "f38c3876-cec6-4b3c-9432-1aba3d50398c",
      "name": "AI Agent: Legga",
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3,
      "position": [
        256,
        0
      ]
    },
    {
      "parameters": {
        "options": {}
      },
      "id": "45a5ec15-fe48-4ca4-86a6-3a5a6d4491cf",
      "name": "Build Log Entry",
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        720,
        0
      ]
    },
    {
      "parameters": {
        "mode": "insert",
        "memoryKey": {
          "__rl": true,
          "mode": "list",
          "value": "vector_store_key"
        }
      },
      "id": "5e5b23ee-f196-4111-bffd-9f1d1387203a",
      "name": "Memory Insert",
      "type": "@n8n/n8n-nodes-langchain.vectorStoreInMemory",
      "typeVersion": 1.3,
      "position": [
        944,
        0
      ]
    },
    {
      "parameters": {},
      "id": "033e472d-8bf5-4302-8ce3-52f8dda02780",
      "name": "Embeddings Cohere1",
      "type": "@n8n/n8n-nodes-langchain.embeddingsCohere",
      "typeVersion": 1,
      "position": [
        1024,
        224
      ]
    }
  ],
  "pinData": {},
  "connections": {
    "Embeddings Cohere": {
      "ai_embedding": [
        [
          {
            "node": "Memory Retrieve",
            "type": "ai_embedding",
            "index": 0
          }
        ]
      ]
    },
    "Memory Retrieve": {
      "ai_tool": [
        [
          {
            "node": "AI Agent: Legga",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Anthropic Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent: Legga",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Execute Workflow Trigger": {
      "main": [
        [
          {
            "node": "AI Agent: Legga",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent: Legga": {
      "main": [
        [
          {
            "node": "Build Log Entry",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Build Log Entry": {
      "main": [
        [
          {
            "node": "Memory Insert",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Embeddings Cohere1": {
      "ai_embedding": [
        [
          {
            "node": "Memory Insert",
            "type": "ai_embedding",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": true,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "fd97e8ec-74ca-436a-b341-6bfc1a439e6c",
  "meta": {
    "instanceId": "41b9538f904e6a4c613136f9059a403582c2aac64350ef0da9fc201fc16cf494"
  },
  "id": "ZSboX3q8HQPUB95l",
  "tags": []
}
