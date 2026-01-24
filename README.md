# Network Security System

A comprehensive machine learning-based network security system designed to detect and classify malicious network activities. This project implements an end-to-end pipeline for network intrusion detection, leveraging advanced machine learning algorithms to identify potential security threats in real-time.

## Overview

Network security threats are constantly evolving, making traditional signature-based detection methods insufficient. This system implements a machine learning approach that adapts to new attack patterns and provides accurate threat detection. It processes network traffic data, extracts relevant features, and uses trained models to classify traffic as normal or potentially malicious, offering a production-ready solution for cybersecurity professionals and organizations.

## Key Features

- End-to-end machine learning pipeline for network intrusion detection
- Automated data ingestion and validation from MongoDB
- Feature engineering and preprocessing with schema validation
- Multiple model training capabilities with hyperparameter optimization
- Model versioning and artifact management
- RESTful API for real-time predictions
- Interactive web interface for threat analysis
- Docker containerization for easy deployment
- CI/CD pipeline integration with GitHub Actions
- Comprehensive logging and monitoring

## Tech Stack

**Programming Language**
- Python 3.8+

**Machine Learning & Data Science**
- scikit-learn - Model training and evaluation
- pandas - Data manipulation and analysis
- numpy - Numerical computations
- imbalanced-learn - Handling class imbalance

**Web Framework**
- Flask - API and web application development

**Database**
- MongoDB - NoSQL database for data storage

**DevOps & Deployment**
- Docker - Containerization
- GitHub Actions - CI/CD automation
- AWS (optional) - Cloud deployment

**Development Tools**
- pytest - Unit testing
- logging - Application monitoring

## Project Architecture
```
Network-Security-System/
│
├── .github/
│   └── workflows/          # CI/CD pipeline configurations
│
├── networksecurity/        # Main application package
│   ├── components/         # Data ingestion, transformation, training modules
│   ├── entity/             # Configuration and artifact entities
│   ├── pipeline/           # Training and prediction pipelines
│   ├── utils/              # Utility functions and helpers
│   └── constants/          # Project constants and configurations
│
├── Network_Data/           # Raw network traffic datasets
│
├── data_schema/            # JSON schema for data validation
│
├── final_model/            # Trained model artifacts
│
├── valid_data/             # Validated datasets
│
├── templates/              # HTML templates for web interface
│
├── app.py                  # Flask web application
├── main.py                 # Training pipeline execution
├── push_data.py            # MongoDB data ingestion script
├── test_mongodb.py         # Database connection testing
│
├── Dockerfile              # Container configuration
├── requirements.txt        # Python dependencies
├── setup.py                # Package installation configuration
└── README.md               # Project documentation
```

## Installation and Setup

### Prerequisites

- Python 3.8 or higher
- MongoDB (local or cloud instance)
- Git
- Docker (optional, for containerized deployment)

### Clone the Repository
```bash
git clone https://github.com/Tushar973/Network-Security-System.git
cd Network-Security-System
```

### Create Virtual Environment
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate
```

### Install Dependencies
```bash
pip install -r requirements.txt
```

### Environment Configuration

Create a `.env` file in the root directory with the following variables:
```env
MONGO_DB_URL=mongodb://localhost:27017
DB_NAME=network_security
COLLECTION_NAME=network_data
```

### Initialize Database
```bash
# Test MongoDB connection
python test_mongodb.py

# Push training data to MongoDB
python push_data.py
```

## Running the Application

### Train the Model

Execute the training pipeline to build and save the machine learning model:
```bash
python main.py
```

This will:
- Ingest data from MongoDB
- Validate data against the defined schema
- Perform feature engineering and transformation
- Train the model with cross-validation
- Save model artifacts to `final_model/`

### Start the Web Application

Launch the Flask application for predictions:
```bash
python app.py
```

The application will be available at `http://localhost:5000`

### Docker Deployment

Build and run the application using Docker:
```bash
# Build Docker image
docker build -t network-security-system .

# Run Docker container
docker run -p 5000:5000 network-security-system
```

## How to Use

### Web Interface

1. Navigate to `http://localhost:5000` in your web browser
2. Upload a CSV file containing network traffic data
3. The system will process the data and display predictions
4. Review the classification results and confidence scores

### API Endpoint

#### Predict Network Threat

**Endpoint:** `POST /predict`

**Request Format:**
```bash
curl -X POST http://localhost:5000/predict \
  -F "file=@network_data.csv"
```

**Response Format:**
```json
{
  "predictions": [0, 1, 0, 1],
  "probabilities": [
    [0.92, 0.08],
    [0.15, 0.85],
    [0.88, 0.12],
    [0.23, 0.77]
  ],
  "status": "success"
}
```

Where:
- `0` = Normal traffic
- `1` = Malicious/Anomalous traffic

### Input Data Format

The system expects CSV files with the following features:

- Network packet metadata (source/destination IP, ports)
- Protocol information
- Packet size and timing features
- Connection state flags
- Statistical features derived from traffic patterns

Refer to `data_schema/` for complete schema specifications.

## Model Performance

The trained model achieves the following performance metrics on the test dataset:

- Accuracy: ~95%
- Precision: ~93%
- Recall: ~94%
- F1-Score: ~93.5%

These metrics demonstrate the model's effectiveness in identifying network security threats while minimizing false positives.


## Future Improvements

- Implement real-time network packet capture and analysis
- Add support for deep learning models (LSTM, CNN) for sequence analysis
- Integrate threat intelligence feeds for enhanced detection
- Develop a comprehensive dashboard with visualization of network threats
- Implement automated model retraining with new data
- Add multi-class classification for specific attack types (DDoS, Malware, Phishing)
- Create alerting mechanisms for critical threats
- Implement explainable AI features for prediction interpretation
- Add support for distributed deployment across multiple network segments
- Develop mobile application for remote monitoring

