# Adv_ML_NLP
The goal of the project is to provide a data text synthesis of a massive corpora of scientific articles
about natural language processing.
This amount of data is not really big, just 44Mo, but is big enough to be too complicated to be
processed by hand.


# **Project Report : Text Synthesis**

**Dataframe initialization**

We chose to use the pandas dataframe format to manipulate our dataset. Since the .xml, we chose to focus only on the French texts since they are much more numerous than the English ones. For our analyses, we created the following columns : Title, Date, Abstract, Corpus and Keyword. 

**Preprocessing**

For the pre-processing phase, we proceeded as follows. First, we remove all the apostrophes present in the text (ex: "the plane" becomes "the plane"). Second, we remove the special characters (ex: "(see image)" becomes "see image". Thirdly, we remove the accents (ex: "element" becomes "element").

The rest of the preprocessing consists in the detection of stopwords in order to lighten the content of the corpus so as to keep only the meaningful words.

![](https://lh3.googleusercontent.com/H-51WrPUsNL778Jb_-LXYcL_Ox0zl5PFOTwHV8hjcmTRYFOhhbEbB5o945JRI5kow1K8IeNG2qOuLppdlRVCWYCBsEUoqkbO_SXD7XawAv2G758vHyDNk6XwU7wupHr5KclM55ah)

The last step of the preprocessing consists in using a lemmatizer in order to keep only the root of each word. 
For this, we tried two different lemmatizers:
French Lefff Lemmatizer => This last one worked only for common names and is pretty slow.
Spacy => Works for all types of words but is very slow and does not recognize some words.


If you look at the following screenshot, you may see errors. We notice that verbs ending with "s" are considered as plural nouns (e.g. "consideron"). We can also notice that some words are not always treated in the same way (ex: "grammair" and "grammaire").
An additional reason to limit the use of the lemmatizer is the execution time which is quite long (5 minutes) compared to the few seconds of the previous functions.


**Wordcloud**

Library used: WordCloud.

This library is based on the calculation of the frequency of each word of the text. These values are stored in a dictionary and then displayed via matplotlib.

This first analysis consists in observing the most pronounced words each year in the different scientific articles, all in a visual way.

During our analysis of the word clouds for each year, we notice the presence of unmeaningful words like the word 'avoir' which is present every year. To overcome this problem, we can use a library to tag the words in order to focus on common nouns only for example.

Nevertheless, this approach does not seem interesting to us because it only counts the occurrences of words in the texts to highlight those that are the most pronounced.

Moreover, when observing the results, we notice that the words found each year do not vary much. Very often the same words are found such as “corpus”, "système", “analyse”, “texte”, “traitement” or “article”.

Here is a comparison of the first three years of the dataset with the last three:

![](https://lh3.googleusercontent.com/LwIfPUSZF6aplbECJpfvIEcgCHA_Fa8dWMBG2wQq8gBvOOv44sFD4L9kX3Hxs1QGTJ3PdQzBBUdyU_uZhwExCKQfGsbqaQ1qdmzcuKOr) ![](https://lh5.googleusercontent.com/Y4Nl0XXPOH2nJ1ZSr3A1Nd2luo9iuE0GiYFi9J8OXVU25Rj-LRUX0ylyuSHKmz6YrBPSX9Va5Vm1dY0w9UdjC1SyUeAZoB7aiZISRcNm)

On these images, we can still observe the strong presence of the term "analyse" in the early years and of the term "résultat" in the later years. We can assume that with the advancement of Natural Language Processing technologies, the models used are more and more complex and provide more concrete results rather than an analysis on existing technologies.

**Bar chart**

To test a new approach, we decided to perform the same operation, i.e. counting occurrences, on the abstracts of the dataset but to perform a different representation: a bar chart.

The result obtained on the set of abstracts is as follows:

![](https://lh6.googleusercontent.com/Wre7TTJqIjg0RZ-KuVx8tFaWgIiHEjdvHNsfkvF-_-utFlAp-rD3TNIgjCypVSxsZ1e8SHYBzIyQkZCtfI__jWz5Fh47d64tK4NHq1xL)

We can notice on the diagram above that the verb "avoir" is far too present in the dataset. Furthermore, the removal of accents in French transforms the "à" into "a", which increases their occurrence artificially.

We also note the strong presence of "ce" that we had not previously noticed.

**Enhanced Word Cloud and Bar Chart**

In order to correct these problems and get more interesting results, we have made the following choices :

- Make a test without using the French lemmatizer because it is not 100% operational. For example, we can quote the word "corpus", which is transformed into "corpu" because it is interpreted as a plural.
- We will also add a preprocessing step to remove words of 3 letters or less. Thus removing many spurious words that are not considered stop words like "a"

With these rules, we get the following results:

![](https://lh5.googleusercontent.com/dvcJ7UdJG0oydsfWpmnOztRYITmIqaECIzTmj7jHdhwyY8txharH7cdEDeJcerzTUnr1NgvqzWjKKxr-V9OCYn_BLHi5d7ETc046Prpl)

![](https://lh3.googleusercontent.com/KiUGGq61gfq1UTcwamqWYAb1SpaizZpwth5Y0fRZw-ssMcrmRuyewUKVWJxR1OzV3viaOHXTqTdt0C9lnIZqhb3fTtXc17muKV0vzTsg) ![](https://lh6.googleusercontent.com/b0qbAotycNnR_I5Cch4Jg4YHwLDV3a04uK1BxOCN3hhde1RmLty1Mgeh3gER1FsGOZnNUF0YpPbH1sP0gfWEfeeS3DAIrLA7eO3XXKpD) 
![](https://lh6.googleusercontent.com/eVr9x-C9ZYPVgmMw4VjYQq0H3-PdU1Q_tDj7K43n-gSj73hHHuWvOmOvPIVOD8HvQ6p0rX0UyEGT0qjqV6mmg3O7bOAYuT-EWjRbKvlk)


We thus obtain more significant results because the words are heavier in meaning (note the presence of the word "cette" in 3rd position).
For the interpretation of these results, one can note the strong presence of the term "corpus" in this set of articles on the bar chart. If we combine this information with the fact that the word corpus is not present in the word clouds of the early years, we can deduce that the use of a text corpus as a dataset is recent. This can be explained quite naturally with the evolution of computer science, because today we can quickly process more text than before. As the amount of data is also higher, it is easier to find more content to analyze.
The presence of the term "article" is also not surprising, given the fact that when writing a research paper, one cites other articles.
