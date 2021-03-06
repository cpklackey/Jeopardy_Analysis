### Problem Statement

As a fan of Jeopardy, if one was to prepare to go on the show or just wanted to practice being better at it, how could one devise a study plan?
If you had all the questions and answers for every Jeopardy show, that would be useful. However, 35 years of shows is a lot to study. The goal of this project is to analyze all the data from every Jeopardy show and build a model that constructs the most frequently used keywords for the most frequently occurring answers. Then look at how much of an advantage this would give you, if you concentrated on studying just this subset.
The measure would be the actual dollar amount increase you could potentially gain on one particular show. Actually winning the show depends on what the other contestants score, so that would not be realistic to take into account. The idea here is that if you could increase your own performance, then it follows that you would have a better chance of winning.
The final output will be an online dashboard in which one can choose topics and associated keywords as word clouds and learn what answers are most commonly associated with those keywords.
A recent contestant from October of 2020 who is a data scientist had a similar idea and analyzed years jeopardy data and constructed flash cards of word clouds keywords. My approach will be similar but the end result will be online for anyone to use. Here is a link to his blog: https://colindavy.medium.com/how-i-won-jeopardy-with-data-science-c2e9b52a1958


### Background

Watching recent shows I noticed knowing who a particular Secretary of State is comes up often as a question. So, I played a game that if I did not know the answer and had to guess I would pick Madeline Albright. The next show I watched this question did come up and Madeline Albright was indeed the correct answer. I could follow the same logic with Russian composers, American Authors, etc.… Then if I prepared myself well in all of these types of questions, I could potentially increase the amount of money I could earn in one game.
In Jeopardy, games often come down to one question being the difference, often the Final Jeopardy question but also getting Daily Doubles and high score questions can be significant to your final score.
I found a dataset on Kaggle of 350,000 actual Jeopardy questions which is the basis for this study: https://www.kaggle.com/prondeau/350000-jeopardy-questions/code


### Exploratory Data Analysis

I Looked at the data and decided to approach this as analyzing not by category but by the most frequently occurring answers that have occurred in Jeopardy shows.
I found 43554 unique answers in the dataset.  By filtering out the number of occurrences to only include those that appeared more than 11 times, I reduced
the number of answers to 5168.  This still accounted for 40% of the total questions in the dataset.

### Keyword Extraction

My aim was to extract the most relevant keywords from a give set of questions for a particular answer.  I tested out newer types of models: yake, rake,
spacy entity recognition, and suma. I decided to take a deep dive into the yake extraction model and tested the model out with different hyperparameters,
notably its de-duplication threshold and max_words parameters.  Through statistical analysis using a manufactured scoring system and 2 sample T-Testing, I decided on a
final model and built an online dashboard to display the results.

### Conclusions and Recommendations

-- We built a model using YAKE to extract keywords for frequently occurring Jeopardy answers and can confidently say that with the model we chose, given a set of keywords we extracted for an answer, that set of keywords will be unique to our answer.

-- We also built an online dashboard where word clouds of the keywords can be generated for any of the top answers we chose. In the future, this can be continually updated with current Jeopardy data as all show data can be scraped directly from the Jeopardy archives.

-- Some of the key advantages of the Yake Model is that it is corpus, domain, and language independent. It solely relies on the statistical features of text.

-- Yake also has built in pre-processing (i.e., removing stopwords), de-duplication, and scaling.

-- Yake not only returns keywords but an individual score and ranking for each keyword.

-- Some of the key features of words that Yake uses for scoring are: Casing, Word Position (in relation to the document), Word Frequency, Word Relatedness to Context(number of different terms that occur before and after), and WordDifSentence(frequency of occurrences in different sentences).

-- In consideration of our model, we preserved casing and sentence structure when we prepared our text.

On a final note, this Jeopardy dataset is a rich and robust set of data and there is certainly much more that can be explored. In my process here, I really learned the value of keyword extraction and natural language processing in general and why these are so important and relevant to Data Science today.


### Link to Jupyter Workbook:

 [`Jeopardy_Analysis`](./Jeopardy.ipynb)


### Link to Online Dashboard:

https://share.streamlit.io/cpklackey/jeopardy-dashboard/main/Jeopardy_Flash_Cards.py
