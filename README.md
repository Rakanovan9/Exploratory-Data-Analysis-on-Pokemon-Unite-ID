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
8. Making a Box Plot
9. Correlation

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

