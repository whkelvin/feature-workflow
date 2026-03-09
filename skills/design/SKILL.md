---
description: Design the implementation plan for a feature - frontend, backend, and API specs
disable-model-invocation: true
---

# Feature Design

You are helping the user create a detailed implementation plan for a feature that has already been explored.

## Arguments

`$ARGUMENTS` is the feature name (kebab-case). If empty, ask the user for the feature name.

## Prerequisites

Read `./feature/<feature-name>/exploration.md` first. If it doesn't exist, tell the user to run `/feature-workflow:explore <feature-name>` first.

## Output Structure

Create the following directory structure under `./feature/<feature-name>/design/`:

```
design/
├── frontend/
│   ├── components/
│   │   └── <component-name>.md    # One file per new/modified component
│   └── keyflow/
│       └── <feature-name>.md      # Feature flow + test strategy
├── backend/
│   ├── db-models/
│   │   └── <model-name>.md        # One file per new/modified table
│   └── endpoints/
│       └── <endpoint-name>/
│           └── implementation.md   # Implementation + testing strategy
└── api/
    └── <endpoint-name>.md          # API specification per endpoint
```

## Frontend Design — for each file, include:

- **Components**: What new components to add? What existing components can be reused? Props, state, and behavior for each.
- **API calls**: What does each API call look like? Any new client-side API code needed? Changes to existing API code?
- **State management**: New state needed? Existing state to rely on? State shape and where it lives.
- **Side effects**: Does this change impact other parts of the UI? State updates after API calls?
- **Notifications**: Should we show notifications after actions complete? What messages?
- **Tests**: E2E tests for the happy path. What to assert.

## Backend Design — for each file, include:

- **Database**: New tables? Modified tables? Full migration details with column types, constraints, indexes.
- **Endpoints**: URL, HTTP method, handler logic step-by-step.
- **Authentication**: What auth mechanism? How is the user identified?
- **Authorization**: Who can call this endpoint? Role/permission checks.
- **Request/Response**: Full request model with validation rules. Response model for each status code.
- **Validation**: How are request models validated? What errors are returned for invalid input?
- **Response codes**: Every possible HTTP status code and when it's returned.
- **Background tasks**: Anything to offload? What triggers them?
- **Logging & error handling**: Debug query logging, exception handling, error response format.
- **Tests**: Unit tests for each endpoint. What to mock, what to assert.

## API Specification — each endpoint file must follow this format:

```markdown
# EndpointName

## Method
GET | POST | PUT | PATCH | DELETE

## URL
/api/v1/resource/:id

## Parameters

### Path Parameters
- `id` (string, required): Resource identifier

### Query Parameters
- `page` (number, optional): Page number

## Request Body

\```typescript
interface CreateResourceRequest {
  name: string;
  description?: string;
}
\```

## Responses

### 200 OK

\```typescript
interface CreateResourceResponse {
  id: string;
  name: string;
  createdAt: string;
}
\```

### 400 Bad Request

\```typescript
interface ErrorResponse {
  error: string;
  details?: string[];
}
\```

## Authentication
look at current code base to see what it uses and asks the user if the same pattern should be used

## Authorization
look at the current permission system in place and asks the user who has access to this endpoint.

## Examples

\```bash
curl -X POST https://api.example.com/api/v1/resource \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{"name": "example"}'
\```
```

## Working Rules — YOU MUST FOLLOW THESE STRICTLY

1. **Ask strictly ONE question at a time.** Never ask multiple questions in the same turn. One question per message, no exceptions.
Use the AskUserQuestion tool for discrete choices throughout this planning process. However, use natural text questions when:
The question is truly open-ended with unlimited valid answers
You need detailed explanations that don't fit 2-4 options
You can't anticipate reasonable options upfront
2. Each question should be a **proposal** for one part of the implementation. Present your proposal and ask the user to confirm or revise. Present multiple proposals when appropriate and allow the user to pick the best one or allow the user to specify more details.
3. Follow this structured design path in order:
   - **API/Endpoint definition**: Propose each endpoint one at a time (URL, method, request/response shape).
   - **Frontend implementation**: Propose components, state, and flows one at a time. Give a summary of the hollistic implementation before showing each proposal.
   - **Database design**: Propose table schemas and migrations one at a time.
   - **Backend implementation**: Propose handler logic, auth, validation one endpoint at a time.
4. After each section is confirmed, write the corresponding files to disk immediately.
5. After all sections are complete, present a summary of all files created.

## If Resuming

If design files already exist, read them and ask the user where they'd like to pick up or revise.
