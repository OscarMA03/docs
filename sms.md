# CONFIGURATION POST FOR COMPANIES
## Getting Configurations
**Endpoint:** `POST /api/config?companyId=123`

### Description
Retrieves company configuration settings for initializing the AI agent with company-specific information.

### Request Body
```json
{
    "companyID": int - [required] - Unique identifier for the company,
    "companyAuth": string - [required] - Authentication token/API key,
    "companyUrl": string - [required] - Company's API endpoint,
    "companyName": string - [required] - Official business name,
    "companyNumber": string - [required] - Callback number for follow-ups,
    "serviceLabeltype": string - [optional] - What to call the appointment (per Jonathan),
    "aiDisclosure": boolean - [optional] - Whether agent announces it's AI,
    "knowledgeBase": string - [optional] - Knowledge base URL/reference,
    "businessHours": string - [optional] - When to offer appointments,
    "serviceAreas": string - [optional] - Geographic restrictions,
    "handOff": string - [optional] - Create task to callback at later time
}
```

### Response
```json
{
    "success": boolean,
    "data": { /* config object */ },
    "error": string
}
```

### Questions : 
#### Where are we storing this information?
#### Do we store this information on another database to keep it simple?
#### If stored on Builder Prime DataBase, will there be an API endpoint we hit or will they be able to create a query that will give us all this information? 
#### would each agent have a hardcoded companyId value when hitting the GET api/config?

---

# SMS POST WITH AI SMS AGENT

## Getting Previous Messages
**Endpoint:** `POST /api/prev-messages`

### Description
Retrieves conversation history between customer and company for AI context.

### Request Body
```json
{
    "organizationID": int - [required] - Organization identifier,
    "customerPhoneNumber": string - [required] - Customer's phone number,
    "companyPhoneNumber": string - [required] - Company's phone number,
    "locations": [
        {
            "id": int - [required] - Location identifier,
            "name": string - [optional] - Location name
        }
    ],
    "messages": [
        {
            "id": int - [required] - Message identifier,
            "message": string - [required] - Message content,
            "sentBy": string - [optional] - Sender (customer/company/ai),
            "mediaUrls": string - [optional] - Comma-separated media URLs
        }
    ]
}
```

### Response
```json
{
    "success": boolean,
    "data": {
        "conversationHistory": [],
        "messageCount": int
    },
    "error": string
}
```

---