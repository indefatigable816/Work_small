---
title: Based on Cheng's benchmarking of four protein embe...
updated: 2026-02-08T15:45:05
created: 2026-01-20T23:50:59
---

PM

![image1](../../../../resources/470e2ff33d6f4f6ba557ccc8a37aec5f.png)

![image2](../../../../resources/ee44f6c0a2c94c0b99e03486ee5a50bb.png)

<span style='background:white'>Based on Cheng's benchmarking of four protein embeddings for enzymatic kinetic parameter prediction:</span>
<span style='font-weight:bold;background:white'>For Mutant Enzymes:</span>
- <span style='font-weight:bold;background:white'>MuteRPM</span><span style='background: white'>emerged as the winner, showing generally more accurate and stable performance across multiple datasets and evaluation metrics (Pearson correlation and RMSE)</span>
- <span style='background:white'>This held true across different data split modes (random split, cold protein, and cold metabolite)</span>
<span style='font-weight:bold;background:white'>For Wild-Type Enzymes:</span>
- <span style='font-weight:bold;background:white'>ESM2</span><span style='background: white'>and</span><span style='font-weight:bold;background:white'>ESM1B</span><span style='background:white'>performed best, with very close performance to each other</span>
- <span style='background:white'>They consistently outperformed other embeddings in wild-type enzymatic kinetic parameter predictions</span>
<span style='font-weight:bold;background:white'>Evaluation Approach:</span>
<span style='background:white'>The benchmarking used:</span>
- <span style='background:white'>Multiple machine learning models (random forest, support vector machine, XGBoost, and 2D graph neural networks)</span>
- <span style='background:white'>Multiple datasets (LTLEM, MPEK, CatBread, and in-house datasets)</span>
- <span style='background:white'>Different split strategies (random, cold protein, cold metabolite) to test generalization</span>
- <span style='background:white'>Two metrics: Pearson correlation and Root Mean Square Error (RMSE)</span>
<span style='font-weight:bold;background:white'>Key Insight:</span><span style='background:white'>The results suggest that</span><span style='font-weight:bold;background:white'>mutation-specific embeddings (MuteRPM) are superior for mutant enzyme predictions</span><span style='background:white'>, while</span><span style='font-weight:bold; background:white'>comprehensive general protein models (ESM2/ESM1B) are better for wild-type enzymes</span><span style='background:white'>. This indicates that specialized embeddings aligned with the prediction task (mutation-aware vs. general) provide better performance.</span>

*From \< <https://zoom.localhost/index-5.1.10652.html#/aic>\>*

![image3](../../../../resources/af8057fa11df4a8fa455afe5d2c450c6.png)

![image4](../../../../resources/f4bb203700224816aaa62d9fc98bafb1.png)

![image5](../../../../resources/0740fb2e93124e5d8baeabf7f45d658c.png)

![image6](../../../../resources/135a790609634740806325c6378e8811.png)

<span style='background:white'>Based on the conversation, the specific token accuracy numbers weren't shared, but Cheng mentioned the validity rate was around 20% (improved from \<10%), which suggests the token accuracy may also be relatively low.</span>
<span style='background:white'>Possible reasons for low token accuracy in SMILES generation include:</span>
- <span style='color:#323539'>**Complex chemical syntax**- SMILES strings require precise character sequences; a single wrong token makes the entire molecule invalid</span>
- <span style='color:#323539'>**Long sequence dependencies**- The model needs to track parentheses, branches, and ring closures across long sequences</span>
- <span style='color:#323539'>**Limited training data**- Enzyme-catalyzed reactions may have fewer examples compared to general chemical reactions</span>
- <span style='color:#323539'>**Challenging task**- Predicting product molecules from mutant enzyme sequences is inherently difficult, requiring the model to learn complex structure-function relationships</span>
<span style='background:white'>Cheng mentioned this is ongoing optimization work, so improvements in model architecture, training strategies, or data augmentation could help increase token accuracy over time.</span>

*From \< <https://zoom.localhost/index-5.1.10652.html#/aic>\>*

