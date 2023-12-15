# Project 3: Information Extraction

**Objectives:** Train an information extraction model and analyze its results.

**What to turn in:** A jupyter notebook containing all your code and results. When asked to discuss results, create a Markdown cell for your text. 

<!-- In some cases, I ask for graphs to illustrate distributions and modeling results. You can create these using python libraries (matplotlib, seaborn) if you are familiar and comfortable using these libraries (not required), or if not, you can use other tools like Excel or Google Sheets to produce graphs, and embed them in the notebook in a Markdown cell (Edit -> Insert Image). If you use python to make plots, you can modify you environment to include matplotlib and seaborn, and you can assume I have access to these libraries in my environment as well. If you make graphs elsewhere and embed them, make sure you upload those images when submitting your assignment as well. -->

Please name the file `<uwnetid>-project3.ipynb`, replacing `<uwnetid>` with your UW net ID. Turn the file in via Canvas.

All commands in the notebook should be able to run assuming the data files are located under the relative path `data/`. Label cell for each problem, and make sure I can easily find where your answers are and what they are! Points may be deducted if answers are disorganized and/or can't be easily found!

**Due date:** Thursday, November 16, 2023 EOD

Some starter code is provided to you in `demo.ipynb`. Please run the starter code to download the necessarily libraries into your environment. There are also instructions in the demo on how to download word2vec vectors.

**Total points:** Graded out of 100 points (There are 120 total points available in this project assignment, meaning there are 20 built-in bonus points.)

## Analyze the output of an off-the-shelf NER model on scientific literature

You will use two off-the-shelf NER models to analyze a sample of COVID-19 literature from the CORD-19 dataset.

1. (5 pt) Load the dataset in `data/cord19_sample/`. A readme file has been provided describing its contents. Answer the following:
* How many papers are included in this dataset?
* What is the distribution of papers by source?
* When were the earliest and latest papers published?

2. (10 pt) You should represent each paper as a document by concatenating its title and abstract together, separated by a space. Instantiate a spaCy model trained on web text (`en_core_web_sm`). Use this model to process all documents in the dataset; keep the NER results for each document.

3. (10 pt) Analyze the NER results to answer the following:
* What is the average number of entities per document?
* What is the average number of entities of each type per document?

4. (10 pt) What is the most common span (a span is the actual text that was identified as a named entity) for each entity type?

5. (10 pt) Now, instantiate a scispaCy model (`en_core_sci_sm`). Process all documents in the dataset again using this new model, and keep the NER results for each document. Perform the same analysis from questions 3 and 4 on the NER results from the scispaCy model. Discuss how these results differ from the spaCy web text model.

6. (10 pt) Output all of the unique entity spans that include the character sequence "covid" from the outputs of the scispaCy model (you should ignore case, i.e., matches for "Covid" or "COVID" should also be returned). Do these spans all correspond to the same entity? Discuss whether your outputs from this search sufficiently identify all papers from the dataset that are about "COVID-19".

## Train a custom model for named entity recognition

You will train an NER model on a classic NER dataset: CoNLL2003, released as part of the CoNLL-2003 shared task. The dataset consists of Reuters news stories between August 1996 and August 1997 that have been tagged with named entities of types location (LOC), organization (ORG), person (PER), and misc (MISC). There are one train split and two test splits in the data subdirectory.

7. (5 pt) Load the train, testa, and testb splits of the CONLL-2003 dataset (in the `/data/conll2003/` subdirectory). Compute the following statistics:
* How many sentences are in each split?
* What are the mean, min, and max lengths of sentences by split?

8. (10 pt) Sentences have been pre-tokenized in this dataset. If you followed the directions in the demo.ipynb for preprocessing, you will wind up with a data format where each token will be represented as a tuple of the form (word, pos, label), where the pos is the part-of-speech tag and label is the NER tag we are interested in learning. Compute the following for the NER tags:
* What is the distribution of NER labels in this dataset by split? (How many tokens are associated with each label in each of the splits?)
* Is there anything strange or unexpected about this label set and the counts?

9. (20 pt) Train a CRF model on the **train** set. Instead of the features given in the demo, use word2vec vector elements as features. This means the input features into the CRF model should be 300-dimensional. If you cannot get this to train, you can reduce the dimensionality by just using the first 100 dimensions of the word2vec vector (or even fewer dimensions), as long as you can demonstrate that you can adapt the word2vec vector as features.

10. (10 pt) Make predictions using your trained model on the **testa** split. Output a classification report that reports per-class performance, as well as micro- and macro- averaged metrics. Do not include the 'O' label when computing metric averages.

11. (10 pt) Discuss the differences between the macro- and micro- averaged results and what this means about the performance of your model.

12. (10 pt) Discuss differences in per-class performance. What are some things you might try to improve the performance for classes with low F1.