## Project Description

This respository contains Python Jupyter notebooks, .CSV files and plots from search results of Google Scholar using past winners of Nobel Prizes as a starting point.  With the names of winners in science fields (Economics, Physics, Chemistry, Medicine) from 2017-2019 that had Author pages on Google Scholar (15 names gave results), the obtain.ipynb Notebook got detailed information for each, using a modified version of `scholarly` (original package available through `pip install scholarly` or at https://pypi.org/project/scholarly/).  With the information from the Author page, it then retrieved further details about each of the first five publications listed.  From those, it found the first three (at most) authors that were not recent Nobel Prize winners that were listed as an author of those publications.  It then searched for detailed author information and the first five publications listed on their Author pages. This resulted in information for 16 non-Nobel Prize winners that had written a publication with a Nobel Prize winner (one degree away).  The abstracts from publications for both groups of authors were tokenized, lemmatized and analyzed with TF-IDF (term frequency - inverse document frequency). These values were reduced with t-SNE to two dimensions and plotted with three different color codes to make any patterns more noticeable (see the images folder).  No patterns were particularly stark, which was borne out with a t-test for significance across each abstract's average TF-IDF value. A `keras Sequential` model gave a 58% test accuracy when modeling with that feature (labeled `coauthor`) as the target.

### Informational files

* presentation.pdf is a PDF of PowerPoint slides for a business audience explaining the findings of this project

* this README.md file gives an overview of the contents of this repository

* LICENSE.md contains the license information for this repository

#### Two notebooks

* obtain.ipynb is python code in Jupyter using BeautifulSoup and a modified version of `scholarly` to search for Nobel Prize winner publications, co-authors and their publications with Google Scholar. It further uses `scholarly` and `BeautifulSoup` to parse the results and saves each author and publication as its own .CSV file.  Those files are not in this repository individually, but have been concatenated into the authors.csv (in files), publications.csv, copublications.csv, and unfilledpubs.csv (all in csvdata).  In total, there was information on 31 authors that had results that won a Nobel Prize in the period 2017 to 2019 or were one degree away from one of those winners, for 75 publications from 15 winners and 70 publications from 16 first-degree-related authors.

* analysis.ipynb is a Jupyter notebook of python that analyzes the information from obtain.ipynb, specifically TF-IDF on the text of abstracts from publications.csv and copublications.csv, ultimately looking at 76 records.  It then runs keras Sequential models to see how accurately it can predict using TF-IDF for whether an abstract was listed on a Nobel Prize winner's Author page or on a winner's co-author's page (58% accuracy) or what Nobel scientific field (physics, chemistry, economics or medicine) it falls into (19% accuracy).


### files folder
contains two .CSV files:

* one is authors.csv with the author details for Nobel Prize winners and available co-authors

* the other file is science10years.csv with details on Nobel Prizes with each row for an individual that has won a Nobel Prize in Medicine, Physics, Economics or Chemistry in the years ranging from 2010 to 2019.


### csvdata folder
Contains .CSV files created at several points in analysis.ipynb:

* publications.csv and copublications.csv are filled publication information compiled from obtain.ipynb for Nobel Prize winners and first-degree authors, respectively

* unfilledpubs.csv are minimal details for the first 20 publications listed for every filled author, concatenated from obtain.ipynb Author page results

* pubs_with_abstracts.csv is details for all publications.csv and copublications.csv records that had abstracts (where the `bib_abstract` feature was not null)

* abstractsinfo.csv is similar to the above, except it has an additional feature `area` indicating which of four fields of study the publication falls into

* abstracts76.csv is abstractsinfo.csv without duplicate publications, resulting in 76 records

* abs76coords.csv is like abstracts76.csv with 2 coordinate columns for TF-IDF values that were reduced down from tfidfalues.csv so the values could be plotted in two dimensions

* tfidfvalues.csv is TF-IDF values for every word, name, unit of measurement, or sequence of numbers in all the abstracts that were tokenized and lemmatized where each row corresponds to a record in abstracts76.csv and abs76coord.csv.


### images folder
Contains three plots, each with different colors for the same TF-IDF values stored in tfidfvalues.csv, reduced to two dimensions which are stored in abs76coords.csv:

* dots-by-author.png distinguishes by the author of the abstracts; each color represents a different author

* dots-by-field.png distinguishes by the field the abstract falls into, based on the field of a connected Nobel Prize

* dots-by-winner.png distinguishes by whether an abstract was from a publication listed for a Nobel Prize-winner or a first-degree author