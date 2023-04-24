# Data Bias in Algorithms as a Result of Language

# API Documentation

This project utilizes the Pandas library and Stack Overflow modules to build tables.

Pandas: https://pandas.pydata.org/pandas-docs/stable/reference/index.html

Stack Overflow: https://stackoverflow.com/questions/40206249/count-of-most-popular-words-in-a-pandas-dataframe

# License

MIT License

Copyright (c) 2022 cwolfhope

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

# Exploring the scored dataset

Where did the model make mistakes?

Through visual inspection of the dataframes, the first observation that is blantantly available to any observer is the fact that the lowest scores represented in the data, are made up of majorily by entries in languages other than English. Considering these entries in the data, this creates a cause for question over whether these entries represent a larger trend in the data that could account for potential bias in the algoritms used within the Perspective API.

If we apply a threshhold to the data (in this case only viewing scores above 0.75), we can observe that within the top 50 most commonly used words, all of the words are from the english dictionary. However, if we consider before the prevelence of non-english comments in the lower scores of the data, this highlights a discrepency: Either there is not enough entries from other languages in the dataset (which is likely) or there is an algorithmic bias that gives entries in languages other than english lower toxicity scores (which would represent an obvious bias).

# Designing and performing tests

The threshhold for toxicity scores used universally across this project is 0.75 (all scores above the 0.75 marker). This was selected so that only the scores that were most guarenteed to be toxic would be used when comparing english language scores with those of other languages.

Hypothesis: The Perspective model has a bias that categorizes comments in other languages as less toxic than comments in English.

To assess the validity of this hypothesis, we must make a comparison between how the Perspective API scores comments in english vs other languages. For this test, we will be using English and Spanish as our designated languages. I have compiled a new dataset with the data points categorized as "comment_text" (referring to un-translated comments) and "translated_text" (referring to original comments that have been translated via excel's build in translator). The comments within this dataset consist of 10, randomly selected (via Pandas.sample()), comments from the original 'labeled_and_scored_comments' dataset that have been translated and also included within the dataset.

The new dataset containing the translations of the original randomly selected comments, was then processed to compile scores for each entry (both non-translated and translated). These scsores were then entered into new datasets and processed to provide descriptive statistics for each respectively.

# Analyzing the data

By making a direct comparison between the two tables, containing the descriptive statistics for both sets of scores for the datasets, we are able to observe that there is a substantial difference between the values that appear between both. At every point in the dataset, there is a difference of more than 1 whole point in score between the translated and non-translated datasets. The mean and scores at all percentiles of the translated data is less than the original, non-translated comments. Even at the extreme, the max values of the translated comments are less than the original comments.


# Results

There is an apparent bias in the way that the Perspective API scores comments in English vs that of comments in other languages. While the tests that were conducted in this project only utilized Spanish as an alternative to English, given the prevelence of different languages besides Spanish in the lowest scores within the original dataset, it is likely that the same pattern would occur in other languages. In all cases, the comments that were in Spanish, were scored less than the same comment in English. The differences in these scores were very extreme, often accounting for multiple points of difference between the original comments and the translated comments. This trend is most likely caused by not enough datapoints from other languages besides English being included in the dataset when the Perspective algorithm was trained.


