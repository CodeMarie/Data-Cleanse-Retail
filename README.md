# Dash Data Cleanse - Retail Project 
## _Repository Part One of Two_

## Installation requirements

Installations required if not already installed and at current level of Pip: 
At the time of developing pip was used rather than pip3 for the upgrade and further information about Pip use this link [here](https://pip.pypa.io/en/stable/installation/)
 
The requirements for this data cleaning module include jupyter notebooks which uses the extension ipynb and Pandas.
If not already globally installed the terminal use the command

```sh
pip install notebook
pip install pandas
```

- Setting up the environment 

To work with Python in Jupyter Notebooks, you must activate a Python or Anaconda environment in VS Code which you've installed the Jupyter package. Using the shortcut Command Palette (Ctrl+Shift+P) and from dropdown Select Interpreter. For this project select the Python environment from Select Interpreter was used.

Create a file with the extension ipynb, this file is called cleanse.ipynb, you can select a kernel from the top right of the workbook. 
This will produce cells which can be ran all at the same time or can run independently for speed in data assessments.

Using standard convention
In the cell of this cleanse.ipynb file 

```sh
import numpy as np
import os 
import pandas as pd
```

If uploading to Github or similar, a .gitignore file must be made to hold the raw data which is in the region of 7Gb of data. 

## Data Files 
There are a mix of csv and json files for the retail branch information which has the year, month, day, hour, product, quantity, and amount for purchased in GBP. 
In the upload to Github these were placed within a folder called raw-data and Non-branch data which were added to the gitignore file. 
There is a terminologies.txt which indicates which naming conventions have been employed throughout the branch data. As there are variations in some datasets, the header was set to use product and quantity to be iterated during the merge of the files. 

NB As some of the shops were not opened until after 2010, although 10 years of data is hoped to be displayed, there are exceptions where the data will back from the opening e.g. from 2011, 2012 or 2013.

## Project Brief 

- 1. Track the most purchased and least purchased products & product categories
overall, per region and per county (limit to top 5 and least 5)
- 2. Track the best performing branches overall per region and per county (performance is
measured in both item quantity sold and monetary value of sales made, limit to best
10 and worst 10)
- 3. Per hour sales for the top 10 branches identified
- 4. Identify the top 10 and bottom 10 profitable branches and indicate how profitable they
are. (Calculate profitability by subtracting expense from total sales)

A link to user stories can be found [here](https://docs.google.com/document/d/1EYUmi04A2ciJxW3AZM5q8ZRx0Iqf0PqBJJLc8ZMccrI/edit?usp=sharing)


## Development Diary 

- A cleanse-data.ipybn was used for the cleansing of the data. 

- Column naming inconsistencies 
The terminologies.txt which was provided by the customer for the project demonstrates there are renaming differences, e.g. product, sku, and item within the branch.csv and branch.json files. As the products_list.csv uses the term products this will be used in renaming and the same for quantity.
 
A new_header variable was saved the preferred header columns. 
As it is not possible to go through the files individually, which hints to the need for iteration using the filename of branches.
Research into creation of a table using the filename resulted in the use of os and listdir() to be able to specify the path for the files to be found and iterated through. 

NB to use ensure you have import os and that you only have the relevant csv files within the directory you have specified in the path finder. If any csvs are created as part of the code these will need to be placed in a subfolder if the code is to be re-run to avoid interpretation errors when viewing the file directory. 

There are different steps to add the files for CSV as to json in terms of the syntax for how the new_header is added e.g. new_header, axis=1 for json and for csv initially setting the header as none and using name to add the header i.e header=0, names=new_header

The product list is in a separate xlsx, as the branch information has a different naming convention for products, e.g. SKU a renaming of headers for consistency is needed at the time of merge. 

Fulfilling Brief requirement - no.1 

When the tail of the product category information was displayed it indicated there was an inconsistency in the category of fruits & vegetables. This was also created as a category in the non-plural 'fruits & vegetable' therefore this was replaced to the plural form.

Fulfilling Brief requirement - no.2 
Performance in the brief was unclear as referring to the terminology.txt the calculation of the performance indicator is already present in 'amount_in_gbp'  which 'contains the sum obtained from the transaction'. As sales in terms of amount_of_gbp was not taken by the brief description the performance was defined from the brief description as quantity by amount_of_gbp.

Fulfilling Brief requirement - no.3 
The top performing branches and worst will be established from the created csvs from the Brief no.2. A csv with a groupby of branchname and the time parameters which is summed to the amount of gbp was also created at the end of the cleanse.ipynb file. 

- Fulfilling Brief requirement - no.4 
To fulfil brief point 4 a total expenses from the four expenses is require. Also the profitability is needed using the amount_in_gbp subtracting from the total expenses After this a groupby of all branches can be used to sum up for the rows. This then allows the top 10 and bottom 10 profitable branches (using ascending = False) to indicate how profitable the branches are. 
are. 

- Problems encountered

As the files provided were very large, the computer processing power meant running the code caused a lot of time delays.

There were mixed string characters as values under the quantity and amount_in_gbp files. These were initially tried to be replaced however, as more than 5 occurrances were detected a regex and to_numeric() was used instead. 
# all_csv_files['amount_in_gbp'].replace('23a39.2000000000003', 0, inplace=True)
# all_csv_files['quantity'].replace('6qw2', 0, inplace=True)

The Bassetlaw_outlet.csv was requested to be added to the dataset which only contained files for 2013. This is the file which had a lot of unexpected values.

## Part Two 

The link to the Repository for the Second Part i.e. the Dash Application can be found [here](https://github.com/CodeMarie/final-project-part-2-dash-app/tree/deploy-main)

## References 

- Jupyter Notebooks in Visual Code https://code.visualstudio.com/docs/datascience/jupyter-notebooks
