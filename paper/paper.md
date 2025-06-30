---
title: 'BioHackathon2024 Report: A Tool for Recommending Human Phenotype Ontology Terms for Deep Phenotyping Based on Statistical Data'
title_short: 'BH2024 Report: HPO Term Recommender'
tags:
  - HPO term recommender
  - co-occurrence analysis
  - phenotype
  - rare disease
authors:
  - name: Marlon Arciniega-Sanchez
    orcid: 0009-0005-1835-1399
    affiliation: 1
  - name: Atsuko Yamaguchi
    orcid: 0000-0001-5050-2509
    affiliation: 2
  - name: Orion Buske
    orcid: 0000-0001-5050-2509
    affiliation: 3
  - name: Toyofumi Fujiwara
    orcid: 0000-0001-5050-2509
    affiliation: 4
affiliations:
  - name: International Laboratory for Human Genome Research, Laboratorio Internacional de Investigación sobre el Genoma Humano, Universidad Nacional Autónoma de México, Mexico City 76230, Mexico
    index: 1
  - name: Tokyo City University, Tokyo, Japan
    index: 2
  - name: PhenoTips, Toronto, Canada
    index: 3
  - name: Database Center for Life Science, Joint Support-Center for Data Science Research, Research Organization of Information and Systems, Chiba, Japan
    index: 4
date: 31 August 2024
cito-bibliography: paper.bib
event: BH24
biohackathon_name: "BioHackathon 2024"
biohackathon_url:   "https://2024.biohackathon.org/"
biohackathon_location: "Fukushima, Japan, 2024"
group: HPO term recommender group
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/biohackathon-japan/bh24-hpo-suggest
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: First Author \emph{et al.}
---

# Abstract

The Human Phenotype Ontology (HPO) has established itself as a crucial resource for researchers and clinicians in the rare disease field, offering a standardized vocabulary for over 8,000 phenotypic abnormalities since its introduction in 2008. Widely adopted for patient phenotyping, HPO enhances the accuracy of clinical descriptions, making it an integral component in the creation of patient profiles within registries. Its hierarchical structure and interoperability with other ontologies have expanded its utility in computational tools like PubCaseFinder and LIRICAL, which support differential diagnosis and variant identification. Despite HPO's widespread adoption, accurately identifying and recommending relevant phenotypes for deep phenotyping remains a significant challenge. To address this, we developed a tool that recommends HPO terms based on a co-occurrence matrix derived from seven years of PubCaseFinder queries, totaling approximately 80,000 searches. These queries, primarily from undiagnosed patients with suspected rare and genetic diseases, average 4.27 HPO terms per search, spanning from root to leaf terms. In this study, we split the search queries into training and test datasets to construct a co-occurrence matrix and evaluate the predictive accuracy of our tool. Our findings demonstrate that utilizing extensive HPO-based patient profiles from registries as training data significantly enhances the tool's accuracy. This tool, therefore, holds substantial potential for supporting deep phenotyping in various systems, contributing to more precise patient profiling and diagnosis, and ultimately improving patient outcomes.


# Introduction

The Human Phenotype Ontology (HPO) has become an indispensable resource for researchers and clinicians in the field of rare diseases. Since its introduction in 2008, HPO has grown to include a standardized vocabulary of phenotypic abnormalities associated with over 8,000 diseases [@citation:robinson2008human]. This comprehensive and well-defined set of terms has facilitated patient phenotyping, allowing for more accurate and detailed descriptions of clinical abnormalities [@citation:kohler2014human]. As a result, HPO has become the de facto standard for patient phenotyping in rare diseases, widely adopted by researchers, clinicians, informaticians, and patient registry systems globally [@citation:kohler2019expansion].

HPO's hierarchical organization and interoperability with other ontologies have significantly enhanced its utility in computational tools [@citation:kohler2019encoding]. By using HPO for creating patient profiles, patient repositories such as PhenomeCentral [@citation:buske2015phenomecentral] and IRUD [@citation:adachi2017japan], both participants in the Matchmaker Exchange project, facilitate the precise description and comparison of clinical features across patients [@citation:boycott2022seven]. PubCaseFinder, a phenotype-driven differential diagnosis tool, leverages HPO to generate ranked lists of rare diseases by comparing patient phenotypes with known disease profiles [@citation:fujiwara2018pubcasefinder]. Similarly, LIRICAL utilizes HPO terms to identify potential disease-causing variants from whole-exome or whole-genome sequencing data [@citation:robinson2020interpretable]. These systems underscore the critical role of HPO in modern medical research and diagnostics.

