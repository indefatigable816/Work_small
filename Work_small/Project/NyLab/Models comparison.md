---
title: Models comparison
updated: 2026-03-12T21:35:38
created: 2026-03-12T21:14:52
---

Models comparison
Thursday, March 12, 2026
9:14 PM

I'll search the Boltz GitHub repository to get accurate information about Boltz2's capabilities.Based on my examination of the Boltz2 GitHub repository, here's the refilled table with accurate information about Boltz2:

\| Category \| Item \| AlphaFold3 \| Boltz2 \| MutaDB \|
\|----------\|------\|-----------\|--------\|---------\|
\| \*\*Input\*\* \| Input \| Protein sequence \| Protein sequence \| Protein sequence \|
\| \| Multiple chains \| TRUE \| TRUE \| \|
\| \| Small molecules \| TRUE (via CCD codes or SMILES) \| TRUE (via SMILES, ligand support) \| \|
\| \| DNA/RNA input \| TRUE (DNA and RNA chains supported) \| TRUE (DNA and RNA chains supported) \| \|
\| \| MSA requirement \| Optional (auto-generated if not provided) \| Required \| \|
\| \| Template usage \| Optional (customizable) \| Customizable (use_templates parameter) \| FALSE \|
\| \*\*Output\*\* \| Structure (mmCIF) \| TRUE \| TRUE \| FALSE \|
\| \| Confidence metrics \| pLDDT, PAE, pTM, ipTM \| pLDDT, PAE, iPTM \| Binding score \|
\| \| Interface confidence \| ipTM, chain pair metrics \| iPTM \| \|
\| \| Per-residue confidence \| pLDDT (per-atom) \| pLDDT \| \|
\| \| Error estimate \| PAE, contact_probs \| PAE, contact probabilities \| \|
\| \*\*Model architecture\*\* \| Model type \| Diffusion-based + Transformer \| Diffusion-based + Pairformer (64 blocks) \| \|
\| \| Diffusion model \| TRUE \| TRUE \| \|
\| \| Structure representation \| Atom-level \| Atom-level \| \|
\| \| End-to-end prediction \| TRUE \| TRUE \| \|
\| \*\*Prediction scope\*\* \| Monomer prediction \| TRUE \| TRUE \| \|
\| \| Protein–protein complex \| TRUE \| TRUE \| \|
\| \| Protein–ligand complex \| TRUE (ligands as CCD or SMILES) \| TRUE (ligands via SMILES/CCD molecules) \| \|
\| \| Protein–nucleic acid \| TRUE (DNA/RNA chains) \| TRUE (DNA/RNA chains) \| \|
\| \*\*Training / Data\*\* \| Training dataset \| PDB + proprietary datasets \| PDB-derived datasets \| \|
\| \| Training objective \| Structure generation \| Structure generation + Affinity prediction \| \|
\| \*\*Performance\*\* \| Typical GPU requirement \| High (A100/H100 recommended, Compute Capability ≥8.0) \| Moderate–High \| \|
\| \| Runtime per complex \| minutes–hours \| minutes–hours \| \|
\| \| Use case \| General biomolecular structure prediction \| Fast structure & affinity prediction \| \|

\*\*Key Boltz2 Updates from the Repository:\*\*
\- \*\*Ligand Support\*\*: Boltz2 supports small molecule ligands through SMILES and CCD codes
\- \*\*Nucleic Acids\*\*: Explicitly supports DNA and RNA chains
\- \*\*Affinity Prediction\*\*: Boltz2 has a dedicated affinity model (boltz2_aff.ckpt) for binding affinity prediction
\- \*\*Architecture\*\*: Uses a Pairformer with 64 blocks (vs 48 in other configurations) with diffusion-based structure generation
\- \*\*Template Support\*\*: Customizable template usage via use_templates parameters
\- \*\*Output Confidence\*\*: Provides pLDDT, PAE, and iPTM metrics for confidence assessment
\- \*\*Constraints\*\*: Supports pocket constraints and contact constraints for guided prediction
