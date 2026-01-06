# 🎫 SmartTicket — NLP-Based Automated Customer Support Ticket Classification System

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

SmartTicket is an end-to-end, production-oriented NLP-based customer support ticket classification system that automatically routes incoming support requests to the correct department using deep learning.

This project closely mimics **real enterprise support automation pipelines** used by SaaS companies, IT service providers, and large-scale platforms to reduce manual triage effort and improve response times.

> 🚫 Not a toy sentiment analysis or spam classifier  
> ✅ A **full ML + API + Database system** with real operational relevance

---

## ⭐ Key Features

- 🔹 Deep learning–based **multi-class text classification**
- 🔹 **BiLSTM / GRU architecture** (industry-accepted NLP baseline)
- 🔹 **FastAPI backend** for real-time inference
- 🔹 **MongoDB Atlas** as the system of record
- 🔹 Stores raw tickets, predicted queue, confidence, and timestamps
- 🔹 **Swagger UI** for API testing and documentation
- 🔹 Optional **Streamlit web interface** for interactive demos
- 🔹 Designed for **cloud & Hugging Face deployment**

---

## 🧠 Problem Statement

Modern customer support teams receive thousands of tickets daily related to:

- 🔧 Technical issues
- 💳 Billing & payments
- 🔐 Account access
- 📦 Product support
- 📞 Sales & pre-sales
- 📮 General inquiries

### The Challenge

❌ **Manual ticket triaging** is:
- Time-consuming
- Costly
- Error-prone
- Difficult to scale

### The Solution

**SmartTicket** automatically:
1. ✅ Analyzes ticket subject + body text
2. ✅ Predicts the most relevant support queue
3. ✅ Stores predictions for analytics & workflow automation

This enables:
- ⚡ **Faster response times**
- 🧑‍💻 **Reduced human workload**
- 📊 **Data-driven support optimization**

---

## 📊 Dataset

| Property | Details |
|----------|---------|
| **Source** | Kaggle — Customer Support Ticket Classification |
| **Type** | Realistic customer support emails |
| **Language** | English |
| **Structure** | Subject + Body + Queue |
| **Preprocessing** | Minimal (production-realistic) |

### Target Labels (Queues)

- 💻 **Technical Support**
- 💰 **Billing & Payments**
- 🧑‍💼 **Customer Service**
- 🖥️ **Product Support**
- 🌐 **IT Support**
- 📞 **Sales / Pre-Sales**
- 📮 **General Inquiry**

This dataset reflects **real enterprise helpdesk routing logic**, making it ideal for industrial NLP applications.

---

## 🏗️ System Architecture

```
Customer Ticket
(Subject + Body)
        │
        ▼
Text Preprocessing
(Tokenization & Padding)
        │
        ▼
Embedding Layer
        │
        ▼
BiLSTM / GRU
(Context Understanding)
        │
        ▼
Softmax Classifier
(Queue Prediction)
        │
        ▼
FastAPI Backend
        │
        ▼
MongoDB Atlas
(Persistent Storage)
        │
        ▼
Analytics / UI / Dashboard
```

### Architecture Highlights

- **Text Fusion**: Subject + Body for richer context
- **Sequence Modeling**: Captures real customer language patterns
- **API-First Design**: Ready for integration with real systems
- **Database-Centric**: Every prediction is stored and traceable

---

## 🛠️ Tech Stack

### Machine Learning
- **Framework**: TensorFlow / Keras
- **Model**: BiLSTM / GRU
- **Text Processing**: Tokenization, Padding, Embeddings
- **Evaluation**: Accuracy, Precision, Recall, F1-score

### Backend & Infrastructure
- **API**: FastAPI
- **Server**: Uvicorn (ASGI)
- **Database**: MongoDB Atlas (Cloud)
- **Data Handling**: NumPy, Pandas

### Frontend / Deployment
- **Web UI**: Streamlit (optional)
- **Hosting**: Hugging Face Spaces (planned)
- **Docs**: Swagger UI

---

## 📈 Model Performance (Representative)

| Metric | Score |
|--------|-------|
| **Training Accuracy** | ~90–92% |
| **Validation Accuracy** | ~87–89% |
| **Test Accuracy** | ~85–88% |

### Key Training Insights

- ✔ Stable convergence within **10–15 epochs**
- ✔ Strong generalization without aggressive cleaning
- ✔ Balanced performance across queues
- ✔ Realistic confusion between overlapping departments

