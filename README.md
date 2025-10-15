# Hybrid SFANC‑FxNLMS Active Noise Control System (using Deep Learning)

[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/)  
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)  

This repository provides the implementation of the **Hybrid SFANC‑FxNLMS algorithm** for Active Noise Control (ANC) as proposed in the paper:

> “A Hybrid SFANC‑FxNLMS Algorithm for Active Noise Control Based on Deep Learning” (IEEE Signal Processing Letters, 2022)  
> Authors: Zhengding Luo, Dongyuan Shi, Woon‑Seng Gan
>
> "Optimised Deep Learning ANC with FxEHCAF Algorithm "
> 
> Authors: Krishna Kumar, Devansh Wadhvana, Hard Kapadia

The hybrid approach combines a **lightweight 1D CNN** for selecting a pre-trained control filter per frame and the **FxNLMS** algorithm to dynamically update its coefficients at the sampling rate.

---

## 📂 Repository Structure

```
Hybrid‑SFANC‑FxNLMS-Active-Noise-Control-System-using-Deep-Learning/
│
├── Primary and Secondary Path/        # (Likely measurement data or simulation path models)
├── Real Noise Examples/               # Real-world noise WAV/recordings
├── Trained models/                    # Pre-trained CNN models (e.g. model.pth)  
├── __pycache__/  
├── Bcolors.py  
├── Combine_SFANC_with_FxNLMS.py        # Main script combining modules  
├── Control_filter_selection.py         # CNN filter-selector module  
├── Disturbance_generation.py           # Generates synthetic noise for training/testing  
├── FxNLMS_algorithm.py                # Implementation of FxNLMS  
├── Network.py                          # CNN network architecture  
├── README.md  
├── README.txt  
├── Reading_path_test.py  
├── SFANC‑FxNLMS for ANC.ipynb          # Jupyter notebook demo / experiments  
└── loading_real_wave_noise.py          # Script to load real noise files  
```

---

## 📝 What It Does / Overview

- Trains a **1D convolutional neural network (CNN)** to **choose** the best pre-trained control filter given a noise frame.  
- After selecting, uses the **FxNLMS algorithm** to **adaptively update** the coefficients of that filter at the sample level.  
- The hybrid method is designed to **speed up convergence**, **improve noise attenuation**, and **adapt better** to varying acoustic conditions.  
- You can run real-world tests using `SFANC‑FxNLMS for ANC.ipynb`, with the provided real noise recordings.  

---

## 🛠️ Setup & Usage

### Requirements

- Python 3.9 or newer (tested with 3.9.7)  
- PyTorch (1.10.1)  
- Jupyter Notebook  
- Standard Python libs: `numpy`, `scipy`, `matplotlib`, etc.

You can install dependencies via:

```bash
pip install -r requirements.txt
```

*(If you don’t already have `requirements.txt`, generate one including your needed libs.)*

### Running the Project

1. **Pre-trained model usage**  
   Use the CNN model already saved in `Trained models/model.pth` to run the hybrid algorithm without retraining.  

2. **Train the CNN filter selector**  
   The repo description states:  
   > They generated 80,000 broadband noise tracks (1 s each) with random bands, amplitudes, backgrounds for train/validation/test.  
   Use your training script (if present) or adapt `Disturbance_generation.py` + `Network.py` to train.

3. **Run hybrid SFANC + FxNLMS**  
   Use `Combine_SFANC_with_FxNLMS.py` or the Jupyter notebook `SFANC‑FxNLMS for ANC.ipynb` on real noise examples in `Real Noise Examples/`.  

4. **Loading real noise**  
   Use `loading_real_wave_noise.py` to load and preprocess real recordings.

5. **Testing path / setup**  
   `Reading_path_test.py` likely helps evaluate primary and secondary path responses or test the system behavior under path variations.

---

## 📊 Expected Results & Performance

- The hybrid algorithm aims to **overcome slow convergence** typical of standard adaptive methods, while achieving **better noise reduction** than the base SFANC method.  
- Real noise tests in the notebook should illustrate attenuation levels and convergence plots.

---

## 🎯 How to Cite This Work

If you use or extend this repository in your research, please cite the original paper:

```
@ARTICLE{9761749,
  author={Luo, Zhengding and Shi, Dongyuan and Gan, Woon‑Seng},
  journal={IEEE Signal Processing Letters},
  title={A Hybrid SFANC‑FxNLMS Algorithm for Active Noise Control Based on Deep Learning},
  year={2022},
  volume={29},
  pages={1102‑1106},
  doi={10.1109/LSP.2022.3169428}
}
```

---

## ⚠️ Notes & Tips

- Ensure **sampling rate consistency** across your noise signals, network input, and FxNLMS algorithm.  
- The CNN acts at the **frame level**, while FxNLMS works at **sample level**.  
- You may need to **modify filter lengths**, **step sizes**, or **CNN architecture** when moving to new acoustic environments.  
- Use the provided real noise examples to validate the approach under real-world conditions.

---

## 📬 Contact / Acknowledgments

- For queries on the original algorithm: Zhengding Luo (LUOZ0021@e.ntu.edu.sg), Dongyuan Shi (dongyuan.shi@ntu.edu.sg)  
- For modifications, issues, or enhancement suggestions, feel free to open an issue in this repo.

---

## 🏷️ License

This repository is distributed under the **MIT License**. See the [LICENSE](LICENSE) file for more details.

---

**Tip:** Once you paste this into your repo, you can enhance it further by adding:

- Project **logo or a figure** (from your paper)  
- **Badges** (build, coverage, GitHub Actions)  
- **Demo GIFs or audio samples**  
- More **examples / tutorials**
