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

├── Dataset_Extracted │ └── data_100 │ ├── cnn_five_para │ ├── FOX_five_para │ ├── NYT_five_para │ └── WSJ_five_para

*Note: Ensure the `DATA_DIR` variable in the script matches your local folder path.*

## Usage

1.  **Run the Pipeline**
    Execute the Python script or Jupyter Notebook:
    ```bash
    python gun_violence_analysis.py
    ```
    *(Or open the notebook and run all cells)*

2.  **Process Flow**
    * The script first loads and cleans the text data.
    * It applies `fastcoref` to resolve entity mentions.
    * It extracts descriptors and generates semantic clusters.
    * It prints the statistical results (Chi-Square tests) to the console.
    * It displays a heatmap visualization of frame distributions.

## Output
The project generates the following outputs:

* **Console Output:** Statistical significance results (p-values) for each framing cluster.
* **Visualizations:** A heatmap showing the frequency of specific frames across different news outlets.
* **Data Export:** A CSV file named `Final_Processed_Dataset_with_Clusters.csv`. This file contains:
    * `outlet`: The news source (CNN, FOX, etc.)
    * `context`: The full sentence containing the entity.
    * `descriptors_list`: The specific words extracted (e.g., "young", "fired").
    * `cluster_label`: The semantic category assigned to the description.

<img width="1116" height="590" alt="image" src="https://github.com/user-attachments/assets/3dc18657-dfbc-411e-b754-a3b4c01cbefe" />

--- Chi-Square Test Results ---

Frame                                    | P-Value    | Result

-----------------------------------------------------------------
Passive State (was, being)               | 0.1409     | Not Significant

Investigation Status (active, identified) | 0.9693     | Not Significant

Attribution (said, told)                 | 0.2371     | Not Significant

Identity & Outcome (dead, former, old)   | 0.0068     | **SIGNIFICANT**

Event Context (transpired)               | 0.0050     | **SIGNIFICANT**

## Methodology Notes
* **Coreference Resolution:** Utilized `fastcoref` (LingMess architecture) for high-speed, accurate entity resolution.
* **Clustering:** Employed Sentence-BERT (`all-MiniLM-L6-v2`) for embeddings, reduced via UMAP, and clustered using DBSCAN (with a K-Means fallback for sparse data).
* **Statistical Test:** Pearson’s Chi-Squared Test of Homogeneity ($p < 0.05$ threshold).