Despite the HPO’s success, one of the ongoing challenges in its application is the accurate and effective identification of patient's phenotypes for deep phenotyping [@citation:shen2017phenotypic; @citation:son2018deep; @citation:steinhaus2022deep; @citation:wang2022deep; @citation:havrilla2022phenominal]. The ability of deep phenotyping not only helps in creating a more complete patient profile but also enhances the accuracy of computational diagnostic tools that rely on phenotype-based comparisons [@citation:yuan2022evaluation].

To address this challenge, we developed a new tool designed to recommend HPO terms closely related to one or more given HPO terms. This tool recommends HPO terms based on a co-occurrence matrix of HPO terms, which was created from seven years' worth of queries consisting of combinations of HPO terms entered into PubCaseFinder [@citation:fujiwara2022advances]. For seven years, PubCaseFinder has processed approximately 80,000 searches, primarily consisting of phenotypes from undiagnosed patients suspected of having rare and genetic diseases. On average, each query includes 4.27 HPO terms, ranging from those near the root to leaf terms, covering a wide spectrum of HPO terms. In this study, we divided the search queries into training and test datasets, created a co-occurrence matrix using the training dataset, and demonstrated the predictive accuracy of our tool using the test dataset. We also show that by using the vast HPO-based patient profiles maintained by patient registries as training data, it is possible to build a more accurate tool. This tool facilitates more accurate and comprehensive deep phenotyping in many existing systems. This, in turn, can lead to more precise creating patient profiles and diagnoses, ultimately contributing to better patient outcomes.


# Method

## 1. Data Preprocessing

**Data Collection:**  

We employed two main data sources: PubCaseFinder query logs and annotations from the Human Phenotype Ontology (HPO). From the PubCaseFinder logs, we extracted 71,029 queries between June 8, 2021, and August 26, 2024. Additionally, we incorporated 12,629 HPO annotations related to rare diseases  [@citation:robinson2008human].

**Data Collapsing:**  
To eliminate biases due to user repetition, we conducted the following steps:

    - Find queries that start with the same N terms (N = 1 or 2)  
    - Then:  
        - Sort the lines  
        - Remove duplicates  
        - Remove prefix lines  

**Training Datasets:**  

   - For the training of our models, we used three different datasets:
        - Training dataset 1: collapsed file from 2021–2023.
        - Training dataset 2: Training dataset 1 + collapsed file from January 1, 2024 to May 2, 2024.
        - Training dataset 3: Training dataset 1 + HPO annotation file.

**Test Dataset:**  
We used queries from the collapsed file from May 2, 2024 to August 26, 2024.

![Data preprocessing and generation of data collection](./images/Data_preprocessing.png)

## 2. Models employed

### Co-occurrence Analysis
![Co-ocurrence model constructions using the three training datasets](./images/Co-ocurrence_model.png)

### Word2Vec Model




## Evaluation

To evaluate the performance of our models after training with different datasets, we employed two validation strategies using the test dataset **(Fig. 3)**. 

The first approach considered the order of the elements within each query. We then input each HPO term from the query into the model and assessed whether the next term in the query was part of the top-k predicted terms. 

In contrast, the second evaluation approach depended on the order of the terms in the query. For each query, we iteratively give one term at a time as input to the model and verify whether any of the remaining terms of the query on evaluation were part of the predicted terms.

These two evaluation approaches allowed us to compare the importance of the term order on the model’s prediction performance and validate whether the prediction was order-dependent or irrelevant to the prediction accuracy. 

![Method analysis image](./images/method_analysis.png)


# Results
## Data Preprocessing
### Data Collection
During data preprocessing, we generated statistical summaries for PubCaseFinder logs by obtaining the frequency of each HPO term to visualize the users' first 20 most-used HPO terms (Fig. 4). We also transformed all the HPO terms in the file to the main branches of HPO and calculated the percentages of terms used for each root (Fig. 5).

