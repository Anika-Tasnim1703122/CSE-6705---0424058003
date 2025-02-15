# AutoNSGACytoNet Framework

## Step-by-Step Guidelines to Run the AutoNSGACytoNet Framework

### 1. Collect Data
- Collect **GDC TCGA gene expression RNAseq TPM data** for the following **Pancancer Cohorts**:
  - BRCA
  - LAML
  - LUAD
  - LUSC
  - COAD
  - SKCM
  - GBM
  - LIHC
- Data can be obtained from [Xena Browser](https://xenabrowser.net/datapages/).
- Already downloaded data is available in the **Dataset** folder.

### 2. Data Organization
- The **Dataset** folder contains directories named after each cancer type.
- Each directory contains `.tsv` format files.
- The `.tsv` files must be **transposed** to use genes as features.
- Merge transposed files using the **merging script** to generate the final dataset.
- **Note:** Set the dataset directory/path manually before running the code.

### 3. Preprocessing
- Use the **Preprocessing Data** notebook to generate a **preprocessed CSV file**.
- The preprocessed dataset is stored as `Preprocessed_8_cancer_genes.csv` in **Google Drive**.
- **Note:** Set the dataset directory/path manually before running the code.

### 4. Autoencoder-Based Feature Selection
- Input: `Preprocessed_8_cancer_genes.csv`
- Run the notebook **`autoencoders-with-cv.ipynb`** to generate:
  - `top_0.5_percent_features_cv.csv`
  - `top_0.25_percent_features_cv.csv`
  - `top_1.0_percent_features_cv.csv`
- **Note:** This notebook requires manual path adjustments.

### 5. NSGA-2 Feature Selection
- Run the notebook **`nsga2-with-rf-cv2.ipynb`**.
- Inputs:
  - `Preprocessed_8_cancer_genes.csv`
  - `top_0.5_percent_features_cv.csv`
  - `top_0.25_percent_features_cv.csv`
  - `top_1.0_percent_features_cv.csv`
- **Note:** Set the path manually.

### 6. NSGA-2 Output
- Running **`nsga2-with-rf-cv2.ipynb`** generates:
  - `NSGA2_77_compression_1.csv`
  - `NSGA2_308_compression_3.csv`
  - `NSGA2_154_compression_2.csv`

### 7. Protein-Protein Interaction (PPI) Network
- Use the gene subset from `NSGA2_308_compression_3.csv`.
- Upload this gene set to the **STRING database** to generate a **PPI network**.
- Download the network as `.tsv`.
- The file is also available in **Google Drive** as `string_interactions.tsv`.

### 8. Cytoscape Analysis
- Upload `string_interactions.tsv` to **Cytoscape** software with **cytoHubba dependency**.
- Select **13 hub genes** for evaluation.
- Cytoscape is an **open-source tool**.

### 9. Final Evaluation
- Run the **`classification.ipynb`** notebook.
- Inputs:
  - `Preprocessed_8_cancer_genes.csv`
  - The gene subset from Cytoscape (already hardcoded in the notebook).
- The output will include the desired **evaluation metrics**.

---

### **Notes:**
- Ensure all paths are set correctly before running scripts.
- Required data files are available in the **Google Drive** link.
- Use **Jupyter Notebooks** for execution.
- Install necessary dependencies before running the framework.

---

### **References**
- [Xena Browser](https://xenabrowser.net/datapages/)
- [STRING Database](https://string-db.org/)
- [Cytoscape](https://cytoscape.org/)

---

### **Necessary URL & Guidelines to run the Pipeline **
https://docs.google.com/document/d/1Dye8n9VxON_aXV4vLiQDhgUGNL6AiMhh/edit?usp=sharing&ouid=113103077976971185909&rtpof=true&sd=true

