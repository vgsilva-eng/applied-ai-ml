

Define a problem using a dataset (publicly available or self-provided) and describe it in terms of its real-world organizational or business application. The complexity level of the problem should be at least comparable to one of your assignments. The problem should use at least two different types of AI and machine learning algorithms that we have studied in this course, such as Classification, Clustering, and Regression, in an investigation of the analytics solution to the problem. This investigation must include some aspects of experimental comparison. Depending on the problem, you may choose to experiment with different types of algorithms, e.g., different types of classifiers, and some experiments with tuning parameters of the algorithms. Alternatively, if your problem is suitable, you may use multiple algorithms (Clustering + Classification, etc.). Note that if there are a larger number of attributes in your selected dataset, you can try some type of feature selection to reduce the number of attributes. You may use summary statistics and visualization techniques to help you explain your findings in this project.

AI and Machine Learning Problems and Datasets:

For this teamwork project, you may choose your own AI research problem and dataset. It can be a problem or a challenge from your workplace or one found in an online data source, such as KaggleLinks to an external site. or the UCI Machine Learning RepositoryLinks to an external site.. A list of potential project ideas is provided below for your reference, but feel free to choose any AI challenges not in this list that excites you the most:

The application of AI techniques, such as machine learning and deep learning algorithms, to the healthcare and medical field has gained a lot of traction in the last few years. There are medical datasets, such as the Digital Database for Screening Mammography (DDSM), with a low signal-to-noise ratio that is available through open source projects, such as the Cancer Imaging Archive ProjectLinks to an external site.. Make informed decisions in determining which classification algorithms you learned from this class can be used to detect disease, and also offer some interpretation of your model's findings.
Can we predict human activity from smartphone sensor data? Classify the readings from multiple sensors in a smartphone to identify activities like walking, walking upstairs, walking downstairs, sitting, standing, and lying. UCI has produced a labeled datasetLinks to an external site. related to this task.
Understanding gender bias in book reviews using the techniques and data from this projectLinks to an external site., along with the codeLinks to an external site..
Image classification is another alternative project. Use a pre-trained network or train your own (or some combination of both!) to classify images into specific categories. Some interesting datasets to use for this problem include the following: 
The notMNIST dataset Links to an external site.expands on the classic MNIST dataset of handwritten digits: These are digits rendered in stylistic forms that you might see in logos as opposed to handwritten digits. The goal is to predict the digit from the image. 
The UCR Time SeriesLinks to an external site. archive contains several time series datasets extracted from scientific publications.
You may also consider a more straightforward classification problem as a project, such as those from competition sites such as KaggleLinks to an external site. or other open datasets. However, if you take this option, apply your creative spin on these projects rather than just "training a classifier." These projects are often unrealistically "clean" for a practical project. In particular, for structured datasets with 10 - 20 features, you will want to explain what the model learned, not just report accuracy. For example, explore variable importance to understand which features were most important in making good predictions. Then you may want to compare results with simpler models that use only these important features. If those simpler models work well, that is an interesting, actionable result—we can get adequate results by collecting just a few key features. Examples are: 
Predict the loan status [fully paid, late, etc.] of a Lending Club loan, given the borrower's information.
Predict whether a transaction is fraudulent, given anonymized credit card transactions.
Use NYSE data and fundamental metrics to predict things like one-day-ahead prediction, the quality of momentum strategies, or security clustering strategies.
Use data on a breast cancer tumor to predict whether it is benign or malignant.
Build a network to predict who will die in the next season of Game of Thrones.


Dataset Selected:

https://archive.ics.uci.edu/dataset/193/cardiotocography

pip install ucimlrepo
from ucimlrepo import fetch_ucirepo 
  
# fetch dataset 
cardiotocography = fetch_ucirepo(id=193) 
  
# data (as pandas dataframes) 
X = cardiotocography.data.features 
y = cardiotocography.data.targets 
  
# metadata 
print(cardiotocography.metadata) 
  
# variable information 
print(cardiotocography.variables) 
