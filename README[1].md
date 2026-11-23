# Task 4: Final Bioinformatics Research Report
**SWYNEX Bioinformatics Internship**

* **Author:** Avnika Gehlot (B.Sc. Biotechnology, NIMS University, Jaipur)
* **Program:** SWYNEX Bioinformatics Internship (Capstone Report)
* **Date:** November 23, 2026
* **Full Report Document:** [`Task4_Final_Bioinformatics_Report.docx`](Task4_Final_Bioinformatics_Report.docx)

---

## 1. Research Question
* **Primary Biological Question:** Which differentially expressed genes and enriched signaling pathways (such as Wnt/beta-catenin) distinguish early-onset colorectal cancer (CRC) tumors from patient-matched normal adjacent colonic mucosa in public RNA-Seq data ([NCBI GEO: GSE251845](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE251845))?
* **Technical Quality Question:** Do sequencing reads maintain acceptable base-calling accuracy (`Q20`/`Q30`), follow an unimodal GC% distribution without contamination peaks, and show independence between GC% and base-call quality?

## 2. Methods
* **Dataset & Source:** Documented open-access human bulk RNA-Seq dataset **GSE251845** (Illumina NovaSeq 6000, `44` paired tumor/normal samples from `22` patients) and evaluated a reproducible `1,000 × 100 bp` FASTQ-style sequencing dataset (`seed=42`, Phred+33) in Python (`NumPy`, `pandas`, `SciPy`, `Matplotlib`).
* **Statistical & Visual Analysis:** Computed per-read GC%, mean/minimum Phred scores, global Q20/Q30 fractions, a one-sample t-test on GC%, and Pearson linear correlation (`r`, `p`-value) between GC% and mean Phred quality.

## 3. Key Results
| Metric | Result | Interpretation |
| :--- | :--- | :--- |
| **Per-Read GC Content** | Mean = `49.77%`, SD = `9.38%` | Unimodal bell-shaped distribution with no bimodal contamination peaks. |
| **Q20 / Q30 Base Accuracy** | `99.30% >= Q20` \| `68.75% >= Q30` | Strong base-calling accuracy with normal 5' to 3' cycle decay (`Q37` to `Q24`). |
| **GC% vs. Phred Correlation** | Pearson `r = -0.010` (`p = 0.740`) | No linear bias between GC composition and base-calling quality. |

![Figure 1: Per-Base Phred Quality](Fig1_Per_Base_Quality.png)
![Figure 2: GC Distribution and Correlation](Fig2_GC_and_Correlation.png)

## 4. Limitations
1. **Technical QC ≠ Biological Proof:** High Phred scores and balanced GC% verify sequencing quality but do not prove differential gene expression or clinical disease outcomes.
2. **No Reference Alignment:** FASTQ quality metrics do not measure genome mapping uniqueness, splice accuracy, or PCR duplicate rates.
3. **Benchmark Scope:** The `1,000 × 100 bp` dataset validates the Python QC workflow; paired-patient differential expression modeling (`~ Patient + Condition`) on all 44 `GSE251845` samples and wet-lab RT-qPCR validation are required for biological confirmation.

## 5. References
1. Marx, O., Mankarious, M., & Yochum, G. (2024). *Identification of unique gene expression and splicing events in early-onset colorectal cancer*. Frontiers in Oncology, 14, 1365762. PMID: 38680862 (`GSE251845`).
2. Ewing, B., & Green, P. (1998). *Base-calling of automated sequencer traces using Phred. II. Error probabilities*. Genome Research, 8(3), 186–194.
3. Andrews, S. (2010). *FastQC: A Quality Control Tool for High Throughput Sequence Data*. Babraham Bioinformatics.
4. Harris, C. R., et al. (2020). *Array programming with NumPy*. Nature, 585, 357–362.
5. Virtanen, P., et al. (2020). *SciPy 1.0: Fundamental algorithms for scientific computing in Python*. Nature Methods, 17, 261–272.
