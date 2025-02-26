# PII Splicing Documentation

We are seeking to collate research and documentation of existing text de-identification tools to understand the the current landscape. We are also collecting information about de-identification in the context of other data modalities, in the hopes of applying similar principles to text de-identification.

## Definitions
P: number of PII elements in a given text

N: number of non-PII elements in a given text

TP: PII elements correctly identified as PII

FP: non-PII elements incorrectly identifies as PII

TN: non-PII elements correctly identified as non-PII

FN: PII elements incorrectly identified as non-PII

We should calculate across multiple benchmarking texts

**Sensitivity = TP/P which should be as close as possible to 1 (FNR close to 0)**

**Specificity = TN/N should be as high as possible but can be sacrificed for higher Sensitivity**

Note: Due to the high imbalance, TP/P is going to be a number very close to 1 anyways so we may want to use log(1-TP/P) = log(FNR) instead.

Due to the nature of the PII splicing program, we prioritize sensitivity, not specificity

## Research Questions
- Which metrics are most critical for de-identification?
    - False Negative Rate (FNR): PII incorrectly identified as non-PII ("PII Miss Rate")
    - False Positive Rate (FPR): Non-PII incorrectly identified as PII ("Overshoot Rate")
    - Some may have differing thresholds for both FNR and FPR. For example, one may prefer a model with a low FNR and they may be okay with a higher FPR.
- Which performance thresholds should we be aiming for?
    - This [paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC4989908/#S10) in the Discussion section suggests 95% as a threshold. Their [Table 6](https://pmc.ncbi.nlm.nih.gov/articles/PMC4989908/#T6) shows that several teams reach that threshold when considering HIPAA-PHI categories with token-based evaluation.
    - The paper makes a distinction between entity-based and token-based evaluation in the [Evaluation](https://pmc.ncbi.nlm.nih.gov/articles/PMC4989908/#S6) section.
        - Entity-based requires that the PHI is exactly matched, as well as its tag name and type.
        - Token-based is more liberal and only requires that all the parts that are PHI are identified in some fashion.
        - Token-based could be more appropriate, since the removal of the PHI and not the categorization is a higher priority.
- Can we define and/or quantify how identifying a piece of information is?
    - [Direct and quasi-identifiers.](https://www.sciencedirect.com/science/article/pii/S1532046416300697)
- How can we simulate a real-world attack / attempt of re-identification?
- Should we distinguish open-set vs. closed-set identification?
    - [Dementia Bank's IRB section (subsection: Voiceprints)](https://talkbank.org/share/irb/) has thoughts on this.
- What requirements will real-world data stewards need to fulfill for de-id before data sharing?
    - Perhaps their IRB/consent process defines that a "reasonable" effort has been made. How does that translate to our metrics (FNR, FPR, etc.) here?
- What can we learn from successful de-identification and data sharing from other data modalities?
    - [ADRCs share SCAN-compliant brain MRIs to LONI](https://scan.naccdata.org/), which are then de-identified and defaced.

## Existing Text De-identification Tools

| Name | Type | PDF |  Year |
| - | - | - | - |
| [A unified framework for evaluating the risk of re-identification of text de-identification tools](https://www.sciencedirect.com/science/article/pii/S1532046416300697) | Existing Tools | [PDF](existing_tools/1-s2.0-S0885230824001293-main.pdf) | 2016 |
| [An Extensible Evaluation Framework Applied to Clinical Text Deidentification Natural Language Processing Tools: Multisystem and Multicorpus Study](https://pubmed.ncbi.nlm.nih.gov/38805692/) ([GitHub](https://codeberg.org/HeiderLab/ots-deidentification))| Existing Tools | [PDF](existing_tools/jmir-2024-1-e55676.pdf) | 2024 |
[You Are What You Write: Author re-identification privacy attacks in the era of pre-trained language models](https://www.sciencedirect.com/science/article/pii/S0885230824001293) | Existing Tools | [PDF](existing_tools/re-id-privacy-attacks.pdf) | 2025 |
[DeIDClinic: A Multi-Layered Framework for De-identification of Clinical Free-text Data](https://arxiv.org/abs/2410.01648) | Existing Tools | [PDF](existing_tools/2410.01648v1.pdf) | 2024 |
| [Enhancing the De-identification of Personally Identifiable Information in Educational Data](https://arxiv.org/html/2501.09765v1) | Existing tools | [PDF](existing_tools/2501.09765v1.pdf) | 2025 |

## Metrics
| Name | Type | PDF | Year | 
| - | - | - | - |
| [Analyzing Leakage of Personally Identifiable Information in Language Models](https://arxiv.org/pdf/2302.00539), especially PII reconstruction/inference | Metric | [PDF] (existing_tools/2302.00539v4.pdf) | 2023 |

## MRI De-identification

| Name |  Type | PDF |
| - | - | - |
[Changing the face of neuroimaging research: Comparing a new MRI de-facing technique with popular alternatives](https://www.sciencedirect.com/science/article/pii/S1053811921001221) | MRI De-id | mri_deid/1-s2.0-S1053811921001221-main.pdf |
[Identification of Anonymous MRI Research Participants with Face-Recognition Software](https://pmc.ncbi.nlm.nih.gov/articles/PMC7091256/) | MRI De-id | mri_deid/nihms-1563447.pdf |
[Reconstructing faces from fMRI patterns using deep generative neural networks](https://www.nature.com/articles/s42003-019-0438-y) | MRI De-id | mri_deid/s42003-019-0438-y.pdf | 
