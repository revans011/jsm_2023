

Basically, what is happening is the undetected positives are reducing the effect size. 


Long Abstract

Title: Design Considerations for Positive-Unlabled GWAS Studies
Author: Richard Evans



Purpose – We investigated sample size considerations for case-unlabled-control studies with an emphasis on canine GWAS studies.

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

Findings – 

Research limitations/implications – Most of the research is based on anecdotal research. Very little has been written on how to fix this problem.

Practical implications – This paper brings this issue to the forefront in an effort to engage the reader, college administrators and educators.

Social Implications – This paper is the building block for future research on this topic. The culture of the college classroom, teaching and learning could be affected by this issue. The hiring, training and evaluation of college instructors could be impacted if colleges and universities choose to investigate the issue of grade inflation at their institutions.

Originality/value – The paper begins with an overview of previous research in this area and then moves on to what is currently being implemented to curb grade inflation. The authors then propose several methods and possible solutions which could be implemented to deal with this problem.


This table suggest that it is BETTER TO BE UNBALANCED--the goal is to minimze the number
of unlabeled positives

n.cases	n.controls.unlabeled	trt.eff	prop.nondetect	n.nodetec	tru.minus.pu	pu.less.tru	p.tru
80			120					0.4			0.1			12			-0.0305553		0.6880	0.0502065
100			100					0.4			0.1			10			-0.0265240		0.7002	0.0500223
120			80					0.4			0.1			8			-0.0222058		0.7104	0.0610979

That make sense becuase few wrongly labeled data means less bias pulling the two groups together. The wrongly labeled positives pull the means closer togther so that the THE EFFECT SIZE BECOMES SMALLER.

RICH use formulas to show that a mixture distribution (of positive and negative) averageed with positive distribution bring the means closer together.

MAY BE BETTER TO HAVE A SMALLER SAMPLE SIZE
This table was meant to check if balance was more important than sample size
So the best was for the largest sample size but unbalanced toward labeled positive cases
n.cases	n.controls.unlabeled	trt.eff	prop.nondetect	n.nodetec	tru.minus.pu	pu.less.tru	p.tru
60			120					0.4			0.1				12		-0.0432026	0.6505000	0.0679540
70			120					0.4			0.1				12		-0.0387561	0.6536667	0.0574749
80			120					0.4			0.1				12		-0.0332350	0.6805000	0.0495099
120			60					0.4			0.1				6		-0.0245107	0.6936667	0.0885766
120			70					0.4			0.1				7		-0.0227336	0.6961667	0.0706366
120			80					0.4			0.1				8		-0.0214813	0.7051667	0.0574158

so (a) tru.minus.pu got smaller , which is good because it mean bias decreased, even though it was wrong more often.



n.cases	n.controls.unlabeled	trt.eff	prop.nondetect	n.nodetec	tru.minus.pu	pu.less.tru	p.tru
120	80	0.4	0.01	1	-0.0031828	0.7674	0.0552154
80	120	0.4	0.01	1	-0.0025346	0.7698	0.0566062
100	100	0.4	0.01	1	-0.0019571	0.7808	0.0505785







[1] "different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   120   |     80     |  0.4  |    0.01    |     1     |   0.00253    |    0.77     | 0.0587 | 0.0612 |
|   80    |    120     |  0.4  |    0.01    |     1     |   0.00235    |    0.775    | 0.0549 | 0.0573 |
|   100   |    100     |  0.4  |    0.01    |     1     |    0.0025    |    0.783    | 0.0505 | 0.053  |

[1] "different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   80    |    120     |  0.4  |    0.05    |     6     |    0.0152    |    0.732    | 0.0529 | 0.0681 |
|   100   |    100     |  0.4  |    0.05    |     5     |    0.0126    |    0.74     | 0.0513 | 0.064  |
|   120   |     80     |  0.4  |    0.05    |     4     |     0.01     |    0.746    | 0.0566 | 0.0667 |

[1] "different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   80    |    120     |  0.4  |    0.1     |    12     |    0.0305    |    0.676    | 0.0511 | 0.0816 |
|   100   |    100     |  0.4  |    0.1     |    10     |    0.025     |    0.695    | 0.0514 | 0.0763 |
|   120   |     80     |  0.4  |    0.1     |     8     |    0.0228    |     0.7     | 0.0597 | 0.0825 |

[1] "decreased treatment effect different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru | p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:-----:|:-----:|
|   100   |    100     |  0.1  |    0.1     |    10     |    0.0143    |    0.508    | 0.435 | 0.449 |
|   80    |    120     |  0.1  |    0.1     |    12     |    0.0152    |    0.509    | 0.432 | 0.447 |
|   120   |     80     |  0.1  |    0.1     |     8     |   0.00723    |    0.521    | 0.434 | 0.442 |

