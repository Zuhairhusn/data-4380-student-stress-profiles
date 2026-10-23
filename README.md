# Student Stress Profiles: An Unsupervised Machine Learning Study

**Course:** DATA 4380: Data Problems  
**Institution:** University of Texas at Arlington  
**Student Author:** Zuhair Syd  
**Instructor:** Dr. Masoud Rostami  
**Date:** Fall 2026  

---

## 1. Project Overview & Research Question

This repository contains the complete codebase, data processing pipeline, and unsupervised machine learning models for investigating student stress profiles among STEM university students.

### Core Research Question:
> *"Can unsupervised learning identify distinct student stress profiles, which variables contribute the most to profile identification, and does this change between genders?"*

Through feature engineering, multi-label binarization, correlation audits (Cramér's V and Pearson), and clustering model benchmarking (K-Means vs. GMM vs. Agglomerative Hierarchical), this study identifies **three statistically and clinically distinct student stress archetypes** and proves that peer social support acts as a primary protective buffer against academic burnout.

---

## 2. Repository Directory Structure

In compliance with the **DATA 4380 Submission Requirements**, the repository is structured as follows:

```text
├── tabular/
│   ├── data/
│   │   ├── survey.csv                   # Raw survey dataset (87 rows, 21 attributes)
│   │   └── survey_preprocessed.csv      # Clean, multi-hot and ordinally encoded dataset (87 rows, 38 features)
│   ├── figures/
│   │   ├── 01_lifestyle_and_workload_dashboard.png
│   │   ├── 02_stress_relief_frequencies.png
│   │   ├── 03_core_correlation_heatmap.png
│   │   ├── 04_kmeans_pca_stress_profiles.png
│   │   ├── 05_gender_profile_disparity.png
│   │   ├── 06_clustering_benchmark_comparison.png
│   │   ├── 07_cluster_profiles_comparison_lineplot.png
│   │   ├── 08_elbow_and_silhouette_evaluation.png
│   │   └── 09_cluster_feature_importance.png
│   ├── Student_Stress_Profiles_Solo_Project.ipynb    # Fully executed Jupyter Notebook with all outputs visible
│   └── Student_Stress_Profiles_Presentation.pptx     # 22-slide presentation deck matching course rubrics
├── requirements.txt                     # Pinned Python package dependencies for exact reproducibility
└── README.md                            # Complete documentation, methodology, and execution instructions
```

*(Note: For projects focusing exclusively on tabular/unsupervised data problems, the `/tabular/` directory houses the complete end-to-end pipeline).*

---

## 3. Dataset Description & Key Statistics

* **Cohort:** $N = 87$ undergraduate students in technical STEM majors (Data Science: 41, Computer Science: 34, IT: 9, Software Engineering: 3) across universities in Pakistan.
* **Gender Breakdown:** 63 Males (72.4%), 24 Females (27.6%).
* **Quality & Integrity:** 0 missing values across all modeled attributes.
* **Key Baseline Findings:**
  * **Sleep Deprivation:** 63.2% of students sleep $<7$ hours/night (57.5% modal at 4–6 hours).
  * **Physical Inactivity:** 48.3% participate in zero weekly sports or exercise.
  * **Academic Workload:** 69.0% rate their workload as heavy or very heavy (4 or 5 out of 5); zero students rated it light (1).
  * **Study Satisfaction Paradox:** Despite high workloads, 66.7% report high study satisfaction ($\ge 4/5$, mean 3.93), showing that distress is driven by coursework volume and physical exhaustion rather than disliking their field.

---

## 4. Methodology & Key Machine Learning Highlights

1. **Multi-Label Binarization (`MultiLabelBinarizer`):**  
   Parsed multi-select checkbox survey responses (`stress_relief_activities`) from 38 fragmented text combinations into 8 clean binary indicators without causing a feature explosion.
2. **Multicollinearity & Distance Protection (Cramér's V):**  
   Audited categorical dependencies and discovered high associations ($V > 0.60$) between university campus, major, and class year due to cohort sampling. Deliberately excluded raw demographic labels from Euclidean distance clustering to prevent the model from grouping students by campus instead of psychological state.
3. **Model Selection & Optimization Benchmarking:**  
   Benchmarked K-Means, Agglomerative Hierarchical Clustering, and Gaussian Mixture Models (GMM) across $k \in [2, 5]$ using Silhouette scores. **K-Means ($k=3$)** was chosen as optimal, capturing a crucial intermediate profile that binary $k=2$ models erase. Mathematical convergence was validated via a dual-axis Elbow Curve (Inertia drop from 645.9 to 581.2).
4. **Supervised Cluster Validation:**  
   Trained a 5-fold cross-validated Random Forest classifier on cluster labels, achieving **82.7% ($\pm 7.4\%$) out-of-fold accuracy**, proving that cluster boundaries are sharp, learnable, and statistically distinct.
5. **The Three Discovered Student Archetypes:**
   * **Profile 1: Resilient / Low Stress (25.3%, $N=22$):** Low distress (depression: 1.86, anxiety: 2.05), manageable workload, adequate sleep (7–8 hrs).
   * **Profile 2: Socially Buffered (26.4%, $N=23$):** Carries the *highest academic workload (4.22)* and *highest academic pressure (4.17)* in the entire study, yet remains protected from clinical depression (2.61) due to superior social relationships (**3.91 out of 5**) and high study satisfaction (**4.35 out of 5**).
   * **Profile 3: Severe Distress / High Burden (48.3%, $N=42$):** Compounding depression (4.26), anxiety (4.21), extreme isolation (4.31), chronic sleep deprivation ($<6$ hrs), and broken social support (2.14).
6. **Gender Disparity:**  
   Revealed a 20% vulnerability gap: **62.5% of female students fall into the Severe Distress profile** (vs. 42.9% of males). Females manifest distress primarily as academic/GPA performance anxiety, while males manifest distress primarily as future career dread.

---

## 5. Environment Setup & Instructions to Run

### Prerequisites
* Python 3.10+ (tested on Python 3.11 / 3.12)
* Jupyter Notebook or JupyterLab

### Installation
Clone the repository and install the dependencies:
```bash
git clone https://github.com/Zuhairhusn/data-4380-student-stress-profiles.git
cd data-4380-student-stress-profiles
pip install -r requirements.txt
```

### Running the Notebook
Launch Jupyter inside the `/tabular/` directory:
```bash
cd tabular
jupyter notebook Student_Stress_Profiles_Solo_Project.ipynb
```
Select **Kernel $\rightarrow$ Restart & Run All** to reproduce all preprocessing steps, statistical tables, benchmark outputs, and inline visualizations.

---

## 6. Author & Disclosure
* **Author:** Zuhair Syd (DATA 4380, Fall 2026)
* **Technical Assistance:** Google Gemini (AI pair-programming for visualization styling and script automation; all modeling decisions, data audits, and clinical interpretations directed and verified by the author).
