{
  "nodes": [
    {
      "parameters": {
        "promptType": "define",
        "text": "=Message: {{ $json.Message }}",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        -464,
        -272
      ],
      "id": "893f6a78-7fc6-4e37-a2c7-184416fd1499",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "model": "openrouter/free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        -496,
        32
      ],
      "id": "4a65842f-d3eb-4b8c-a884-d74c5079dfa7",
      "name": "OpenRouter Chat Model",
      "credentials": {
        "openRouterApi": {
          "id": "eeeVXLDiwH7K91l8",
          "name": "OpenRouter account"
        }
      }
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "first",
        "responseMode": "responseNode",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2.1,
      "position": [
        -960,
        -272
      ],
      "id": "63caf3a5-afda-4709-a78f-ed6771713132",
      "name": "Webhook",
      "webhookId": "4beaa9c0-7bf6-4762-9565-895aa7e03691"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "b83c0d86-ab7b-45c1-b652-f59a1a20326b",
              "name": "Message",
              "value": "={{ $json.body.message }}",
              "type": "string"
            },
            {
              "id": "75acfe80-61ea-475d-b34a-fa72b874ba5e",
              "name": "User id",
              "value": "={{ $json.body.userId }}",
              "type": "string"
            },
            {
              "id": "94bcaca9-bcb1-4362-a929-afbc00327e7d",
              "name": "Country",
              "value": "={{ $json.headers['cf-ipcountry'] }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -752,
        -272
      ],
      "id": "3b870e34-4766-4e89-9919-c5a486f0e220",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "respondWith": "json",
        "responseBody": {
          "reply": "={{ $json.output || 'Default reply from n8n' }}"
        },
        "options": {
          "responseCode": 200
        }
      },
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1.5,
      "position": [
        64,
        -288
      ],
      "id": "9621d741-71c5-4bf5-a1ad-6bc0b9ba0e17",
      "name": "Respond to Webhook1"
    }
  ],
  "connections": {
    "AI Agent": {
      "main": [
        [
          {
            "node": "Respond to Webhook1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenRouter Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Webhook": {
      "main": [
        [
          {
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "pinData": {
    "AI Agent": [
      {
        "output": "Hi there! 😊 How can I help you today?"
      }
    ]
  },
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "86d81f670c962873ff00838d1f71a4d53552e327fd745f40e6a14070c5e01c4c"
  }
}
