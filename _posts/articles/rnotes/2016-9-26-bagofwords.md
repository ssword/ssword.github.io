# Some tip on bag of words process

Most of the contents here are taking from the package documentation repectively. 

R packages for bag of works:

* tm
* qdap

## **freq_terms {qdap}**

### Description

> Find the most frequently occurring terms in a text vector.

### Usage

```R
    freq_terms(text.var, top=20, at.least=1, stopwords=NULL,
      extend=TRUE, ...)
```

## **VectorSource {tm}**

### Details

>A vector source interprets each element of the vector x as a document.

## **Corpus {tm}**

### Details

> All extension classes must provide accessors to extract subsets( **\[** ), individual documents( **\[\[** ), and metadata(**meta**). The function **length** must return the number of documents, and **as.list** must construct a list holding the documents.

## **VCorpus {tm}**

### Details

A volatile corpus is fully kept in memory and thus all changes only affect the corresponding **R** object. The fucntion **Corpus** is a convenience alias to **VCorpus**

### Usage

```r
    VCorpus(x, readerControl=list(reader=reader(x)), language="en")

    as.VCorpus(x)
```

### Functions work as named for text cleaning:

* **tolower {Basic}**
* **removePunctuation {tm}**
* **removeNumbers {tm}**
* **stripWhitespace {tm}**
* **bracketX {qdap}** : Remove all text within brackets
* **replace_number {qdap}** : Replace numbers with their word equivalents
* **replace_abbreviation {qdap}** : Replace abbreviations with their full text equivalents
* **replace_contraction {qdap}** : Convert contractions back to their base words.
* **replcae_symbol {qdap}** : Replace common symbols with their word equivalents
* **stopwords {tm}**
* **stemDocuments {tm}**
* **stemCompletion {tm}**


### Code example:

```R
    clean_corpus <- function(corpus){
      corpus <- tm_map(corpus, removePunctuation)
      corpus <- tm_map(corpus, stripWhitespace)
      corpus <- tm_map(corpus, removeNumbers)
      corpus <- tm_map(corpus, content_transformer(tolower))
      corpus <- tm_map(corpus, removeWords, 
                   c(stopwords("en"), "amp"))
      return(corpus)
    }
```

## **TermDocumentMatrix {tm}**

### Usage 

```R
    TermDocumentMatrix(x, control = list())
    DocumentTermMatrix(x, control = list())
    as.TermDocumentMatrix(x, ...)
    as.DocumentTermMatrix(x, ...)
```
## **wordcloud {wordcloud}**

### Usage

We often use wordcloud with RColorBrewer for eye-catching color patterns. 

```R
    ## maximum n is 8-12
    palettes = brewer.pal(n, name)
    wordcloud(words,freq,scale=c(4,.5),min.freq=3,max.words=Inf,
	random.order=TRUE, random.color=FALSE, rot.per=.1,
	colors=palettes,ordered.colors=FALSE,use.r.layout=FALSE,
	fixed.asp=TRUE, ...)
```


### Details

> If freq is missing, then words can either be a character vector, or Corpus. If it is a vector and freq is missing, standard stop words will be removed prior to plotting.





