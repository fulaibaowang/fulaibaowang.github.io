---
title: "0-NGS"
permalink: /publication/0-NGS
date: 2025-02-17
---
| Layer / Goal                                      | Widely used method(s)             | Paired newer method(s)                                      | Why the newer one is superior                                         | **Main purpose**                                              |
| ------------------------------------------------- | --------------------------------- | ----------------------------------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------- |
| **DNA: genome & SVs**                             | Short-read WGS (Illumina)         | Long-read WGS (PacBio HiFi, ONT Q20+); hybrid assemblies    | Resolves repeats & SVs; phasing/haplotypes; fewer mapping ambiguities | Detect SNVs, indels, SVs, CNVs, haplotypes                    |
| **DNA: methylation**                              | WGBS / RRBS                       | EM-seq / TAPS; ONT direct 5mC calling                       | Less DNA damage, GC bias; direct multi-base detection                 | Base-level 5mC/5hmC methylome and allele-specific methylation |
| **Chromatin accessibility**                       | ATAC-seq / scATAC                 | Multiome (ATAC+RNA); long-read ATAC                         | Joint regulatory info; better peak-to-gene linkage                    | Identify open chromatin regions, TF footprints                |
| **Protein–DNA binding**                           | ChIP-seq                          | CUT&Tag / CUT&RUN                                           | Higher signal-to-noise, lower input, fewer artifacts                  | Map TF or histone mark binding sites                          |
| **3D genome**                                     | Hi-C (in situ)                    | Micro-C; HiChIP; single-cell Hi-C                           | Nucleosome resolution, mark-anchored loops, single-cell structure     | Reveal chromatin loops, domains, and genome folding           |
| **RNA: expression**                               | RNA-seq (ribo-minus, stranded)    | Long-read RNA-seq (Iso-Seq, ONT); UMI-based high-throughput | Full-length isoforms, better quant accuracy                           | Quantify transcript abundance and differential expression     |
| **RNA: isoforms & splicing**                      | Junction-aware short-read RNA-seq | Long-read RNA/cDNA sequencing                               | Unambiguous isoforms, fusion/splice variant resolution                | Study alternative splicing, fusions, and isoform diversity    |
| **Nascent transcription / kinetics**              | PRO-seq / GRO-seq                 | TT-seq; SLAM-seq / TimeLapse-seq                            | Time-resolved labeling; synthesis/decay rates                         | Measure transcriptional dynamics, initiation, and elongation  |
| **RNA–protein binding**                           | eCLIP / iCLIP                     | iCLIP2 / irCLIP / RNP-MaP                                   | Higher positional accuracy, captures weak interactions                | Identify RNA-binding protein targets and motifs               |
| **RNA modifications (post-RNA)**                  | MeRIP-seq (m6A-IP)                | miCLIP2; direct RNA nanopore sequencing                     | Base-level m⁶A/ψ/m⁵C detection; antibody-free                         | Map chemical RNA modifications (m⁶A, m⁵C, ψ)                  |
| **Translation**                                   | Ribo-seq                          | QTI/GTI-seq; disome-seq                                     | Detects initiation, ribosome collisions                               | Measure translation efficiency, start-site mapping            |
| **Proteome quantification**                       | DDA LC-MS/MS                      | DIA/SWATH; PASEF-DIA; single-cell proteomics                | Fewer missing values, reproducible quantification                     | Identify and quantify proteins in bulk or single cells        |
| **Protein post-translational modification (PTM)** | Phospho-enrichment + DDA          | DIA phospho-proteomics; FAIMS/tims ion-mobility             | Higher PTM coverage, multiplexing, improved quant                     | Identify and quantify phospho/acetyl/ubiquitin sites          |
| **Protein interactions / proximity**              | AP-MS / Co-IP-MS                  | BioID / TurboID / APEX                                      | Captures transient and weak interactors; spatial context              | Detect protein–protein interactions and local neighborhoods   |
| **Spatial multi-omics**                           | Visium (10x)                      | Slide-seqV2; MERFISH / CosMx / Xenium                       | Higher plex & subcellular resolution; multi-modal                     | Map RNA/protein distribution within tissue context            |
| **Single-cell multi-omics**                       | Separate scRNA/scATAC             | Same-cell multiome (ATAC+RNA), SHARE-seq, Paired-Tag        | Links regulatory chromatin to RNA output directly                     | Integrate regulatory and expression layers per cell           |


           ┌────────────────────────────────────────────────────────┐
           │                    GENOME / DNA                        │
           └────────────────────────────────────────────────────────┘
                │
                │   ┌──────────────────────────────────────────────────┐
                ▼   │                                                  │
        ┌───────────────┐     ┌─────────────────────┐     ┌────────────┐
        │  WGS (Illumina│     │ Methylation assays  │     │ Chromatin  │
        │  Long-read HiFi│     │  (WGBS, EM-seq,    │     │ accessibility│
        │  /ONT)        │     │  ONT 5mC)          │     │  (ATAC-seq) │
        └───────────────┘     └─────────────────────┘     └────────────┘
                │                          │                   │
                ├──────────────┬────────────┴──────────┬────────┤
                │              │                       │
        Protein–DNA binding   3D chromatin           Multiome link
     (ChIP-seq / CUT&Tag)     (Hi-C / Micro-C)      (ATAC + RNA)
                │
                ▼
        ┌────────────────────────────────────────────┐
        │                 TRANSCRIPTOME               │
        └────────────────────────────────────────────┘
                │
       ┌────────────────────┬────────────────────────────┬───────────────────┐
       │                    │                            │                   │
 RNA expression & isoforms  Nascent transcription      RNA–protein binding  RNA modifications
 (RNA-seq / Iso-Seq)        (PRO-seq / TT-seq)        (eCLIP / iCLIP2)     (MeRIP / miCLIP / 
                                                                              nanopore direct)
       │                    │                            │                   │
       └────────────────────┴─────────────┬──────────────┴───────────────────┘
                                          │
                                          ▼
                                 ┌────────────────┐
                                 │ TRANSLATION    │
                                 │ (Ribo-seq,     │
                                 │  disome-seq)   │
                                 └────────────────┘
                                          │
                                          ▼
                                ┌──────────────────────────┐
                                │       PROTEOME           │
                                │ (DIA / SWATH, PTMs,      │
                                │  single-cell MS)         │
                                └──────────────────────────┘
                                          │
                        ┌─────────────────┴──────────────────┐
                        │ Protein interactions / proximity   │
                        │ (AP-MS, BioID, APEX)              │
                        └────────────────────────────────────┘
                                          │
                                          ▼
                              ┌───────────────────────────┐
                              │   Spatial multi-omics     │
                              │ (Visium, MERFISH, CosMx) │
                              └───────────────────────────┘
