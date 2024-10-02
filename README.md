# Exploratory Data Analysis on Pokemon Unite Dataset
My first attempt at EDA on Pokemon Unite Stats, which cover

0. Loading The Data
1. Basic Information
2. Duplicate or Unique Values
3. Unique Values Visualisation
4. Finding Null Values
5. Replacing Null Values (If Found)
6. Replacing Null Values (If Found)
7. Finding out data types from the dataset to ease the process
8. Filtering Data
9. Making a Box Plot
10. Correlation

## 0. Loading The Data
![image](https://github.com/user-attachments/assets/4fb880f7-b1cd-4be5-b11e-14bbf7cad966)
With Python, we can import libraries such as Pandas to load the Dataset, Seaborn, and matplotlib to visualize the data.

To load the dataset I use.
```py
df = pd.read_csv("FILE DIRECTORY")
```
To find the file directory we can place the CSV files in the same folder as the code or we can click the CSV file and click Copy Path.
![image](https://github.com/user-attachments/assets/2508b422-98ad-48d7-a0dd-0d41aabb4cea)

Your code should look like this.
```py
df = pd.read_csv("C:\Users\PC\Documents\PokemonUniteData.csv")
df
```

And the output should look like this.
![image](https://github.com/user-attachments/assets/9d45db83-5846-4c4f-97d9-db40e0dd537d)

## 1. Basic Information
After loading the datasets, we need to see the information about the dataset.
By using

```py
df.info()
```
We can see information about the dataset, such as data types, non-null count, and column names.
![image](https://github.com/user-attachments/assets/f0e65c39-5094-41a0-946a-da88ab8f221f)

## 2. Duplicate or Unique Values
After analyzing the information about the dataset, we will try to find if there are any duplicates or missing values.
```py
df_duplicate = df.duplicated().sum()


df_unique = df.nunique()


print("Amount of duplicates found in data :",df_duplicate,"\n")
print(df_unique)
```

With `.duplicated()` we can see if the data is duplicated or not through the boolean output. False is for non-duplicated data, and True is for duplicated data. After that, we use `.sum()` to add up all the False/True and see how many duplicated data are there.

moving into the `.nonique()` it counts up how many unique strings, int, float all different data types on the column.

If done properly the output should look like this.

![image](https://github.com/user-attachments/assets/4d5a7b47-0973-4226-90d4-ca977d56cf58)

From this, we can assume that there's no duplicated data and we can also see multiple unique data for each column 

## 3. Unique Values Visualisation
Now for the Visualisation part, we're gonna use mathplotlip as plt

```py
plt.figure(figsize=(10, 6))
df_unique.drop(["Name", "Description"]).plot(kind='bar', color='skyblue')
plt.title("Number of Unique Values in Each Column")
plt.ylabel("Count of Unique Values")
plt.xticks(rotation=45)
plt.show()
```

`figure()` Sets the canvas size for the visualization.

`drop(["Name", "Description"])` Removes unnecessary columns from the dataset.

`title()` Adds a title at the top center of the visualization.

`ylabel()` Labels the y-axis of the graph.

`xlabel()` Labels the x-axis of the graph.

`xticks(rotation=45)` Rotates the x-axis labels by 45 degrees to ensure they fit.

`show()` Displays the final visualization.
![image](https://github.com/user-attachments/assets/4f161895-ff18-4bc1-858a-f29b20445eee)

## 4. Finding Null Values
Finding missing or Null Values from the dataset is mandatory for EDA because we need clear and intact data without any missing values.

```py
df_null = df.isnull().sum()
print("Amount of Missing Vales found in data")
df_null
```

`isnull()` decides if the data is missing or empty.
`sum()` add up the entire array, row, or list.
![image](https://github.com/user-attachments/assets/3efc0c6b-eef1-4551-9402-00240f9f98cb)

As we can see here. There's no Missing Data we can assume that our data is fully intact and we can skip to Number 7

## 7. Finding out data types from the dataset to ease the process
Before we make the visualization we need to figure out what are the data type that's available on the dataset. We can figure that out by using this `dtypes`
```py
df.dtypes
```
![image](https://github.com/user-attachments/assets/7a99bd70-1e5c-4ea2-9db8-f29b6e7755e1)

## 8. Filtering Data
This part is required to filter out the unnecessary data that will clog up the visualization.

We will start filtering it by UsageDifficlty
```py
df_usagedifficulty_Novice= df[df['UsageDifficulty'] == "Insert Difficulty"]
print("Amount of Pokemon that has the Usage Difficulty of Insert Difficulty :",len(df_usagedifficulty_Novice))
df_usagedifficulty_Novice.head()
```
Since there are only 3 Usage Difficulty available it's Novice, Intermediate, and Expert. We can just replace the "Insert Difficulty" as the Difficulty stated earlier

![image](https://github.com/user-attachments/assets/fcf0b76b-2522-41e5-af9c-0344665f6368)

Here's an example output of the filtered dataset UsageDifficulty Novice.

Before we go for the visualization part. we need to add a column. It's total stats
```py
df['Total Stats'] = df[['Offense', 'Endurance', 'Mobility', 'Scoring', 'Support']].sum(axis=1)
df.head()
```

So we sum up Offense, Endurance, Mobility, Scoring, and Support and use `axis=1` to the new column on the right part of the dataset.

the new dataset should look like this
![image](https://github.com/user-attachments/assets/285126dd-4c01-4fd7-be00-2a4c4eda1d60)

Another example of filtering by Range or Melee column
```py
df_melee = df[df['Ranged_or_Melee'] == "Melee"]
df_ranged = df[df['Ranged_or_Melee'] == "Ranged"]
```

## 9. Making a Box Plot
Now into the visualization.

```py
plt.figure(figsize=(10, 6))
sns.boxplot(x='UsageDifficulty', y='Total Stats', data=df)
plt.title('Comparison of Total Stats by Usage Difficulty')
plt.xlabel('UsageDifficulty')
plt.ylabel('Total Stats')
plt.show()
```


`figure(figsize=(10, 6))`: Sets the canvas size to 10x6 for the visualization.
`sns.boxplot(x='UsageDifficulty', y='Total Stats', data=df)`: Creates a boxplot comparing 'Total Stats' across different 'UsageDifficulty' categories using the dataset `df`.
`title('Comparison of Total Stats by Usage Difficulty')`: Adds a title at the top center of the visualization.
`xlabel('UsageDifficulty')`: Labels the x-axis as 'UsageDifficulty'.
`ylabel('Total Stats')`: Labels the y-axis as 'Total Stats'.
`show()`: Displays the final product of the visualization.



