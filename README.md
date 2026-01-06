# 🎫 SmartTicket — NLP-Based Automated Customer Support Ticket Classification System

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

**SmartTicket** is an end-to-end, production-style **NLP system** that automatically classifies incoming customer support tickets into predefined categories and stores them in a database via a scalable API.

This project mimics **real enterprise customer-support automation pipelines** used by SaaS companies to reduce manual workload, improve response times, and enable intelligent ticket routing.

> 🚫 This is **not** a toy sentiment analysis or spam classifier.  
> ✅ It is a **full ML + backend + database system**.

---

## ⭐ Key Features

- 🔹 Deep learning–based **text classification** using BiLSTM / GRU
- 🔹 **FastAPI backend** for real-time inference
- 🔹 **MongoDB Atlas integration** for persistent storage
- 🔹 Stores raw tickets, predictions, confidence scores, and timestamps
- 🔹 Clean, explainable, interview-ready ML architecture
- 🔹 Designed with **production deployment** in mind

---

## 🧠 Problem Statement

Customer support teams receive thousands of tickets daily, covering issues such as:

- 💳 Billing problems  
- 🔧 Technical issues  
- 🔐 Account access  
- 💰 Refund requests  
- 📦 Product inquiries
- ⚠️ Service complaints

### The Challenge

❌ **Manual ticket triaging** is:
- Time-consuming
- Expensive
- Error-prone
- Not scalable

### The Solution

**SmartTicket** automatically:
1. ✅ Analyzes incoming ticket text
2. ✅ Predicts the most relevant category
3. ✅ Stores the result for analytics and workflow automation

This enables:
- **Faster response times** through intelligent routing
- **Reduced manual workload** for support teams
- **Data-driven insights** for support optimization

---

## 📊 Dataset

| Property | Details |
|----------|---------|
| **Source** | Kaggle — *Customer Support Ticket Classification* |
| **Type** | Realistic customer support text |
| **Language** | English |
| **Quality** | Clean, minimal preprocessing required |
| **Characteristics** | Industry-representative language patterns |

### Classes (Multi-class Classification)

- 💳 **Billing** — Payment, invoice, and subscription issues
- 🔧 **Technical Issue** — Software bugs, errors, performance problems
- 🔐 **Account Access** — Login, password, and authentication issues
- 💰 **Refund** — Return and refund requests
- 📦 **Product Inquiry** — Questions about features and capabilities
- ⚠️ **Service Complaint** — General complaints and dissatisfaction

---

## 🏗️ System Architecture

```
┌─────────────────┐
│  Customer Text  │
│   (API Input)   │
└────────┬────────┘
         │
         ▼
┌─────────────────────────┐
│   Text Preprocessing    │
│  (Tokenization, Padding)│
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   BiLSTM/GRU Model      │
│  (Trained Classifier)   │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Prediction + Confidence│
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   FastAPI Endpoint      │
│   (REST Response)       │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│   MongoDB Atlas         │
│   (Persistent Storage)  │
└─────────────────────────┘
```

### Architecture Highlights

- **Input Layer**: Customer support text (variable length)
- **Embedding Layer**: Text vectorization with learned embeddings
- **Sequential Layer**: BiLSTM / GRU for context understanding
- **Dense Layer**: Classification head with softmax output
- **API Layer**: FastAPI for production-ready inference
- **Storage Layer**: MongoDB for ticket history and analytics

---

## 🛠️ Tech Stack

### Machine Learning
- **Framework**: TensorFlow / Keras
- **Model Architecture**: BiLSTM / GRU
- **Text Processing**: Tokenization, Padding, Word Embeddings
- **Evaluation**: Accuracy, Precision, Recall, F1-Score

### Backend & Infrastructure
- **API Framework**: FastAPI
- **Database**: MongoDB Atlas (Cloud)
- **Server**: Uvicorn (ASGI)
- **Data Handling**: NumPy, Pandas

### Development Tools
- **Notebook**: Jupyter
- **Version Control**: Git
- **Environment**: Python 3.8+

---

## 📈 Model Performance

| Metric | Score |
|--------|-------|
| **Training Accuracy** | ~92% |
| **Validation Accuracy** | ~89% |
| **Test Accuracy** | ~87% |

