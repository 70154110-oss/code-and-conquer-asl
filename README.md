# 🤟 The Silent Gap — ASL Sign Language Classification

**Forman CS Club AI Hackathon 2026**  
**Team: CODE AND CONQUER**

---

## 👥 Team Members
- Muhammad Faizan
- Laraib Zafar
- Eshal Tanveer

---

## 🏆 Results
| Leaderboard | Score |
|-------------|-------|
| Public | 0.48833 |
| Private | 0.49300 |

---

## 🎯 Problem Statement
Classify 29 ASL hand signs from images — full alphabet (A–Z) plus `space`, `del`, and `nothing`.  
Dataset: ~87,000 training images, ~17,000 test images.

---

## 🧠 Approach

### Models Used
- **MobileNetV2** — pretrained on ImageNet, fine-tuned for ASL
- **EfficientNetB0** — pretrained on ImageNet, fine-tuned for ASL

### Ensemble Strategy
Final prediction = weighted average:
| Model | Weight |
|-------|--------|
| MobileNetV2 (base) | 40% |
| EfficientNetB0 (base) | 40% |
| MobileNetV2 + contrast TTA | 10% |
| EfficientNetB0 + brightness TTA | 10% |

### Training Config
| Setting | Value |
|---------|-------|
| Image Size | 224×224 |
| Batch Size | 32 |
| Max Epochs | 25 (EarlyStopping) |
| Optimizer | Adam (lr=1e-4) |
| Loss | Categorical Crossentropy (label smoothing=0.1) |
| Validation Split | 15% |

### Augmentation
- Random Rotation (±8%)
- Random Translation (±10%)
- Random Zoom (±12%)
- Random Contrast (±20%)
- Random Brightness (±12%)

### Callbacks
- EarlyStopping (patience=5)
- ReduceLROnPlateau (factor=0.5, patience=2)
- ModelCheckpoint (best val_accuracy)

---

## 📁 Repository Structure
```
code-and-conquer-asl/
├── notebook.ipynb        # Training notebook (Kaggle)
├── submission.csv        # Final predictions
├── app.py                # Streamlit demo app
├── README.md
├── .gitignore
└── LICENSE
```

---

## 🚀 How to Run

### Training
1. Open `notebook.ipynb` on Kaggle
2. Add competition dataset
3. Run all cells — `submission.csv` is generated automatically

### Demo App
```bash
pip install streamlit opencv-python numpy
streamlit run app.py
```

---

## ❌ What Didn't Work
- MobileNetV3Small — very low accuracy (~43%)
- Simple CNN — good accuracy but weaker than transfer learning
- High learning rates during fine-tuning — unstable

## 🔮 What We'd Build Next
- Real-time webcam ASL detection with actual model inference
- Flutter mobile app for deaf community
- Two-way bridge: hearing user types, deaf user sees signs
- Word-level prediction instead of letter-by-letter

---

*AI Hackathon 2026 · Forman Computer Science Club · Forman Christian College*
