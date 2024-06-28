# Synthetic promoter design in Escherichia coli based on multinomial diffusion model

## Model Architectures

The models discussed in this paper are all detailed in the wiki documentation of our [GPro](https://github.com/WangLabTHU/GPro/tree/main/gpro) package, which is publicly available. We would be delighted if you also wished to try out our toolkit!

|Models|Wiki|Description|
|----|----|----|
| CNN|https://github.com/HaochenW/Deep_promoter| Our Predictive Model|
| WGAN| https://github.com/WangLabTHU/GPro/wiki/4.1.1-WGAN| Generator|
| MDM| https://github.com/WangLabTHU/GPro/wiki/4.1.2-Diffusion| Generator|

A simple diagram of our MDM model can be described as follows:

<div align=center>
<img src="https://github.com/qxdu/MDM/assets/59758004/a3e0a537-0d3a-4774-a9f9-d9305e5b0634" width="700px">
</div>

In this paper, we also provided related models in https://github.com/qxdu/MDM/tree/master/models . 
ddsm-main is available at https://github.com/jzhoulab/ddsm/tree/main/promoter_design , while promodiff is available at checkpoint is available at https://github.com/wangxinglong1990/Promoter_design/ .

## Motif Features Enrichment

To adapt to the cellular environment, we should ensure the generated promoters follow the key feature distributions of the natural promoter sequences.  Here we perform multiple comparisons of our MDM with DDSM, WGAN, PromoDiff and PPSM. 
  
Our datasets for similarity analysis contain 4 benchmarks (ecoli_50, ecoli_165, yeast_80, yeast_1000) from GPro: https://github.com/WangLabTHU/GPro/wiki/7.-Datasets . Refer to our provided wiki for more detailed information about these benchmarks.


|Metrics|Codes|Description|
|----|----|----|
| weblogos | https://github.com/WangLabTHU/GPro/wiki/4.4.5-WebLogo | The weblogo of MDM-generated sequences should have highly conserve motif features | 
| spacer region| https://github.com/qxdu/MDM/blob/master/evaluation/gap_simulation.py | The inter motif distance is typically around 17 bp|
| 6-mer frequency | https://github.com/qxdu/MDM/blob/master/evaluation/kmer_frequency.py | 6-mer frequency of samples generated by models |
| sample diversity | https://github.com/qxdu/MDM/blob/master/collapse/evaluate.py | sample diversity of generated sequences | 
| blast-n analysis | https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&BLAST_SPEC=GeoBlast&PAGE_TYPE=BlastSearch | Avoid homologous recombination |
  

All avaiable results have been provided in https://github.com/qxdu/MDM/tree/master/evaluation/results , while samples generated by models are provided in https://github.com/qxdu/MDM/tree/master/evaluation/comparison . A simple diagram of k-mer frequency of our MDM is as follows:


<div align=center>
<img src="https://github.com/qxdu/MDM/blob/master/evaluation/results/kmer_mdm.png" width="700px">
</div>

A comparison of kmer similarity on 4 benchmarks is as follows:

![Fig2_kmer](https://github.com/qxdu/MDM/assets/59758004/dc3bd3cb-fa38-4e6d-b74d-624b6211b884)


## Mode Collapse Analysis

Mode collapse occurs when the generator and discriminator of a GAN converge to a local minimum (Caccia et.al., 2018), with the generation of datas only follow one or a few specific patterns. This phenomenon is particularly severe in discrete data spaces, such as DNA. Previous promoter generation approach with WGAN employed Wasserstein distance, gradient penalty (Gulrajani et.al., 2017) and resblock to address this issue, but we still encountered mode collapse during the training process, where every sequence resembled a same pattern like "AAA...AAA". Here, MDM has converted the estimation process into a transformation from  $x_t$ to $x ̂_0$, which eliminates the risk of being trapped in local minima. We conducted experiments on multiple datasets and various sampling scales, and the MDM did not experience mode collapse even once. This demonstrates the robustness of our model.

Inner Levenshtein Distances can be shown as follows. 

<div align=center>
<img src="https://github.com/qxdu/MDM/assets/59758004/de3cb25a-ed2a-4eb5-b441-bc46465d408e" width="700px">
</div>

Our evaluation codes are under https://github.com/qxdu/MDM/tree/master/collapse , and results of multiple criterias have also been provided.

## Weak Signal Decoupling
The abilities of model to decouple complex signals and preserve natural weak signals are particularly important. We conducted an in silico experiment to evaluate these capacities of our model. Relevant codes are provided in https://github.com/qxdu/MDM/tree/master/heatmap . Samples generated by our models and results are provided in https://github.com/qxdu/MDM/tree/master/heatmap/result . All available motifs are downloaded from [JASPAR](https://jaspar.elixir.no/) .

A simple results of our MDM is shown as follows:

<div align=center>
<img src="https://github.com/qxdu/MDM/blob/master/heatmap/result/gap_mdm.png" width="700px">
</div>

## Bioloigical Validation

Results are provided in paper and supplementary materials. We performed [DDM-MDS algorithms](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2007-8-5-r83) on our dataset, demonstrating a higher likelihood of rpoD17 motif occurence. This might account for the better performance of our MDM.

<div align=center>
<img src="https://github.com/qxdu/MDM/assets/59758004/877a0733-c66e-4c0e-89f7-5304bbca478a" width="700px">
</div>

## Citations
[1] Wang Y, Wang H, Wei L, et al. Synthetic promoter design in Escherichia coli based on a deep generative network[J]. Nucleic Acids Research, 2020, 48(12): 6403-6412.

[2] Hoogeboom E, Nielsen D, Jaini P, et al. Argmax flows and multinomial diffusion: Learning categorical distributions[J]. Advances in Neural Information Processing Systems, 2021, 34: 12454-12465.

[3] Avdeyev P, Shi C, Tan Y, et al. Dirichlet Diffusion Score Model for Biological Sequence Generation[J]. arXiv preprint arXiv:2305.10699, 2023.

[4] Guo Z, Liu J, Wang Y, et al. Diffusion models in bioinformatics and computational biology[J]. Nature Reviews Bioengineering, 2023: 1-19.

[5] Wang H, Du Q, Wang Y, et al. GPro: generative AI-empowered toolkit for promoter design[J]. Bioinformatics, 2024, 40(3): btae123.