[1] "increased treatment effect different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru |  p.tru   |   p.pu   |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:--------:|:--------:|
|   100   |    100     |   1   |    0.1     |    10     |   7.31e-06   |    0.794    | 4.61e-07 | 7.78e-06 |
|   80    |    120     |   1   |    0.1     |    12     |   1.95e-05   |    0.843    | 1.82e-06 | 2.14e-05 |
|   120   |     80     |   1   |    0.1     |     8     |   2.25e-05   |    0.864    | 3.07e-06 | 2.56e-05 |

[1] "different sample sizes to assess balance vs unbalanced"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   25    |    175     |  0.4  |    0.1     |    18     |    0.111     |    0.512    | 0.103  | 0.214  |
|   175   |     25     |  0.4  |    0.1     |     2     |    0.0184    |    0.644    | 0.196  | 0.215  |
|   80    |    120     |  0.4  |    0.1     |    12     |    0.0329    |    0.674    | 0.0525 | 0.0854 |
|   95    |     95     |  0.4  |    0.1     |    10     |    0.0262    |    0.696    | 0.0574 | 0.0836 |
|   120   |     80     |  0.4  |    0.1     |     8     |    0.0222    |    0.708    | 0.0629 | 0.0851 |





Show in New Window
[1] 0.3821521
[1] 1.198871
[1] 0.1005191
Show in New Window
[1] "different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   120   |     80     |  0.4  |    0.01    |     1     |    0.0027    |    0.768    | 0.0574 | 0.0601 |
|   80    |    120     |  0.4  |    0.01    |     1     |    0.0022    |    0.774    | 0.0529 | 0.0551 |
|   100   |    100     |  0.4  |    0.01    |     1     |   0.00208    |    0.776    | 0.0545 | 0.0566 |

[1] "different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   80    |    120     |  0.4  |    0.05    |     6     |    0.0148    |    0.723    | 0.0522 | 0.067  |
|   100   |    100     |  0.4  |    0.05    |     5     |    0.0118    |    0.749    | 0.0501 | 0.0619 |
|   120   |     80     |  0.4  |    0.05    |     4     |    0.0108    |    0.741    | 0.0584 | 0.0692 |

[1] "different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   80    |    120     |  0.4  |    0.1     |    12     |    0.0321    |    0.686    | 0.0515 | 0.0836 |
|   100   |    100     |  0.4  |    0.1     |    10     |    0.025     |    0.705    | 0.0518 | 0.0767 |
|   120   |     80     |  0.4  |    0.1     |     8     |    0.0213    |    0.711    | 0.0604 | 0.0817 |

[1] "decreased treatment effect different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru | p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:-----:|:-----:|
|   80    |    120     |  0.1  |    0.1     |    12     |    0.0165    |    0.503    | 0.432 | 0.449 |
|   120   |     80     |  0.1  |    0.1     |     8     |    0.0128    |    0.508    | 0.434 | 0.447 |
|   100   |    100     |  0.1  |    0.1     |    10     |   0.00943    |    0.516    | 0.442 | 0.452 |

[1] "increased treatment effect different patterns for the same sample size"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru |  p.tru   |   p.pu   |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:--------:|:--------:|
|   120   |     80     |   1   |    0.1     |     8     |   1.72e-05   |    0.865    | 2.63e-06 | 1.98e-05 |
|   80    |    120     |   1   |    0.1     |    12     |   1.66e-05   |    0.786    | 7.83e-07 | 1.74e-05 |
|   100   |    100     |   1   |    0.1     |    10     |   1.21e-05   |    0.877    | 1.77e-06 | 1.38e-05 |

[1] "different sample sizes to assess balance vs unbalanced"


| n.cases | n.unl.ctrl | t.eff | prp.nondet | n.nodetec | pu.minus.tru | pu.less.tru | p.tru  |  p.pu  |
|:-------:|:----------:|:-----:|:----------:|:---------:|:------------:|:-----------:|:------:|:------:|
|   25    |    175     |  0.4  |    0.1     |    18     |    0.115     |    0.504    | 0.105  |  0.22  |
|   80    |    120     |  0.4  |    0.1     |    12     |    0.0321    |    0.667    | 0.0512 | 0.0834 |
|   95    |     95     |  0.4  |    0.1     |    10     |    0.0293    |    0.692    | 0.0593 | 0.0885 |
|   120   |     80     |  0.4  |    0.1     |     8     |    0.0233    |     0.7     | 0.0556 | 0.079  |
|   175   |     25     |  0.4  |    0.1     |     2     |    0.0169    |    0.645    | 0.191  | 0.208  |

Time difference of 94.61871 mins