# Data analysis - Pandas
# Pandas Tutorial

 # Reading Data with Pandas

## Introduction

Another library that is integral to data science is Pandas. Have you ever looked at a table of data, maybe excel, and thought, "I wish I had that in a format I could use in Python!"? We'll you're in luck because that is exactly the type of problem that this new library can solve for us. In this lesson, we will introduce the ways in which Pandas is used and why it is such a powerful tool. We'll also show exactly how to get started using Pandas and common operations. 

## Objectives
* Importing Pandas
* Creating a DataFrame
* Reading a CSV

## Importing Pandas

The first thing we do with all librarys is import them into our code. And we know that our code is usually following some kind of pattern or convention, right? Well, Pandas is no exception to that. Just as we alias the NumPy library import `as np`, we alias Pandas `as pd`. Let's check it out.


```python
import pandas as pd
print(pd)
```

    <module 'pandas' from '/usr/local/lib/python3.6/site-packages/pandas/__init__.py'>


Great! we have Pandas imported and aliased, so that, now we can refer to the Pandas module as simply `pd`.

# Creating a DataFrame

A DataFrame is a new data type for us. So, in order to understand what a DataFrame is, it is important to have a visualization of the object. Below, we are taking some lists (some multi-dimensional), and using it to create a Pandas DataFrame.

Essentially, a DataFrame is an organized, formatted object containing rows and columns with data contained in the cells between the rows and colums. You can think of it as almost the Python equivalent of looking at a matrix in a CSV or excel file.

First, let's see the DataFrame without any real values populated. We will create the DataFrame with just columns and Rows.

> The syntax for creating a DataFrame is:


```python
pd.DataFrame(DATA, COLUMNS, INDEX(optional))
# without an index, the left column will just auto index using integers (i.e. 1, 2, 3, etc.)

OR

pd.DataFrame(data=['Python', 'Pandas', 'Flatiron School'], 
             columns=['Coolest Programming Lang','Neatest Python Library','Best Programming School']
            )
```


```python
days_of_class = ['day1', 'day2', 'day3', 'day4']
attendance = ['absent', 'present']
empty_students = []
pd.DataFrame(data=empty_students, columns=attendance, index=days_of_class)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>absent</th>
      <th>present</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>day1</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>day2</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>day3</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>day4</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Now, if we add in a list of lists such as 4 lists containing 1 student who was absent, and 1 student who was present all inside another list (i.e. `[ [1,2], [1,2], [1,2], [1,2] ]`), we can provide the data we need for our DataFrame! 

Don't think too much about the multidimensional list. We will see those again in the future. But for now, focus on DataFrames! Below, we are creating the list of lists that will be used to show absent and present students for class.


```python
present_stds = ['Anna', 'Billy', 'Meghan', 'George']
absent_stds = ['Hunter', 'Francine', 'Gail', 'Tucker']
students = [[absent_stds[0], present_stds[0]], [absent_stds[1], present_stds[1]], [absent_stds[2], present_stds[2]], [absent_stds[3], present_stds[3]]]

pd.DataFrame(students, index=days_of_class, columns=attendance)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>absent</th>
      <th>present</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>day1</th>
      <td>Hunter</td>
      <td>Anna</td>
    </tr>
    <tr>
      <th>day2</th>
      <td>Francine</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>day3</th>
      <td>Gail</td>
      <td>Meghan</td>
    </tr>
    <tr>
      <th>day4</th>
      <td>Tucker</td>
      <td>George</td>
    </tr>
  </tbody>
</table>
</div>



Now, let's see what we were talking about when we said our DataFrame would **auto index**... Well, our DataFrame will always need an index (or line number) and without the days of the week as our indexes, our DataFrame will populate the index with a list of integers for the number of rows of data in the DataFrame. Let's look at the same example as we have from above, but this time without the index.


```python
pd.DataFrame(students, columns=attendance)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>absent</th>
      <th>present</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Hunter</td>
      <td>Anna</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Francine</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Gail</td>
      <td>Meghan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tucker</td>
      <td>George</td>
    </tr>
  </tbody>
</table>
</div>



Now, it looks like we have a *day **0***, but that's alright. The important thing here is to note that without data for your index, Pandas will simply use integers to denote rows. In fact, if we remove the data for the columns, Pandas will also use integers to create column titles. 


```python
pd.DataFrame(students)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Hunter</td>
      <td>Anna</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Francine</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Gail</td>
      <td>Meghan</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tucker</td>
      <td>George</td>
    </tr>
  </tbody>
</table>
</div>



## Reading a CSV File

Okay, so, we have a brief introduction into Pandas and DataFrames. Now, while we *can* create DataFrames like we did above, we will largely be using pandas to read large files with **C**omma **S**eparated **V**alues and create DataFrames using those values. 

This is immensly useful for us since we will largely be using data that already exists somewhere to create insights and analytics. Taking the already existing information and importing it into a format that we can use to save, manipulate, and query is exaclty what we will use Pandas for. Let's take a look1

In our directory already, we have a csv file named `attendance.csv`. To get the information we want out of this file, we will need to read it first. To do that, we will use a method Pandas provides called `read_csv`, which whill do just that. It reads the file, and knowing that it is a CSV, it will create a DataFrame formatted in the way we want (i.e. with headers on the first line and all subsequent new lines will be the data listed underneath the headers).


```python
csv = pd.read_csv('attendance.csv')
csv # this is our data frame that pandas has created with the information in our attendance csv file
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NAME</th>
      <th>Day 1</th>
      <th>Day 2</th>
      <th>Day 3</th>
      <th>Day 4</th>
      <th>Day 5</th>
      <th>Day 6</th>
      <th>Day 7</th>
      <th>Day 8</th>
      <th>Day 9</th>
      <th>Day 10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Jeffrey</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Michelle</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Carl</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chris</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kris</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>David</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Hank</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Gregory</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Anna</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Jordan</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Kayla</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Tucker</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Pattie</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Morgan</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Max</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Rick</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Stephanie</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



Now we might be wondering, "Great we can read a csv and make a DataFrame, but what can I do with this DataFrame?" 

Well, typically you will want to take this new information and turn it into some data type we can more easily work with, like a dictionary.

To do this, we can use the `to_dict()` method provided by Pandas, which uses the information in our DataFrame to create a dictionary.


```python
attendance_dict = csv.to_dict()
print(attendance_dict)
```

That is definitely a dictionary, but it looks a little confusing. We essentially have a the data from our DataFrame but the way it is formatted, each column is a key, which then points to another dictionary object with the values for that column, with each key being the row that data is on. 
To make this data a but more readable, and easy to work with, we will pass in the `'records'` argument to the `.to_dict()` method, which will then give us a list of dictionary objects, where the keys are the column names and point to the data for each row of data making it as if each row is its own discrete object.


```python
attendance_dict = csv.to_dict('records')
print(attendance_dict)
```

> **Note:** A 0 stands for 'absent' and a 1 stands for 'present' in the attendance data above.

Now that we have our data in a format that we know how to work with more easily, we can begin to use this information more easily in our programs

We can analyze the the attendance data to see things like *which day had the most absences?*, *is there a pattern to any spikes in absences or lack of absences?*, etc.

## Summary

In this lesson, we introduced pandas and DataFrames. We looked at common applications for using DataFrames as well as practiced using Pandas ino rder to extract data from a CSV file to use it in our program in Python. We will continue to grow our Pandas skills as we continue learning more about Data Science and working with data in Python.
