# Gene of interest recommendation system and logistic prediction model for colorectal carcinoma

## INTRODUCTION:
In today's era of big data, Recommendation Systems (RS) have become integral to our digital lives, significantly impacting the fields of information science and consumer experiences. [1] The rapid growth of the internet and e-commerce has expedited the evolution of RS, which is designed to curate and provide personalized content recommendations tailored to individual users. The integration of Big Data into RS has further propelled the field, promising more precise and efficient recommendations. In light of the abundant healthcare data available, there is a growing interest in applying RS to gene selection when presented with a disease dataset, particularly an expression matrix. [2] 

A logistic regression model is used when the outcome of interest is binary. The term “logistic” refers to the underlying “logit” (log odds) function that is used to model the binary outcome. Logistic regression describes and estimates the relationship between a binary dependent variable (the presence or absence of colorectal cancer, for instance) and one or more independent variables (covariates or explanatory variables). [3]

Colorectal cancer ranks as the third most common cancer on a global scale, comprising approximately 10% of all cancer diagnoses and standing as the second leading cause of cancer-related deaths worldwide. Its prevalence is predominantly observed in the older population, with many cases occurring in individuals aged 50 and above. Colorectal cancer is frequently identified in advanced stages, leading to limited treatment options. There is a pressing need to identify gene markers for colon cancer to reduce fatalities and enhance early detection. The application of RS would facilitate the rapid and precise detection of genes of interest, significantly improving targeted therapy for colon cancer. [4]

## RESEARCH PROBLEM:

The pressing concern addressed in this study lies within the realm of colorectal cancer, a formidable global health challenge. Despite being the third most common cancer worldwide, colorectal cancer continues to claim the lives of countless individuals. A significant proportion of cases remain undetected until advanced stages, severely limiting treatment options. Consequently, there exists an urgent need to identify specific gene markers associated with colon cancer. Early detection and targeted therapeutic interventions hold the key to mitigating fatalities and improving patient outcomes.

With the rise of Precision medicine tailoring therapies specific to the patients has proved to be effective in managing and curing the condition. In this study, we are trying to create an algorithm to calculate the top genes of interest and prediction model so that therapy can be specifically targeted for each patient.

## METHODS: 

Utilizing data sourced from the TCGA-COAD project [5], which comprises RNA-seq gene expression data from 481 primary tumor samples and 41 Normal samples. The TCGA-COAD transcriptome profiling of normal and tumor samples was obtained using the TCGAbiolinks R package [6]. The samples with missing meta data were dropped and DESeq2 R package [7] was utilized to perform differential gene expression and get the highly differential genes to perform further analysis.

The data is split into test and train sets with an 80:20 ratio, the system computes and suggests the top N genes of interest to enhance the precision of cancer detection and enable more targeted therapeutic interventions. The RS algorithm assesses gene precision and coverage to gauge the efficacy of gene recommendations, and logistic regression model for diagnosis holds a promise for advancements in the early detection and treatment of colorectal cancer.

## EXPERIMENTAL DESIGN:

**_Gene interest calculation:_**

The gene expression data is log-transformed, and the top 1000 genes are selected and stored in a matrix form (dual mode matrix). A single gene network is constructed by cross-multiplication of the gene expression matrix with itself. A similarity matrix [8] is constructed and used to generate the gene of interest by matrix multiplication of the similarity matrix with the gene expression matrix. The gene of interest is then sorted to get the gene ranking. [9]

<p align="centre">
  _Gene single network(G): G = Ge * Ge_ 
  
  _Gene similarity matrix (Ja): Jaij = gij/(gii+gjj-gij)_ 
  
  _Gene interest (Gi): Gi = Ja * Ge_
  
  _Gene Rank (GR): GR = sort (Gi)_
</p>


**_Logistic Regression Model:_** 

A logistic regression model has been employed from scratch to predict the patient diagnosis from the gene expression data and covariates like age, stage of tumor and sex. Data preprocessing was performed to convert the categorical variables like stage of tumor, sex, and diagnosis into numerical indices.



## Model:  
 

The Python sklearn package [10] was utilized to split the data into training and test sets, with 80% allocated to the training data and 20% to the test data. Initially, a random weight vector was generated using the np.random function [11], and this vector was employed to make the initial predictions prior to optimization.

The data was linearly fitted by multiplying the weight vector with the x data and then transformed using the sigmoid activation function. Predictions were made based on whether the transformed data exceeded a threshold of 0.5 or not.

