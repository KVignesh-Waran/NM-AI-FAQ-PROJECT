# AI FAQ Assistant API

An AI-powered intelligent customer support and FAQ backend built with Node.js, Express, MongoDB, and Google Gemini API.


---

## Features
- **JWT Authentication:** Stored securely in HTTP-only cookies (Access + Refresh tokens).
- **Role-Based Access Control:** Distinct authorization for Users and Admins.
- **Dynamic FAQ Management:** Full CRUD operations for FAQ Q&A pairs.
- **Knowledge Base Parsing:** Upload and parse PDF/Document files using Multer.
- **AI-Powered Search:** Natural language query resolution via Google Gemini API.

---

#Setup & Installation

### 1. Install Dependencies
```bash# 
npm install
```
```
2. Configure Environment Variables (.env)
env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/ai_faq_dk JWT_ACCESS_SECRET=your_access_secret_key JWT_REFRESH_SECRET=your_refresh_secret_key GEMINI_API_KEY=your_gemini_api_key
```
```
3. Start the Server
bash
node index.js
```
Project Structure
```
ai-faq-assistant/
├── index.js
├── uploads/
└── src/
    ├── controllers/
    │   ├── authController.js
    │   ├── faqController.js
    │   └── adminController.js
    ├── middleware/
    │   ├── auth.js
    │   └── upload.js
    ├── models/
    │   ├── User.js
    │   ├── FAQ.js
    │   └── QueryLog.js
    ├── routes/
    │   ├── auth.js
    │   ├── faq.js
    │   └── admin.js
    └── utils/
        ├── db.js
        ├── gemini.js
        └── pdfParser.js

```
API Reference

### 1. Auth Routes (/api/auth)

| Method | Endpoint | Request Body | Description |
| :--- | :--- | :--- | :--- |
| POST | /register | name, email, password | Register a new user |
| POST | /login | email, password | Login user & generate tokens |
| POST | /refresh | — | Refresh expired access token |
| POST | /logout | — | Logout and clear user cookies |

### 2. FAQ & AI Routes (/api/faq) — Requires Login

| Method | Endpoint | Request Body / Notes | Description |
| :--- | :--- | :--- | :--- |
| POST | /ask | question | Submit natural language query to Gemini AI |
| GET | / | — | Fetch all FAQs |
| GET | /categories | — | Fetch all FAQ categories |
| POST | /upload-doc | form-data | Upload PDF/Doc for knowledge base context |
| POST | /feedback | queryId, rating | Submit response feedback |

### 3. Admin Routes (/api/admin) — Admin Role Only

| Method | Endpoint | Request Body | Description |
| :--- | :--- | :--- | :--- |
| POST | /add | question, answer, category | Add a new FAQ pair to database |
| PUT | /update/:id | question, answer, category | Update existing FAQ pair |
| DELETE | /delete/:id | — | Delete an FAQ entry |
| GET | /analytics | — | Get query metrics & unanswered logs |


---

### Cookie Details

| Cookie Name | Expiry Time | Security Flags |
| :--- | :--- | :--- |
| accessToken | 15 Minutes | HttpOnly, SameSite=Strict |
| refreshToken | 7 Days | HttpOnly, SameSite=Strict |

```
