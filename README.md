# 🧠 Brain Tumor Classifier API

A Flask REST API that classifies brain MRI scans into 4 categories using a CNN model trained with Keras/TensorFlow.

## Classes
- Glioma
- Meningioma
- No Tumor
- Pituitary

## Model Info
- Input: 256×256 RGB image
- Architecture: Sequential CNN (5× Conv2D + MaxPooling, 3× Dense)
- Output: 4-class Softmax

---

## Running Locally

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py
```

## API Endpoints

### `GET /`
Health check.

### `POST /predict`
Upload an MRI image and get a prediction.

**Request:** `multipart/form-data` with key `file`

**Response:**
```json
{
  "prediction": "Glioma",
  "confidence": 97.43,
  "all_probabilities": {
    "Glioma": 97.43,
    "Meningioma": 1.12,
    "No Tumor": 0.88,
    "Pituitary": 0.57
  }
}
```

## Testing with curl

```bash
curl -X POST http://YOUR_EC2_IP:5000/predict \
  -F "file=@/path/to/mri_scan.jpg"
```