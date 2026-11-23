# College projects

I put these notebooks together so I could revisit what I built in college and see which conclusions still hold up. The original files keep their old code and outputs. Each folder has a short report and a separate notebook for the checks I could run again.

| Project | What I found when I went back through it |
|---|---|
| [Soil moisture](projects/soil_moisture_prediction/) | Three regressors, all with test R² below 0.01. I had scaled the features before the split and filtered outliers using the target. The revised notebook fits preprocessing on the training set and includes a mean baseline. |
| [Tweet sentiment](projects/tweet_sentiment_analysis/) | I implemented logistic regression from scratch using word frequencies. The notebook prints 99.5% accuracy on its NLTK test split. That score says little about newer tweets or other datasets. |
| [GRU text generation](projects/gru_text_generation/) | The notebook prints perplexity of 7.23 after loading a checkpoint. The training demo shown separately runs for one step, so I can't attribute that score to it. |
| [Premier League analysis](projects/epl_analysis/) | I recovered both original notebook variants and the CSVs. The reviewed notebook counts wins across 4,560 matches and 12 seasons. Total wins favor teams that played more seasons. |

To run the reviewed notebooks, install `jupyterlab numpy pandas scikit-learn nltk` in a Python environment. Set the working directory to the relevant project folder so its `data/` paths resolve. Sentiment needs NLTK's `twitter_samples` and `stopwords` corpora. The original soil CSV and the GRU training files and checkpoint are still missing; the reviewed notebooks explain what can be checked without them.

The source files came from my [original repository](https://github.com/mayurshimbre123/mayurshimbre). See the [evidence audit](docs/EVIDENCE_AND_RESUME_AUDIT.md) for the distinction between saved results and fresh checks. My newer [AI engineering projects](https://github.com/mayurshimbre123/AI_Rag_Projects_Handson) are in a separate repo.