---

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- MongoDB Atlas account (free tier works)
- pip or conda

### 1️⃣ Clone Repository
```bash
git clone https://github.com/RansiluRanasinghe/SmartTicket-NLP-Customer-Support.git
cd SmartTicket-NLP-Customer-Support
```

### 2️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 3️⃣ Configure MongoDB
Create a `.env` file:
```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/
DATABASE_NAME=smartticket
COLLECTION_NAME=tickets
```

### 4️⃣ Train Model (Optional)
```bash
jupyter notebook
# Run training notebook
```

### 5️⃣ Start API Server
```bash
uvicorn main:app --reload
```

### 6️⃣ Open Swagger UI
👉 [http://localhost:8000/docs](http://localhost:8000/docs)

---

## 📡 API Endpoints

### Health Check
```http
GET /health
```

**Response:**
```json
{
  "status": "healthy",
  "model": "loaded",
  "database": "connected"
}
```

---

### Classify Ticket
```http
POST /classify
```

**Request Body:**
```json
{
  "subject": "Payment failed",
  "body": "My card was charged but the transaction failed"
}
```

**Response:**
```json
{
  "predicted_queue": "Billing & Payments",
  "confidence": 0.93,
  "timestamp": "2024-01-06T10:30:00Z"
}
```

---

### Retrieve Tickets
```http
GET /tickets?limit=10
```

**Response:**
```json
{
  "tickets": [
    {
      "ticket_id": "507f1f77bcf86cd799439011",
      "queue": "Billing & Payments",
      "confidence": 0.93,
      "timestamp": "2024-01-06T10:30:00Z"
    }
  ],
  "total": 10
}
```

---

## 🧪 Example Usage

### cURL
```bash
curl -X POST "http://localhost:8000/classify" \
  -H "Content-Type: application/json" \
  -d '{
    "subject": "Payment failed",
    "body": "My card was charged but the transaction failed"
  }'
```

### Python
```python
import requests

url = "http://localhost:8000/classify"
data = {
    "subject": "Can't login",
    "body": "Password reset link not working"
}

response = requests.post(url, json=data)
print(response.json())
```

### JavaScript
```javascript
const response = await fetch('http://localhost:8000/classify', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    subject: 'Refund request',
    body: 'I want to cancel my subscription and get a refund'
  })
});

const result = await response.json();
console.log(result);
```

---

## 🌐 Streamlit Web Interface (Optional)

An interactive web UI for ticket classification:

- ✅ Enter ticket subject and body
- ✅ View predicted queue & confidence
- ✅ Designed for **Hugging Face Spaces** deployment
- ✅ Ideal for demos and recruiter walkthroughs

### Run Streamlit App
```bash
streamlit run app.py
```

---

## 🔮 Future Enhancements

- [ ] **Multi-language** ticket classification
- [ ] **Priority prediction** (Low / Medium / Critical)
- [ ] **Sentiment analysis** integration
- [ ] **Admin analytics dashboard**
- [ ] **Email ingestion automation**
- [ ] **Active learning loop** for continuous improvement

---

## 📌 Why This Project Stands Out

This project clearly outperforms:
- ❌ Sentiment analysis demos
- ❌ Spam classifiers
- ❌ Notebook-only ML projects

### What Makes It Different

✔ **End-to-end NLP system**  
✔ **Production-ready API**  
✔ **Database-backed ML workflow**  
✔ **Real enterprise use case**  
✔ **Interview-ready architecture**  
✔ **Cloud & deployment aware**

### Skills Demonstrated
- NLP model development
- API design and implementation
- Database integration
- System architecture
- Production ML thinking

---

## 🎯 Use Cases

This system can be adapted for:
- **SaaS companies** — Customer support automation
- **E-commerce** — Order inquiry routing
- **Healthcare** — Patient inquiry triage
- **Finance** — Support request categorization
- **Education** — Student query management

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Connect

**Ransilu Ranasinghe**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ransilu-ranasinghe-a596792ba)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/RansiluRanasinghe)
[![Email](https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:dinisthar@gmail.com)

**Interests:**  
NLP • Machine Learning • Backend Engineering • Production ML Systems

---

<div align="center">

**⭐ If you find this project valuable, consider giving it a star!**

**Built with 🧠 TensorFlow, ⚡ FastAPI, 🍃 MongoDB & 🎨 Streamlit**

</div>
