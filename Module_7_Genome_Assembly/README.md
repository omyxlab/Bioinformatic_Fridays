# Module 7: Genome Assembly

This module is where you rebuild genomes from sequencing reads and identify what you have assembled. You will assemble long reads de novo, remove host contamination, annotate the contigs with BLAST, and then use a reference to guide assembly and generate a consensus sequence.

It builds on [Module 1](../Module_1_Bioinformatics_Foundations/README.md), which introduced alignment, reference-based and de novo assembly, contigs, and graphs, and on [Module 6](../Module_6_Omics_QC_Trimming/README.md), which covers quality control.

## Learning objectives

By the end of this module, you will be able to:

- Explain what genome assembly is, why it matters, and the difference between de novo and reference-based strategies
- Choose assembly software suited to short reads, long reads, or both
- Remove host reads, assemble long reads with Flye, and identify contigs with BLAST
- Map long reads to a reference and generate a consensus sequence

## Lessons

| Lesson | Title | Focus |
|--------|-------|-------|
| 1 | Genome assembly foundations | What assembly is, why it matters, de novo versus reference-based, software for short and long reads, and an end-to-end pipeline overview |
| 2 | De novo assembly (hands-on) | Long-read de novo assembly using `barcode57` and `barcode58`, including host-read filtering, Flye assembly, and a BLAST annotation workflow |
| 3 | Reference-based assembly | Long-read reference-guided assembly against combined ACMV DNA-A and DNA-B, with mapping QC and consensus sequence generation |

## Module toolbox

Lessons 2 and 3 use the dedicated `bioinfo` environment:

```bash
conda activate bioinfo
```
