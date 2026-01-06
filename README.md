# malma-make/zapier-documentation

malma.ai – API Documentation

Official API documentation for the Make.com or Zapier integration with malma.ai.
This document describes the workspace-based endpoints used to retrieve agents and create new leads within a Malma workspace.

🔐 Authentication

Every request must include a Workspace API Token.
This token identifies the workspace and scopes all API operations.

Headers
Authorization: Bearer <workspace_api_token>
Content-Type: application/json

🌍 Base URL
https://app.malma.ai/api

📚 Endpoints
1) GET /api/workspace/agents

Returns all agents belonging to the workspace associated with the provided API token.

Request
GET https://app.malma.ai/api/workspace/agents
Authorization: Bearer <workspace_api_token>

Response
[
  {
    "label": "Agentur Demo malmachen",
    "value": "dde9943e-7b68-429e-a21f-edd28fb6bab5"
  },
  {
    "label": "Autohaus Demo malmachen",
    "value": "7a629724-e582-4320-a7f4-71084e397121"
  },
  {
    "label": "Immobilien Demo malmachen",
    "value": "c7a9d8e9-c25c-4552-9ca5-56a0345c3388"
  },
  {
    "label": "Solar Demo malmachen",
    "value": "de962c9d-a7ed-4706-b9e0-03818d626c62"
  },
  {
    "label": "Lukas",
    "value": "c319752f-6dde-4c0f-9a94-4e16cbee7e86"
  }
]

Error Cases
Status	Meaning
401	Invalid or missing API token
403	Workspace not accessible
500	Internal server error

This endpoint is optimized for Make.com oder Zapier dynamic dropdowns using the label / value response structure.

2) POST /api/workspace/create-lead

Creates a new lead and assigns it to a specific agent within the workspace.

Request
POST https://app.hotcalls.ai/api/workspace/create-lead
Authorization: Bearer <workspace_api_token>
Content-Type: application/json

Body
{
  "agent_id": "c319752f-6dde-4c0f-9a94-4e16cbee7e86",
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "phone": "+49123456789"
}

Response
{
  "success": true,
  "lead_id": "7c91b2bb-6fc5-4cb1-abbd-7eecb8ec7981"
}

Field Requirements
Field	Required	Type / Format
agent_id	✔	UUID
first_name	optional	string
last_name	✔	string
email	optional	valid email
phone	✔	string (E.164 recommended)
Error Cases
{
  "error": "Agent not found",
  "status": 404
}


Common errors:

Error	Reason
Invalid API token format	Token missing or belonging to wrong workspace
Agent not found	Provided agent_id does not exist
Missing fields	Required fields missing
500 Internal error	Unexpected server problem
🔌 Make.com Integration Notes

RPC dynamic dropdowns expect objects in { label, value } format.

Workspace API tokens should be added through a Make API Key Connection.

Error messages are structured for Make.com validation.

Endpoint /api/workspace/agents requires no query parameters, as the workspace is determined automatically via the token.

All sensitive headers (including tokens) should be sanitized in logs.

🧑‍💻 Developer Contact

malmachen GmbH
Email: einfach@malmachen.com

Website: https://malmachen.com
