**SingleCell Internship - Stage 2**

**Single-Cell RNA-seq Analysis of Lung Sample Using a Standard Scanpy Workflow**

**Objective**

Identify the tissue of origin and biologically interpret the cell types present in a single-cell RNA-seq dataset.

**Workflow Summary**

**0\. Tools & Dataset Preparation**

**Installed and imported:**  
scanpy, anndata, igraph, celltypist, decoupler, fa2-modified, pandas, seaborn.

**Dataset:**  
.h5ad file loaded and explored to inspect structure, metadata, and gene/cell counts.

**1\. Pre-processing: Quality Control & Normalization**

**Quality Control Steps**

- Removed duplicated gene names.
- Calculated QC metrics:
  - genes per cell
  - UMI counts
  - mitochondrial, ribosomal, hemoglobin gene content
- Thresholds considered: **MT < 5%**, **RIBO < 10%**, **HB < 5%**
- **Filtering not required** due to low contamination (MT < 2%, RIBO < 5%, no HB).
- Doublet removal using **Scrublet**.

**Normalization**

- Standard Scanpy normalization workflow.
- Selected **1,000 highly variable genes** for downstream analysis.

**2\. Cell Population Analysis**

**Dimensionality Reduction**

- Performed **PCA** on HVGs.

**Clustering**

- Built neighborhood graph.
- Ran **Leiden clustering** to define transcriptionally distinct groups.
- Visualized results with **UMAP**.

**Cell Type Annotation**

- Used canonical marker genes + references (e.g., PanglaoDB).
- Performed enrichment with decoupler.
- Projected annotated cell identities onto UMAP.

**Findings**

**Identified 11 Cell Types**

- **Alveolar macrophages** (dominant population)
- **T cytotoxic cells**
- **T memory cells**
- **Gamma delta T cells**
- **NK cells**
- **Monocytes**
- **Plasma cells**
- **T cells (general)**
- **Memory B cells**
- **Epiblast-like cells**
- **Platelets**

**Immune Lineage Composition**

- **Lymphoid lineage:** ~77%
- **Myeloid lineage:** ~32%
- **Non-immune:** epiblast-like cells, platelets

**Biological Interpretation**

**1\. Tissue Origin**

The dataset **does not resemble bone marrow**.  
Instead, cell composition strongly indicates **lung tissue**, specifically **bronchoalveolar lavage (BALF)**:

- Presence of **alveolar macrophages** (lung-resident)
- Absence of **HSCs, progenitors, erythroid lineage, megakaryocytes, stromal cells**
- Dominance of mature, tissue-resident, and mucosal immune cells

**2\. Health State of the Patient**

The relative abundances suggest **moderate to significant inflammation**, consistent with **ongoing infection**, likely viral.

Key indicators:

- **Monocytes 12%** → high recruitment to lung
- **Alveolar macrophages reduced** from expected 80-95% → dilution by infiltrating immune cells
- **Lymphocytes expanded to ~67%** → strong adaptive immune activation
- **Elevated NK and cytotoxic T cells** → typical of viral response

Overall, the immune landscape represents an **inflamed lung environment** with active innate and adaptive responses.

**Conclusion**

- The sample originates from **lung / BALF**, not bone marrow.
- The immune profile indicates **active infection or significant inflammation**.
- Identified populations reflect a **robust antiviral and inflammatory response** involving monocytes, cytotoxic T cells, NK cells, γδ T cells, and antibody-producing plasma cells.
