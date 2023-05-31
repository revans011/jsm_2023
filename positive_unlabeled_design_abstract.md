2023-05-25

Richard Evans \
Clinical and Translational Science Institute \
University of Minnesota \
evan0770@umn.edu

## Design Considerations for Positive-Unlabeled GWAS Studies

### Long Abstract

### Purpose

In genome-wide association studies (GWAS), negative control groups are sometimes unlabeled, which means they are a mixture of unaffected cases and undetected affected cases. The unlabeled aspect of the data is usually handled in the data analysis rather than the design phase of the study. We considered the design phase, and investigated the effect using unlabeled control groups on the power of the association tests in GWAS studies.

### Background

Genome wide association studies of cranial cruciate ligament disease (CCLD) in dogs use case-control designs. The case are truly positive CCLD cases because they are enrolled from the set of dogs who have undergone CCL surgery. The controls are typically five-years-old or older with no history of CCLD and pass an orthopedic veterinary exam by a board-certified surgeon. CCLD GWAS studies usually enroll as many dogs as they possibly can without regard to the balance between the numbers of cases and controls.

For example, Healy enrolled 161 affected dogs and 55 control dogs, giving about a 3:1 ratio of cases to controls for N=216 dogs, while 

It is the control group that is of interest to us because some of those dogs are not truly CCLD-negative dogs. Some will get CCLD in the future, and so genetically belong in the CCLD cases group. Other control dogs may have sub-diagnostic disease. For example, a dog might appear sound on physical exam and enrolled in the control group, but actually have force-platform-detectable hindlimb lameness. Such a dog should not be in the control group because the lameness might be subclinical CCLD.

Using data science terminology, the identified cases are "labeled" positive, but the control data is "unlabeled," because it may be affected or unaffected. These kind of data are called positive-unlabeled, presence-absence or presence-only data. Treating the unlabeled group as unaffected is called the _naive model_. The proportion of affected dogs in the unaffected control group is called the nondetection rate or undetected rate.

There are many articles describing methods for analyzing positive-unlabeled data. Our objective was to tackle the problem from the study design angle. Using a simulation, we describe how statistical power changes while varying proportion of undetected positives in the naive controls, and varying the imbalance between the numbers of cases and naive controls.

### Aims

We have two aims. The first aim is to provide sample-size criteria for GWAS researchers who are considering using the naive model. The second aim is to help veterinarians and clients assess the credibility of diagnostic tests developed from GWAS data.

### Methodology

There were two simulation studies. The first looked at the effect the non-detection proportion on power to detect an association between disease status (affected or unaffected) and a genotype. The second looked at the effect of group imbalance on power. The parameters chosen to mimic canine CCLD GWAS studies, in particular, Healey et al. (2019), which used 161 dogs affected with CCLD, and 55 unlabeled dogs as controls. That study was chosen because it was generally similar to other GWAS studies, and because it has the most extreme imbalance.

Using that paper, and some others (REF), the proportion of non-detected cases in the simulation ranged from 0 percent to 10 percent (although other kinds of studies may have higher proportions). The simulated sample size was 200, but we varied the sample size between the numbers of cases and controls, and used 0.5 as the effect size. That effect size was chosen because for N=200 it yielded powers around 80% for Welsh's t-test as the outcome. 

The true model has the known affected group, but also knows the labels of the group of unlabeled data and knows which members of that groups are affected, and analyses them accordingly.

The simulation assessed the models' differences using two outcomes. One was general agreement, that is, the proportion of times inferences from both models agreed on statistical significance. The other outcome significant agreement, that is, the proportion of times the inferences agreed and were both less that 0.05.

There were two simulations. The first simulation was a simple one. We sampled cases and controls under various parameter scenarios from two normal distributions and then compared their means with Wilcoxon rank-sum tests.

The second simulation

### Findings

Undetected positives in the control group reduced the power of the association test. Figure 1 shows the percent reduction in power with and without unlabeled control groups. The beginning of the curves, where the proportion on undetected positives is zero, is the case where the naive model is the correct model. As expected, The unbalance sample size examples show a reduction in power relative to the balanced design. For all three curves, as the proportion of undetected positives increases, the power decreases. 

The columns "No. not det" and "p-value difference" show that for the same N=200 sample size, the difference in p-values decreases as the number of of non-detected cases decreases. For this example, and unbalanced design minimizes the difference in p-values suggesting the the inferences will be similar. However the balanced design give the smallest p-value.

Research limitations/implications – Basically, what is happening is the undetected positives are reducing the effect size. Using the four real sample sizes, It doesn't appear the sample size or imbalance matters much  for bias. Prop.non-detected matters. also treatment effect matters. Larger effect size means more bias.

### Practical implications

However, the undetected-positive rate for CCLD GWAS studies is small, certainly less that 10 percent, and the low rate causes only small biases in odds ratio estimates. However, this study shows that unlabeled data also affect the inferences, and we show that even a few positive cases in the negative controls can affect the power of the study. Fortunately, positive-unlabeled data appears to reduce power, making the results reported in CCLD GWAS studies conservative.

# Researcher should account for 

## References

Baird AE, Carter SD, Innes JF, Ollier WE, Short AD. Genetic basis of cranial cruciate ligament rupture (CCLR) in dogs. Connective tissue research. 2014 Aug 1;55(4):275-81.

Baker LA, Momen M, McNally R, Berres ME, Binversie EE, Sample SJ, Muir P. Biologically enhanced genome-wide association study provides further evidence for candidate loci and discovers novel loci that influence risk of anterior cruciate ligament rupture in a dog model. Frontiers in Genetics. 2021 Mar 5;12:593515.

Bekker J, Davis J. Learning from positive and unlabeled data: A survey. Machine Learning. 2020 Apr;109:719-60.

Cook SR, Conzemius MG, McCue ME, Ekenstedt KJ. SNP‐based heritability and genetic architecture of cranial cruciate ligament rupture in Labrador Retrievers. Animal genetics. 2020 Oct;51(5):824-8.

Engdahl K, Emanuelson U, Höglund O, Bergström A, Hanson J. The epidemiology of cruciate ligament rupture in an insured Swedish dog population. Scientific Reports. 2021 May 5;11(1):1-1.

Gu W, Swihart RK. Absent or undetected? Effects of non-detection of species occurrence on wildlife–habitat models. Biological conservation. 2004 Apr 1;116(2):195-203.

Healey E, Murphy RJ, Hayward JJ, Castelhano M, Boyko AR, Hayashi K, Krotscheck U, Todhunter RJ. Genetic mapping of distal femoral, stifle, and tibial radiographic morphology in dogs with cranial cruciate ligament disease. PloS one. 2019 Oct 17;14(10):e0223094.

Lydersen S. Balanced or imbalanced samples?. Tidsskrift for Den norske legeforening. 2018 Sep 17.

McManus IC. The power of a procedure for detecting mixture distributions in laterality data. Cortex. 1984 Sep 1;20(3):421-6.

## Appendix 1.
Table 1. Sample sizes for four GWAS studies of CCLD. The last columns shows the number of affected cases in the control group assuming 10 percent non-detection rate. 

|   Study |   N   | Cases | Naive controls | Max No. undetected positives (10%) |
|:-------------------:|:-----:|:-----:|:--------------:|:-------------:|
| Baird et al. (2014)     | 217   | 91    | 126       |  13     |
| Baker et al. (2021)     | 397   | 156   | 241       |  24     |
| Cook et al. (2020)      | 333   | 190   | 143       |  14     |
| Healy et al. (2019)     | 216   | 161   | 55        |  6      |
