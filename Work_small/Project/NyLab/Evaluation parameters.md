---
title: Evaluation parameters
updated: 2026-02-13T11:05:19
created: 2026-02-13T11:03:23
---

AM

- <span style='font-style:italic;background:white'>ranking_score</span><span style='background:white'>: A scalar ranging from -100 to 1.5 that can be used for ranking predictions. It combines</span><span style='font-style:italic;background:white'>ptm</span><span style='background: white'>,</span><span style='font-style:italic;background:white'>iptm</span><span style='background:white'>,</span><span style='font-style:italic; background:white'>fraction_disordered</span><span style='background:white'>and</span><span style='font-style:italic;background:white'>has_clash</span>into a single number with the following equation:  
  0.8 × ipTM + 0.2 × pTM + 0.5 × disorder − 100 × has_clash

*From \< <https://alphafoldserver.com/guides#section-3:-interpreting-results-from-alphafold-server>\>*
- <span style='background:white'>Meanwhile, ipTM measures the precision of predictions of each single entity in the context of the whole macromolecular complex. ipTM is also available for every pair of entities within the complex: this is called pairwise ipTM.</span>
- <span style='background:white'>The values of pTM and ipTM provided by AlphaFold 3 should be interpreted in the same way as those reported by AlphaFold 2. For instance, an ipTM score above 0.8 indicates a confidently predicted interaction. For more details, see "</span>[<span style='background:white'>Confidence scores in AlphaFold Multimer</span>](https://www.ebi.ac.uk/training/online/courses/alphafold/inputs-and-outputs/evaluating-alphafolds-predicted-structures-using-confidence-scores/confidence-scores-in-alphafold-multimer/)<span style='background:white'>".</span>

*From \< <https://alphafoldserver.com/guides#section-3:-interpreting-results-from-alphafold-server>\>*

