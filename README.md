# Information Retrieval

- [Information Retrieval](#information-retrieval)
  - [Introduction](#introduction)
  - [Implementation](#implementation)
  - [Results](#results)
  - [Sources](#sources)

## Introduction

Information retrieval (IR) is the activity of obtaining Information system resources that are relevant to an information need from a collection of those resources.  Searches can be based on full-text or other content-based indexing. This repository houses a single notebook that implements search on full-text based indexing, on a small corpus made of tweets and a unique ID for each.

An information retrieval process begins when a user enters a query into  the system. Queries are formal statements of information needs, for  example search strings in web search engines. In information retrieval a query does not uniquely identify a single object in the collection.  Instead, several objects may match the query, perhaps with different  degrees of relevancy. The notebook in this repository uses a TF-IDF score to identify the degree of relevancy.

## Implementation

1. First builds an inverted index of all tweets, treating each tweet as a single  document
2. Implements a small Earley parser based on the `lark` library that can process simple queries like `eggs and cheeese` or `eggs or (cheese and ham)`, etc.
3. Extends the search implementation to also return a TF-IDF scoring of the results, and sorts them based on relevancy.

## Results

Parse tree for `"egg and (cheese or with)"` -

```
start
  do_and
    search	egg
    do_or
      search	cheese
      search	with
```

Parse tree for `"(A or B and C) and (D and E)"` -

```
start
  do_and
    do_and
      do_or
        search	A
        search	B
      search	C
    do_and
      search	D
      search	E
```

Search results without TF-IDF for `eggs and cheese or rice` -

```
Parsed search query into tree: start
  do_or
    do_and
      search	egg
      search	cheese
    search	rice

Found 7 documents.

ID:	81503002321616896
Tweet:	Bacon/cheddar slider topped w/fried egg & Blue cheese slider topped w/avocado & purple cherokee tomato

ID:	81587643376336896
Tweet:	RT TAG_USERNAME : I want a steak and cheese egg roll right now .

ID:	81673244926685184
Tweet:	I think I want some cheese eggs and pancakes ... but will I cook ? Where's my gf . This ain't right to make such a hard decision

ID:	81736742478155778
Tweet:	Made myself some scrambled eggs with cheese and bacon bits

ID:	82650970722533376
Tweet:	I went swimming , then ate asparagus bacon egg cheese biscuit goodness , then watched Date Night . It was ... it was good . TAG_FINAL_HASHTAGS

ID:	85032815321825280
Tweet:	Cheese hashbrowns , turkey bacon , veggie tofu scramble , rice , french toast , scrambled eggs , strawberries & cantaloupe . TAG_FINAL_HASHTAGS

ID:	86441828815089664
Tweet:	RT TAG_USERNAME : RT TAG_USERNAME : Pancakes , bacon , eggs w/ cheese , & hashbrown casserole on deck TAG_HASHTAGS < ~i want sum !!!!! Ok it's good too
```

Search results for `"eggs and cheese or rice"` -

```
Parsed search query into tree: start
  do_or
    do_and
      search	egg
      search	cheese
    search	rice

Found 7 documents.

Score:	0.16783216783216784
ID:	85032815321825280
Tweet:	Cheese hashbrowns , turkey bacon , veggie tofu scramble , rice , french toast , scrambled eggs , strawberries & cantaloupe . TAG_FINAL_HASHTAGS

Score:	0.07758620689655173
ID:	81736742478155778
Tweet:	Made myself some scrambled eggs with cheese and bacon bits

Score:	0.0703125
ID:	81587643376336896
Tweet:	RT TAG_USERNAME : I want a steak and cheese egg roll right now .

Score:	0.044117647058823525
ID:	81503002321616896
Tweet:	Bacon/cheddar slider topped w/fried egg & Blue cheese slider topped w/avocado & purple cherokee tomato

Score:	0.03515625
ID:	81673244926685184
Tweet:	I think I want some cheese eggs and pancakes ... but will I cook ? Where's my gf . This ain't right to make such a hard decision

Score:	0.03169014084507042
ID:	82650970722533376
Tweet:	I went swimming , then ate asparagus bacon egg cheese biscuit goodness , then watched Date Night . It was ... it was good . TAG_FINAL_HASHTAGS

Score:	0.029801324503311258
ID:	86441828815089664
Tweet:	RT TAG_USERNAME : RT TAG_USERNAME : Pancakes , bacon , eggs w/ cheese , & hashbrown casserole on deck TAG_HASHTAGS < ~i want sum !!!!! Ok it's good too
```

## Sources

- Wikipedia article on Information Retrieval