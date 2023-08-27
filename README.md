# Football-player-evaluation-and-recomendation-using-AI
Scraped data from websites are used for player evaluation and recommendation - visualized using XAI

ScrapePlayerData:
Dynamically formed the url to scrape statistics of player from football statistics website.
Scraped statistics are stored as excels.

ScrapeDataMerge:
HTML table data was pre-processed and and tranformed into dataframes.
Scraped excels are merged together using concat function to form a single dataframe for further processing

Dataset:
processed dataset included 171 columns.
Data was highly positively skewed.
correlation between variables was at a higher degree.

Pre-processing:
data cleaning - Data cleaning involves only including meaningful data for further processing.
Missing values were imputed or removed.

Rating Generation:
Feature selection - Columns with correlation coefficients of the independent variables in relation to 'goal' variable exceeding 0.4 were considered relevant for the attacker-focused analysis, with this threshold set based on the distribution of the goal column's correlation values, where the 50th percentile was 0.23 and the maximum post-normalization value was 0.97.
Z-score normalization emerged as the preferred choice as it maintained the relativity of outliers within the data.
Weight for the columns filtered was generated using a correlation coefficient such that the combined weight of all the features doesn't exceed 100.
Weight and normalized z score value were multiplied to generate a rating for each player.
Results - Players were rated with rating lead by Messi and Ronaldo.

Similar player identification:
The above implementation is utilized to generate weight and feature selection as the goal is to identify similar players based on their attacking prowess
Owing to the nature of the dataset (positive skew, highly correlated variables) KNN was utilized to find similar players.
KNN - distance metric "Minkowski" , p="2"
Results - For Lewandowski suggested players were Cristiano Ronaldo, Andre silva, Harry kane.

Position identification
With all the relevant features selected excluding GK columns, KNN for clustering was implemented to classify players by their position.
The algorithm was executed with an accuracy of 84% when K =7.
The optimal K value was identified by plotting the resulting clusters in 2d space using PCA and ensuring their boundaries are well confined and defined covering all the points.

XAI - LIME
The scaled train dataset containing the independent feature values is passed to the LIME tabular explainer. 
A Lime instance is initialized for the tabular explainer that generates the explanations for individual player statistics. 
The individual data point will be passed as an argument to the explainer.
The predict_proba function of the LIME explainer is used along with KNN to predict the probability of the data point being allocated to a specific class.
LIME results pointed out the probability of a specific record being classified across target variables.
It also listed out the importance of all the features and their corresponding values.
This visualization helps the stakeholders to understand more about their model and improve the performance of the model. 





