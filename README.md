#  Symptom-Based Disease Prediction System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-Pattern%20Matching-blueviolet?style=for-the-badge)


**An AI-powered healthcare chatbot that leverages Machine Learning and NLP to predict diseases from user-reported symptoms — with voice interaction support.**

[ Overview](#-overview) • [ Features](#-features) • [ Project Structure](#️-project-structure) • [ Installation](#️-installation) • [ Usage](#-usage) • [ Model Details](#-model-details) • [ Dataset](#-dataset) • [ Roadmap](#️-roadmap)

</div>

---

##  Overview

This project implements a conversational healthcare chatbot that predicts diseases based on symptoms entered by the user. It employs two complementary machine learning classifiers — a **Decision Tree** and a **Support Vector Machine (SVM)** — to provide robust, dual-validated disease predictions.

The chatbot interacts with users in a step-by-step dialogue, collects symptoms, evaluates severity, and outputs:
-  **Predicted disease(s)**
-  **Disease description**
- **everity assessment** (consult doctor or take precautions)
-  **Recommended precautions**
- **Text-to-speech output** for an accessible, natural experience

>  **Disclaimer:** This tool is intended for educational and informational purposes only. It is **not a substitute for professional medical advice**. Always consult a qualified healthcare provider for medical decisions.

---

##  Features

| Feature | Description |
|---|---|
|  **Dual ML Models** | Decision Tree + SVM for cross-validated, reliable predictions |
|  **Conversational UI** | Step-by-step symptom collection via interactive chat |
|  **Text-to-Speech** | Voice output using `pyttsx3` for accessible interaction |
|  **NLP Pattern Matching** | Regex-based symptom matching handles partial and fuzzy inputs |
|  **Severity Scoring** | Calculates condition severity from symptom weights and duration |
|  **Rich Output** | Returns disease descriptions, precautions, and doctor recommendations |
|  **EDA Visualizations** | Seaborn/Matplotlib charts for dataset exploration |

---

##  Project Structure

```
Symptom-Based-Disease-Prediction-System/
│
├──  Symptom_Based_Disease_Prediction_Chatbot.ipynb   # Main notebook (EDA + Model + Chatbot)
├── Symptom_Based_Disease_Prediction_Chatbot.html    # Exported HTML view of the notebook
├──  requirements.txt                                  # Python dependencies
├── LICENSE                                           # MIT License
├──  README.md                                         # Project documentation
│
└──  Data/
    ├── Training.csv             # Training dataset (symptoms → prognosis)
    ├── Testing.csv              # Holdout test dataset
    ├── Symptom_severity.csv     # Severity weight per symptom
    ├── symptom_Description.csv  # Disease descriptions
    └── symptom_precaution.csv   # Recommended precautions per disease
```

---

## Installation

### Prerequisites
- Python **3.9+** (developed on 3.11)
- Jupyter Notebook / JupyterLab

### 1. Clone the Repository
```bash
git clone https://github.com/Aditya07129/symptom-based-disease-prediction-system.git
cd symptom-based-disease-prediction-system
```

### 2. Create a Virtual Environment (Recommended)
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

> **Note for Linux/macOS users:** `pyttsx3` requires `espeak` for text-to-speech.
> ```bash
> sudo apt-get install espeak    # Debian/Ubuntu
> brew install espeak            # macOS (Homebrew)
> ```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook
```

Open `Symptom_Based_Disease_Prediction_Chatbot.ipynb` and run all cells.

---

##  Usage

Once all cells are executed, the chatbot starts an interactive session in the notebook output:

```
------- HealthCare ChatBot -------

Your Name? → John
Hello, John

Enter the symptom you are experiencing → fever
Searches related to input:
  0) high_fever
  1) mild_fever
Select the one you meant (0 - 1): 0

Okay. From how many days?: 3

Are you experiencing any of the following?
  headache? : yes
  fatigue? : yes
  ...

You may have Typhoid.
<Disease Description>

Take following measures:
  1) Eat high calorie meals
  2) Avoid going outside
  ...
```

---

##  Model Details

### Algorithms Used

| Model | Role | Key Metric |
|---|---|---|
| **Decision Tree Classifier** | Primary predictor — traverses symptom tree to reach diagnosis | Cross-Val Score: ~97% |
| **Support Vector Classifier (SVC)** | Secondary validator — confirms or provides alternate diagnosis | Test Accuracy: ~100% |

### Workflow

```
Raw Symptoms Input
       ↓
NLP Pattern Matching (regex)
       ↓
Decision Tree → Primary Disease Prediction
       ↓
Secondary SVM Prediction
       ↓
Severity Calculation (symptom weights × duration)
       ↓
Output: Disease + Description + Precautions
```

### Data Preprocessing
- **Label Encoding** — converts string prognosis labels to numerical classes
- **Train/Test Split** — 67% train / 33% test (`random_state=42`)
- **Cross-Validation** — 3-fold CV on the Decision Tree model

---

##  Dataset

The dataset maps **132 symptoms** to **41 diseases** using binary feature vectors.

| File | Rows | Description |
|---|---|---|
| `Training.csv` | 4,920 | Primary training data |
| `Testing.csv` | 42 | Holdout evaluation set |
| `Symptom_severity.csv` | 133 | Severity weight (1–7) per symptom |
| `symptom_Description.csv` | 41 | Short descriptions of each disease |
| `symptom_precaution.csv` | 41 | Up to 4 precautions per disease |

**Source:** Adapted from the [Kaggle Disease Symptom Dataset](https://www.kaggle.com/datasets/itachi9604/disease-symptom-description-dataset).

---

##  Tech Stack

| Technology | Purpose |
|---|---|
| **Python 3.11** | Core language |
| **Pandas / NumPy** | Data manipulation |
| **scikit-learn** | ML model training & evaluation |
| **pyttsx3** | Offline text-to-speech engine |
| **Seaborn / Matplotlib** | EDA visualizations |
| **re (regex)** | NLP symptom pattern matching |
| **Jupyter Notebook** | Interactive development environment |

---

##  Roadmap

- [ ]  Deploy as a Flask / FastAPI web application
- [ ]  Build a React Native mobile app
- [ ] Integrate a Transformer-based NLP model (e.g., BioBERT) for free-text symptom extraction
- [ ]  Expand dataset to cover 200+ diseases
- [ ]  Add user session history and personalized health tracking
- [ ]  Multi-language support

---

##  Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'feat: add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

##  Author

**Aditya**
- GitHub: [@Aditya07129](https://github.com/Aditya07129)

---

<div align="center">



*Built  for accessible healthcare information

</div>
