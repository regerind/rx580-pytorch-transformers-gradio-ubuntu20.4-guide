# Setting Up Gradio, PyTorch, and Transformers on RX580

## Prerequisites
Before you begin, ensure you have followed the installation guide for ROCm and TensorFlow:
- [Installation of ROCm and TensorFlow on Ubuntu 20.04 LTS for Radeon RX580](https://github.com/Grench6/RX580-rocM-tensorflow-ubuntu20.4-guide)

## Steps to Set Up Gradio, PyTorch, and Transformers

### 1. Create a Python Virtual Environment
```bash
python3 -m venv rocm_env
source rocm_env/bin/activate
```

### 2. Install TensorFlow ROCm
```bash
pip3 install -Iv tensorflow-rocm==2.2.0
pip uninstall protobuf && pip install protobuf==3.20.*
pip uninstall numpy && pip install numpy==1.19.5
```

- **Handling NumPy Installation Issues**  
  If you encounter the following error:
  ```
  WARNING: No metadata found in ./rocm_env/lib/python3.8/site-packages
  Found existing installation: numpy 1.24.4
  error: uninstall-no-record-file
  ```
  Resolve it by:
  ```bash
  rm -rf ./rocm_env/lib/python3.8/site-packages/numpy*
  pip install numpy==1.19.5
  ```

### 3. Install Compatible Transformers Version
Install either version 4.0.0 or 4.1.0:
```bash
pip install transformers==4.0.0
pip install accelerate
```

### 4. Install PyTorch ROCm
Download the compatible version of PyTorch:
- Visit: [PyTorch ROCm Downloads](https://download.pytorch.org/whl/torch/)
- Search for and download: `torch-1.7.1+rocm3.8-cp38-cp38-linux_x86_64.whl`
- Install it using:
```bash
pip install "filepath/torch-1.7.1+rocm3.8-cp38-cp38-linux_x86_64.whl"
```
Make sure to replace `"filepath/"` with the actual path.

### 5. Check GPU Recognition with PyTorch
Test if PyTorch recognizes your GPU:
```python
import torch

print("CUDA available:", torch.cuda.is_available())
if torch.cuda.is_available():
    print("Number of GPUs:", torch.cuda.device_count())
    print("GPU Name:", torch.cuda.get_device_name(0))
else:
    print("No GPU detected")
```

- **Verify ROCm Configuration**: If `torch.cuda.is_available()` returns `False`, check your ROCm installation.

### 6. Install Gradio
If PyTorch recognizes your GPU, proceed to install Gradio:
```bash
pip install gradio
```

### 7. Handle Dependencies
Given the older versions of NumPy, you may need to update additional packages:
```bash
pip uninstall numpy && pip install numpy==1.19.5
pip uninstall matplotlib && pip install matplotlib==3.3.4
pip uninstall pandas && pip install pandas==1.2.5
```

## Conclusion
You should now have Gradio, PyTorch, and Transformers set up and ready to use with your RX580. Make sure to test the installations by running a sample Gradio app.
