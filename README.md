
# Bottle Status Detection API

## Overview
This project implements a Flask-based API that classifies beer bottles as "open" or "closed" based on provided images. It leverages deep learning and containerization for deployment and scalability. The solution is designed as a proof of concept (PoC) for real-world applications in scalable environments.

---

## Features
- Classifies bottle status as **"open"** or **"closed"**.
- Returns a **confidence score** for each classification.
- Provides a REST API endpoint (`/classify`) for submitting images.
- Includes logging for requests and errors.
- Dockerized for easy deployment.
- Scalable and designed for high-throughput scenarios.

---

## Requirements

### Prerequisites
- **Python 3.9+**
- **Docker**

### Python Libraries
The following libraries are required and are listed in `requirements.txt`:
- Flask
- TensorFlow
- Pillow
- NumPy
- scikit-learn
- Requests

To install the dependencies locally:
```bash
pip install -r requirements.txt
```

---

## Running the Application

### Locally (Without Docker)
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the Flask application:
   ```bash
   python app.py
   ```

4. Access the API at `http://127.0.0.1:5000`.

### Using Docker
1. Build the Docker image:
   ```bash
   docker build -t flask-app .
   ```

2. Run the container:
   ```bash
   docker run -p 5000:5000 flask-app
   ```

3. Access the API at `http://127.0.0.1:5000`.

---

## API Usage

### Endpoint
- **POST** `/classify`

### Request
- **Header**: `Content-Type: multipart/form-data`
- **Body**: An image file (`jpeg`, `png`, or `jpg`).

### Example with `curl`
```bash
curl -X POST -F "file=@path/to/image.jpg" http://127.0.0.1:5000/classify
```

### Response
Returns a JSON object with the classification result and confidence score.
```json
{
  "Bottle_Status": "open",
  "Confidence": 0.85
}
```

### Error Handling
- Missing file:
  ```json
  {
    "error": "No file uploaded"
  }
  ```
- Invalid file type:
  ```json
  {
    "error": "Unable to process image"
  }
  ```

---

