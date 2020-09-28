<h1>Inverted Index Generator</h1>

<p>
  This is an Inverted Index Generator implementated in Python3. 

  Inverted Index is a list of postings of all unique terms for all documents in a corpus. It is an index data structure storing a mapping from content, such as words or numbers, to its locations in a document or a set of documents. It is used for text search in large document sets.
</p>

<hr>

## Usage 🔧

It is currently trained on the given corpus. However, it can be trained on any other corpus by providing appropriate path in cell# 1. 

```
path = r".\alldocs"
```

<hr>

## Working ✨

### Tokenizer

- Make list of all files found in that given path directory.
- Extract the document text and split the text into tokens using regex.
- Convert all tokens to lowercase.
- Remove punctuation and numbers.
- Use nltk stopwords list and apply stopping (I removed 179 stopwords. These words are quite redundant which increases the index size by a sizeable factor. However, they play no useful role in searching.)
- Apply porter stemming to the document.
- Tokenizer writes two files:
  - docids.txt – A file mapping a document's filename (without path) to a unique integer, its DOCID. Each line is formatted with a DOCID and filename separated by a tab, as follows: 1234\t32435
  - termids.txt – A file mapping a token found during tokenization to a unique integer, its TERMID. Each line is formatted with a TERMID and token separated by a tab, as follows: 567\tapple

### Inverted Index Generation

- Create a file term_index.txt – An inverted index containing the file position for each occurrence of each term in the collection. 
- Each line contains the complete inverted list for a single term TERMID; a list of DOCID,POSITION values as follows:
  
  347 1542 567 432,43 456,33 456,41
  - 347: TERMID
  - 1542: Total number of occurrences of the term in the entire corpus
  - 567: Total number of documents in which the term appears
  - 432: Document Id in which term appears
  - 43: Position of term in document 432

- In order to support more efficient compression, it uses delta encoding to the inverted list. The first DOCID for a term and the first POSITION for a document is stored normally. Subsequent values are stored as the offset from the prior value. Instead of encoding an inverted list like this:

  347 1542 567 432,43 456,33 456,41.

- It encodes it like this:

  347 1542 567 432,43 24,33 0,8

- In order to do this, DOCIDs and POSITIONs are sorted in ascending order using merge sort.

Note: This programs generates inverted index using both; hashmap and without hashmap.

### Reading Inverted Index

- Now that we have an inverted index of the corpus, we'll want to be able to do something with it. For now, we just pull upsome statistics from the index. For any term TERM, we stem the term and then list the following term information. For example: center

- Listing for term: center
  - TERMID: 5
  - Number of documents containing term: 3221
  - Term frequency in corpus: 21461

<hr>

## Author 👋

You can get in touch with me on my LinkedIn Profile:

#### Ahmad Shafique

[![LinkedIn Link](https://img.shields.io/badge/Connect-ahmadshafique-blue.svg?logo=linkedin&longCache=true&style=social&label=Connect)](https://www.linkedin.com/in/ahmad-shafique)

You can also follow my GitHub Profile to stay updated about my latest projects: [![GitHub Follow](https://img.shields.io/badge/Connect-ahmadshafique-blue.svg?logo=Github&longCache=true&style=social&label=Follow)](https://github.com/ahmadshafique)


If you liked the repo then please support it by giving it a star ⭐!

<hr>

## Contributions Welcome ✨

![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)

If you find any bug in the code or have any improvements in mind then feel free to generate a pull request.

<hr>

## License 📄

[![MIT](https://img.shields.io/cocoapods/l/AFNetworking.svg?style=style&label=License&maxAge=2592000)](LICENSE)

Copyright (c) 2020, Ahmad Shafique
