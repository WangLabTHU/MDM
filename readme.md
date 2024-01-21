# Synthetic promoter design in Escherichia coli based on multinomial diffusion model

## Model Architectures

The models discussed in this paper are all detailed in the wiki documentation of our [GPro](https://github.com/WangLabTHU/GPro/tree/main/gpro) package, which is publicly available. We would be delighted if you also wished to try out our toolkit!

|Models|Wiki|Description|
|----|----|----|
| CNN_K15|https://github.com/WangLabTHU/GPro/wiki/4.2.1-CNN-K15| Our Predictive Model|
| WGAN| https://github.com/WangLabTHU/GPro/wiki/4.1.1-WGAN| Generator|
| MDM| https://github.com/WangLabTHU/GPro/wiki/4.1.2-Diffusion| Generator|

A simple diagram of our MDM model can be described as follows:

<div align=center>
<img src="https://github.com/qxdu/MDM/assets/59758004/f8ed6eba-8456-4472-a89b-648d13ab78f5" width="700px">
</div>

In this paper, we also provided related models in https://github.com/qxdu/MDM/tree/master/models . 
ddsm-main is available at https://github.com/jzhoulab/ddsm/tree/main/promoter_design , while promodiff is available at checkpoint is available at https://github.com/wangxinglong1990/Promoter_design/ .

## Motif Features Enrichment

To adapt to the cellular environment, we should ensure the generated promoters follow the key feature distributions of the natural promoter sequences.  Here we perform multiple comparisons of our MDM with DDSM, WGAN, PromoDiff and PPSM. 

|Comparisons|Codes|Description|
|----|----|----|
|

## Mode collapse Analysis

Mode collapse occurs when the generator and discriminator of a GAN converge to a local minimum (Caccia et.al., 2018), with the generation of datas only follow one or a few specific patterns. This phenomenon is particularly severe in discrete data spaces, such as DNA. Previous promoter generation approach with WGAN employed Wasserstein distance, gradient penalty (Gulrajani et.al., 2017) and resblock to address this issue, but we still encountered mode collapse during the training process, where every sequence resembled a same pattern like "AAA...AAA". Here, MDM has converted the estimation process into a transformation from  $x_t$ to $x ̂_0$, which eliminates the risk of being trapped in local minima. We conducted experiments on multiple datasets and various sampling scales, and the MDM did not experience mode collapse even once. This demonstrates the robustness of our model.

Inner Levenshtein Distances can be shown as follows. 

<div align=center>
<img src="https://github.com/qxdu/MDM/assets/59758004/de3cb25a-ed2a-4eb5-b441-bc46465d408e" width="700px">
</div>

Our evaluation codes are under https://github.com/qxdu/MDM/tree/master/collapse , and results of multiple criterias have also been provided.

