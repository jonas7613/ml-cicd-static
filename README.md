# Drug Classification 



## Architecture Overview

```
GitHub Repository (Source code, dataset, training script, workflows)
       │
       ▼
GitHub Actions CI (Install dependencies → Format check → Train model → Evaluate → Generate CML report)
       │
       ▼
Versioned Deployment Artifacts (Trained ONNX & Joblib model, metrics, confusion matrix)
       │
       ▼
Hugging Face Static Space (Static HTML/JS application + ONNX model artifact)
       │
       ▼
User's Browser (Loads interface and executes inference locally using ONNX Runtime Web)
```

## Repository Structure

```
.
├── .github/
│   └── workflows/
│       └── ci.yml             # GitHub Actions CI/CD workflow
├── app/
│   ├── index.html             # Client-side ONNX Runtime Web app
│   └── README.md              # Hugging Face Space metadata
├── data/
│   └── drug200.csv            # Training dataset
├── model/
│   ├── drug_model.joblib      # Serialized scikit-learn pipeline
│   └── drug_model.onnx        # Exported ONNX model for browser inference
├── results/
│   ├── confusion_matrix.png   # Confusion matrix visualization
│   └── metrics.txt            # Model evaluation metrics & classification report
├── Makefile                   # Automation targets (install, format, train, eval)
├── requirements.txt           # Python dependencies
├── train.py                   # Model training and ONNX export script
└── README.md                  # Project documentation
```

## Local Development & Testing

1. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Verify code formatting**:
   ```bash
   black --check train.py
   ```

3. **Train the model and export ONNX**:
   ```bash
   python train.py
   ```

4. **Review evaluation metrics**:
   ```bash
   cat results/metrics.txt
   ```

## CI/CD Pipeline & GitHub Setup

### Required GitHub Secrets

In your GitHub repository, navigate to **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:

| Secret Name | Value | Description |
| :--- | :--- | :--- |
| `HF_TOKEN` | `hf_...` | Hugging Face user access token with **write** permissions |
| `HF_SPACE_ID` | `YOUR_USERNAME/SPACE_NAME` | Example: `Jonathan73820/ml-cicd-static` |

*Note: GitHub automatically provides `GITHUB_TOKEN` for CML evaluation comments.*
