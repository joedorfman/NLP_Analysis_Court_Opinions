# Capstone

Summary of Key Notebooks:

00_Case_Data_from_API.ipynb

Notebook documenting the retrieval of basic case citation information from the Court Listener site, via its API.


01_Text_Data_from_API.ipynb

Notebook documenting the retrieval of full text data from the Court Listener site, via its API.


02_Establish Recommender Matrix.ipynb

Notebook documenting the creation of an item-based collaborative recommender system for identifying court cases that were similarly cited to the particular case of interest


03_Text_Pre-Processing.ipynb

Pre-processing of opinion text, for use in NLP software such as Word2Vec and Doc2Vec.  Fitting of Word2Vec model.

04. Word2Vec.ipynb

Examination of individual word vectors.  Computation of inter-case distances based on the average word vector for each case.  Comparison between this approach and the citation-based recommender system.

05. Network Analysis

Very brief network analysis of the citation structure of the cases under consideration.

06. Doc2Vec.ipynb

Computation of inter-case distances based on the document vectors for each case.  Comparison between this approach and the citation-based recommender system.

08. Classification 

Classification of cases as originating in the 9th circuit, or not, based solely on document vector information.