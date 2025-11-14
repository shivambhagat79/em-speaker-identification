## MA515 – Fundamentals of Data Science

### EM–GMM Speaker Recognition (VoxCeleb1_Indian)

### Overview

- Goal: Identify the speaker of a short audio clip using Gaussian Mixture Models (GMMs) trained with the Expectation–Maximization (EM) algorithm.
- Approach: Train one GMM per speaker on MFCC features; predict by selecting the model with the highest average log-likelihood on the test clip.

### Team – For The Day Ones

- Shivam Bhagat (2022CSB1123)
- Prachi Chhabra (2022EEB1200)
- Saharsh Saxena (2022CBS1116)
- Pratibha Garg (2022EEB1204)
- Ishaan Sharma (2022EEB1173)
- Saaransh Sharma (2022CSB1114)

### Dataset

- Name: VoxCeleb1_Indian (subset with Indian celebrity speakers).
- Format: WAV audio files organized by speaker and YouTube video segment.
- Expected path in this repo: `dataset/vox1_indian/content/vox_indian/`
- Example structure:
  - `dataset/vox1_indian/content/vox_indian/<speaker_id>/<video_id>/<audio_files>.wav`

### Features and Models

- Features: Mel-Frequency Cepstral Coefficients (MFCCs).
  - Hyperparameter `n_mfcc`: number of MFCC coefficients per frame.
- Model: Custom EM-based Gaussian Mixture Model (no external GMM library).
  - Hyperparameter `n_components`: number of Gaussian components per speaker.
  - Regularized covariances and numeric safeguards for stability.

### Results (from notebook run)

- Optimal hyperparameters: `n_mfcc = 12`, `n_components = 16`.
- Final accuracy: `88.48%` (test clips correctly classified over total).
- Observation: A moderate MFCC count and mixture size balanced detail and stability.

### Repository Structure (abridged)

- `main.ipynb` – End-to-end workflow: data split, feature extraction, model training, evaluation, hyperparameter sweeps, and final run.
- `requirements.txt` – Python dependencies.
- `dataset/` – Data root; see structure above.
- `results/` – Placeholder for any saved outputs (optional, not required by the notebook).

### Requirements

- Python 3.x
- Packages (from `requirements.txt`):
  - `numpy`
  - `matplotlib`
  - `librosa`

### Setup

```powershell
# From repo root
python -m venv .venv; .\\.venv\\Scripts\\Activate.ps1
pip install -r requirements.txt
```

### Running the Notebook

1. Ensure the dataset is available under `dataset/vox1_indian/content/vox_indian/` with the expected speaker/video hierarchy.
2. Open `main.ipynb` and run cells sequentially:
   - Data loading and splitting
   - MFCC feature extraction
   - GMM training (one model per speaker)
   - Evaluation and hyperparameter sweeps
   - Final run with best hyperparameters

### Configuration Notes

- The dataset path is set in the notebook via:
  - `dataset_path = 'dataset/vox1_indian/content/vox_indian/'`
- Random shuffle affects the train/test split; results may vary unless a seed is fixed.
- Audio sampling uses the file’s native sample rate (`sr=None` in `librosa.load`).

### Reproducing Hyperparameter Sweeps

- The notebook sweeps:
  - `n_mfcc` over `[2, 6, 12, 18, 24]` (with `n_components=16`)
  - `n_components` over `[2, 6, 12, 18, 24]` (with `n_mfcc=8`)
- Accuracy vs. hyperparameter plots are displayed inline (`matplotlib`).

### Acknowledgements

- VoxCeleb creators and community for the underlying dataset and structure.
- `librosa` for audio loading and MFCC feature extraction utilities.
