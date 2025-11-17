# Prerequisites & Environment Setup

This document lists all the prerequisites for setting up the development environment  
for the Loan Default ML + MLOps project.

---

# 1. System Requirements

### Recommended
- CPU: 4+ cores  
- RAM: 8GB minimum (16GB recommended)  
- GPU (optional but recommended): NVIDIA GPU with CUDA 11.8 or 12.1  
- OS: Windows / Linux / macOS

---

# 2. Install Python

Recommended version:
Python 3.10 or 3.11


Check:
python --version


---

# 3. Create Virtual Environment

### Windows (PowerShell)
```powershell
python -m venv ml-env
.\ml-env\Scripts\activate
```
### macOS / Linux

python3 -m venv ml-env
source ml-env/bin/activate

4. Install Requirements

Once the environment is active:
pip install -r requirements.txt

This installs:
numpy, pandas
scikit-learn
PyTorch (CPU by default)
MLflow
FastAPI
DVC
Evidently
LightGBM / XGBoost
Notebook tools


5. Install PyTorch With CUDA Support (Optional)

If your machine has an NVIDIA GPU, install PyTorch CUDA manually.

Check CUDA version on system:
nvidia-smi

Install PyTorch GPU build:
CUDA 12.1
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

CUDA 11.8
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

Verify GPU access:
import torch
print(torch.cuda.is_available())
print(torch.cuda.get_device_name(0))
