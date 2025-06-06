# End to End Phishing URL Detection with BERT

This project end to end phishing URL detection system using BERT model fine-tuning and provides a Flask API for real-time predictions. It has CI/CD pipeline using GitHub Actions and AWS.

## Project Structure

```
.
├── app.py                 # Flask application
├── main.py               # Model training script
├── requirements.txt      # Python dependencies
├── Dockerfile           # Docker configuration
└── .github/workflows/   # GitHub Actions workflows
```


## Setup

1. Clone this repository:
   ```
   git clone https://github.com/darshan8850/Finetune-Bert-Phishing-URL-Detection.git
   cd Fine-Tuning-BERT-Model-for-Text-Classification
   ```


## Setup Instructions

### Prerequisites

1. Python 3.9+
2. Docker
3. AWS Account with:
   - EC2 instance
   - ECR repository
   - IAM user with appropriate permissions

### Local Development

1. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the Flask application:
   ```bash
   python app.py
   ```

### Docker Deployment

1. Build the Docker image:
   ```bash
   docker build -t phishing-url-detection .
   ```

2. Run the container:
   ```bash
   docker run -p 5000:5000 phishing-url-detection
   ```

### AWS Deployment

1. Set up GitHub Secrets:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `EC2_HOST`
   - `EC2_USERNAME`
   - `EC2_SSH_KEY`

2. Create an ECR repository:
   ```bash
   aws ecr create-repository --repository-name phishing-url-detection
   ```

3. Push to main branch to trigger deployment

## API Endpoints

### Health Check
```
GET /health
```
Response:
```json
{
    "status": "healthy"
}
```

### Predict URL
```
POST /predict
```
Request body:
```json
{
    "url": "https://example.com"
}
```
Response:
```json
{
    "url": "https://example.com",
    "prediction": "Safe",
    "confidence": 0.95
}
```
## Additional Resource

The project uses a custom dataset for phishing URL classification, available at `darshan8950/phishing_url_detection_BERT` 
on the Hugging Face Hub.


The base model used is `bert-base-uncased`, which is fine-tuned for binary classification of URLs as safe or potentially 
phishing.
After fine-tuning, the model's performance can be evaluated using accuracy and AUC metrics. Refer to the output of `main.
py` for detailed results.

### Fine Tuned Model - [Link](https://huggingface.co/datasets/darshan8950/phishing_url_detection_BERT)
### Dataset - [Link](https://huggingface.co/datasets/darshan8950/phishing_url_classification)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request
