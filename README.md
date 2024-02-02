# ISE 291 Project
## Main Objectives
The main objective is to learn about how different factors affect video game reception (i.e. whether the video games has been well accepted or not)
## Dataset
The dataset can be found at: https://www.kaggle.com/datasets/thedevastator/global-video-game-sales-ratings/data
Data Set Description:

"This dataset consists of records from Metacritic providing insight into global video game ratings and sales. Traditionally categorised by genre, publisher, platform and rating, this data also includes additional descriptive attributes such as 'story focus', 'gameplay focus', and whether it is a 'series game'. These unique descriptors give valuable perspective on the video game industry, presenting an invaluable resource to evaluate the effect of focusing on storytelling upon video game sales and ratings.

The wide-reaching implications of this data are immense - from understanding complex customer ‘gamer’ engagement processes across different markets & genres to exploring how narrative elements have become increasingly commonplace in popular titles. In addition to traditional research topics ranging from rating vs success relationships or the importance of series games in retention - all these aspects combined present endless possibilities for deeper studies into an ever-evolving field!

Ultimately, this dataset gives researchers the power to profoundly analyse trends within the gaming market with informative and expansive details regarding popularity - helping developers craft engaging experiences for all customers worldwide. Henceforth we invite you on a journey into uncovering surprising revelations that may form part of wider conversations & culture surrounding gaming!"

Data Fields Description:

| Field           | Description                                             |
|-----------------|---------------------------------------------------------|
| Name            | The name of the video game. (String)                    |
| Platform        | The platform the game was released on. (String)         |
| Year_of_Release | The year the game was released. (Integer)               |
| Genre           | The genre of the game. (String)                         |
| Publisher       | The publisher of the game. (String)                     |
| NA_Sales        | The sales of the game in North America. (Float)         |
| EU_Sales        | The sales of the game in Europe. (Float)                |
| JP_Sales        | The sales of the game in Japan. (Float)                 |
| Other_Sales     | The sales of the game in other regions. (Float)         |
| Global_Sales    | The total sales of the game across all regions. (Float) |
| Critic_Scores   | The score given to the game by critics. (Float)         |
| Critic_Count    | The number of critics who reviewed the game. (Integer)  |
| User_Score      | The score given to the game by users. (Float)           |
| User_Count      | The number of users who reviewed the game. (Integer)    |
| Developer       | The developer of the game. (String)                     |
| Rating          | The rating of the game. (String)                        |

## Operationalize
1. Discovery
    1. First, download the available csv files and import the data set. This is a form of indirect data collection
2. Data Preparation
    1. Clean the data by resolving incosistencies
    2. Impute missing data
3. Model Planning
    1. Perform an exploratory analysis
        1. Check for any patterns in univariate graphs (histograms and count plots)
        2. Check for any patterns between 2 fields (bivariate graphs such as scatter plots)
        3. Check for any patterns between several fields (multivariate graphs such as heatmaps)
        4. Make sure to check for correlations
    2. Identify your independent variables and your target (dependent) output variable
    3. Transform your data accordingly:
        1. Platform --> One Hot Encoding (Nominal Data / Is not ordered)
        2. Year_of_Release --> MinMaxScaler (Year is not normally distributed and has short known range for the numbers)
        3. Genre --> One Hot Encoding (Nominal Data)
        4. Publisher --> Frequency Encoding (Nominal Data)
        5. NA_Sales & EU_SALES & JP_Sales & Other_Sales --> We map it to the proportion of Global_Sales. e.g., for NA_Sales, we use NA_Sales / Global_Sales
        6. Global_Sales --> StandardScaler
        7. Critic_Score --> MinMaxScaler (range is known (0 - 100 at max))
        8. Critic_Count --> StandardScaler
        9. User_Score --> MinMaxScaler (range is known (0 - 10 at max))
        10. User_Count --> StandardScaler
        11. Developer --> Frequency Encoding
        12. Rating --> Label Encoding (Ordinal Data / Data is ordered
4. Model Building
    1. Split your data into training and testing data, in this project a test size of 0.3 was used
    2. Choose several appropiate methods, for this project, linear regression, XGBoost regression, and a neural network were used
    3. Compare the test MSE values of the different models and choose the appropiate model

Some issues in this methodology include:
- The naturally high count of outliers
- Lack of understanding why each field affects the result accordingly
- Lack of more diverse data
- The success of a game depends on outside factors as well
- Game success is highly unpredictable
- Dataset had too many null values

## Conclusion
To conclude, we managed to create a model (XGBoost Regression) that accurately predicts the User_Score using given data. As such, we achieved our intended goal. We also noticed several trends and patterns between different fields. For instance, Sales between US and EU seemed to be correlated as opposted to with Japan. Moreover, the correlation between user scores and critic scores is significantly weaker than expected. It can also be observed that games with E rating sold very well. In addition, games with T rating tended to have better scores as opposed to games with an E10+ rating.
