# TopoID — Multi-Camera Person Re-Identification

TopoID is a multi-camera person tracking and re-identification system that detects individuals across multiple video streams and assigns them consistent global identities. Built for surveillance and monitoring scenarios where people move through overlapping or non-overlapping camera fields.

---

## 🚀 Features

- **Multi-camera support** — Process 12+ video streams simultaneously
- **Person detection** — YOLOv11x (Extra Large, 56.9M parameters) for high-accuracy human detection
- **Single-camera tracking** — DeepOcSort algorithm via BoxMOT for per-camera trajectory tracking
- **Cross-camera re-identification** — RGB histogram feature extraction + cosine similarity matching to recognize the same person across different cameras
- **Global ID assignment** — Assigns consistent identities across the entire camera network
- **Feature buffering** — Stores appearance features for robust and stable matching

---

## 🧠 How It Works

```
Video Streams (MP4)
       │
       ▼
 YOLOv11x Detection  ──►  DeepOcSort Tracking  (per camera)
       │
       ▼
 RGB Histogram Feature Extraction (per tracked person)
       │
       ▼
 Cosine Similarity Matching across cameras  (threshold: 0.90)
       │
       ▼
 Global ID Mapping  →  global_id_mapping.json
```

---

## 🛠️ Tech Stack

| Component | Library / Model |
|---|---|
| Person Detection | [Ultralytics YOLOv11x](https://github.com/ultralytics/ultralytics) |
| Single-Camera Tracking | [BoxMOT – DeepOcSort](https://github.com/mikel-brostrom/boxmot) |
| Feature Extraction | RGB Histograms (OpenCV) |
| Similarity Matching | Cosine Similarity (scikit-learn) |
| Video Processing | OpenCV |
| Deep Learning Backend | PyTorch / TorchVision |
| Data Processing | NumPy, Pandas, SciPy |

---

## 📂 Project Structure

```
TopoID/
├── TopoID.ipynb   # Main notebook
└── README.md
```

**Expected input directory (runtime):**
```
/content/cameras/
├── cam1.mp4
├── cam2.mp4
└── ...
```

**Outputs:**
- Per-frame detection labels in YOLO `.txt` format
- `global_id_mapping.json` — maps local per-camera IDs to global person IDs

---

## ⚙️ Configuration

| Parameter | Value | Description |
|---|---|---|
| `det_thresh` | 0.25 | Detection confidence threshold |
| `max_age` | 90 | Max frames to keep a lost track |
| `min_hits` | 5 | Min detections before track is confirmed |
| `iou_threshold` | 0.3 | IoU threshold for association |
| `similarity_threshold` | 0.90 | Cosine similarity cutoff for re-ID |
| `imgsz` | 1280 | Input resolution for YOLO inference |

---

## 🖥️ Requirements

```
ultralytics
boxmot
opencv-python
torch
torchvision
scikit-learn
numpy
pandas
scipy
```

---

## 📖 Usage

1. Upload your video files to `/content/cameras/`
2. Open `TopoID.ipynb` in Jupyter / Google Colab
3. Run all cells
4. Results will be saved as YOLO-format labels and `global_id_mapping.json`

---

## 📄 License

MIT License

---

> Developed by [MehmetPekerr](https://github.com/MehmetPekerr)
