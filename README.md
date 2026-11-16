# NeuroPulse: LSTM-Based Synthetic ECG Signal Generation

**An academic deep learning project exploring synthetic ECG signal generation using Long Short-Term Memory (LSTM) networks.**

## Project Overview

NeuroPulse explores the application of Long Short-Term Memory (LSTM) neural networks to learn sequential patterns in electrocardiogram (ECG) signals and generate experimental synthetic ECG continuations.

The project uses the **MIT-BIH Arrhythmia Database**, specifically Record 100, and implements two approaches:

1. **Continuous ECG LSTM:** Next-sample prediction using sliding windows, followed by autoregressive signal continuation.
2. **Heartbeat-Based LSTM:** Normal heartbeat extraction using ECG annotations, followed by sequence-to-sequence next-sample prediction and experimental heartbeat continuation.

The aim is to investigate how LSTM models learn ECG signal patterns. The generated signals are experimental and are not clinically validated.

## Objectives

- Load and explore ECG recordings from the MIT-BIH Arrhythmia Database.
- Perform ECG signal filtering and preprocessing.
- Develop an LSTM model for continuous ECG next-sample prediction.
- Extract annotated normal heartbeats and prepare heartbeat sequences.
- Develop a second LSTM model for heartbeat sequence prediction.
- Evaluate both models using Mean Squared Error (MSE) and Mean Absolute Error (MAE).
- Explore autoregressive generation of synthetic ECG signal continuations.

## Dataset

**MIT-BIH Arrhythmia Database**

- Record used: `100`
- Sampling frequency: 360 Hz
- Signal: First ECG channel
- Source: [PhysioNet – MIT-BIH Arrhythmia Database](https://physionet.org/content/mitdb/1.0.0/)

The dataset includes ECG recordings and corresponding annotations used to identify heartbeat events.

## Technologies Used

- Python
- Google Colab
- TensorFlow / Keras
- NumPy
- Pandas
- Matplotlib
- SciPy
- Scikit-learn
- WFDB

## Methodology

### 1. Data Acquisition and Exploratory Data Analysis

- Downloaded MIT-BIH Record 100 using the WFDB Python package.
- Inspected ECG signal characteristics.
- Examined descriptive statistics, signal distribution and missing values.
- Visualized the original ECG waveform.

### 2. Signal Preprocessing

- Applied a Butterworth bandpass filter with cutoff frequencies of 0.5–40 Hz.
- Split the continuous recording chronologically into training (70%), validation (15%) and testing (15%) partitions.
- Applied MinMax scaling using training data.

### 3. Experiment 1 – Continuous ECG LSTM

- Created sliding-window sequences using 180 previous samples.
- Developed a stacked LSTM architecture for next-sample prediction.
- Evaluated predictions using the held-out test partition.
- Generated a 5-second autoregressive ECG continuation.

### 4. Experiment 2 – Heartbeat-Based LSTM

- Used WFDB annotations to identify normal (`N`) heartbeat events.
- Extracted heartbeat segments containing 216 samples (0.6 seconds).
- Used 0.2 seconds before and 0.4 seconds after the annotated beat location.
- Developed a sequence-to-sequence LSTM model for within-beat next-sample prediction.
- Generated an experimental heartbeat continuation from a held-out beat prefix.

## Experimental Results

The following metrics were obtained from the executed notebook:

| Experiment           |   Test MSE | Test MAE |
| -------------------- | ---------: | -------: |
| Continuous ECG LSTM  | 0.00000917 | 0.001338 |
| Heartbeat-Based LSTM | 0.00004579 | 0.003015 |

The metrics are calculated on normalized/scaled signal values.

These results measure next-sample prediction performance on the respective test partitions. They do not establish clinical validity or prove that generated signals reproduce realistic ECG morphology.

## Repository Structure

```text
NeuroPulse-LSTM-ECG-Generation/
│
├── NeuroPulse.ipynb
├── README.md
└── requirements.txt
```

The notebook also contains code to save generated signal CSV files, evaluation summaries and trained models into `neuropulse_outputs/` and `neuropulse_models/` when executed.

## How to Run

1. Clone or download this repository.
2. Open `NeuroPulse.ipynb` in Google Colab.
3. Install the required dependencies using:

```bash
pip install -r requirements.txt
```

4. Run the notebook cells in sequence.
5. The notebook downloads MIT-BIH Record 100 through WFDB.
6. Review the plots, model evaluation results and generated signal outputs.

A Google Colab environment is recommended.

## Limitations

- The experiments use a single ECG recording (Record 100).
- Results from one recording may not generalize to other individuals or ECG recordings.
- Autoregressive generation can accumulate prediction errors.
- Low next-sample prediction error does not necessarily indicate realistic synthetic ECG morphology.
- The generated signals have not undergone clinical validation.

## Future Scope

- Evaluate the models on additional MIT-BIH records.
- Explore alternative deep learning architectures.
- Improve long-term signal generation stability.
- Investigate more comprehensive signal-quality evaluation metrics.
- Compare different generative modelling approaches.

## References

1. Moody, G. B., & Mark, R. G. (2001). The impact of the MIT-BIH Arrhythmia Database. *IEEE Engineering in Medicine and Biology Magazine*, 20(3), 45–50.
2. [MIT-BIH Arrhythmia Database – PhysioNet](https://physionet.org/content/mitdb/1.0.0/)
3. [WFDB Python Documentation](https://wfdb.readthedocs.io/)
4. [TensorFlow Documentation](https://www.tensorflow.org/guide/keras)

## Disclaimer

This project is developed for academic and educational purposes only. The generated ECG signals are experimental outputs and are not clinically validated. They must not be used for medical diagnosis, treatment or clinical decision-making.

---

**Author:** Frinu P. Sunny

**Project:** NeuroPulse – LSTM-Based Synthetic ECG Signal Generation
