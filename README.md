# **Google Gemini-1.5-Pro Chat App**
A **simple yet powerful chatbot** built using **Google Gemini-1.5-Pro**, **LangChain**, and **Streamlit**. This project demonstrates how to use LangChain’s **implicit chaining (`|` operator)** to process user queries efficiently.

---

## **Features**
**Uses LangChain for modular AI workflows**  
**Powered by Google Gemini-1.5-Pro** for intelligent responses  
**Streamlit UI** for easy user interaction  
**Dynamic prompt handling** using `ChatPromptTemplate`  
**Automatic output parsing** for clean responses  

---

## **Prerequisites**
Ensure you have the following installed:
- **Python 3.8+**
- **Google API Key** (for Gemini)
- **Streamlit** (`pip install streamlit`)
- **LangChain & Dependencies**

---

## **Environment Setup:**
* py -3.10 -m venv myvenv
    
* myvenv\Scripts\activate

* python -m pip install --upgrade pip
* pip install --upgrade --quiet  langchain-google-genai pillow
* pip install streamlit
* pip install python-dotenv

* Get a Google API key: Head to https://ai.google.dev/gemini-api/docs/api-key to generate a Google AI API key.

---

## **Code Explanation**
### **1. Load Dependencies**
```python
import streamlit as st
from dotenv import load_dotenv
from langchain_core.prompts import ChatPromptTemplate
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.output_parsers import StrOutputParser
```
- **Streamlit (`st`)** → Creates a simple UI for the chatbot.
- **LangChain (`ChatPromptTemplate`, `ChatGoogleGenerativeAI`, `StrOutputParser`)** → Handles AI logic.
- **dotenv (`load_dotenv`)** → Loads API key securely from `.env`.

---

### **2. Load API Key**
```python
load_dotenv()
```
- Reads environment variables, including the **Google Gemini API Key**.

---

### **3. Define Gemini LLM**
```python
llm = ChatGoogleGenerativeAI(
    model="gemini-1.5-pro",
    temperature=0,
    max_tokens=None,
    timeout=None,
    max_retries=2,
)
```
- **Model:** `"gemini-1.5-pro"`
- **Temperature:** `0` (makes responses deterministic)
- **Retries:** `2` (ensures resilience to failures)

---

### **4. Create a Prompt Template**
```python
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a chatbot"),
    ("human", "Question:{question}")
])
```
- **System Message:** Sets chatbot behavior.
- **Human Message:** Formats user input dynamically.

---

### **5. Define Output Parser**
```python
output_parser = StrOutputParser()
```
- Extracts **clean text** from Gemini’s response.

---

### **6. Create the Processing Chain**
```python
chain = prompt | llm | output_parser
```
- **`|` operator** chains prompt → Gemini LLM → Output parser.
- **Avoids need for `LLMChain`**, making it more compact.

---

### **7. Streamlit UI**
```python
st.title('Langchain Chat App With Gemini')
input_text = st.text_input("Enter your question here")
```
- Displays **app title**.
- Provides an **input box** for user queries.

---

### **8. Execute Chatbot Logic**
```python
if input_text:
    st.write(chain.invoke({'question': input_text}))
```
- Sends user question to Gemini via LangChain.
- Displays **formatted AI response**.

---

## **Running the App**
To launch the Streamlit app, run:
```bash
streamlit run gemini_app_qa.py
```
This will open the chatbot in your **browser**.

---

## **References**
- [LangChain Documentation](https://python.langchain.com/)
- [Google Gemini API](https://ai.google.dev/)
- [Streamlit Documentation](https://docs.streamlit.io/)

---

### **License**
This project is licensed under **MIT License**.
