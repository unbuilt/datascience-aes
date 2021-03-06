# chmullig's Kaggle Essay Code

For http://inclass.kaggle.com/c/columbia-university-introduction-to-data-science-fall-2012,
as part of the class http://columbiadatascience.wordpress.com.

Implements a few models using R and python.

## Requirements:
* Python (only tested with 2.7)
  * nltk
  * scikit-learn
  * pandas
  * PyEnchant
* R
  * RandomForest
  * gbm
  * plyr
  * MASS
  * ggplot2 (soft requirement)
  * reshape (soft requirement)

## Features Created/Used
* number of characters
* numer of sentances
* number of words
* number of syllables
* number of distinct words
* words / sentances
* characters / words
* syllabels / words
* spell_mistakes
* correctly spelled words / total words
* flag for starting with dear
* flag if has semicolon
* flag if has exclamation point
* flag if has question mark
* number of double quotes
* flag if has at least 2 double quotes
* flag indicating whether proper quote punctuation is more common or not (1 if ." is more common than "., -1 if less common, 0 if tied/neither)
* counts of parts of speech (from NLTK)
* rollups for number of nouns, verbs, adjectivs, adverbs, superlatives
* flag for ending with a preposition
* counts of the NER words (eg number of times they used @MONEY)
* TF-IDF word and bigram frequencies that were then PCA'd down to 50 cells.

## Models Used
* First model was OLS linear regression using a subset of the variables. I trained 5 models, one per essay set, with identical formulas. Shockingly good.
* Second model was Random Forest regression, again 5 models. Using more variables.
* Third model was GBM, same formula as random forest, using 5 models.

Also tried doing rfm and gbm with one model using set as a predictor, but it didn't seem to perform as well.

## Basic workflow in buildModel.sh.

1. Run basic_tags.py on test.tsv and train.tsv. This creates almost all the
features/tags/variables we need to use

2. Run add_tfidf.py train_tagged.csv test_tagged.csv 50` to create tf-idf
word vectors for each essay, and PCA down to a more usable 50 variables.

3. Run the R script basicModel.R to create and predict models.
