# Misinformation and Opinion Project 

# Overview

This repository contains all code, data, documentation, and reports for the Misinformation group project. It was completed for COLX523 and COLX581 classes as part of the Master of Data Science - Computational Linguistics program at UBC. All credit for project origins to Garrett Nicolai at UBC. The work was completed by Nicole Shantz, Shiao-li Green, Jennifer Flake, and Rachelle De Jager. Additional annotation support was provided by Jasmine Zheng.

We investigated linguistic markers, including adjectives, capitalization, exclamation, hedging, and profanity, as signals for automated classification of misinformation and opinion in short social media and news items.

The purpose of the project was to first apply computational linguistics methods including traditional logistic regression, convolutional neural networks (CNN), and various ensembling approaches. We also explored annotations and inter-annotator agreement analysis. The second phase incorporated natural language processing methods for low-resource languages, including transfer learning, multi-task learning, active learning, bootstrapping, and few-shot learning.

---
# Dataset

As a foundational corpus, we used the [`Hugging Face Twitter Misinformation Dataset (Minassian)`](https://huggingface.co/datasets/roupenminassian/twitter-misinformation). We altered the corpus by annotating a subset of 1,000 examples to include relevant linguistic markers for misinformation, opinion, and fact. We labelled adjectives, capitalized words, exclamation marks, hedging words, and profanity. 

---

# Results

Our best misinformation classifier — a **Motivated Ensemble** combining logistic regression and CNN — achieved a **Macro F1 of 0.918**, meaningfully outperforming individual models. Our best opinion classifiers **Motivated Ensemble and Soft-Vote Ensemble** achieved a **Macro F1 of 0.761**.

Across both tasks, ensembling the top logistic regression and CNN models consistently outperformed any single model or enhancement strategy (transfer learning, multi-task learning, active learning, bootstrapping, or few-shot learning), suggesting the two model families capture different signals that are stronger when combined.

Misinformation classification outperformed opinion classification by roughly 0.16 Macro F1 points. This gap reflects the inherently subjective nature of the opinion label. Misinformation correlates more strongly
with surface-level stylistic signals (capitalization, exclamation, hedging), while opinion is
more subtle and context-dependent. 

For full methodology, experimentation details, and limitations, see the [final report](reports/final_report_Linguistic_Misinformation_Markers.pdf).

---
## Quickstart
 
Clone the repo, set up the environment, and launch the app:
 
```bash
git clone https://github.com/rdjg34/misinformation.git
cd misinformation
 
# Create and activate the conda environment
conda env create -f environment.yml
conda activate colx_523
 
# Start the FastAPI backend (from the app directory)
cd app
uvicorn be_fast:app --reload --port 8000
 
# In a separate terminal, start the Streamlit frontend (from the app directory)
streamlit run linguistic_markers_app.py
```
 
The app will open in your browser via Streamlit's local server. See [App_Setup_Instructions.md](documentation/App_Setup_Instructions.md) for more detail.
 
### No-setup option: run via Docker
 
If you'd rather skip the conda/Python setup, you can run the app directly with Docker Desktop. Make sure Docker Desktop is open and running first.
 
```bash
tar -xvf linguistic_markers_app.tar
cd app
docker-compose up --build
```
 
Then open http://localhost:8501 in your browser. See [docker-instructions.md](documentation/docker-instructions.md) for full details.
 
---

 
## Repository Structure
 
- **`app/`** — FastAPI backend and Streamlit frontend for the interactive search app
- **`data/`** — Raw and preprocessed datasets, final train/dev/test splits, and lexicons (COLX523; see [`data/raw/`](data/raw/), [`data/preprocessed/`](data/preprocessed/), [`data/final_splits/`](data/final_splits/), [`data/lexicons/`](data/lexicons/))
- **`documentation/`** — Technical documentation for the app, setup instructions, and Docker usage (COLX523)
- **`reports/`** — Project proposal, teamwork contract, and the final report
- **`src/`** — Source code for data collection, cleaning, and annotation analysis (COLX523)
- **`581_Sprint_1/` – `581_Sprint_4/`** — Modeling code, data, and documentation by sprint (COLX581)
- **`weekly_minutes/`** — Sprint meeting notes and action items

---

## Sprint Navigation

### Data & Interface (COLX523)

| Sprint | Focus | Explore |
|--------|-------|---------|
| Sprint 1 | Repo setup and team planning | — |
| Sprint 2 | Corpus collection, annotation plan, and annotation schema design | [`src/News_Scraper.py`](src/News_Scraper.py) |
| Sprint 3 | Hand-annotation, inter-annotator agreement study, interface design planning | [`src/Interannotator_Analysis.ipynb`](src/Interannotator_Analysis.ipynb) |
| Sprint 4 | Backend (FastAPI) and frontend (Streamlit) interface development | [`app/`](app/) |
| Sprint 5 | Dockerized the interface for deployment | [`app/Dockerfile`](app/Dockerfile) |

### Modeling (COLX581)

| Sprint | Focus | Explore |
|--------|-------|---------|
| Sprint 1 | Reasoned train/dev/test splitting and baseline models (LogReg, CNN) | [`581_Sprint_1/`](581_Sprint_1/) |
| Sprint 2 | Motivated ensembling and transfer learning | [`581_Sprint_2/`](581_Sprint_2/) |
| Sprint 3 | Multi-task learning with POS features | [`581_Sprint_3/`](581_Sprint_3/) |
| Sprint 4 | Bootstrapping, active learning, and few-shot learning | [`581_Sprint_4/`](581_Sprint_4/) |

For full methodology and results, see the [final report](reports/final_report_Linguistic_Misinformation_Markers.pdf).

---



