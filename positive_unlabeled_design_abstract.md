

Long Abstract

Title: Design Considerations for Positive-Unlabled GWAS Studies
Author: Richard Evans

Purpose – We investigated sample size considerations for case-unlabled-control studies (i.e. postitive-unlabeled data) with an emphasis on canine GWAS studies.

Background – Genome wide association studies (GWAS) of cranial cruciate ligament disease (CCLD) in dogs use case-control designs. The case are truly positive CCLD cases because they are enrolled from the set of dogs who have undergone CCL repair. The controls are typically five-years-old or older with no history of CCLD and pass an orthopedic veterinary exam by a board-certifed surgeon. CCLD GWAS studies usually enroll as many dogs as they possibly can without regard to the balance between the numbers of cases and controls.

It is the control group that is of interest to us because some of those dogs are not truly CCLD-negative dogs, that is, they are false negatives. Some will get CCLD in the future, and so genotypically belong in the CCLD cases group. Other control dogs may have sub-diagnostic disease. For example, a dog might appear sound on physical exam and enrolled in the control group, but actually have force-platform-detectable hindlimb lameness. Such a dog should not be in the control group because the lameness might be subclinical CCLD.

Using data science terminology, the indentified cases are "labled" positive, but the other data is data is "unlabled," because they may be affected or unaffected. These kind of data are called positive-unlabled, presence-absence or presence-only data.

Treating the unlabeled group as unaffected is called the naive model, and the case-control designs that use the naive model are really case-unlabled-control designs.

CCLD GWAS studies assume the naive model because researchers assume the false-negative rate is low, and the low rate causes small biases that have minimal impact on inferences. However, there are more components to false-negative bias than the false-negative rate. Biases can increase or decrease if the property of being false-negative is correlated with a covariate (e.g., a SNP). For example, hypothetically, there could be a set of SNPs that predispose dogs to unstable knees and sub-diagnostic CCLD. The amount of bias also changes if covariates are strongly or weakly assocated with disease state. That is a set of SNPS are strongly or weakly associated with CCLD.

Most PU article develop methods for analyzing PU data. Our objective is to tackle the problem from the study design angle. We simulate CCLD-specific GWAS and show the sample-size conditions for which the biases from naive models are acceptable. Specifically, we show when the naive model and presence-absence models give the same answers while varying the imbalance between the numbers of cases and naive controls.

If the naive model is deemed not acceptable, then many other models and analytical methods are available to use. Some methods were specifically designed for GWAS. However, the naive models in GWAS studies fit into a larger data analyitic framework. Data Scientists have develped methods under the name positive-unlabled data. Statisticians use the terms presence-only or confirmation bias, and wildlife population biologists use the term presence-absence or non-detection. So, there is no shortage of methods to account for false negatives.

Aims – We have two aims. The first aim is to provide study-design critera for GWAS researchers who are considering using the naive model. The second aim is to help veterinarians and clients assess the credability of diagnostic tests developed from GWAS data.

Methodology – This was a simulation study with its parameters chosen to mimic canine CCLD GWAS studies, in particular, Baird et al. That study was chosen because it was generally simialar to other GWAS studies, and because it was particialry easy to understand.

Using that paper, and some others (REF), the proportion of non-detected cases in the simulation ranged from 1 percent to 10 percent (although other kinds of studies may have higher proportions). The simulated sample size was 200, buy we varied the sample size between the numbers of cases and controls, and the effect size.

For outcomes, we compared the naive model to the true model. The true model has a group of affected subjects and  a group of unaffected subjects and all the subjects are labled correctly. To reiterate, the naive model has a group of some of the affected subjects and another group of but has a group of unlabeled subjects, who may be affected or unaffected. that we analyze as is unaffected.

The true model has the known affected group, but also knows the labels of the group of unlabeled data and knows which memebers of that groups are affected, and analyses them accordingly.

The simulation assessed the models' differences using two outcomes. One was general agreement, that is, the proportion of times inferences from both models agreed on statistical significance. The other outcome significant agreement, that is, the proportion of times the inferences agreed and were both less that 0.05.

There were two simulations. The first simulation was a simple one. We sampled cases and controls under various parameter scenarios from two normal distributions and then compared their means with Wilcoxon rank-sum tests.

The second simulation

Findings – In simulation 1, the undetected positives reduced the effect size. So, the mean PU data p-values were always larger than the mean nomimal p-values, Those differences decreased as the number of non-detected positives decreased.

The columns "No. not det" and "p-value difference" show that for the same N=200 sample size, the diffference in p-values decreases as the number of of non-detected cases decreases. For this example, and unbalaced design mimimzes the difference in p-values suggesting the the inferences will be similar. However the balanced design give the smallest p-value.

Research limitations/implications – Basically, what is happening is the undetected positives are reducing the effect size. Using the four real sample sizes, It doesn't appear the sample size or imbalance matters much  for bias. Prop.non-detected matters. also treament effect matters. Larger effect size means more bias.

Practical implications – Reseacher should account for 

Social Implications – This paper is the building block for future research on this topic. The culture of the college classroom, teaching and learning could be affected by this issue. The hiring, training and evaluation of college instructors could be impacted if colleges and universities choose to investigate the issue of grade inflation at their institutions.

Originality – There are many articles describing methods of analyzing PU data, and some describing the analysis of GWAS PU data, but none describe the design of GWAS, PU studies. This article is a first step in considering the study design aspects of GWAS studies.


References

Baird AE, Carter SD, Innes JF, Ollier WE, Short AD. Genetic basis of cranial cruciate ligament rupture (CCLR) in dogs. Connective tissue research. 2014 Aug 1;55(4):275-81.

Baker LA, Momen M, McNally R, Berres ME, Binversie EE, Sample SJ, Muir P. Biologically enhanced genome-wide association study provides further evidence for candidate loci and discovers novel loci that influence risk of anterior cruciate ligament rupture in a dog model. Frontiers in Genetics. 2021 Mar 5;12:593515.

Cook SR, Conzemius MG, McCue ME, Ekenstedt KJ. SNP‐based heritability and genetic architecture of cranial cruciate ligament rupture in Labrador Retrievers. Animal genetics. 2020 Oct;51(5):824-8.

Healey E, Murphy RJ, Hayward JJ, Castelhano M, Boyko AR, Hayashi K, Krotscheck U, Todhunter RJ. Genetic mapping of distal femoral, stifle, and tibial radiographic morphology in dogs with cranial cruciate ligament disease. PloS one. 2019 Oct 17;14(10):e0223094.

Lydersen S. Balanced or imbalanced samples?. Tidsskrift for Den norske legeforening. 2018 Sep 17.

McManus IC. The power of a procedure for detecting mixture distributions in laterality data. Cortex. 1984 Sep 1;20(3):421-6.

