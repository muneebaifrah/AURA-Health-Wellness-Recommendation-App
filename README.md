# 🌿 AURA - Health & Wellness Recommendation App

**AURA** is an AI-powered Health & Wellness Recommendation Application that leverages **Google Cloud Vertex AI** (Gemini Model) to provide **personalized wellness advice** based on health metrics such as steps, calories, sleep hours, and heart rate.  

Developed by **Muneeba Ifrah** and **N. Divya Sri**.

---

## 📜 Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Target Audience](#target-audience)
- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [1. Backend Setup](#1-backend-setup)
  - [2. Google Vertex AI Integration](#2-google-vertex-ai-integration)
  - [3. Deploy to Google Cloud Run](#3-deploy-to-google-cloud-run)
  - [4. Frontend Integration](#4-frontend-integration)
- [Expected Outcome](#expected-outcome)
- [What's Next](#whats-next)
- [Authors](#authors)
- [License](#license)

---

## 📖 Overview
With growing interest in health and wellness, users often seek **personalized, data-driven recommendations** to improve their lifestyle.  
**AURA** uses **Google Vertex AI** to process health metrics and return meaningful, actionable advice in real time.

---

## ❓ Problem Statement
People struggle to convert raw health data into meaningful lifestyle actions.  
We aimed to build a **full-stack AI-driven app** that:
- Collects user health data.
- Processes it using AI (Gemini Model).
- Returns personalized suggestions instantly.

---

## 🎯 Target Audience
- Developers & cloud enthusiasts.
- Anyone with basic knowledge of:
  - Python
  - Flask
  - Cloud deployment
  - REST APIs

---

## ✨ Features
✅ AI-powered health recommendations.  
✅ Scalable **Google Cloud Run** deployment.  
✅ Simple frontend for user input & results.  
✅ Works without managing physical servers.  
✅ REST API integration for flexible usage.  

---

## 🏗 Architecture

**High-Level Architecture:**
1. **Frontend:** HTML, CSS, JS — collects user input & displays recommendations.
2. **Backend:** Flask app — processes data & queries Vertex AI.
3. **AI Layer:** Google Vertex AI (Gemini Model) — generates recommendations.
4. **Deployment:** Google Cloud Run — serverless, scalable hosting.

User → Frontend → Flask Backend → Vertex AI → Recommendations → Frontend

yaml
Copy code

---

## 🛠 Tech Stack
- **Frontend:** HTML, CSS, JavaScript
- **Backend:** Python, Flask
- **AI:** Google Vertex AI (Gemini Model)
- **Deployment:** Google Cloud Run
- **Containerization:** Google Cloud Build / Docker
- **API:** REST

---

## 📦 Prerequisites
- Python 3.8+
- Google Cloud SDK installed
- Git installed
- Google Cloud account with billing enabled
- Vertex AI model deployed
- Basic knowledge of Python, Flask, REST APIs, Google Cloud

---

## ⚙️ Setup Instructions

### **1. Backend Setup**
```bash
# Clone the repository
git clone https://github.com/your-username/AURA-Health-Wellness-Recommendation-App.git
cd AURA-Health-Wellness-Recommendation-App

# Initialize Flask app
pip install -r requirements.txt
requirements.txt

nginx
Copy code
flask
google-cloud-aiplatform
flask-cors
app.py

python
Copy code
from flask import Flask, request, jsonify
from google.cloud import aiplatform

app = Flask(__name__)

@app.route('/recommend', methods=['POST'])
def recommend():
    user_data = request.json
    # Example recommendations
    recommendations = {"suggestions": ["Drink water", "Exercise 30 mins"]}
    return jsonify(recommendations)

if __name__ == '__main__':
    app.run(debug=True)
2. Google Vertex AI Integration
bash
Copy code
# Authenticate
export GOOGLE_APPLICATION_CREDENTIALS="path/to/your-service-account.json"
Prediction Function

python
Copy code
def get_recommendations(user_input):
    client = aiplatform.PredictionServiceClient()
    model_name = "projects/YOUR_PROJECT_ID/locations/YOUR_REGION/models/YOUR_MODEL_ID"
    response = client.predict(model=model_name, instances=[user_input])
    return response.predictions
3. Deploy to Google Cloud Run
Dockerfile

dockerfile
Copy code
FROM python:3.8-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
Build & Deploy

bash
Copy code
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/health-app:latest
gcloud run deploy health-app --image gcr.io/YOUR_PROJECT_ID/health-app:latest --platform managed --allow-unauthenticated
4. Frontend Integration
Example API call:

javascript
Copy code
fetch('https://YOUR_CLOUD_RUN_URL/recommend', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify(userData)
})
.then(res => res.json())
.then(data => console.log(data));
🎬 Expected Outcome
Users input their health data.

Backend processes it via Vertex AI.

Personalized recommendations are returned instantly.

Example:

Input: "I feel tired all the time."

Output: "Increase your water intake. Consider vitamin D supplements."

🚀 What's Next
Implement user authentication.

Train model with larger datasets for better accuracy.

Host frontend as a static site on Google Cloud Storage.

👩‍💻 Authors
Muneeba Ifrah
N. Divya Sri
@
📄 License
This project is licensed under the MIT License. 
