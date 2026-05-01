# AI Neural Style Transfer (AdaIN)

This project lets you blend the content of one image with the artistic style of another using AdaIN (Adaptive Instance Normalization).

Built with Flask and PyTorch, it gives you a simple web interface where you:
- upload a content image,
- upload a style image,
- adjust style strength (`alpha`),
- and generate a stylized output image.

## What is inside this repo

- `NST_Code/app.py` - Flask app for style transfer
- `NST_Code/utils/` - model and utility code
- `NST_Code/train.py` - training script
- `NST_Code/static/uploads/` - uploaded and generated images
- `Demo_IO_Images/` - sample images for testing

## Tech stack

- Python
- Flask
- PyTorch + TorchVision
- Pillow + NumPy

## Local setup (step by step)

### 1) Open terminal in project folder

```bash
cd ai-nst-project
```

### 2) Create and activate virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3) Install dependencies

```bash
pip install -r requirements.txt
```

### 4) Run the app

```bash
python NST_Code/app.py
```

### 5) Open in browser

`http://127.0.0.1:5001`

## How to use the app

1. Upload a **content image** (the structure you want to keep).
2. Upload a **style image** (the visual look you want).
3. Adjust **alpha**:
   - `0.0` = closer to original content
   - `1.0` = stronger style effect
4. Click **Transfer Style**.
5. View/download the generated image.

## Required model files

The app expects these files:

- `NST_Code/vgg_normalised.pth`
- `NST_Code/experiment/final_exp/decoder_final.pth`

If they are missing, the app cannot run inference.

## Optional: training

To explore training options:

```bash
python NST_Code/train.py --help
```

## Deploy on Render

This project includes `render.yaml` and `Procfile`, so deployment is straightforward:

1. Push code to GitHub.
2. In Render, choose **New +** -> **Blueprint**.
3. Select your repo and deploy.

Render uses:
- Build: `pip install -r requirements.txt`
- Start: `gunicorn --chdir NST_Code app:app --bind 0.0.0.0:$PORT --workers 1 --timeout 120`