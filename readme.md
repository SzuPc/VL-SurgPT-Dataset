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
 │           │   └── annotation/
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
              │   └── annotation/
              │       ├── labels.json
              │       └── texts.json
              ├── seq001/
              │   └── ...
              └── seq...
```

## 🏷️ Label Structure

Each frame in the dataset contains two types of annotation:

- 2D coordinates of tracked points (`labels.json`)
- Semantic attributes for each point (`texts.json`)

### 📁`labels.json` File Structure

```
labels.json
├── "0"           # Frame index (as string)
│   ├── [x1, y1]  # Coordinates of point 0
│   ├── [x2, y2]  # Coordinates of point 1
│   ├── ...
│   └── [xN, yN]  # Coordinates of point N or null if obscured
├── "30"
│   └── [...]
└── ...
```

* Keys are frame indices as strings (e.g., `"0"`, `"30"`, …)
* Each frame contains a list of 2D coordinates, one per tracked point

### 📁`texts.json` File Structure

🔹 For Tissue Points

```
texts.json
├── "0"
│   ├── object[0]              # Not real structure, part of a list
│   │   ├── location: "Tissue"
│   │   └── status: ["Pulled"]
│   ├── object[1]
│   │   └── ...
│   └── ...
├── "30"
│   └── [...]
└── ...
```

| Field          | Description                               |
| ---------------- | ------------------------------------------- |
| `location` | Always`"Tissue"`                      |
| `status`   | A list of one or more tissue state labels |

🔹 For Instrument Points

```
texts.json
├── "0"
│   ├── object[0]                   # Not real structure, part of a list
│   │   ├── location: "Instrument"
│   │   ├── instrument_order: 0
│   │   ├── instrument_name: "Fenestrated Bipolar Forceps"
│   │   ├── point_order: 2
│   │   └── status: "Clear View"
│   ├── object[1]
│   │   └── ...
│   └── ...
├── "30"
│   └── [...]
└── ...
```

| Field                  | Description                           |
| ------------------------ | --------------------------------------- |
| `location`         | Always`"Instrument"`              |
| `instrument_order` | Index of the instrument in this frame |
| `instrument_name`  | Name of the instrument                |
| `point_order`      | Index of the point on this instrument |
| `status`           | Visibility status of the point        |

## 📚 Dataset Vocabulary

This section introduces the key terminology and category labels used throughout the dataset. Our dataset defines seven status categories for tissue points, includes seven types of surgical instruments, and specifies four status categories for instrument keypoints as well.

### 🧬 Tissue Point Status Categories

| Status Label           | Description                         |
| ------------------------ | ------------------------------------- |
| Clear View             | Point is clearly visible            |
| Pulled                 | Tissue is under tension or stretch  |
| Reflection             | Surface reflection obscures view    |
| Smoke Obscuration      | Smoke obscures visibility           |
| Instrument Obscuration | Occluded by a surgical instrument   |
| Tissue Obscuration     | Occluded by other tissue structures |
| Out of view            | Point is outside the camera frame   |

### 🛠️ Instrument Categories

| 🛠️ Instrument Name        |
| ----------------------------- |
| Cadiere Forceps             |
| Fenestrated Bipolar Forceps |
| Needle Diver                |
| Clip Applier                |
| Clip                        |
| Tip-Up Fenestrated Grasper  |
| Harmonic Ace Curved Shears  |

### 👁️ Instrument Point Status Categories

| Status Label      | Description                                                              |
| ------------------- | -------------------------------------------------------------------------- |
| Clear View        | Point is clearly visible                                                 |
| Self-occlusion    | Point is occluded by the instrument itself                               |
| External Occlusion | Point is occluded by another object                          |
| Out of view       | Point is outside the camera frame                                        |


