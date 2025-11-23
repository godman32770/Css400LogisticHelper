# Logistic Warehouse Project

This project consists of two main parts:

- **LogisticWarehouseUI**: The frontend web application (React + Vite)
- **backend**: The backend API (FastAPI, OpenRouter, MySQL, LangChain)

---

## Project Structure

```
/frontend   # Frontend (Next)
/backend                 # Backend (FastAPI, MySQL, LangChain)
```

---

## Frontend: LogisticWarehouseUI

A modern React-based web UI for interacting with the chatbot and warehouse system.

### Setup
1. **Install dependencies**
   ```bash
   cd frontend
   npm install
   # or
   yarn install
   ```
2. **Run the development server**
   ```bash
   npm run dev
   # or
   yarn dev
   ```
3. **Open in browser**
   Visit [http://localhost:5173](http://localhost:5173) (default Vite port)

---

## Backend: 

A modular FastAPI project for a chatbot using OpenRouter (OpenAI-compatible API) and MySQL, with LangChain-powered SQL chat and retrieval-augmented memory.

### Features
- **Chatbot API** with FastAPI
- **OpenRouter** (OpenAI-compatible) for LLM responses
- **MySQL** for chat history and context memory
- **LangChain** for natural language to SQL and SQL result explanation
- **Retrieval-augmented**: Chatbot remembers recent conversation from database

### Endpoints
- `POST /chatbot/ask` — Standard chatbot (OpenRouter, remembers last 10 messages)
- `POST /chatbot/db-ask` — Ask about your database (LangChain SQL + OpenRouter, uses chat history from MySQL)

### Environment Variables
Create a `.env` file in the `exxon` directory:
```
OPENROUTER_API_KEY=your_openrouter_api_key
EXXON_DB_URL=mysql+pymysql://user:password@host:port/dbname
```

### Setup
1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
2. **Initialize the database** (creates the Chat table):
   ```bash
   python -m app.init_db
   ```
3. **Run the FastAPI app**
   ```bash
   uvicorn app.main:app --reload
   ```
4. **Test endpoints**
   - Visit [http://localhost:8000/docs](http://localhost:8000/docs) for Swagger UI
   - Use `/chatbot/ask` or `/chatbot/db-ask`

#### Example Request
```json
POST /chatbot/db-ask
{
  "message": "ขอรายการสินค้าพร้อมจัดส่ง 10 อันล่าสุด"
}
```

#### Notes
- Make sure your MySQL server is running and accessible.
- If you get context length errors, reduce the number of chat history messages or limit schema size.
- For LangChain SQL chat, only a few recent messages are used for context to avoid exceeding LLM limits.
