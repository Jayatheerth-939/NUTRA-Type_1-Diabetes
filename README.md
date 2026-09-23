# 🩸 Continuous Blood Glucose Prediction for Type-1 Diabetes

Hey there! Welcome to the repository. This project is focused on predicting blood glucose levels **30 minutes into the future** for Type 1 Diabetes (T1D) patients using deep learning. 

Living with T1D requires a constant balancing act between meals, insulin doses, and daily activity. By providing accurate advance glucose predictions, this model aims to help patients anticipate highs and drops before they happen.

---

## 💡 How It Works

We built a pure **LSTM baseline model** (`PureLSTMGlucosePredictor`) trained on real-world continuous physiological logs from the **OhioT1DM dataset**.

The model processes a **4-hour history window** (48 steps of 5-minute intervals) to predict the glucose level at $T + 30\text{ mins}$.

### What the model looks at (17 total parameters):
* **Physiological Signals:** Raw Continuous Glucose Monitor (CGM) readings, Gaussian-smoothed CGM ($\sigma=1.0$) to reduce sensor jitter, bolus insulin doses, and meal carbohydrate intake.
* **Circadian & Time Signals:** Sine and Cosine trigonometric encodings for time of day, day of week, and month to help the model learn daily body rhythms (like morning glucose spikes).
* **Patient Metadata:** Static baseline vectors representing patient-specific parameters.

---

## 📊 Performance & Clinical Safety

A glucose model doesn't just need to be mathematically accurate—it needs to be **clinically safe**. 

* **Accuracy:** Reaches an **RMSE of ~15–20 mg/dL** and **MAE of ~10–14 mg/dL** on test patients.
* **Clinical Safety:** Over **98%** of predictions land inside **Zones A and B** of the **Clarke Error Grid Analysis (EGA)**. This means the model's predictions lead to safe, benign real-world treatment decisions rather than dangerous miscalculations.

---

## 📈 Visualizations

The notebook includes high-resolution plots evaluating model behavior:
1. **Preprocessing Quality:** Visualizing how 1D Gaussian filtering cleans out raw sensor noise while preserving real physiological peaks.
2. **24-Hour Trajectory Tracking:** Comparing actual vs. predicted glucose curves across daily meals, exercise, and night-time drops.
3. **Clarke Error Grid:** Mapping clinical risk across Zones A through E.

---

## 📁 What's in This Repo?

* `notebook4833f09b9b.ipynb`: Complete Kaggle notebook containing data preprocessing, model training, evaluation, and plotting logic.
* `glucose_lstm_model.pkl`: The complete saved PyTorch model weights, configuration dictionary, and feature scaler (`MinMaxScaler`) ready for inference.

---

## 🚀 Future Roadmap
- [ ] Upgrade the baseline to a full hybrid Transformer-LSTM (**Ls-Encoder**) architecture.
- [ ] Extend prediction horizons out to **60 minutes** and **120 minutes**.
- [ ] Build a lightweight real-time inference script for edge device deployment.
