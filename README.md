This respository contains Python Jupyter notebooks, .CSV files and plots from search results of Google Scholar and past winners of Nobel Prizes.

* presentation.pdf is PowerPoint slides for a business audience explaining the findings of this project

* this README.md file gives an overview of the contents of this repository

* LICENSE.md contains the license information for this repository

#### Two notebooks:

* obtain.ipynb is python code in Jupyter using BeautifulSoup and a modified version of `<scholarly>` to search for Nobel Prize winner publications, co-authors and their publications with Google Scholar. It further uses `<scholarly>` and `<BeautifulSoup>` to parse the results and saves each author and publication as its own .CSV file.  Those files are not in this repository individually, but have been concatenated into the authors.csv (in files), publications.csv, copublications.csv, and unfilledpubs.csv (all in csvdata).  In total, there was information on 31 authors that had results that won a Nobel Prize in the period 2017 to 2019 or were one degree away from one of those winners, for 75 publications from 15 winners and 70 publications from 16 first-degree-related authors.

* analysis.ipynb is a Jupyter notebook of python that analyzes the information from obtain.ipynb, specifically TF-IDF on the text of abstracts from publications.csv and copublications.csv, looking at 84 records in total.  It then runs keras Sequential models to see how accurately it can predict using TF-IDF for whether an abstract was listed on a Nobel Prize winner's Author page or on a winner's co-author's page (43%) or what Nobel scientific field it falls into (17%).


### files folder
contains two .CSV files:

* one is authors.csv with the author details for Nobel Prize winners and available co-authors

* the other file is science10years.csv with details on Nobel Prizes with each row for an individual that has won a Nobel Prize in Medicine, Physics, Economics or Chemistry in the range from 2010 to 2019.


### csvdata folder
contains .CSV files created at several points in analysis.ipynb:

* publications.csv and copublications.csv are filled publication information compiled from obtain.ipynb for Nobel Prize winners and first-degree authors, respectively

* unfilledpubs.csv are minimal details for the first 20 publications listed for every filled author, concatenated from obtain.ipynb Author page results

* pubs_with_abstracts.csv is details for all publications.csv and copublications.csv records that had abstracts (where the bib_abstract feature was not null)

* abstractsinfo.csv is similar to the above, except it has an additional column indicating which of four fielda of study the publication falls into

* abscoords.csv is like abstractsinfo.csv with 2 coordinate columns for TF-IDF values that were reduced down from tfidfwords.csv to be plotted

* tfidfwords.csv is TF-IDF values for every word, name, unit of measurement, or sequence of numbers in all the abstracts that were tokenized and lemmatized where each row corresponds to a row in abstractsinfo.csv, abscoord.csv or pubs_with_abstracts.csv.


### images folder
contains three plots, each with different colors for the same TF-IDF values reduced to two dimensions and without an outlier which is located at index 44 in abstcoords.csv:

* dots-by-author.png distinguishes by the author of the abstracts using authID (0Name, for example)

* dots-by-field.png distinguishes by the field the abstract falls into based on the field a connected Nobel Prize was in

* dots-by-winner.png distinguishes by whether an abstract was from a publication listed for a Nobel Prize winner or a first-degree connected author