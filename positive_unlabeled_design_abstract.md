
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