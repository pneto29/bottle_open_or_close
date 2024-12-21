
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

## Scalability and Infrastructure Design

### Proposed Architecture
- **Load Balancer**: Distributes requests across multiple containers.
- **Docker Swarm/Kubernetes**: Orchestrates multiple containers for horizontal scaling.
- **Caching**: Implements a cache (e.g., Redis) to store frequently accessed results.
- **Cloud Deployment**: Suggested platforms include AWS ECS, Azure Kubernetes Service, or GCP.

### High-Throughput Scenarios
- Simulate 1,000 requests per second using tools like Locust or Apache Benchmark.
- Scale horizontally by adding more containers or vertically by increasing server resources.

---

## Monitoring and Metrics
- **Key Metrics**:
  - Response time
  - Uptime
  - Error rate
- **Tools**:
  - Prometheus + Grafana
  - AWS CloudWatch

---

## Security Measures
- **Input Validation**: Ensure only valid images are processed.
- **Rate Limiting**: Prevent abuse by limiting requests per second per client.
- **Authentication**: Use API keys to control access.

---

## Additional Features (Optional)
- A lightweight web interface using Streamlit for testing the API.
- Deployment on a cloud platform with a live URL for demonstration.

---

## Directory Structure
```
.
|-- app.py                # Flask application
|-- Dockerfile            # Dockerfile for containerization
|-- requirements.txt      # Python dependencies
|-- README.md             # Documentation
|-- model/                # Pre-trained model (.h5 file)
|-- tests/                # Test images
```

---

## Author
- **Your Name**
- Contact: [your-email@example.com](mailto:your-email@example.com)

---

## License
This project is licensed under the MIT License. See the LICENSE file for details.
