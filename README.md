1. Topic and Research Problem:
The topic of my research problem is House Rent Prediction based on Different Attributes of the House.
Renting out real estate is a very challenging task in such a highly competitive and ever changing market. For landlords and property
owners, setting a rent which brings them maximum proitability and which also accustoms the current market pricing is
important as it is not good to lose revenue due to underpricing. While on the other hand, Tenants looking for a home also want to
have the most value out of their money and want a rental price which aligns with their budget constraints.Additionally, trustworthy
data-driven techniques are needed by inancial institutions and real estate agencies to evaluate property values for investments and
market research.

Research Question: 
How can house rent be effectively projected utilizing all the speciied attributes present in a House all the
relevant selecting criteria to aid stakeholders in making educated decisions

Stakeholders and Beneits:
1. Landlords/Property Owners: Proprietors looking to increase rental income by offering competitive prices.Accurate rent
estimates allow them to set competitive rental pricing, maximizing revenue while appealing to tenants.
2. Tenants: Individual looking for property that offer better value for money.Rent projections assist tenants choose properties that
meet their budget and interests, delivering better value for their money.
3. Real Estate Agencies/Financial Institutions:They require precise property assessment in order to conduct market research and
effectively model aid in determining property values for market research and investment objectives, hence improving
decision-making in a volatile market.
2. Data Description
The dataset is a useful resource for analyzing the real estate market and understanding the factors that inluence property pricing
and tenant satisfaction. The dataset has 3477 rows (attribute) and 110 columns (instances) which include 13 columns of loat, 1
column of int and 96 columns of object data types. A data dictionary is provided in the appendix section.
3. Data Ingestion and Cleaning
The dataset which is provided is The dataset having 3477 rows and 110 columns which include 13 columns of loat64, 1 column
of int64 and 96 columns of object data types.
a. Data Ingestion
The data is loaded using the pandas dataframe using the pandas library which contains the read_csv() function. To just get a quick
glance over the dataset, I used the pandas head() method which will display the irst ive rows of the data. To understand the
datatype and the size of the data used in the dataset we can used the pandas attribute which returns object which are df.shape will
return object with the total rows and columns in the dataset and df.dtypes which will return the is an attribute in pandas which
will return object with the total rows and columns in the dataset or either use the info() method.
b. Data Quality Assurance and Cleaning
Duplicated Values: If the dataset contains duplicate values, it will provide a large number of biased results and skew the
statistical analysis, resulting in erroneous results. I am using the duplicated() function to check for duplicate values in the data,
and it appears that there are no duplicate values in the dataset.
Missing Values: To deal with the missing values in my dataset I have done the following steps

First I am listing all the columns having missing values in an array and then calculating the percentage of missing values in my
dataset.I will drop all the columns which have a percentage of missing value more than 25% as keeping them will make the
dataset highly biased and if we impute them they may introduce too much noise. I did this by storing the columns to be dropped in
a different array and dropping all the columns at once using the drop() function in pandas. After dropping all the columns I am left
with 26 columns. Then I am analyzing the data frame column by column and dropping column which are not relevant to the dataset
with the justiication:
Reference number of the EPC report - does not provide useful information about the property and also contains a high proportion
of the 'Not speciied' which will not provide useful insights. I used the strip().str.lower() function to get the count of ‘Not
speciied’.
address - Address can alter the rent of the property but we have more relevant features in the dataset like number of Beds,Baths,
Toilets,,LivingArea, Space, Rent, Costs(Additional Cost) which will provide better predictive analysis about the rent of House.
Yearly theoretical total energy consumption - It only contains 'Not speciied' values whose count is 3476 which will not contribute
to the predictive analysis of the price(Total rent) so it is better to drop the column
space - it is a combination of Beds and LivingArea, as keeping a space column will only create overlapping of the information and
will make the model less stable in future.
Address, Agency, description - possess a large number of missing values and little ability to predict rent, which enables us to
concentrate on relevant features to increase the accuracy of rent prediction. Although they could sway a stakeholder's choice, their
direct inluence on the rental price is limited, and their potential to introduce bias from missing data makes them inadequate for
rent prediction.

