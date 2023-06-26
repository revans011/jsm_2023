# Long abstract: Design Considerations for studies with positive-unlabeled data

2023-06-12 \
Richard Evans \
Clinical and Translational Science Institute \
University of Minnesota \
[Richard Evans' email](evan0770@umn.edu)

## Purpose

In risk association studies, the affected subjects in the positive group are often identified with perfect sensitivity and specificity, but sometimes the disease status of control subjects is not perfectly ascertained. That means the control groups may be mixtures of both unaffected cases and some unidentified affected cases. Those kinds of control groups are called _unlabeled_, because we are not completely sure about the disease labels (affected or unaffected). The entire dataset is referred to as _postitive-unlabeled_ (PU).

 Accounting for the unlabeled aspect of the control groups is usually handled during data analysis. (Bekker XXX, Hastie, Gu), rather than during the study design phase. In this study, we start at the beginning and considered design changes for studies that expect unlabeled control groups. In particular, we considered the effect of unlabeled data on the power of association tests.

~~For example, some affected subjects in the control group may have subclinical or sub-diagnostic disease. For example, in genome-wide association studies of cranial cruciate ligament disease in dogs, the positive groups consist of dogs with surgically stabilized knees, so the ruptured CCL is identified with certainty. However, the control groups consist of dogs who have not yet spontaneously ruptured their CCL. It is possible that some dogs in the control group may have the genotype associated with CCL disease, and just not ruptured by the time of the study. GWAS CCLD researchers mitigate this problem by selecting older dogs for controls. Nevertheless, from a statistical perspective, their control groups are considered unlabeled.~~

## Background

Examples of positive-unlabeled data are also well documented in human medicine, but less so in veterinary medicine. (refs in human medicine) Nevertheless, there are some veterinary studies the fall into the PU framework. For example, genome-wide association studies of cranial cruciate ligament disease (CCLD) in dogs use case-control designs. The affected cases are truly positive CCLD cases because they are enrolled from the set of dogs who have undergone knee stabilization surgery. The controls are typically five-years-old or older with no history of CCLD and pass an orthopedic veterinary exam by board-certified surgeons. However some control dogs will have spontaneous rupture in the future, and so genetically belong in the CCLD affected group. Other control dogs may have sub-diagnostic disease. For example, a dog might appear sound on physical exam and enrolled in the control group, but actually have force-platform-detectable hindlimb lameness. (ref conz eye vs platform) Such a dog should not be in the control group because the lameness might be subclinical CCLD.

There are other plausible examples of PU data in the veterinary literature, typically in risk-factor studies using case-control designs. For example, Arthur et al. (2016) used a case-control design to assess the risk of osteosarcoma following fracture repair. They noted, "There may be additional cases [in the control group] in which implant-related osteosarcoma was diagnosed in the private practice setting without referral...," suggesting that the control group may be PU. For another example, Wylie et al. 2013 studied risk factors for equine laminitis using controls obtained from an owner survey. The authors noted the PU aspect of their data,"Our study relied on owner-reported diagnoses of endocrinopathic conditions, and this may have introduced misclassification bias."

Using data science terminology, the affected cases are "labeled" positive, but the control data is "unlabeled," because dogs may be affected or unaffected. These kind of data are called positive-unlabeled or presence-only data. Treating the unlabeled control group as entirely unaffected is called the _naive model_. The proportion of affected dogs in the unaffected control group is called the _nondetection_ rate or _undetected rate_.

The Biases caused by PU data are well documented in the statistical and data science literature. (ref) The biases due to misclassification can be sometimes be mitigated using models other than the naive model and with the appropriate data analysis, and there are many articles describing methods for analyzing positive-unlabeled data. Bekker provides and excellent summary of methods. Sometimes, however researchers prefer the naive model because they believe that their small nondection rates induce biases that are too small for pracatical consideration. There is some suggestion that nondetection rates under 10% do have little impact on bias.

But bias in estimates (e.g., bias in regression coefficients) is just one part of the results; the other part is inference (e.g., p-values). Central to inference is the power of statistical tests in the study. Power is used in planning a study to as a measure of the ability of the study to make the correct decision. Typically, 80 percent power means that if the groups are truly different, then the statistical test has an 80 percent chance of obtain p<0.05

During the design of a risk association study, a researcher might calculate the sample size they need using the naive model. However, if the data are PU, then the naive model is incorrect and the estimated power may not correct.

In this paper we investigated the effect of PU data on statistical power under the naive model. The reference power is defined as the power when the naive model is correct and the group sizes are balanced. The results are described in terms power loss relative to the reference power, either percent power loss or absolute power loss. These two quantities are analogous to relative risk and absolute risk from epidemiology.

Using a simulation, we described how statistical power changes with varying proportion of undetected positives in the naive controls, and varying the imbalance between the numbers of cases and naive controls.

## Aim

Our aim is to provide sample size guidelines for risk association researchers who are considering analyzing PU data under the naive model.

## Objective

The objective is to report the loss in statistical power due to unlabeled data two ways: as a percentage of the reference power, and as asbolute power loss.

## Methodology

This was a simulation study assessing the power of a univariate association test when planning a risk association study using the naive model with PU data. There are many statistical tests for association (for GWAS, see Pan, XXX), but we calculated the power for a chi-square test (DF=1) because it is a common test. For example, the association between disease state and any binary covariate (e.g., sex, or a SNP) might be tested with a chi-square test with DF=1.


In the context of risk association studies, and all else being equal, the chi-square test would achieve maximum power for a balanced study design and when the naive model is correct (i.e., the undetected rate is zero). We call that maximum power the _reference power_ and reported our results as both percent power loss relative to the reference power and as absolute power loss from reference power. In other words, we are using the chi-square test to show how much statistical power is lost by ignoring the nondetection rate.

The total sample size for the simulation was fixed N=200, which is consistent with Healey (XXX, N=216) and YYY (XXX,N=217). The effect size, 0.5 OR WAS IT 0.3, was chosen because with N=200, the reference power was about 80 percent, which is value that is commonly used in study design. That way, the reference model is the one with standard power of 80 percent. Note that the sample size and effect size are not a key parameters for the simulation, because for any sample size an effect size can be chosen so that power is 80 percent.

 The simulation study varied two study design parameters: the non-detection proportion and group-size imbalance. The proportion of undetected positives in the control group ranged from 0 (the value for reference power) to 10 percent. We used 10 percent as the upper limit because researcher are generally willing to accept detection rates below 10 percent and use the naive model, but change to a PU analysis for rates greater than 10 percent.  
 
 We modeled imbalance using  Healey et al. (2019), which used 161 dogs affected with CCLD, and 55 unlabeled dogs as controls and zzz so that imbalnces ranged from 3:1 and 1:3. That study was chosen because it was generally similar to other GWAS studies, and because it has the most extreme imbalance. We only used two imbalance proportions (1:3 and 3:1) and no imbalance (1:1) because the key parameter for this study was the nondetection proportion.

 The simulated data were generated in XXXX steps using two latent variables with normal distributions. The truly negative cases come from N(0,1). The tru First, using the nondetection rate, 

## Findings

### Loss of power, balanced group sizecccccccccc

Undetected positives in the control group reduced the power of the association test. An example of the reduction in power is in Figure 1. The first point on blue curve in Figure 1 shows the power of the association test when there are no undetected positives in the control group. This point serves as the "referece" power when the proportion of undetected positives is the control group is zero and the naive model is the correct model. As the proportion of undetected positives increases (the x-axis), the blue curves decreases, which means the power is decreasing. The y-axis is the 

RICH THESE ARE RAW POWERS. FIX THE TABLE TO INCLUDE PERCENT LOSS AND ABSOLUTE LOSS

| n.cases | n.naiv.control | prp.nondet | eff.sz | naive.power | cohen |
|:-------:|:--------------:|:----------:|:------:|:-----------:|:-----:|
|   100   |      100       |     0      |  0.21  |    0.822    | 0.229 |
|   100   |      100       |    0.05    |  0.21  |    0.788    | 0.217 |
|   100   |      100       |    0.1     |  0.21  |    0.747    | 0.204 |

### Loss of power, unbalanced group sizes

The $\chi^{2}$ test statistic is not symetric, so the the direction of the 

The columns "No. not det" and "p-value difference" show that for the same N=200 sample size, the difference in p-values decreases as the number of of non-detected cases decreases. For this example, and unbalanced design minimizes the difference in p-values suggesting the the inferences will be similar. However the balanced design give the smallest p-value.


| n.cases | n.naiv.control | prp.nondet | eff.sz | naive.power | cohen |
|:-------:|:--------------:|:----------:|:------:|:-----------:|:-----:|
|   150   |       50       |     0      |  0.21  |    0.706    | 0.19  |
|   150   |       50       |    0.05    |  0.21  |    0.681    | 0.182 |
|   150   |       50       |    0.1     |  0.21  |    0.637    | 0.171 |



| n.cases | n.naiv.control | prp.nondet | eff.sz | naive.power | cohen |
|:-------:|:--------------:|:----------:|:------:|:-----------:|:-----:|
|   50    |      150       |     0      |  0.21  |    0.755    | 0.209 |
|   50    |      150       |    0.05    |  0.21  |    0.709    | 0.196 |
|   50    |      150       |    0.1     |  0.21  |    0.677    | 0.186 |


Research limitations/implications – Basically, what is happening is the undetected positives are reducing the effect size. Using the four real sample sizes, It doesn't appear the sample size or imbalance matters much  for bias. Prop.non-detected matters. also treatment effect matters. Larger effect size means more bias.

### Practical implications

However, the undetected-positive rate for CCLD GWAS studies is small, certainly less that 10 percent, and the low rate causes only small biases in odds ratio estimates. However, this study shows that unlabeled data also affect the inferences, and we show that even a few positive cases in the negative controls can affect the power of the study. Fortunately, positive-unlabeled data appears to reduce power, making the results reported in CCLD GWAS studies conservative.

# Researcher should account for 

# Discussion

There are modest power reductions even for small proportions of undetected positives in the control group. The results for absolute powers appear less dramatic by can affect the sample size. For example, with a 5 percent nondection rate and a balanced study design, the sample size in the context of this simulation would have to be XXXX, which is a zzz percent increase in sample size. 

This was a simulation study to test the power of a single association test. The working example was the association test for a single SNP in a GWAS study, but the simulation results apply to any kind of study with univariate association tests, such as any risk factor study. That is a broad class of studies. Examples include the univariate associations between post-op surgical infections and various surgical conditions (e.g., boarded surgeon vs resident, manufactuer of bone plate). In that case, there may be subdiagnostic infections in the control group. Another example is univariate association tests in veterinary surveys, such as XXX. In that case, there may be subclinical ...

In this simulaion, the undetected positives in the negative group were randomly sampled from the same population as the detected positives in the affected group. That's a common assumption (ref GU and others) but there are other models. For example, the undetected positives in the control group might be a subpopulation of positives defined by another variable. For example, in a CCLD GWAS study, the undetected positives in the control group might be positive dogs with low BCS only. 



 it does not apply to the situation where binary "affectedness" changes as the function of a scaled risk factor variable. Using risk factors for CCLD example, BCS may affect spontaneous rupture. 

This was a simulation study that considered the effect on statistical power of 10 percent or fewer undetected positives in the control group. The simulation used 

Other papers have discussed improved tests and power. (wang, and the pan paper )

## References

Arthur EG, Arthur GL, Keeler MR, Bryan JN. Risk of osteosarcoma in dogs after open fracture fixation. Veterinary Surgery. 2016 Jan;45(1):30-5.

Baird AE, Carter SD, Innes JF, Ollier WE, Short AD. Genetic basis of cranial cruciate ligament rupture (CCLR) in dogs. Connective tissue research. 2014 Aug 1;55(4):275-81.

Baker LA, Momen M, McNally R, Berres ME, Binversie EE, Sample SJ, Muir P. Biologically enhanced genome-wide association study provides further evidence for candidate loci and discovers novel loci that influence risk of anterior cruciate ligament rupture in a dog model. Frontiers in Genetics. 2021 Mar 5;12:593515.

Basu S, Pan W. Comparison of statistical tests for disease association with rare variants. Genetic epidemiology. 2011 Nov;35(7):606-19.

Bekker J, Davis J. Learning from positive and unlabeled data: A survey. Machine Learning. 2020 Apr;109:719-60.

Cook SR, Conzemius MG, McCue ME, Ekenstedt KJ. SNP‐based heritability and genetic architecture of cranial cruciate ligament rupture in Labrador Retrievers. Animal genetics. 2020 Oct;51(5):824-8.

Engdahl K, Emanuelson U, Höglund O, Bergström A, Hanson J. The epidemiology of cruciate ligament rupture in an insured Swedish dog population. Scientific Reports. 2021 May 5;11(1):1-1.

Gu W, Swihart RK. Absent or undetected? Effects of non-detection of species occurrence on wildlife–habitat models. Biological conservation. 2004 Apr 1;116(2):195-203.

Healey E, Murphy RJ, Hayward JJ, Castelhano M, Boyko AR, Hayashi K, Krotscheck U, Todhunter RJ. Genetic mapping of distal femoral, stifle, and tibial radiographic morphology in dogs with cranial cruciate ligament disease. PloS one. 2019 Oct 17;14(10):e0223094.

Lydersen S. Balanced or imbalanced samples?. Tidsskrift for Den norske legeforening. 2018 Sep 17.

McManus IC. The power of a procedure for detecting mixture distributions in laterality data. Cortex. 1984 Sep 1;20(3):421-6.

Wang T, Elston RC. Improved power by use of a weighted score test for linkage disequilibrium mapping. The american journal of human genetics. 2007 Feb 1;80(2):353-60.

Wylie CE, Collins SN, Verheyen KL, Newton JR. Risk factors for equine laminitis: A case-control study conducted in veterinary-registered horses and ponies in Great Britain between 2009 and 2011. The Veterinary Journal. 2013 Oct 1;198(1):57-69.

## Appendix 1.
Table 1. Sample sizes for four GWAS studies of CCLD. The last columns shows the number of affected cases in the control group assuming 10 percent non-detection rate. 

|   Study |   N   | Cases | Naive controls | Max No. undetected positives (10%) |
|:-------------------:|:-----:|:-----:|:--------------:|:-------------:|
| Baird et al. (2014)     | 217   | 91    | 126       |  13     |
| Baker et al. (2021)     | 397   | 156   | 241       |  24     |
| Cook et al. (2020)      | 333   | 190   | 143       |  14     |
| Healy et al. (2019)     | 216   | 161   | 55        |  6      |






