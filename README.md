#Search Engine

A search engine built to search for Links on  Stuff you should know Podcast. 
Use the following link to access it:
[Stuff You Should Know](http://vm520.rz.uni-osnabrueck.de/user180/app.wsgi/)

## Description

The project is completed as part of the course *Artificial Intelligence and the Web* at University of Osnabrück. It consists of the following components:
1. crawler.py - The inital file to be run is this and starts by crawling through a [start url](https://stuffyoushouldknow.com/) and visiting different urls each time while keeping track of unvisited urls so as to avoid getting caught in cycles. The links of https://stuffyoushouldknow.com/ only the  are stored in a text file (*podcasts.txt*) which are then fed to the index function.
2. indexer.py - The contents scrapped from the crawler are then indexed by leveraging the indexing functionality of Whoosh library, as a schema is also instantiated as shown. We also add in the Stemming analyzer as it allows the user to find documents without worrying about word forms and reduces the size of the index, since it reduces the number of separate terms indexed by “collapsing” multiple word forms into a single base word.
```
analyser = StemmingAnalyzer() | CharsetFilter(accent_map)
schema=TEXT(stored=True, analyzer=analyser, spelling=True),
                topic=TEXT(stored=True, analyzer=analyser),
                link=TEXT(stored=True),
                body=TEXT(stored=True, analyzer=analyser)
```
3. search.py - In order to search for particular episode title, the search_term function parses the *search_query* is parsed using `QueryParser` which uses the Or query that specifies that documents that contain more of the query terms score higher. As Whoosh can quickly suggest replacements for mis-typed words by returning a list of words from the index (or a dictionary) that are close to the mis-typed word, we spell-check a user query using the `whoosh.searching.Searcher.correct_query()` method.
4. app.py - This is where all the dots are connected. Using a Flask app, the frontend is rendered and routes for the *homepage* and *search* methods are defined.

### Limitations
As all things, our search engine too, is not perfect. 
- Currently, we can only search for the links which are available on the start page.
- Given the nature of the crawler algorithm, we cannot crawl inside another link.
- We are limited to only a particular website i.e https://stuffyoushouldknow.com/, but in future we'd like to have an search-engine for all links available on the website.

## Getting Started

### Initial Setup:

Clone repo and create a virtual environment
```
$ git clone https://github.com/devashishk99/custom-search-engine.git
$ cd custom-search-engine
$ python3 -m venv venv
```
### Activate virtual environment
Mac / Linux:
```
. venv/bin/activate
```
Windows:
```
venv\Scripts\activate
```

### Dependencies

```
$ pip install -r requirements.txt 
```

### Executing program

* First run the crawler.py file to crawl and scrap data from start url (i.e https://stuffyoushouldknow.com/) and index the data.
```
python3 crawler.py
```
* Once index is ready, run the Flask app and head on to the localhost you can search for the links available on https://stuffyoushouldknow.com/.
```
python3 app.py
```


## Authors

Contributors names:

* Vipra Tyagi



