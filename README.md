# Python with MySQL 
This project contains Python code for preprocessing data imported from a SQL database using pandas. The code includes steps for importing a CSV file, running simple and complex SQL queries, filtering data, and answering practice questions.

## Getting Started

### Prerequisites
- Python 3.x
- pandas library
- SQLAlchemy library
- pymysql library
- MySQL database

### Installing
1. Clone the repository:
   https://github.com/sohanpatel6168/data1202_assignment5.git
   
2. Install required Python libraries:
   ```bash
 pip install pandas sqlalchemy pymysql
```
 

4. Set up MySQL:
 Install MySQL server.
 Create a database and import the vgsales table.
   

## Running the codes
### Breakdown of code
### Part 1: Importing a CSV File
- Reads a CSV file containing video game sales data.
- Filters the DataFrame to find games launched between 2000-2005.

```python
import pandas as pd
input_file_path = r"C:\Users\Durham\Desktop\Duraham\Courses\data1202\vgsales.csv"
input_raw_data = pd.read_csv(input_file_path)
between_00_05 = input_raw_data[(input_raw_data["Year"] >= 2000) & (input_raw_data["Year"] <= 2005)]
print(between_00_05)
```



### Part 2: Running Simple Queries
- Connects to a SQL database.
- Runs a simple query to read data into a DataFrame.
- Provides basic data exploration, including shape, size, column names, and data types.

```python
import pandas as pd
import pymysql
from sqlalchemy import create_engine
engine = create_engine('mysql+pymysql://username:password@host:port/database')
conn = engine.connect()
df = pd.read_sql_query("SELECT * FROM data1202.vgsales", conn)
print(df.head())
print(df.shape)
print(df.size)
print(df.columns)
print(df.dtypes)
print(df.info())
```



### Part 3: Running Complex Queries
- Runs a complex SQL query to calculate sales and market share for Action games released after 2005.

```python
complex_df = pd.read_sql_query('''SELECT
    Round(SUM(NA_Sales)) as 'NA_Sales',
    ROUND(SUM(EU_Sales)) as 'EU_Sales',
    ROUND(SUM(JP_Sales)) as 'JP_Sales',
    ROUND(SUM(Global_Sales)) AS 'Global_Sales',
    ROUND((SUM(NA_Sales)/SUM(Global_Sales)) * 100) as 'NA_GlobalShare'
FROM
    data1202.vgsales
WHERE
    Genre = 'Action'
        AND Year>= 2005''', conn)
print(complex_df.head())
```



### Part 4: WHERE in Python
- Filters the DataFrame for specific conditions, such as games published by Nintendo.
- Finds the maximum sales of Action games in the EU after 2005.

```python
nintendo_games = df[df['Publisher'] == 'Nintendo']
print(nintendo_games.head())
print("The number of Nintendo games is: " + str(len(nintendo_games)))

df = pd.read_csv(input_file_path)
action_05 = df[(df['Genre'] == 'Action') & (df['Year'] >= 2005)]
print(action_05.head())
print("The max sales of action games in EU after 2005 is: " + str(action_05.EU_Sales.max()))
between_00_05 = df[(df["Year"] >= 2000) & (df["Year"] <= 2005)]
print(between_00_05)
```



### Part 5: Practice Questions
- Practice tasks include showing all databases, retrieving sales data between 2000-2005, and identifying data types and column names for the filtered DataFrame.

  
## Deployment
This project does not have a deployment step as it is intended for local analysis and testing.

## Author
### Sohan Patel
- GitHub: sohanpatel6168

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgement
- Thanks to Durham College for the guidance and resources provided.
- The developers of pandas, pymysql, and sqlalchemy for their excellent libraries.
- Special thanks to the open-source community for the libraries and tools used in this project.
