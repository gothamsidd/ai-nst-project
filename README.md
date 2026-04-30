# AI Neural Style Transfer (AdaIN)

A Flask + PyTorch project that applies artistic style transfer to an image using the AdaIN (Adaptive Instance Normalization) approach.

Upload:
- a **content image** (what you want to transform),
- a **style image** (the look you want),
- and control blend strength with an **alpha slider**.

The app then generates a stylized output you can preview and download.

## What this project includes

- A web app for style transfer at `NST_Code/app.py`
- AdaIN model components in `NST_Code/utils/`
- Training script at `NST_Code/train.py`
- Demo inputs in `Demo_IO_Images/`
- Static upload/result handling in `NST_Code/static/uploads/`

## Tech stack

- Python
- PyTorch + TorchVision
- Flask + Flask-WTF + Flask-Bootstrap
- Pillow / NumPy

## Quick start (local)

### 1) Clone and enter project

```bash
git clone <your-repo-url>
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

Open: `http://localhost:5001`

## How to use

1. Upload a content image (jpg/png/jpeg).
2. Upload a style image.
3. Adjust **Style Strength (alpha)**:
   - `0.0` -> closer to original content
   - `1.0` -> stronger style transfer
4. Click **Transfer Style** and download the result.

## Important model files

The web app expects these model weights to exist:

- `NST_Code/vgg_normalised.pth`
- `NST_Code/experiment/final_exp/decoder_final.pth`

If these files are missing, inference will fail at startup.

## Training (optional)

You can train a decoder using:

```bash
python NST_Code/train.py --help
```

The script supports dataset paths, batch size, epochs, checkpoints, and resume options.

## Project structure

```text
ai-nst-project/
├── Demo_IO_Images/
├── NST_Code/
│   ├── app.py
│   ├── train.py
│   ├── templates/
│   ├── static/
│   └── utils/
├── requirements.txt
└── README.md
```

## Notes

- The upload folder is created automatically at runtime.
- GPU is used if available; otherwise CPU mode is used automatically.

## Deploy on Render (one-click)

This repo now includes `render.yaml` and `Procfile`, so Render can deploy it directly.

1. Push your latest code to GitHub.
2. In Render, choose **New +** -> **Blueprint**.
3. Select this repository and deploy.
4. Render will auto-run:
   - Build: `pip install -r requirements.txt`
   - Start: `gunicorn --chdir NST_Code app:app --bind 0.0.0.0:$PORT --workers 1 --timeout 120`

### Required environment variable

- `SECRET_KEY` (Render auto-generates this via `render.yaml`)

### Important for model weights

The app needs these files at runtime:
- `NST_Code/vgg_normalised.pth`
- `NST_Code/experiment/final_exp/decoder_final.pth`

If you move large model files out of Git later, load them during startup from cloud storage or a model registry.