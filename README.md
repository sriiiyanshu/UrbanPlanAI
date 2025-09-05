
# UrbanInfra - AI-Powered Green Space Analysis Tool 🌳

UrbanInfra is a full-stack web application designed to help urban planners, city officials, and community advocates identify areas underserved by green spaces. It leverages Google's Gemini multimodal AI to analyze satellite imagery, providing an actionable "greenery score" and recommending optimal locations for new parks.

*(Recommendation: Record a short GIF of your application workflow and replace the link above.)*

-----

## \#\# Features 🚀

  * **Interactive Map Selection:** Users can pan, zoom, and draw a rectangle on Google Maps to select any urban or suburban area for analysis.
  * **AI-Powered Image Analysis:** Utilizes the Google Gemini API to understand the contents of the generated satellite image.
  * **Greenery Score:** Generates a quantitative "Greenery Score" from 1 (poor) to 10 (excellent) for the selected zone.
  * **Actionable Recommendations:** If an area is underserved, the AI identifies 1-3 optimal locations for new parks, providing a name and justification for each.
  * **Visual Feedback:** Recommended park locations are visually marked on the satellite image for easy identification.

-----

## \#\# Architecture & Tech Stack 🛠️

This project is built with a modern, scalable, serverless architecture.

  * **Frontend (Vercel):** A static HTML, CSS, and JavaScript frontend that interacts with the Google Maps API and our backend service.
  * **Backend (Google Cloud Run):** A containerized Python/Flask API that handles the core logic of communicating with the Google Gemini API.
  * **Google APIs:** Leverages the **Google Maps API** (JavaScript, Drawing, Static Map) and the **Google Gemini API** (Multimodal Analysis).

<!-- end list -->

```
[ User Browser ]
       |
       v
[ Frontend on Vercel ] --(API Call)--> [ Backend on Google Cloud Run ]
       |                                       |
       v                                       v
[ Google Maps API ]                      [ Google Gemini API ]
```

-----

## \#\# Local Development Setup

To run this project on your local machine, follow these steps.

#### **Prerequisites**

  * [Git](https://git-scm.com/)
  * [Python 3.9+](https://www.python.org/)
  * A code editor like [VS Code](https://code.visualstudio.com/) with a live server extension.

#### **1. Clone the Repository**

```bash
git clone https://github.com/sriiiyanshu/UrbanPlanAI.git
cd UrbanPlanAI
```

#### **2. Backend Setup**

The backend runs as a local Flask server.

```bash
# Navigate to the backend directory
cd gcp-backend

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

# Install dependencies
pip install -r requirements.txt

# Set up environment variables (see API Key Setup below)
cp .env.example .env
nano .env  # Edit the .env file with your keys

# Run the backend server
gunicorn --bind localhost:8080 --reload main:app
```

The backend will now be running at `http://localhost:8080`.

#### **3. Frontend Setup**

The frontend is static. You just need to add your Google Maps API key.

1.  Open `index.html` in your code editor.
2.  Find the line with `src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY..."`
3.  Replace `YOUR_API_KEY` with your actual Google Maps API key.
4.  Open `index.html` using a live server to handle requests correctly.

-----

## \#\# API Key Setup 🔑

This project requires two API keys from the Google Cloud Platform.

1.  **Google Gemini API Key:**

      * Enable the "Generative Language API" in your Google Cloud project.
      * Create an API key.
      * Place this key in the `.env` file in the `gcp-backend` folder: `GEMINI_API_KEY="your-gemini-key-here"`.

2.  **Google Maps API Key:**

      * Enable the "Maps JavaScript API" and "Maps Static API".
      * Create an API key.
      * **Important:** For security, restrict this key to your website's domain (HTTP referrers) and to the specific Map APIs you enabled.
      * Place this key in the `<script>` tag at the bottom of `index.html`.

-----

## \#\# Deployment

  * **Backend:** The Flask application is containerized using the provided `Dockerfile` and deployed to **Google Cloud Run**. The build is handled by **Google Cloud Build**.
  * **Frontend:** The static frontend is deployed to **Vercel**. Deployment is continuous and automatic, triggering on every `git push` to the `main` branch.
