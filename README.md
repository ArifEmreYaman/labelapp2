# LabelApp2 — YOLO Image Labeling & Training Tool

A desktop application for labeling images with bounding boxes and training YOLO models — built with PyQt5. Works on **Ubuntu** and **Windows**.

---

## Features

- **Rectangle labeling** — draw bounding boxes with left-click drag
- **Move & resize** — drag boxes to reposition, drag corner handles to resize
- **Right-click menu** — delete or change class of any box
- **Unlimited label classes** — custom names and colors, rename/recolor anytime
- **Auto-save** — annotations saved automatically when switching images
- **Recursive folder scan** — finds images in all subfolders
- **External dataset support** — automatically reads `data.yaml` and `classes.txt` from Roboflow, LabelImg, CVAT exports
- **YOLO training** — supports YOLO11, YOLOv8, YOLOv9, YOLOv10 with live log output
- **Use existing datasets** — directly train from Roboflow/Ultralytics datasets without re-exporting
- **Dark theme** — easy on the eyes during long labeling sessions

---

## Folder Structure

```
your_images/
├── photo1.jpg
├── photo2.jpg
└── labels/                  # auto-created
    ├── photo1.txt
    ├── photo2.txt
    └── labelapp_classes.json
```

---

## Installation

### Requirements

- Python 3.10+
- Anaconda (recommended)
- NVIDIA GPU (optional but recommended for training)

### Setup

```bash
# 1. Clone the repo
git clone https://github.com/ArifEmreYaman/labelapp2.git
cd labelapp2

# 2. Create conda environment
conda create -n labelapp python=3.10 -y
conda activate labelapp

# 3. Install PyQt5 via conda (avoids xcb plugin issues on Linux)
conda install pyqt -y

# 4. Install other dependencies
pip install ultralytics PyYAML numpy opencv-python Pillow
```

---

## Running

```bash
conda activate labelapp
cd labelapp2
python main.py
```

---

## Usage Guide

### 1. Labeling

| Action | How |
|--------|-----|
| Open image folder | `File > Open Folder` or toolbar button |
| Draw bounding box | Left-click and drag on the image |
| Select a box | Left-click on it |
| Move a box | Click inside selected box and drag |
| Resize a box | Drag the white corner handles |
| Delete a box | Right-click → Delete, or select + `Del` key |
| Change box class | Right-click → Change Class |
| Next / Previous image | `D` / `A` keys or toolbar buttons |
| Save | `Ctrl+S` (also auto-saves on image switch) |

### 2. Managing Classes

- Click **+ Add** in the right panel to add a class with a custom color
- **Double-click** a class name to rename it
- Click **Color** to change its color
- Right-click on any bounding box → **Change Class** to reassign

### 3. Training

1. Click **Start Training** in the toolbar
2. Select YOLO model (YOLO11m recommended)
3. Set epochs, batch size, image size
4. Choose output folder
5. Click **Start Training**

> **Tip:** If you open a Roboflow/Ultralytics dataset that already has a `data.yaml`, the dialog will detect it and offer to use it directly — no re-export needed.

---

## Supported Label Formats (import)

The app automatically finds label files in these locations:

| Format | Location |
|--------|----------|
| Our format | `images_folder/labels/image.txt` |
| LabelImg inline | `images_folder/image.txt` |
| YOLO standard | `images_folder/images/` + sibling `labels/` |
| Roboflow | `train/images/` + `train/labels/` |

---

## Supported YOLO Models

| Family | Variants |
|--------|----------|
| YOLO11 | n, s, m, l, x |
| YOLOv8 | n, s, m, l, x |
| YOLOv9 | c, e |
| YOLOv10 | n, s, m, l, x |

---

## Troubleshooting

**Qt platform plugin "xcb" error on Ubuntu:**
```bash
conda install pyqt -y   # use conda's PyQt5 instead of pip
```

**Training fails — "no images found":**
Make sure your output folder exists and you have at least 1 labeled image.

**Classes show as cls0 after reopening:**
The app saves class names to `labels/labelapp_classes.json`. If this file is missing, re-add your classes from the right panel.

---

## License

MIT License — free to use, modify, and distribute.

---

## Author

**Arif Emre Yaman** — [github.com/ArifEmreYaman](https://github.com/ArifEmreYaman)