Transforming Data: I have made numerous transformations to the dataset so that the information we can access is speciic to
the columns. In order to deal with missing values, type conversion is performed in the columns labeled 'LivingArea,' 'Rent,' and
'Costs,' using to_numeric() and replace() functions and I have also used pandas regular expression library to handle complex
patterns in several columns ('Rent,' and 'Costs’). The data type is inally set to integer for numerical data analysis in the data
visualization part. I have dropped the ‘price' and created the new ‘Price'(Total Rent) column as by analyzing I came to know that it
was just the addition of ‘Rent' and ‘Costs' column.In the columns ‘Furnished' and ‘Elevator', I have just replace the missing values
with ‘Unknown' class alongside 'Yes' and ‘No' to preserve the data and useful data gets lost due to dropping of rows and in ‘kitchen'
column just replace unwanted values with the nan so that in the later part we can just drop them.I have also used np.nan to replace
any value in speciic section. In columns 'Primary energy consumption' and ‘CO₂ emission' I have created a function
extracting_numeric_value () to just extract the numeric value so that we can use it during the analysis of numerical data. I have
changed the data type of column wherever required so that I can have a difference between the numerical and categorical data. As
for example ‘Floors' column cannot be a loat it has to be int so we did the conversion. We are substituting the ‘Not Speciied' as
‘Nan' values wherever we are changing the column type to numeric type.
Analyzing Numerical and Categorical data: We are segregating the dataset into numerical data where the data type is either
‘loat' or ‘int ' and categorical data type is ‘object'.
Imputation of Missing Values: To effectively deal with missing data, I used targeted imputation methods. Instead of using a
simple mean for numerical columns, I created numerical_imputation(), which computes the mean based on the optimal interest
rate scenario for the 'Rent (in €)' column. For categorical columns, I created impute_categorical_by_living_area(), which divides
'Living Area' into ive ranges and imputes missing values using the mode within each group. After imputation, I used pandas'
dropna() function to remove any remaining missing values. To ensure accurate analysis, columns 'Bathrooms', 'Bedrooms',
'Toilets', 'Primary Energy Consumption', and 'CO₂ emission' were converted to integers using astype(int). Finally, I reset the index
by calling reset_index(drop=True).
Dealing with the Outliers: Handling outliers is critical to avoiding skewed results. To ilter outliers in numerical columns, I
used the Interquartile Range (IQR) method, which limits data to 1.5 times the IQR from the irst and third quartiles. I accomplished
this using the remove_outliers_iqr() function. For categorical data, I dealt with outliers by converting lists in columns like 'Kitchen'and 'Heating Type' to strings and then categorizing rare values—those occurring in less than 5% of the dataset—as 'Others'. This
approach, made possible by pandas' astype(category) and value_counts() functions, simpliies the data and improves analysis.
Before visualizing the dataset, I summarized numerical columns with pandas' describe() function and calculated summary
statistics for categorical columns.

4. Exploratory Data Analysis
I used EDA to identify relationships in my dataset and analyze trends. I used the EDA to highlight the summary of my dataset. EDA
techniques and the rationale behind them in my dataframe is as follows:
Scatter Plots: I created a scatter plot to show the relationships between numerical variables and Total Rent (in €), which helps to
identify potential correlations and outliers. It helps me to identify the distribution of numerical columns against Total Rent (in €).
Box Plots: I created box plots to compare the distribution of Total Rent (in €) across various categorical variables. They show the
central tendency, spread, and potential outliers for each unique value in the categorical column. It helps us how each unique
variable is inluencing the value of the Total Rent (in €).
Correlation Heatmap: This heatmap effectively summarizes the relationships between numerical variables and Total Rent (in €).
It provides a quick overview of the relationships, strength and direction which can help identify potential key predictors.
Supporting igures:
![image](https://github.com/user-attachments/assets/f1f9e705-d648-4e01-bcb1-13739d59ac37)

Exploratory Data Analysis: Discussion of results
The purpose of exploratory data analysis (EDA) is to investigate the correlations between Total Rent and important characteristic such as Living Area, Bedrooms, and House Type, which are pertinent to House Rent Prediction.
1. The 3D scatter plot (on the left side of the igure) depicts the relationship between Total Rent (in €) (y-axis), Living Area (in m²)
(x-axis), and Bedrooms (z-axis). The color gradient (from purple to yellow) depicts the total rent in euros.
We observe that there is a positive correlation. As Living Area (m²) increases, so does the Total Rent (in €). For a ixed Living Area
(in m²), a higher number of Bedrooms results in a higher Total Rent (in €), though the impact is less pronounced than for Living
Area. The insights suggest that Living Area (in m²) and Bedrooms are signiicant predictors of Total Rent (in €). The inclusion of
these features in the model is likely to improve Total Rent (in €) prediction accuracy.
2.The boxplot (right side of the igure) compares the distribution of Total Rent (in €) among various House Types. Differences in
total rent between different types of houses. Certain house types, such as Exceptional Property, Penthouse, and Villa, have higher
medians and wider interquartile ranges, indicating greater variability and overall higherTotal Rent (in €). Apartments, studios, and
student housing have lower median and more concentrated rent distributions, relecting their affordability.
Exploratory Data Analysis: Discussion of results
The purpose of exploratory data analysis (EDA) is to investigate the correlations between Total Rent and important characteristics
such as Living Area, Bedrooms, and House Type, which are pertinent to House Rent Prediction.
1. The 3D scatter plot (on the left side of the igure) depicts the relationship between Total Rent (in €) (y-axis), Living Area (in m²)
(x-axis), and Bedrooms (z-axis). The color gradient (from purple to yellow) depicts the total rent in euros.
We observe that there is a positive correlation. As Living Area (m²) increases, so does the Total Rent (in €). For a ixed Living Area
(in m²), a higher number of Bedrooms results in a higher Total Rent (in €), though the impact is less pronounced than for Living
Area. The insights suggest that Living Area (in m²) and Bedrooms are signiicant predictors of Total Rent (in €). The inclusion of
these features in the model is likely to improve Total Rent (in €) prediction accuracy.
2.The boxplot (right side of the igure) compares the distribution of Total Rent (in €) among various House Types. Differences in
total rent between different types of houses. Certain house types, such as Exceptional Property, Penthouse, and Villa, have higher
medians and wider interquartile ranges, indicating greater variability and overall higherTotal Rent (in €). Apartments, studios, and
student housing have lower median and more concentrated rent distributions, relecting their affordability.