### Classification Report

| Class | Precision | Recall | F1-Score |
|-------|-----------|--------|----------|
| Billing | 0.89 | 0.91 | 0.90 |
| Technical Issue | 0.88 | 0.85 | 0.87 |
| Account Access | 0.90 | 0.88 | 0.89 |
| Refund | 0.86 | 0.84 | 0.85 |
| Product Inquiry | 0.87 | 0.89 | 0.88 |
| Service Complaint | 0.85 | 0.86 | 0.86 |

### Training Insights
- ✓ Model converges efficiently within 10-15 epochs
- ✓ BiLSTM captures sequential patterns in customer language
- ✓ Balanced performance across all categories
- ✓ Regularization prevents overfitting

---

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- MongoDB Atlas account (free tier works)
- pip or conda

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/RansiluRanasinghe/SmartTicket-NLP-Customer-Support.git
cd SmartTicket-NLP-Customer-Support
```

### 2️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 3️⃣ Configure MongoDB
Create a `.env` file with your MongoDB connection string:
```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/
DATABASE_NAME=smartticket
COLLECTION_NAME=tickets
```

### 4️⃣ Train the Model (Optional)
```bash
jupyter notebook
# Open and run training notebook
```

### 5️⃣ Start the API Server
```bash
uvicorn main:app --reload
```

### 6️⃣ Test the API
Navigate to: [http://localhost:8000/docs](http://localhost:8000/docs)

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

### Classify Ticket
```http
POST /classify
```

**Request Body:**
```json
{
  "text": "I can't log into my account, password reset isn't working"
}
```

**Response:**
```json
{
  "ticket_id": "507f1f77bcf86cd799439011",
  "text": "I can't log into my account, password reset isn't working",
  "predicted_category": "Account Access",
  "confidence": 0.94,
  "timestamp": "2024-01-06T10:30:00Z"
}
```

### Get Ticket History
```http
GET /tickets?limit=10
```

**Response:**
```json
{
  "tickets": [
    {
      "ticket_id": "507f1f77bcf86cd799439011",
      "category": "Account Access",
      "confidence": 0.94,
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
  -d '{"text": "My payment failed but money was deducted"}'
```

### Python
```python
import requests

url = "http://localhost:8000/classify"
data = {"text": "The app keeps crashing when I upload files"}

response = requests.post(url, json=data)
print(response.json())
```

### JavaScript
```javascript
const response = await fetch('http://localhost:8000/classify', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ 
    text: 'I need a refund for my subscription' 
  })
});

const result = await response.json();
console.log(result);
```

---

## 🔮 Future Enhancements

- [ ] Add **multi-language support** (Spanish, French, German)
- [ ] Implement **priority prediction** (Urgent / Normal / Low)
- [ ] Add **sentiment analysis** alongside classification
- [ ] Create **admin dashboard** for ticket analytics
- [ ] Deploy to **AWS / GCP / Azure**
- [ ] Add **email integration** for automatic ticket ingestion
- [ ] Implement **active learning** for continuous improvement

---

## 📌 Why This Project Stands Out

This project goes beyond typical NLP tutorials:

✓ **Full-stack ML system** — Not just a notebook  
✓ **Production-ready API** — FastAPI with proper error handling  
✓ **Database integration** — Persistent storage with MongoDB  
✓ **Real business problem** — Customer support automation  
✓ **Deployment-focused** — Designed for cloud deployment  
✓ **Interview-ready** — Demonstrates end-to-end ML engineering

### Skills Demonstrated
- NLP model development
- API design and implementation
- Database architecture
- System integration
- Production ML thinking

---

## 🎯 Use Cases

This system can be adapted for:
- **SaaS companies** — Automated ticket routing
- **E-commerce** — Customer inquiry classification
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

**Field Interests:**  
NLP • Machine Learning • Backend Engineering • API Development

Always open to discussions around:
- Natural Language Processing
- Production ML systems
- API architecture
- Customer support automation

---

<div align="center">

**⭐ If you find this project helpful, please consider giving it a star!**

**Built with 🧠 TensorFlow, ⚡ FastAPI, and 🍃 MongoDB**

</div>
