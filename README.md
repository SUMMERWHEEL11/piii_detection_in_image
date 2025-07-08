# PII Detection and Redaction System

This project implements a system for detecting and redacting Personally Identifiable Information (PII) and faces from images. It uses OCR, face detection, and PII detection to identify sensitive information and automatically redact it.

## Features

- Text extraction from images using EasyOCR
- Face detection using OpenCV's Haar Cascade Classifier
- PII detection using spaCy NER and regex patterns
- Automatic redaction of detected PII and faces
- REST API for easy integration
- Support for various PII types:
  - Email addresses
  - Phone numbers
  - Aadhar numbers (Indian ID)
  - PAN numbers (Indian tax ID)
  - Date of Birth
  - Names and other personal information

## Prerequisites

- Python 3.8 or higher
- pip (Python package installer)
- Virtual environment (recommended)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd pii-detection-in-image-ML
```

2. Create and activate a virtual environment:
```bash
# On macOS/Linux
python -m venv .venv
source .venv/bin/activate

# On Windows
python -m venv .venv
.venv\Scripts\activate
```

3. Install the required packages:
```bash
pip install -r requirements.txt
```

4. Install spaCy English language model:
```bash
python -m spacy download en_core_web_sm
```

## Project Structure

```
project-pii-detection-iitj/
├── app/
│   ├── main.py           # FastAPI application and endpoints
│   ├── pii_text_ner.py   # PII detection logic
│   ├── face_utils.py     # Face detection utilities
│   └── ocr_utils.py      # OCR and text extraction utilities
├── dataset/              # Directory for test images
├── temp/                 # Directory for temporary files
├── requirements.txt      # Project dependencies
└── README.md            # This file
```

## Running the Application

1. Start the FastAPI server:
```bash
uvicorn app.main:app --reload
```

2. The API will be available at:
   - API Documentation: http://localhost:8000/docs
   - Alternative Documentation: http://localhost:8000/redoc

## API Usage

### Redact Image Endpoint

**Endpoint:** `/redact-image/`

**Method:** POST

**Input:**
- Form data with an image file

**Example using curl:**
```bash
curl -X POST "http://localhost:8000/redact-image/" \
     -H "accept: application/json" \
     -H "Content-Type: multipart/form-data" \
     -F "file=@path/to/your/image.jpg"
```

**Example using Python requests:**
```python
import requests

url = "http://localhost:8000/redact-image/"
files = {"file": open("path/to/your/image.jpg", "rb")}
response = requests.post(url, files=files)

# Save the redacted image
if response.status_code == 200:
    with open("redacted_image.jpg", "wb") as f:
        f.write(response.content)
```

## Testing

1. Place test images in the `dataset` directory
2. Run the main script directly:
```bash
python app/main.py
```

## Dependencies

- opencv-python: Image processing and face detection
- easyocr: Text extraction from images
- mtcnn: Face detection
- fastapi: Web framework
- uvicorn: ASGI server
- tensorflow: Required by EasyOCR
- python-multipart: For handling file uploads
- spacy: Natural language processing for PII detection

## Troubleshooting

1. If you encounter issues with Tesseract:
   - Make sure Tesseract is installed on your system
   - For macOS: `brew install tesseract`
   - For Ubuntu: `sudo apt-get install tesseract-ocr`
   - For Windows: Download and install from the official GitHub releases

2. If face detection model fails to download:
   - Check your internet connection
   - The model will be downloaded automatically on first run
   - You can also manually download the Haar Cascade model from OpenCV's GitHub repository

3. If spaCy model fails to load:
   - Run `python -m spacy download en_core_web_sm` again
   - Check if you have sufficient disk space

## Dataset for Testing

https://drive.google.com/drive/folders/1R9a7o-aKL2mDHVG1KHogsuvxOgpZJTS2?usp=sharing

## License

This code is developed as a project for Master of Technology in Data Engineering  under the guidance of Prof. Pradeep Sasmal, IIT Jodhpur.

This project is licensed under the MIT License.

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.



## DEVELOPERS
1. Nitin Bhoyate - ML Model Development, Development of System using existing ML Models, Complete End to End Implementation of functionalities, evaluation etc. 
2. JAI KISHORE RANA - Data collection and Preprocessing, Documentation
3. Bhaskar Adhikary - Data collection and Preprocessing, UI Design and Development
4. Anand Pandey - Writing code for APIs, - Fast API based apis for integration with Front End, Documentation


## Contact
Bhaskar Adhikary - G24ai2035@iitj.ac.in
