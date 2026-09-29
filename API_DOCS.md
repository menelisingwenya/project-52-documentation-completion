# Consolidated API Documentation (Final Capstone)

**Emganwini Nedbank Hub | Master Project Portfolio**  
*Production API Specification Reference*

---

## Base URL
- Production: `https://nedbank-smartfin-api.onrender.com/api`
- Local Development: `http://localhost:5000/api`

---

## Authentication
Authentication is implemented using JSON Web Tokens (JWT). Send the token in the `Authorization` header with the Bearer prefix:
```http
Authorization: Bearer <your_jwt_token>
```

---

## Endpoints

### 1. Authentication Endpoints
#### `POST /auth/register`
Creates a new customer or advisor user account.
- **Body**: `{ "email": "user@example.com", "password": "Password123!", "firstName": "Thabo", "lastName": "Ndlovu" }`
- **Response (201 Created)**: Returns `{ success: true, token, user }`.

#### `POST /auth/login`
Authenticates credentials and returns a signed JWT.
- **Body**: `{ "email": "user@example.com", "password": "Password123!" }`
- **Response (200 OK)**: Returns `{ success: true, token, user }`.

#### `GET /auth/me`
Returns details of the currently authenticated user session.
- **Response (200 OK)**: Returns `{ success: true, user }`.

---

### 2. User Resource Endpoints
- `GET /users`: Paginated list of users (requires auth).
- `GET /users/:id`: Specific user profile (requires auth).
- `POST /users`: Admin user creation.
- `PUT /users/:id`: Profile updates.
- `DELETE /users/:id`: Account deactivation/removal.

---

### 3. Financial Advisory Post Endpoints
- `GET /posts`: List all published financial guidance articles with category filters.
- `GET /posts/:id`: Read specific guidance article.
- `POST /posts`: Create post (Advisor/Admin auth required).
- `PUT /posts/:id`: Update article (Author/Admin auth required).
- `DELETE /posts/:id`: Remove article (204 No Content).

---

### 4. AI & RAG Endpoints
#### `POST /ai/chat`
Conversational advisory session.
- **Body**: `{ "message": "Can I withdraw early from a 32-day deposit?", "history": [] }`
- **Response (200 OK)**: Returns `{ success: true, reply, tokens }`.

#### `POST /ai/rag`
Grounded inquiry querying verified institutional knowledge.
- **Body**: `{ "question": "What are the requirements for FLISP housing subsidy?" }`
- **Response (200 OK)**: Returns `{ success: true, question, answer, citations: [...] }`.

#### `POST /ai/summarize`
Strict 3-sentence document distillation.
- **Body**: `{ "text": "Contract or disclosure body...", "temperature": 0.3 }`
- **Response (200 OK)**: Returns `{ success: true, summary, tokens }`.

---

### 5. Conversation History Endpoints
- `GET /conversations`: Retrieve active threads for the user.
- `POST /conversations`: Initialize a new thread.
- `GET /conversations/:id`: Retrieve transcript.
- `POST /conversations/:id/messages`: Append user/advisor message exchange.
