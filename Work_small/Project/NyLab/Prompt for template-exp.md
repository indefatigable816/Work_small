---
title: Prompt for template-exp
updated: 2026-03-26T16:14:30
created: 2026-03-26T14:50:17
---

Prompt for template-exp
Thursday, March 26, 2026
2:50 PM

\# Change of project documentation

\## provided the original doc. now there are things to change:
- don't change section 1 to 4
- Don't consider boltzgen in this markdown so delete the part
- Frame next step using design --\> experiment --\> evaluation framework and refer to the image
- Work is done in model linkd, now we focus on af3 and boltz
- Focus next step on template-guided folding --\> evaluation of binding using ipsae and pyrosetta
  - For af3 you need to generate Alphafold3 input files: Af3_input\_\*.json (at most 30 predictions a file) send it to af3 server and download results with the aid of agentic skill /alphafold3-workflow
  - For boltz read
- Additional guidance for agent
  - In boltz prediction commands remember to add these for every prediction
    - -- diffusion_samples 5
    - -- recycling_steps 10
    - -- num_diffusion_samples 25
    - --max_parallel_samples 25
  - use a100: [guide on lsf file writing](https://labs.icahn.mssm.edu/minervalab/documentation/lsf-job-scheduler/)
  - Alphafold3 input examples: C:\Users\indef\Documents\NY\project\PLM_Claude\template_folding\code\AF3\prompts_json
  - Read Links to understand how to perform template guided folding: [alphafold3](https://github.com/google-deepmind/alphafold3.git), [boltz2](https://github.com/jwohlwend/boltz.git)
