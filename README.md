data_folder:'/mnt/c/Yose/Data/vnn_data/active_learning/'

The VNN forum dataset has been:
* cleand from url
* chunked into max token lengt 256 using tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")
* embeddings were calculated using model = SentenceTransformer('all-MiniLM-L6-v2')
* labeled with zeroshot classification (classifier = pipeline("zero-shot-classification", model="facebook/bart-large-mnli"))

---------------------------------------------------------------------------------------------------------------------------------------
annotate_data.ipynb
Text chunks with top scores from zeroshot classification were assesed manually till 100 positive and 100 negative labels were identified. \

Hypothesis for labeling is "this text is racist". 
*Racism is based on the idea that there are different human races. For the current example only hatered white people vs people of colour is considered (thus exluding for example antisemitism)*

---------------------------------------------------------------------------------------------------------------------------------------
supervised.ipynb
Manually annotated dataset of 100 positive and 100 negative labels with hypothesis "This text is racist" from VNN forum are used to train Logistic Regression and Random Forrest models.

---------------------------------------------------------------------------------------------------------------------------------------
active_learning.ipynb
Active learning is used to annotate data. Inital annotated data is 200 datapoints from annotate.ipynb plus any which have been unnotated in earlier runs. Annotated data is split into train data to fit initial learner and test data to evalate accurac score for each iteration. Analysis is done in 384 dimensions, while visualization in 3.
Basic ActiveLearner is initialized with estimators: LogisticRegression or RandomForrest and uncertaquery strategy as query strategy.
Most uncertain points are queried and new accuracy score calculated a predefined number of times.
Query results are saved together with plots and model.





---
Active Learning Literature Survey 2010\
https://burrsettles.com/pub/settles.activelearning.pdf
---
Active training good basic explanation with LogReg and simple code, no module used for active learning\
https://www.geeksforgeeks.org/ml-active-learning/
---
Good overview of Avtive Learning for NLP with refrences within to AL tools and example for text classification with SVM \
https://medium.com/@farnazgh73/ultimate-guide-for-active-learning-main-approaches-3cf53ce207f0
    - data manually removed from pool and added to train efter labeling
---
activeml module
https://pypi.org/project/scikit-activeml/ - bild on scikit learn
* easier way to handle non-labeled data
---
ModAL module for AL tutorial \
https://modal-python.readthedocs.io/en/latest/
    - build on sklearn

* example interactive labeling is requested:
    - https://modal-python.readthedocs.io/en/latest/content/examples/interactive_labeling.html
    - modified in active_learning_tutorial.ipynb  
* poolbased sampling:
    - https://modal-python.readthedocs.io/en/latest/content/examples/pool-based_sampling.html
   
* example of poolbased batched data for labeling:
    - https://modal-python.readthedocs.io/en/latest/content/examples/ranked_batch_mode.html
---
ActiveLab module from CleanLab for AL \
https://cleanlab.ai/blog/active-learning/
* best results