For the first step of our statistical analysis, we noticed that the most used terms are: short stature, intellectual disability, and global developmental delay, in that order (ranging from 1.3% to 1.4%) from a total of 7,544 unique HPO terms from the whole file.

After the first 20 most frequent terms, we observed a long-tail distribution, where each HPO term appeared with extremely lower frequencies compared with the most frequent ones. On average, each term has a frequency of approximately 0.01%. This type of distribution is valuable for gaining insight into the most frequent phenotypes observed in patients, but even more importantly, to learn which phenotypes are relevant for differential diagnosis.

![Graph of the 20 most frequent HPO terms in the log file.
Each line is an HPO term, and the x axis represents its frequency in a percentage scale](./images/HPO_frequency_raw.png)

The goal of collapsing the HPO terms from the user queries into the main roots of the HPO is to analyze the percentage of unique HPO terms in our data, covering the total number of HPO terms in the Ontology. The purpose of translating each unique HPO term into its respective phenotypic abnormality root is to assess the coverage of PubCaseFinder queries and have a clearer idea of the potential of our model if we add more training data from future queries.

After the analysis, we noticed that the unique HPO terms from the log file cover 55.7% of all the HPO terms in the HPO (10,222 HPO terms out of 18,354 from the Phenotypic Abnormality roots) (Fig. 5).  We noticed that the number of unique terms from the log file (7,544) differs from the HPO terms covered in the Phenotypic Abnormality roots because some terms belong to more than one root, so some terms are counted as more than one term when collapsing the HPO terms to their roots.

The root with the highest representation in the users’ queries is growth abnormality (82.5%), and the most underrepresented root is Abnormality of metabolism/homeostasis (22.95%). This statistic provides insights into how well-informed our model is, to have a clearer way of evaluating our model’s performance and its potential to increase its prediction power when more data is added.

![Graph of the percentage of HPO terms covered by each Phenotypic Abnormality root from the Human Phenotype Ontology](./images/Phenotypic_Abnormality_ratio.png)

### Data Collapsing
The data collapsing significantly reduced redundancy, with a 27.28% reduction in data after deduplication, and the number of queries collapsed from 71,029 to 51,647.

We generated a scatter plot using a linear regression model to compare the frequency change after the data-collapsing process (Fig. 6). We also calculated the correlation coefficient between the HPO terms ratio from the original log file and the file with the collapsed queries. The correlation coefficient was 0.995, revealing that after the data cleaning, the HPO frequencies are proportional to the ones observed from the log file without curation, indicating a good collapsing process of the data without affecting the ratio of the terms, which is important for the construction of the co-occurrence matrix.

![Scatter plot comparing the ratios between HPO terms from the PubCaseFinder file with the processed dataset](./images/Scatter_plot.png)

Table: Summary comparison of data subsets
| Data subset       | Number of rows | Avg. HPO terms/row | HPO Coverage (%) |
|-------------------|----------------|---------------------|------------------|
| Training data 1   | 33,733         | 4.17                | 48.99%           |
| Training data 2   | 42,690         | 4.14                | 52.47%           |
| Training data 3   | 46,362         | 8.83                | 88.93%           |
| Test data         | 8,957          | 4.58                | 27.65%           |

## Co-occurrence Analysis

Please keep sections to a maximum of only two levels.

## Evaluation

Please keep sections to a maximum of only two levels.


# Discussion

This document use Markdown and you can look at [this tutorial](https://www.markdowntutorial.com/).

## Machine Learning Model

Please keep sections to a maximum of only two levels.

## Data Redundancy

Please keep sections to a maximum of only two levels.

## Evaluation Metrics

Please keep sections to a maximum of only two levels.

## Next Steps

Please keep sections to a maximum of only two levels.



## Tables and figures

Tables can be added in the following way, though alternatives are possible:

Table: Note that table caption is automatically numbered and should be
given before the table itself.

| Header 1 | Header 2 |
| -------- | -------- |
| item 1 | item 2 |
| item 3 | item 4 |

A figure is added with:

![Caption for BioHackrXiv logo figure](./biohackrxiv.png)

# Other main section on your manuscript level 1

Lists can be added with:

1. Item 1
2. Item 2



...

## Acknowledgements

...

## References
