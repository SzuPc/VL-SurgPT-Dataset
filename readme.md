# VL-SurgPT-Dataset

**VL-SurgPT-Dataset** is a dataset for intraoperative point tracking in robotic surgery, including two categories: **tissue** and **instrument**. The tissue part covers five challenging scenarios (Deformation, Instrument Blocking, Jitter, Reflection, Smoke), while the instrument part provides annotated surgical tool videos for keypoint tracking tasks.

---

## 📂 Dataset Structure

```
dataset/
 ├── tissue_with_text/
 │   ├── 0/  # Deformation
 │       └── ...
 │   ├── 1/  # Instrument Blocking
 │       └── ...
 │   ├── 2/  # Jitter
 │       └── ...
 │   ├── 3/  # Reflection
 │       └── ...
 │   └── 4/  # Smoke
 │       └── left/
 │           ├── seq000/
 │           │   ├── frames/
 │           │   │   └── 00000000ms-00001234ms-visible.mp4
 │           │   └── segmentation/
 │           │       ├── labels.json         # Point tracking labels
 │           │       └── texts.json          # Text annotations
 │           ├── seq001/
 │           │   └── ...
 │           └── seq...
 └── instrument_with_text/
     └── 0/
          └── left/
              ├── seq000/
              │   ├── frames/
              │   │   └── 00000000ms-00001234ms-visible.mp4
              │   └── segmentation/
              │       ├── labels.json
              │       └── texts.json
              ├── seq001/
              │   └── ...
              └── seq...
```

