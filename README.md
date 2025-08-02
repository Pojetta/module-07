# Final Project: Article Summarizer

Complete the tasks in the Python Notebook in this repository.
Make sure to add and push the pkl or text file of your scraped html (this is specified in the notebook)

## Rubric

* (Question 1) Article html stored in separate file that is committed and pushed: 1 pt
* (Question 2) Polarity score printed with an appropriate label: 1 pt
* (Question 2) Number of sentences printed: 1 pt
* (Question 3) Correct (or equivalent in the case of multiple tokens with same frequency) tokens printed: 1 pt
* (Question 4) Correct (or equivalent in the case of multiple lemmas with same frequency) lemmas printed: 1 pt
* (Question 5) Histogram shown with appropriate labelling: 1 pt
* (Question 6) Histogram shown with appropriate labelling: 1 pt
* (Question 7) Cutoff score seems appropriate given histograms: 2 pts (1/score)
* (Question 8) Summary contains a shortened version of the article (less than half the number of sentences): 1 pt
* (Question 8) Summary sentences are in the same order as they appeared in the original article: 1 pt
* (Question 9) Polarity score printed with an appropriate label: 1 pt
* (Question 9) Number of sentences printed: 1 pt
* (Question 10) Summary contains a shortened version of the article (less than half the number of sentences): 1 pt
* (Question 10) Summary sentences are in the same order as they appeared in the original article: 1 pt
* (Question 11) Polarity score printed with an appropriate label: 1 pt
* (Question 11) Number of sentences printed: 1 pt
* (Question 12) Thoughtful answer based on reported polarity scores: 1 pt
* (Question 13) Thoughtful answer based on summaries: 1 pt

## Getting Started

### 1. Create and activate a virtual environment (in terminal)

python3 -m venv .venv  
source .venv/bin/activate

### 2. Upgrade pip, setuptools, and wheel  

pip install pip setuptools wheel

### 3. Install required libraries 

pip install requests  
pip install html5lib  
pip install beautifulsoup4  
pip install matplotlib  
pip install spacy  
pip install spacytextblob

### 4. Download spaCy English language model 

python -m spacy download en_core_web_sm

### 5. Setup and Custom Extensions (in notebook)

import json  
import pathlib  
import pickle  
from collections import Counter  
  
import requests  
from bs4 import BeautifulSoup  
import matplotlib.pyplot as plt  
import spacy  
from spacy.tokens import Doc  
from spacytextblob.spacytextblob import SpacyTextBlob  
  
### 6. Load spaCy model and add spaCyTextBlob to the pipeline  
nlp = spacy.load("en_core_web_sm")  
nlp.add_pipe("spacytextblob")  
  
### 7. Manually register custom extensions for sentiment  
if not Doc.has_extension("polarity"):  
    Doc.set_extension("polarity", getter=lambda doc: doc._.blob.sentiment.polarity)  
  
if not Doc.has_extension("subjectivity"):  
    Doc.set_extension("subjectivity", getter=lambda doc: doc._.blob.sentiment.subjectivity)  
  
if not Doc.has_extension("assessments"):  
    Doc.set_extension("assessments", getter=lambda doc: doc._.blob.sentiment_assessments.assessments)
