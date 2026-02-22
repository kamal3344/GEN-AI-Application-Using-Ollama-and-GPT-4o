# GEN AI Application using Flask + LangChain + GPT-4o / Ollama

A simple yet powerful Generative AI web application built using:

- 🐍 Python (Flask)
- 🔗 LangChain
- 🤖 OpenAI GPT-4o (Cloud Model)
- 🦙 Ollama (Local LLM Support)
- 🎨 Professional HTML + CSS UI

This project demonstrates how to build a real-time AI assistant using LLMs and integrate it with a web interface.

---

# 📌 Project Overview

This application allows users to:

- Enter a question via a web interface
- Send the question to a Large Language Model (LLM)
- Receive intelligent AI-generated responses
- Display the output dynamically on the webpage

The system supports:

✅ OpenAI GPT-4o (Cloud-based LLM)  
✅ Ollama (Local LLM like Gemma, LLaMA, etc.)

---

# 🏗 Architecture

```

User (Browser)
↓
HTML Form (POST Request)
↓
Flask Backend
↓
LangChain Prompt Template
↓
LLM (GPT-4o or Ollama)
↓
Generated Response
↓
Rendered Back to HTML

```

---

# 📂 Project Structure

```

project/
│
├── app.py
├── .env
├── requirements.txt
└── templates/
└── index.html

````

---

# ⚙️ Technologies Used

## 🔹 Flask
Handles web routing and backend logic.

## 🔹 LangChain
Used for:
- Prompt templating
- LLM chaining
- Structured execution pipeline

## 🔹 ChatOpenAI (GPT-4o)
Cloud-based advanced LLM from OpenAI.

## 🔹 Ollama (Optional)
Local LLM runtime for running models like:
- gemma:2b
- llama3
- mistral

## 🔹 StrOutputParser
Extracts clean string output from LLM response.

---

# 🧠 How the Application Works

## 1️⃣ Prompt Template

```python
prompt = ChatPromptTemplate.from_messages(
    [
        ("system", "You are a helpful assistant."),
        ("user", "Question: {question}")
    ]
)
````

### Why use `from_messages()`?

Because chat models are trained using:

* system role
* user role
* assistant role

This ensures better behavior control.

---

## 2️⃣ LLM Initialization

### OpenAI GPT-4o

```python
llm = ChatOpenAI(model="gpt-4o")
```

Requires OpenAI API key.

---

### Ollama Local Model

```python
llm = Ollama(model="gemma:2b")
```

Requires Ollama running locally.

---

## 3️⃣ Creating Chain

```python
output_parser = StrOutputParser()
chain = prompt | llm | output_parser
```

Pipeline structure:

```
Prompt → LLM → Output Parser
```

---

## 4️⃣ Flask Route

```python
@app.route("/", methods=["GET", "POST"])
def home():
    response = ""
    if request.method == "POST":
        user_input = request.form["question"]
        response = chain.invoke({"question": user_input})
    return render_template("index.html", response=response)
```

Flow:

* User submits question
* Flask receives POST request
* LangChain sends prompt to LLM
* Response returned
* Rendered on webpage

---

# 🔐 Environment Variables (.env)

```
OPENAI_API_KEY=your_openai_key
LANGCHAIN_API_KEY=your_langsmith_key
LANGCHAIN_PROJECT=GENAI_APP
```

---

# ▶️ How to Run the Project

## Step 1: Install Dependencies

```bash
pip install flask langchain langchain-openai langchain-community python-dotenv
```

If using Ollama:

```bash
pip install langchain-ollama
```

---

## Step 2: If Using Ollama

Install Ollama from:
[https://ollama.com](https://ollama.com)

Pull model:

```bash
ollama pull gemma:2b
```

Start server automatically (Ollama runs on port 11434).

---

## Step 3: Run Flask App

```bash
python app.py
```

Visit:

```
http://127.0.0.1:5000/
```

---

# 🎨 Frontend UI Features

* Modern gradient background
* Centered responsive card layout
* Animated response section
* Clean typography
* Mobile-friendly design

---

# 🔄 Switching Between GPT-4o and Ollama

To use GPT-4o:

```python
from langchain_openai import ChatOpenAI
llm = ChatOpenAI(model="gpt-4o")
```

To use Ollama:

```python
from langchain_community.llms import Ollama
llm = Ollama(model="gemma:2b")
```

No other changes required.

---

# 💰 Cost Considerations

| Model  | Cost                           |
| ------ | ------------------------------ |
| GPT-4o | Paid (OpenAI billing required) |
| Ollama | Free (Runs locally)            |

LangChain and Flask are free.

---

# Possible Enhancements

* Add chat history (multi-turn conversation)
* Add loading spinner
* Add streaming responses
* Integrate RAG (Vector DB + Retrieval)
* Add authentication system
* Deploy to cloud (Render, AWS, Azure)

---

# Learning Outcomes

From this project you understand:

* How LLMs are integrated into web apps
* How prompt templates work
* How LangChain chains operate
* Difference between cloud and local models
* Backend-Frontend LLM communication


