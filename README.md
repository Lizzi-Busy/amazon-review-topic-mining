# Topic Mining on Amazon Smartphone Reviews

This project established a Latent Dirichlet Allocation (LDA) model in R to examine topical tendencies from a corpus of 20,000+ Amazon smartphone reviews over the past six years. 

Key ideas include: topic modeling, POS tagging, clustering, and time series.


## Dependencies

**R packages**
- `tm` 
- `spacyr`
- `textstem`
- `quanteda`
- `topicmodels` 
- `lda` 
- `wordcloud`
- `ggplot2`


## Data

The empirical data of this project comprises over 20,000 Amazon smartphone reviews spanning Jan 2013 – Dec 2018 that Griko Nibras has compiled and provided on his website (https://www.kaggle.com/grikomsn/amazon-cell-phones-reviews#20190928-reviews.csv). 

The dataset includes both locked and unlocked carriers, and scoped on 9 brands: Apple, Google, Huawei, Motorola, Nokia, OnePlus, Samsung, Sony, Xiaomi.

## Method

**Pre-processing**

Keywords: pos tagging, lemmatization, stopword removal

<details>
  <summary>Click to expand</summary>
  
*Lemmatization* The tokens in the corpus were lemmatized and converted to lower case in order to reduce the inflectional forms from each word to a common base or root.

*Stopword Removal.* Although creating a document-feature matrix is completely automatic, we can control the output by pre-processing the corpus. It is standard practice to remove common syntactical stopwords (such as *the* and *of*) and tokens associated with our search terms (such as *mobile* and *phone*). These words occur so frequently, and with such regularity in all documents, that they overwhelm topical variability. To avoid this situation, we used `quanteda` package in R to remove stopwords and search terms. 

*Non-Standard Word Removal.* It was determined that standard stopword removal is not sufficient for this corpus. Smartphone reviews have properties that differ from the scientific journals and news articles typically used in topic modeling. Most obviously different is the use of series and version labels for electronic products. For example, in "Moto Z Droid version XT1635", the phrases "Z Droid" and "XT1635" do not hold any semantic meaning. They are tantamount to proper nouns for a particular Motorola release. These words are not useful in detecting meaningful topics in our data. Therefore, we used POS tagger in `spacyr` to identify word types and eliminate all non-standard dictionary words from the corpus. That helped us reduce runtime while still having good results.
</details>

**Modeling**

Keyword: LDA!

<details>
  <summary>Click to expand</summary>
  
The main objective of this project is to analyze topical tendencies of Amazon smartphone reviews. The simplest approach is to count tokens. But if we use word counts to draw conclusions about the topical trending across different reviewers and time frames, we risk making mistakes because words are variable and ambiguous. Variability arises because reviewers often have a choice of several synonyms. In order to make claims about topical tendencies, we would have to summarize the results of hundreds of word associations, which is quite onerous. Ambiguity adds further complications: if we count the occurrence of a single word, we may unwittingly conflate multiple meanings of that word (i.e. “pixel” as a picture element and “pixel” as a Google smartphone).

Statistical topic models, such as Latent Dirichlet Allocation (LDA), use contextual clues to group related words and distinguish between uses of ambiguous words. The model employs the "bag of words" approach to text analysis. That is, it assumes a document is generated by picking a set of k topics and then for each topic picking a set of words. There is an important parameter that must be specified upfront: k, the number of topics that the algorithm should use to classify documents. Small k tends to result in topics of a broad and general nature; larger k is usually associated with more focused topics and slower computation. There is a tradeoff between accuracy and efficiency. After much trial and error, it was determined that k=8 yielded the most semantically meaningful results in a reasonble runtime. 

The topic model will contribute to this project in two ways. Firstly, the model reduces the dimensionality of the corpus by assigning each word to one (or more than one) of the eight clusters or topics. This level of complexity is rich enough to express much of the variability of the corpus, but small enough to be interpreted by humans. Secondly, the model is able to identify the primary topic in each document. When linked with time series data, the model offers a way of exploring macro scale topic trend over time.
</details>


## Walkthrough

TBD

