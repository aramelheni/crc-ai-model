# Colorectal Cancer Prediction with Gut Microbiome Data

This project builds a machine learning model to **predict colorectal cancer (CRC)** based on the **gut microbiome composition** of patients, using **16S rRNA sequencing data** collapsed at the genus level.

---

## Project Workflow

### 1. Load the Data

* **`metadata.csv`**: Includes `SampleID` and whether the patient has CRC.
* **`seqtab_nochim.csv`**: Rows = samples, Columns = ASVs (amplicon sequence variants), Values = counts.
* **`taxa.csv`**: Maps ASVs to their taxonomic classification (e.g., Genus, Family).

---

### 2. Map ASVs to Genera

* Use the `taxa.csv` table to map each ASV to its genus.
* Missing genera are labeled as **Unassigned**.
* Rename ASV columns from IDs (e.g., `ASV_1234`) to genus names (e.g., `Bacteroides`).

---

### 3. Collapse to Genus Level

* Some ASVs belong to the same genus.
* Combine all columns with the same genus name by summing their counts per sample.

---

### 4. Join with Metadata

* Merge CRC status (from `metadata.csv`) with genus-level abundances.
* Save as **`seqtab_genus`**.
* Final table structure:

  * **Rows** = samples (patients’ stool samples).
  * **Columns** = bacterial genera (e.g., *Bacteroides*, *Prevotella*).
  * **Values** = read counts per genus.

---

### 5. Normalize the Microbiome Data

* Convert raw counts to **relative abundances** (percentage per sample).
* Prepare:

  * **X** = features (genus abundances)
  * **y** = labels (CRC status)

---

### 6. Split the Dataset

* Perform an **80/20 train-test split**.

---

### 7. Train a Random Forest Classifier

* Fit a **Random Forest** model to learn relationships between microbial genera and CRC status.
* Uses an ensemble of decision trees.

---

### 8. Evaluate Model Performance

* Report:

  * Precision
  * Recall
  * F1-score
  * Accuracy

---

### 9. Identify Important Genera

* Extract feature importance from the Random Forest.
* Highlight genera most predictive of CRC status.

---

## Dependencies

* Python 3.8+
* pandas, numpy, scikit-learn, matplotlib/seaborn (for analysis & visualization)

---

## Usage

1. Place the input files (`metadata.csv`, `seqtab_nochim.csv`, `taxa.csv`) in the working directory.
2. Run the preprocessing script to generate `seqtab_genus`.
3. Train the Random Forest model.
4. Evaluate results and inspect important genera.

---

## Output

* Trained model performance metrics.
* List of key microbial genera predictive of CRC.

---

## License

This project is open-source and available under the MIT License.