The weight vector was optimized to minimize the loss of predictions, utilizing a regularization rate of 0.0001 and learning rate of 0.01 over 100 epochs of iterations. Subsequently, data predictions were conducted again to evaluate how the optimization affected the accuracy of predictions.

## EXPERIMENTAL RESULTS:

**_Recommendation system:_** The gene single network creation resulted in a gene * gene matrix. This matrix is converted into similarity with diagonals as 1 and the higher the score more similar the genes are. Gene of interest matrix is a gene * sample matrix which has the values of each gene for the sample based on their similarity. These are then ranked to get the top genes.

 

**_Logistic regression:_**  The model created with sample weights that are generated at random showed that the matrix is not predicting the class 0 with all class 0 misclassified as class 1. To correct this optimization with 0.0001 regularization and 0.01 learning rate method showed that the model was able to predict all the data with 100% accuracy.

  

## Discussion about results:

This study focuses on integrating Recommendation Systems (RS) and logistic regression to address the critical issue of colorectal cancer. RS, rooted in big data, offers personalized gene recommendations, an asset in the era of precision medicine. The logistic regression model complements this approach by predicting patient diagnoses, facilitating targeted therapeutic interventions.

The pressing concern of colorectal cancer's impact is highlighted, emphasizing its global prevalence and the need for early detection strategies. The RS algorithm, using RNA-seq data from the TCGA-COAD project, computes top gene recommendations. These genes are vital in understanding and addressing colorectal cancer at a molecular level.

The gene interest calculation method involves log transformation, gene network construction, and similarity matrix generation. This process yields a ranked list of genes, providing a foundation for the subsequent logistic regression model. The logistic regression model, initially hindered by misclassifications, is successfully optimized with regularization, and learning rate adjustments, achieving a remarkable 100% accuracy in predicting patient diagnoses.

## Conclusion:

The integration of RS and logistic regression presents a promising avenue for advancing precision medicine in colorectal cancer. By combining personalized gene recommendations with accurate prediction models, this study lays the groundwork for tailored therapeutic strategies. The ability to compute top genes of interest ensures a targeted approach to cancer treatment, a crucial step in managing and potentially curing colorectal cancer.
Moving forward, the study's findings offer insights into the potential clinical applications of RS and logistic regression in the realm of cancer research. The success in optimizing the logistic regression model signifies a robust framework for enhancing diagnostic accuracy. These methodologies, when applied synergistically, contribute to a more effective and personalized approach to colorectal cancer management, holding implications for broader applications in precision medicine.



## References: 
1. Fayyaz Z, Ebrahimian M, Nawara D, Ibrahim A, & Kashef, R. (2020). Recommendation systems: Algorithms, challenges, metrics, and business opportunities. applied sciences, 10(21), 7748.
2. Chang V. Towards data analysis for weather cloud computing. (2017). Knowl Based Syst. 
3. Zabor EC, Reddy CA, Tendulkar RD, Patil S. Logistic regression in clinical studies. International Journal of Radiation Oncology* Biology* Physics. 2022 Feb 1;112(2):271-7.
4. World Health Organization. (2023, July 11). Colorectal cancer. https://www.who.int/news-room/fact-sheets/detail/colorectal-cancer.
5. National Cancer Institute. (2019). The Cancer Genome Atlas - Colon Adenocarcinoma (TCGA-COAD) Data. Genomic Data Commons. https://portal.gdc.cancer.gov/projects/TCGA-COAD .
6. Colaprico A, Silva TC, Olsen C, Garofano L, Cava C, Garolini D, Sabedot TS, Malta TM, Pagnotta SM, Castiglioni I, Ceccarelli M. TCGAbiolinks: an R/Bioconductor package for integrative analysis of TCGA data. Nucleic acids research. 2016 May 5;44(8):e71-.
7. Love MI, Huber W, Anders S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. Genome biology. 2014 Dec;15(12):1-21.
8. Vorontsov IE, Kuakovskiy IV, Makeev Vj. Jaccard index-based similarity measure to compare transcription factor binding site models. Algo Mole Biol, 2013;8(1)1.
9. Hu J, Sharma S, Gao Z, & Chang V. (2018). Gene-based collaborative filtering using recommender system. Computers & Electrical Engineering, 65, 332-341.
10. Pedregosa F, Varoquaux, Ga el, et al. Scikit-learn: Machine learning in Python. Journal of machine learning research. 2011; 12:2825–30.
11. Harris CR, Millman KJ, van der Walt SJ, Gommers R, Virtanen P, Cournapeau D, et al. Array programming with NumPy. Nature. 2020; 585:357–62.
