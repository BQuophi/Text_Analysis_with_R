# Text Analysis with R
![image](https://github.com/user-attachments/assets/82c4ed86-5672-4292-b208-6b07e73e24a3)

[Image Source](https://www.datanami.com/2016/11/21/text-analytics-machine-learning-virtuous-combination/)

This project demonstrates basic text analysis using R, covering tokenization, word frequency analysis, and filtering of stopwords. The analysis is applied to the text of "Frankenstein" by Mary Shelley. The project aims to provide a practical introduction to Natural Language Processing (NLP) concepts and techniques using R.

## Table of Contents  

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Step-by-Step Guide](#step-by-step-guide)
    1. [Loading and Tokenizing Text](#loading-and-tokenizing-text)
    2. [Word Frequency Analysis](#word-frequency-analysis)
    3. [Filtering Stopwords](#filtering-stopwords)
5. [Custom Function for Text Analysis](#custom-function-for-text-analysis)
6. [Resources](#resources)

## Introduction

The purpose of this project is to explore basic text analysis techniques using R. Text analysis, a subset of Natural Language Processing (NLP), involves processing and analyzing large collections of text data to extract meaningful information. This project covers essential NLP concepts such as tokenization, word frequency analysis, and filtering of stopwords.

### NLP Concepts Used in This Project

1. **Tokenization**: Tokenization is the process of breaking down text into smaller units, such as words or sentences. In this project, we use tokenization to split the text into individual words and sentences.

2. **Word Frequency Analysis**: This technique involves counting the occurrences of each word in the text. By analyzing word frequencies, we can identify the most common words and gain insights into the text's content.

3. **Stopwords Filtering**: Stopwords are common words (e.g., "and", "the", "is") that usually do not carry significant meaning and are often removed from text analysis to focus on more meaningful words. This project demonstrates how to filter out stopwords from the text.

## Installation

To run this project, you need to have R and RStudio installed on your system. You also need to install the following R packages:

```R
install.packages("tidyverse")
install.packages("tokenizers")
```

## Usage

1. Clone the repository to your local machine.
2. Open the R script in RStudio.
3. Run the script to perform the text analysis.

## Step-by-Step Guide

### Loading and Tokenizing Text

First, we load the necessary packages and create a variable containing a sample text. 

```R
library(tokenizers)
library(tidyverse)

text <- paste("You will rejoice to hear that no disaster has accompanied the commencement of an enterprise which you have regarded with such evil forebodings. I arrived here yesterday, and my first task is to assure my dear sister of my welfare and increasing confidence in the success of my undertaking")
```

We then tokenize the text into words.

```R
words <- tokenize_words(text)
words <- words[[1]]
```

### Word Frequency Analysis

Next, we create a table of word frequencies and convert it into a data frame.

```R
tab <- table(words)
tab <- data_frame(word = names(tab), count = as.numeric(tab))
tab <- arrange(tab, desc(count))
```

### Filtering Stopwords

We load a dataset of word frequencies and join it with our word frequency table to filter out stopwords.

```R
wordfreq <- read_csv("https://raw.githubusercontent.com/BrockDSL/R_for_Text_Analysis/master/wordfrequency.csv")
tab <- inner_join(tab, wordfreq)
filtered_tab <- filter(tab, frequency < 0.01)
```

## Custom Function for Text Analysis

We create a function that performs the entire text analysis process, including tokenization, word frequency analysis, and filtering of stopwords.

```R
top_words <- function(fulltext) {
  words <- tokenize_words(fulltext)
  words <- words[[1]]
  tab <- table(words)
  tab <- data_frame(word = names(tab), count = as.numeric(tab))
  tab <- arrange(tab, desc(count))
  wordfreq <- read_csv("https://raw.githubusercontent.com/BrockDSL/R_for_Text_Analysis/master/wordfrequency.csv")
  tab <- inner_join(tab, wordfreq)
  return(filter(tab, frequency < 0.01))
}

# Try out your new function by running on the text variable
top_words(text)
```

## Resources

- [Text Analysis with R](https://brockdsl.github.io/Text-Analysis-with-R/)
- [GitHub Repository for Text Analysis with R](https://github.com/BrockDSL/Text-Analysis-with-R)
- [Basic Text Processing in R](https://programminghistorian.org/en/lessons/basic-text-processing-in-r)

This project provides a practical introduction to basic text analysis techniques using R, suitable for beginners and those looking to explore NLP concepts.
