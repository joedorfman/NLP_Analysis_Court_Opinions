# Capstone

Executive Summary

The goal of my work was to examine the utility of a number of data science tools for an attorney who might be seeking to: (1) Find the central cases from a large collection of cases, (2) Find cases that are similar to those already under consideration, or (3) Sort cases into groups based on some sort of vector representation of the cases that is lower-dimensional than a bag-of-words model.

For purposes of analysis, I focused on court of appeals decisions resolving cases under Section 7 of the Endangered Species Act (ESA).  I selected this legal topic because: 

(1) At the sub-Supreme Court level, the case law is dominated by the thinking of a single appellate jurisdiction (the 9th circuit, covering the far western U.S)  

(2) The case law is abundant and contains repeating textual 

(3) The case law is easy to specify using a boolean search of a legal database; and

(4) I have some subject matter expertise with this topic.

Underlying court decisions are government documents free of copyright.  Court decisions are collated and freely available for download, via API, from the Court Listener database.

Much of my work relates to unsupervised methods for characterizing legal opinions as relatively low dimensional vectors (i.e., low dimensional relative to a naive bag-of-words approach).  In order to measure whether these "case vectors" are meaningful, I primarily relied on two appraoches: 

(1) Looking for correlation between inter-case cosine distances, as computed using different approaches for case vectorization.  If there is corellation, I would take that as evidence that there the vectorization of the case was capturing some underlying signal about the content of the case.

(2) Evaluating whether the vectors are useful for a supervised binary classification task.  Supervised learning on court opinions is generally a labor-intensive project, because it generally requires hand-coding numerous cases based on human legal analysis of each case.  In order to avoid the need for this, I classified cases based on jurisdiction of origin (from the 9th circuit vs. from elsewhere in the country).  To avoid "give away" data such as the name of the judge or the name of the jurisdiction in the text itself, I excised the leading and trailing 500 words of text from each opinion.

Overall, I found:

(1) Filtering cases based on network centrality, within the network of other cases on the same topic, is a simple and straightforward technique to identify important a subset of important cases.

(2) Because the information on the citation linkages between opinions is readily available in machine-readable format, court opinions are amenable to the construction of collaborative recommender systems.  Under such systems, Cases X and Y are similar if subsequent cases that tend to cite X also tend to cite Y (or vice versa).  Similarity analysis based on a recommender system can recommend further cases to read, beyond the cases flagged as most central.

(3) The words in cases can be vectorized using contextual embedding tools like Word2Vec.  These words can then be averaged to generate a single vector for each case.  Representation of a case via word-averaging correllates with representation of the same case via the recommender system.  The corellation is weak, but statistically signficant. (Between .214 and .246 at 95% confidence, computed using bootstrap estimation.)  

(4) Document-level contextual vectors for an opinion text can also be developed using Doc2Vec.  When Doc2Vec is trained with separate labels for each document, it represents the cases in a manner that hardly correlates with the arrangement of cases found by the citation-based recommender system.  

(5) However, Doc2Vec representations appear to be extremely useful for classification purposes.  Doc2Vec can be trained on cases with binary labels and then individual document vectors can be inferred for training and test set observations, without relying on label information.  These document vectors give good results as features in both a simple logistic regression and a support vector classifier.  I obtained AUC-ROC scores in the high 80s/low 90s.  

Limitations:
The training of the neural net to generate Word2Vec and Doc2Vec embeddings did not appear to be deterministic, despite setting a numpy random seed at the beginning of the notebook and (separately) for the train-test split.  Repeated runs on the notebook generate different AUC-ROC values in the range of the high 80s/low 90s.

Please see Capstone presentation.pptx for graphs and further discussion of my work.

Directory of Key Notebooks:

00_Case_Data_from_API.ipynb

Notebook documenting the retrieval of basic case citation information from the Court Listener site, via its API.

01_Text_Data_from_API.ipynb

Notebook documenting the retrieval of full text data from the Court Listener site, via its API.

02_Establish Recommender Matrix.ipynb

Notebook documenting the creation of an item-based collaborative recommender system for identifying court cases that were similarly cited to the particular case of interest

03_Network Analysis

Brief network analysis of the citation structure of the cases under consideration.

04_Text_Pre-Processing.ipynb

Pre-processing of opinion text, for use in NLP software such as Word2Vec and Doc2Vec.  Fitting of Word2Vec model.

05_Word2Vec.ipynb

Examination of individual word vectors.  Computation of inter-case distances based on the average word vector for each case.  Comparison between this approach and the citation-based recommender system.

06_Doc2Vec.ipynb

Computation of inter-case distances based on the document vectors for each case.  Comparison between this approach and the citation-based recommender system.

07_Classification 

Classification of cases as originating in the 9th circuit, or not, based solely on document vector information.

