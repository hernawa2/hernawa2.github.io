---
layout: page
permalink: /research/
title: Research
description: 
nav: true
---

## Interests

- **Causal Network:** Bayesian Network for regression and classification problem.
- **Parallelized Bayesian Inference:** Parallel Markov Chain Monte Carlo, Langenvin/Hamiltonian Monte Carlo.
- **Statistical machine learning and pattern recognition:** classification, regression, clustering.
- **Applications to Risk & Supply Chain Modeling:** Probabilistic modeling, Gaussian Process Regression.


<details markdown="1">
<summary> <b>Overview</b> (<i>click to expand</i>) </summary><p>

I am interested in the statistical, mathematical and computational aspects
of methodologies for problems that arise in data science, especially for *large and complex data*. My research combines the following themes.

- Developing statistical methodologies for complex and high-dimensional data to make
*interpretable and efficient inferences* by exploiting low-dimensional structures in the data.

- Constructing *computationally efficient and robust algorithms* for large-scale data analysis, in particular through spectral methods and convex optimization.

- Studying the theoretical aspects of the above problems within a formal statistical framework to *quantify uncertainty* and to better *understand their non-asymptotic performance
and limitations*.

- Applying these methodologies to relevant scientific problems,  with a special focus on neuroscience applications to understand the connectivity of the brain.

Broadly speaking, my work can be classified into three areas: statistical modeling,
estimation and inference for *network analysis*, supervised and unsupervised *machine learning* methods for
complex data types, and methodology and theory for *pattern recognition* in graphs.

</p></details>

<details>
<summary> <b>Network analysis</b> (<i>click to expand</i>) </summary><p>

The analysis of network data has received increasing attention motivated by the study of complex systems with interactive units. Examples of these systems appear
in social, biological and technological networks, among others fields. My work in this area focuses in addressing estimation and inference problems by exploiting low-dimensional representations using a combination of latent space models and spectral graph inference. I have worked in developing new methodologies with provable theoretical guarantees for performing network inferences tasks including community detection, dimensionality reduction, or graph hypothesis testing, particularly for problems involving multiple networks.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/FB-SPCA.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/FB-latentpositions-laplacian.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>


**References**

* **Overlapping community detection in networks via sparse spectral decomposition**<br>
*Jesús Arroyo*, Elizaveta Levina<br>
*Sankhya A (Special Issue on Network Analysis)* (2020), accepted pending minor revisions.<br>
[[preprint]](https://arxiv.org/abs/2009.10641)[[code]](https://github.com/jesusdaniel/spcaCD)
* **Inference for multiple heterogeneous networks with a common invariant subspace**<br>
*Jesús Arroyo*, Avanti Athreya, Joshua Cape, Guodong Chen, Carey E. Priebe, Joshua T. Vogelstein<br>
*Journal of Machine Learning Research* (2020), to appear.<br>
[[preprint]](https://arxiv.org/pdf/1906.10026.pdf)[[R code]](https://github.com/jesusdaniel/mase)[[Python code]](https://graspy.neurodata.io/reference/embed.html#graspologic.embed.MultipleASE)
* **Joint embedding of graphs**<br>
Shangsi Wang, *Jesús Arroyo*, Joshua T. Vogelstein, Carey E. Priebe<br>
*IEEE Transactions on Pattern Analysis and Machine Intelligence* (2019), in press.<br>
[[journal]](https://ieeexplore.ieee.org/abstract/document/8889404/) 
* **Multiple Network Embedding for Anomaly Detection in Time Series of Graphs**<br>
Guodong Chen, *Jesús Arroyo*, Avanti Athreya, Joshua Cape, Joshua T Vogelstein, Youngser Park, Chris White, Jonathan Larson, Weiwei Yang, Carey E Priebe<br>
[[preprint]](https://arxiv.org/abs/2008.10055)

</p></details>




<details>
<summary>  <b>Statistical Learning</b> (<i>click to expand</i>)</summary> 

Modern high-dimensional settings in statistics and machine learning are often concerned with
variable selection or regularization approaches to reduce the dimension of the problem and
to discover meaningful associations between variables. These tasks become more challenging
in complex datasets with additional multi-scale structure in the variables, such as networks,
tensors or multimodal data, which often show strong dependence associations between variables. I have worked in developing
new techniques to study these problems by introducing novel regularizations and methodologies that deal with the
complexity of the data effectively in supervised learning with network-valued covariates, dimensionality reduction, graphical model learning, and applications to brain network classification.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid mx-auto d-block" src="{{ '/assets/img/fMRI-classification.png' | relative_url }}" alt="Graph classification" title="Graph classification"/>
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/fMRI1.png' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        <img class="img-fluid" src="{{ '/assets/img/Brain_network_steve_ind27_s.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>

**References**

* **Network classification with applications to brain connectomics**<br>
*Jesús D. Arroyo Relión*, Daniel Kessler, Elizaveta Levina, Stephan F. Taylor<br>
*The Annals of Applied Statistics* (2019), 13(3), 1648-1677.<br>
[[journal]](https://projecteuclid.org/euclid.aoas/1571277767) 
* **Efficient distributed estimation of inverse covariance matrices**<br>
*Jesús Arroyo*, Elizabeth Hou<br>
*IEEE Statistical Signal Processing Workshop (SSP)* (2016), pages 1-5.<br>
[[conference proceedings]](https://ieeexplore.ieee.org/abstract/document/7551705)
* **Simultaneous prediction and community detection for networks with application to neuroimaging**<br>
*Jesús Arroyo*, Elizaveta Levina<br>
[[preprint]](https://arxiv.org/pdf/2002.01645.pdf)[[code]](https://github.com/jesusdaniel/glmblock)


</details>

<details>
<summary> <b>Pattern Recognition</b> (<i>click to expand</i>)</summary><p> 

Identifying patterns or similarities between nodes is an important task in the study of network data. *Graph matching* is the problem of finding a meaningful correspondence between the nodes of two or more networks, and has applications in fields such as neuroscience, image processing or data security. Part of my work has focused in studying this problem from a statistical framework, by developing flexible and tractable statistical models and efficient computational tools, and analyzing the theoretical performance and limitations of these methodologies.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid w-50 mx-auto d-block" src="{{ '/assets/img/GM-problem.png' | relative_url }}" alt="Graph matching problem" title="Graph matching problem"/>
    </div>
</div>

**References**

* **Maximum Likelihood Estimation and Graph Matching in Errorfully Observed Networks**<br>
*Jesús Arroyo*, Daniel L. Sussman, Carey E. Priebe, Vince Lyzinski<br>
*Journal of Computational and Graphical Statistics* (2021)<br>
[[journal]](https://www.tandfonline.com/doi/full/10.1080/10618600.2021.1872582)[[preprint]](https://arxiv.org/pdf/1812.10519.pdf) [[code]](https://github.com/dpmcsuss/gmmle)
* **Graph matching between bipartite and unipartite networks: to collapse, or not to collapse, that is the question**<br>
*Jesús Arroyo*, Carey E. Priebe, Vince Lyzinski<br>
[[preprint]](https://arxiv.org/abs/2002.01648)


</p></details>
