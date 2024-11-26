# AURA-Health-Wellness-Recommendation-App
The project applies *Google Cloud Vertex AI* for making decisions, namely, sharing practical wellness advice based on the health metrics data (steps, calories, sleep, heart rate, etc.). The *Gemini model* produces hypotheses and checks solutions. This work was completed by Muneeba Ifrah and N. Divya Sri.





[5:21 pm, 26/11/2024] Divya2~~: Building a Health Wellness Recommendation Application on Google Cloud Run
Introduction | Overview
Problem Statement
With the increasing emphasis on health and wellness, users often seek personalized insights to improve their lifestyle. Our challenge was to create an AI-powered Health Wellness Recommendation Application that delivers tailored suggestions to users.

Target Audience
This blog is aimed at developers and cloud enthusiasts with basic knowledge of Python, Flask, and cloud deployment.

Goal
By the end of this blog, you’ll learn how to:

Design a backend using Flask.
Integrate AI-powered recommendations using Google Vertex AI.
Deploy the application on Google Cloud Run without needing Docker.
Design
High-Level Architecture
The project consists of thr…
[5:23 pm, 26/11/2024] muneeba ifrah: # AURA-Health-Wellness-Recommendation-App
The project applies Google Cloud Vertex AI for making decisions, namely, sharing practical wellness advice based on the health metrics data (steps, calories, sleep, heart rate, etc.). The Gemini model produces hypotheses and checks solutions. This work was completed by Muneeba Ifrah and N. Divya Sri.
[5:23 pm, 26/11/2024] Divya2~~: Building a Health Wellness Recommendation Application on Google Cloud Run
Introduction | Overview
Problem Statement
With the growing health and wellness focus, users actively look for personalized suggestions about improving their lifestyle. It was our challenge to build an AI-enabled Health Wellness Recommendation Application that would provide tailored suggestions to users.

Target Audience
This blog is targeted at developers and cloud enthusiasts with an average knowledge of Python, Flask, and cloud deployment.

Goal
By the end of this blog, you’ll learn how to:

Design a backend using Flask.
Integrate AI-powered recommendations using Google Vertex AI.
Deploy the application on Google Cloud Run without needing Docker.
Design
High-Level Architecture
The project consists of three key components:

Frontend: A simple and responsive interface built with HTML, CSS, and JavaScript for user interaction.
Backend: A Flask application that processes user data, interacts with Vertex AI for recommendations, and returns results to the frontend.
Cloud Deployment: The backend is containerized and deployed onto Google Cloud Run for scalability and ease of access.

Design Choices

Google Cloud Run: This is chosen because of its serverless architecture-no need to deal with a server
Vertex AI: Simplified model deployment and management for AI-based recommendations
REST API: Easy, clear communication between frontend and the backend
Prerequisites
Before starting, make sure that you have the following:

Software:
Python 3.8+
Google Cloud SDK installed
Git installed
Accounts & Access:
A Google Cloud account with billing enabled
A Vertex AI model running
 Foundation Knowledge:
Python and Flask
REST APIs Basics
Familiarity with Google Cloud Console
Step-by-Step Instructions
1. Setup the Backend
 Baselining
Initialize a Flask application
Create a flask project with your API endpoints definition.

python
Copy code
from flask import Flask, request, jsonify

app = Flask(_name_)

@app.route('/recommend', methods=['POST'])
def recommend():
    user_data = request.json
    # Process data and invoke AI model
    recommendations = { "suggestions": ["Drink water", "Exercise 30 mins"]
return jsonify(recommendations)

if _name_ == '_main_':
    app.run(debug=True)
Install Dependencies
Create a requirements.txt file with the following:


Copy code
flask
google-cloud-aiplatform
flask-cors
Install them:


bash
Copy code
pip install -r requirements.txt
2. Integration with Google Vertex AI

Authenticate with Google Cloud:
bash
Copy code
export GOOGLE_APPLICATION_CREDENTIALS="path/to/your-service-account.json"
Fetch the model ID and create a function to make predictions:
python
Copy code
from google.cloud import aiplatform

def get_recommendations(user_input):
    client = aiplatform.PredictionServiceClient()
    model_name = "projects/YOUR_PROJECT_ID/locations/YOUR_REGION/models/YOUR_MODEL_ID"
    response = client.predict(model=model_name, instances=[user_input])
return response.predictions
3. Deploy the Backend to Google Cloud Run

Containerize the Application
Create a Dockerfile:

Dockerfile
Copy code
FROM python:3.8-slim
WORKDIR /app
COPY. .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
Use Google Cloud Build
Use Google Cloud Build instead of local Docker to containerize and push the image:

bash
Copy code
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/health-app:latest
Deploy to Cloud Run
Deploy the image:

bash
Copy code
gcloud run deploy health-app --image gcr.io/YOUR_PROJECT_ID/health-app:latest --platform managed --allow-unauthenticated
4. Connect Frontend and Backend

In your JavaScript frontend, use fetch to call the API:
javascript
Copy code
fetch('https://YOUR_CLOUD_RUN_URL/recommend', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(userData)
})
.then(response => response.json())
.then(data => console.log(data));
Result / Demo
Expected Outcome
After completing the steps:

Your application will take user data as input and provide personalized health recommendations.
Users will use the frontend, which will send data to a backend API on Google Cloud Run.
For example,
User types "I feel tired all the time."
App suggests: "Increase your water intake. Consider vitamin D supplements."
What's Next?
Implement user authentication with session management.
Improve the AI model by providing more training data for better recommendations.
Deploy the frontend as a static web app on Google Cloud Storage.
End
This two-day project demonstrated how to build and deploy a full-stack application using Google Cloud Run and Vertex AI. With this experience, we’re excited to enhance our application further and share it with users globally.
