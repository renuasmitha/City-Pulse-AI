#  CityPulse AI — Smart Waste Management Platform

**Making waste management smarter through computer vision, digital twin simulation, and data-driven recommendations.**

CityPulse AI is an intelligent waste management dashboard designed to help visualize waste collection operations, monitor bin status, identify waste categories from images, and explore smarter collection strategies through a simulated waste management ecosystem.

Built for **Code Clash**, the project combines a web-based dashboard with a Python backend and computer vision capabilities to demonstrate how technology can support more efficient waste management.

---

##  Key Features

###  1. Smart Waste Management Dashboard

* Monitor waste-bin status and fill levels.
* Visualize waste management activity through interactive charts and graphs.
* View collection priorities and operational recommendations.
* Access bin, fleet, and collection information from a centralized interface.

###  2. Computer Vision-Based Waste Scanning

* Upload images for waste-category detection.
* Use a pretrained YOLO-World model to identify prompted object categories.
* Connect image analysis with the waste management dashboard.
* Keep waste-category detection separate from bin-fill estimation.

**Note:** Detection results are model predictions and may require manual verification. Reliable bin-fill estimation requires a suitable fill-classification model.

###  3. Digital Twin Simulation

* Represent waste collection operations through a simulated environment.
* Visualize bin and fleet information.
* Explore how collection activities affect the dashboard.
* Demonstrate potential improvements to waste collection planning.

The current digital twin uses simulated operational data rather than a live municipal infrastructure connection.

###  4. Fleet and Collection Monitoring

* View fleet information and collection activity.
* Track simulated collection operations.
* Visualize bin status changes during supported collection workflows.
* Explore collection priorities through the dashboard.

###  5. Data-Driven Recommendations

* Display recommendations based on available waste-management information.
* Highlight collection priorities and potential operational improvements.
* Demonstrate how dashboard data can support decision-making.

The current recommendation system uses backend logic; it does not use a generative AI service.

---

##  Technology Stack

| Component         | Technologies                         |
| ----------------- | ------------------------------------ |
| Frontend          | HTML, CSS, JavaScript                |
| Backend           | Python, FastAPI                      |
| Computer Vision   | YOLO-World, Ultralytics              |
| API Communication | REST API                             |
| Visualization     | Interactive dashboard charts and map |
| Development       | Visual Studio Code, Git, GitHub      |

*The table lists the project's core technologies. Additional libraries may be used by individual components.*

---

##  System Architecture

```text
              USER
                │
                ▼
       Web Dashboard
       HTML / CSS / JS
                │
                ▼
         FastAPI Backend
                │
       ┌────────┼─────────┐
       │        │         │
       ▼        ▼         ▼
   Bin Data   Fleet     Collection
              Data        Data
       │
       ▼
   Recommendation
       Logic

       Image Upload
            │
            ▼
    Vision Analysis API
            │
            ▼
       YOLO-World
            │
            ▼
   Detected Object Categories
```

The frontend communicates with the FastAPI backend through API endpoints. Uploaded images are processed by the vision service, while dashboard operations and recommendations are handled by backend logic.

---

##  Live Demo

**Live Project:** https://city-pulse-ai-frontend.vercel.app/

Explore the deployed dashboard to see the project's interface and supported features.

*Note: Image scanning requires a running backend with the necessary vision dependencies and model weights. A static frontend deployment alone does not provide the backend functionality.*

---

##  Run Locally

### Prerequisites

* Python installed
* Internet access for downloading pretrained model weights when needed
* Git, if cloning the repository

### 1. Clone the repository

```bash
git clone https://github.com/renuasmitha/City-Pulse-AI.git
cd CityPulseAI
```

Replace `https://github.com/renuasmitha/City-Pulse-AI.git` with your actual repository URL.

### 2. Start the backend

Open a terminal in the project folder:

```powershell
cd backend
python -m pip install -r requirements.txt
python -m uvicorn main:app --reload
```

The backend runs at:

`http://127.0.0.1:8000`

### 3. Start the frontend

Open a second terminal in the project folder:

```powershell
cd frontend
python -m http.server 5500
```

Open the dashboard:

`http://127.0.0.1:5500`

### 4. Test the vision service

Check vision dependency readiness:

`http://127.0.0.1:8000/api/vision/status`

Explore the API documentation:

`http://127.0.0.1:8000/docs`

Select **AI waste scanner** in the dashboard to test image analysis.

The first image analysis may take longer because pretrained YOLO-World weights need to be downloaded. Internet access is required for this download, but no API key is needed.

---

## Computer Vision Configuration

The project separates waste-object detection from bin-fill estimation.

* `computer vision/waste_vision.py` detects prompted waste categories using YOLO-World.
* `computer vision/vision.py` estimates fill only for recognized fill-class labels.
* `backend/main.py` provides dashboard endpoints and `POST /api/vision/analyze`.

To configure local model weights, set the appropriate environment variables:

* `CITYPULSE_YOLO_MODEL`
* `CITYPULSE_WASTE_MODEL`

Use valid local model paths.

A generic pretrained object detector does not reliably estimate how full a waste bin is. Fill estimation depends on a compatible custom fill model and recognized fill classes.

---

## Implementation Notes

For transparency, the current implementation has the following limitations:

Bin, fleet, and collection records are stored in backend memory and reset when the server restarts.
Fleet routing and telemetry use demonstration data.
Recommendations are generated using backend logic rather than a generative AI model.
Waste-object detection depends on pretrained model predictions and is not guaranteed to classify every item correctly.
A deployed static frontend cannot independently run the local FastAPI vision service.

These boundaries distinguish the features currently implemented from capabilities that could be added in future versions.

## Future Improvements

Potential next steps include:

1. Integrating a generative AI model for contextual waste-management recommendations.
2. Training and integrating a dedicated model for reliable bin-fill estimation.
3. Connecting to real-time bin sensors and fleet telemetry.
4. Implementing persistent storage for bins, collections, and fleet records.
5. Improving collection-route optimization.
6. Deploying the backend and computer vision service to an accessible hosting environment.

These are proposed improvements, not claims about existing functionality.


## The Vision

CityPulse AI explores how computer vision, simulation, and data-driven decision-making can contribute to smarter waste management.

By bringing waste detection, operational monitoring, and collection insights together in one dashboard, the project demonstrates a practical starting point for more efficient and technology-enabled waste management systems.

Built with curiosity, collaboration, and a vision for smarter waste management.

