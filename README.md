# AI-Engineered-Proteins-A-De-Novo-Approach-to-Rapidly-Suppress-Human-To-Human-Hantavirus-Transmission

This project was aimed to engineer and optimize de novo miniprotein binders targeting the highly conserved fusion loop ANDV glycoprotein c (Gc).

## Overview
Andes virus (ANDV) is a highly pathogenic hantavirus capable of causing Hantavirus Cardiopulmonary Syndrome (HCPS). Although monoclonal antibodies represent a potential therapeutic strategy, their development and production can be time-consuming and costly. This project therefore explores the computational design of de novo nanoprotein binders targeting the Gc glycoprotein of ANDV.

The target protein structure (PDB ID: 6Y5W) was analyzed to identify binding hotspot residues within the target region. RFdiffusion was used to generate binder backbones around selected hotspots (B739, B766, and B900), producing five candidate backbone designs with lengths of 50–70 amino acids. ProteinMPNN was subsequently used to design amino acid sequences conditioned on each generated backbone.

The resulting candidates were evaluated using AlphaFold2 and Rosetta through multiple structural and interface metrics, including binder pLDDT, ipTM, interface PAE, RF-to-AF2 RMSD, Rosetta ΔG, Packstat, and unsatisfied hydrogen bonds. Although individual designs showed favorable performance in specific metrics, no candidate performed consistently well across all validation criteria. In particular, the low AlphaFold2 interface confidence observed across the designs indicates that further optimization is required before experimental validation.

## Workflow
<p align="center">
  <img src="figures/workflow.png" width="850">
</p>
The computational pipeline consists of three major stages:
1. **Backbone generation — RFdiffusion**
2. **Sequence design — ProteinMPNN**
3. **Structural and interface validation — AlphaFold2 & Rosetta**


## Methodology

### 1. Target Preparation
- Target structure: ANDV Gc glycoprotein (PDB: 6Y5W)
- Selected hotspot residues: B739, B766, B900

### 2. Backbone Generation — RFdiffusion
**Input**
- Target protein structure
- Hotspots: B739, B766, B900
- Binder length: 50–70 aa

**Process**
RFdiffusion was used to generate binder backbones around the
selected binding hotspots.

**Output**
- 5 candidate binder backbones (.pdb)

### 3. Sequence Design — ProteinMPNN
RFdiffusion-generated backbones were provided to ProteinMPNN
for sequence design.

Parameters:
- 8 sequences per backbone
- Sampling temperature: 0.1

**Output**
- Candidate binder sequences (.fasta)

### 4. Structural Validation — AlphaFold2
Candidate sequences were evaluated using:
- Binder pLDDT
- ipTM
- Interface PAE
- RF → AF2 RMSD

### 5. Interface Evaluation — Rosetta
Protein–protein interfaces were further assessed using:
- Interface ΔG
- Packstat
- Unsatisfied hydrogen bonds

## Results

### Structural Validation
<p align="center">
  <img src="figures/binder_structures.png" width="800">
</p>

| Design | Binder pLDDT ↑ | ipTM ↑ | Interface PAE ↓ (Å) | RF→AF2 RMSD ↓ (Å) | Rosetta ΔG ↓ (REU) | Packstat ↑ | Unsat H-bonds ↓ |
|---|---:|---:|---:|---:|---:|---:|---:|
| Design 0 | 40.62 | **0.12** | 26.28 | **4.13** | **-55.71** | 0.565 | 15 |
| Design 2 | 46.06 | **0.12** | **26.25** | 6.32 | -10.66 | **0.703** | **1** |
| Design 3 | 36.04 | **0.12** | 26.64 | 18.36 | -49.55 | 0.613 | 11 |
| Design 1 | 43.29 | 0.11 | 26.74 | 7.36 | -32.05 | 0.668 | 8 |
| Design 4 | **46.09** | 0.10 | 26.96 | 5.52 | -19.01 | 0.657 | 4 |

### Key Findings

- **Design 0** showed the lowest RF→AF2 RMSD (4.13 Å) and the
  most favorable Rosetta ΔG (-55.71 REU).
- **Design 2** achieved the highest Packstat (0.703) and only
  one unsatisfied hydrogen bond.
- Binder pLDDT and ipTM remained low across all candidates.
- Interface PAE remained high across all candidates.
- No design performed consistently well across all evaluation metrics.

## Limitations

Although several candidates showed favorable performance in individual
metrics, none performed consistently well across all validation criteria.

In particular, the relatively low binder pLDDT and ipTM values and high
interface PAE indicate limited confidence in the predicted binder–target
interfaces. Further rounds of backbone generation, sequence optimization,
and computational validation are therefore required before experimental
testing.

These results suggest that additional optimization and redesign are
required before proceeding to experimental validation.
