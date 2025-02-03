# scGPT-GBM-classifier

This repository contains two folders (final_analysis & testing_examples) using Richards 2021 data and Neftel 2019 data, respectively. Inside each folder, you will find two Jupyter notebooks for analyzing glioblastoma data using scGPT. 

The workflow is as follows:

1. **Embedding and Classification**  
   `scGPT_Embedding_Tasks_GBM_Classifier.ipynb`  
   This notebook:
   - Connects to Google Drive and sets up the environment.
   - Downloads necessary scGPT model checkpoints and data from Google Drive.
   - Loads and preprocesses the GBM datasets.
   - Embeds reference and query data using scGPT.
   - Maps cell type annotations from a reference dataset to a query dataset.
   - Computes performance metrics and plots a confusion matrix of predicted vs. true labels.

2. **UMAP Post-Processing**  
   `scGPT_Post_Processing_UMAP_GBM_Classifier.ipynb`  
   This notebook performs the following:
   - Loads the concatenated embedded AnnData object from the first notebook.
   - Computes neighbourhood graphs, UMAP embeddings, and clustering.
   - Visualizes the results (e.g., UMAP plots with cell type labels).
   - Optionally, computes the Adjusted Rand Index (ARI) to evaluate clustering performance.

---

## Requirements

- **Runtime**  
  We recommend Google Colab with a runtime that supports Python ≤3.10. For best performance:
  - Use **L4** GPUs (or A100 for faster embedding tasks) with Google Colab Pro.
  - If using the free version (T4 GPU), follow the instructions in the testing_examples notebooks.

- **Python Version**  
  The notebooks are designed for Python 3.10.12.  
  **IMPORTANT:** In Colab, set your runtime to "fallback" to Python 3.10 if you see Python 3.11 was loaded.

- **Dependencies**  
  The notebooks install and upgrade packages such as `scgpt`, `wandb`, `faiss-gpu`, `scanpy`, `torch`, among others.  
  For the full list for reproducibility, see the last cell of each notebook (i.e., `pip freeze`).

---

## Setup & Usage

1. **Open the Notebooks in Google Colab**

2. **Set Up the Runtime**
   - Connect to a GPU runtime (L4 is recommended).
   - Use the Command Palette to select "Use fallback runtime version" so that the Python version is set to 3.10.12.

3. **Mount Your Google Drive**
   - Both notebooks require you to mount your Google Drive to read/write data and save generated files (e.g., embedded AnnData objects, UMAP coordinates).

4. **Run Notebook Cells Sequentially**
   - Start with the embedding notebook to generate the reference and query embeddings.
   - Then run the UMAP post-processing notebook to visualize the embeddings and evaluate the performance metrics (e.g., ARI).

5. **Data Access**
   - The notebooks download data from Google Drive. Make sure you have proper access or adjust the URLs if you use your own data.

---

## External Data Sources

- **GBmap Datasets**  
  GBmap data was downloaded via [CELLxGENE](https://cellxgene.cziscience.com/collections/999f2a15-3d7e-440b-96ae-2c806799c08c). Included in this analysis is the "Core" GBmap atlas. Read more: [GBmap Pre-print](https://doi.org/10.1101/2022.08.27.505439).
  
- **Neftel 2019 Datasets**  
  Neftel 2019 data is available via [Broad Single Cell Portal](https://singlecell.broadinstitute.org/single_cell/study/SCP393). Data for this analysis was filtered from the original GBmap data. Read more: [Neftel 2019 Cell Publication](https://doi.org/10.1016/j.cell.2019.06.024).

- **Richards 2021 Dataset**  
  Richards 2019 data was downloaded and available via [CReSCENT](https://crescent.cloud) and [Broad Single Cell Portal](https://singlecell.broadinstitute.org/single_cell/study/SCP503). Richards tumour data for this analysis was filtered from the original GBmap data and GSC data (glioblastoma stem cells) from CReSCENT. Read more: [Richards 2021 Nature Cancer Publication](https://doi.org/10.1038/s43018-020-00154-9).
---

## Additional Notes

- **FAISS Installation**  
  The first notebook checks for `faiss` installation for fast similarity search. If it is not installed, you can follow the [FAISS installation guide](https://github.com/facebookresearch/faiss/wiki/Installing-Faiss).

- **Customization**  
  You can modify cell type keys (`annotation_level_3` or `cell_type`) and other parameters (like the number of nearest neighbors `k`) to suit your analysis.

- **scGPT**  
  This repository is based on the [scGPT GitHub tutorial](https://github.com/bowang-lab/scGPT/blob/main/tutorials/zero-shot/Tutorial_ZeroShot_Reference_Mapping.ipynb). Read more: [scGPT 2024 Nature Methods Publication](https://doi.org/10.1038/s41592-024-02201-0).

- **Contact**  
  If you run into any problems, please contact Suluxan Mohanraj or leave a GitHub issue in this repository!
