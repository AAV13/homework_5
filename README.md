# Comparative Analysis of Gun Violence Coverage Across News Outlets

## Project Overview
This project applies Natural Language Processing (NLP) techniques to analyze how four major news outlets (CNN, Fox News, The New York Times, and The Wall Street Journal) frame victims and shooters in gun violence incidents. 

The pipeline performs the following tasks:
1.  **Context Extraction:** Identifies relevant text segments using coreference resolution (resolving pronouns like "he" to "the shooter").
2.  **Description Extraction:** Uses dependency parsing to extract adjectives and verbs associated with entities.
3.  **Semantic Clustering:** Clusters these descriptions using SBERT embeddings and DBSCAN/K-Means to identify common "frames" (e.g., Mental Health, Youth, Violence).
4.  **Statistical Analysis:** Conducts Chi-Square tests to determine if the usage of these frames differs significantly across news outlets.

## Prerequisites
* Python 3.8 or higher
* Jupyter Notebook (optional, if running the `.ipynb` file)

## Installation

1.  **Clone or Download the Repository**
    Ensure all files are in a single directory.

2.  **Install Dependencies**
    Run the following command to install the required Python libraries:
    ```bash
    pip install -r requirements.txt
    ```

3.  **Download Language Models**
    The project requires the English language model for spaCy:
    ```bash
    python -m spacy download en_core_web_sm
    ```

## Dataset Structure
The script expects the dataset to be unzipped and organized in the following structure:
