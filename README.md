## EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION
### Aaron Siegfreid R. Jugo
### 2ECE-A
### September 19, 2026

### Objectives:
At the end of this laboratory activity, the student should be able to:
1. Filter tabular data using several categorical and numerical conditions;
2. Construct focused DataFrames by selecting relevant features;
3. Summarize the relationship between categorical features and a numerical variable; and
4. Communicate a data comparison using clear and correctly labeled plots.

The student must use the same ECE Board Exam 2 dataset supplied for Experiment 4. Work in a Jupyter Notebook using Pandas and a Python plotting library used in class. Use the dataset's existing column labels, including Name, Gender, Track, Hometown, Math, GEAS, Electronics, and Average.
- Derive all tables and plot values from the dataset. Do not manually type rows, category means, or plotted values.
- When applying more than one condition, make every condition explicit in the filtering expression.
- Keep the original DataFrame unchanged.
- Every graph must have a title, axis labels, readable category labels, and a consistent scale appropriate to the data.
- Display every requested result in an executed notebook cell.
----------------------------------------------------------------------------------------------------
### A. VISAYAS COMMUNICATION DATAFRAME
Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order: Name, Gender, Math, Electronics, Average.
Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

Code:

```
import pandas as pd
import matplotlib.pyplot as plt
```
```
df = pd.read_excel('board2.xlsx')
df ['Average'] = (df.Math + df.Electronics + df.GEAS + df.Communication)/4

display (df)
```


```
VisComm = df[(df['Hometown'] == 'Visayas') &
             (df['Track'] == 'Communication')
             ][['Name', 'Gender', 'Math', 'Electronics', 'Average']]

display (VisComm)

print ("Number of Rows:", len(VisComm))
```

Output: 

The output aligned with the required result:
- Displayed Data Frame

<img width="670" height="437" alt="image" src="https://github.com/user-attachments/assets/2bd7bf16-73d4-45c9-a13b-7324585dccc8" />

- Displayed Visayas Communication Data Frame and the number of rows

<img width="362" height="185" alt="image" src="https://github.com/user-attachments/assets/d6328eb2-4c3b-4728-94d8-ce6c5b9e5408" />


`​`​`
Number of Rows: 5
`​`​`

-----------------------------------------------
### B. VISAYAS FEMALE DATAFRAME

Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only: Name, Track, GEAS, Electronics, Average. Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter.

Code:

```

VisFemale = df[(df['Hometown']=='Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
display (VisFemale)

print ("\nFemale Students in Visayas that averages at least 60 in GEAS and Electronics")
display (VisFemale[VisFemale['Average']>=60])
```


Output: 

The output aligned with the required result:

- Displayed female data frame, and the average of at least 60


<img width="378" height="212" alt="image" src="https://github.com/user-attachments/assets/6aaf83b1-ef3d-4104-be00-059418dfd023" />


    
`​`​`
Female Students in Visayas that averages at least 60 in GEAS and Electronics
`​`​`



<img width="407" height="162" alt="image" src="https://github.com/user-attachments/assets/458551d0-9e6f-4679-88b3-f79a0eca6c61" />

--------------------------------------------------------------

### C. CATEGORY-AVERAGE VISUALIZATION

Examine how the recorded Average differs across the three categorical features: Track, Gender, and Hometown. 

a. For each feature, compute the mean of the average for every category using Pandas. 

b. Display the three summary tables. 

c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown. d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

Code:

```
#A 
m_track = df.groupby('Track')['Average'].mean().reset_index()
m_gender = df.groupby('Gender')['Average'].mean().reset_index()
m_hometown = df.groupby('Hometown')['Average'].mean().reset_index()

#B
print("\nMean Average by Track")
display(m_track)

print("\nMean Average by Gender")
display(m_gender)

print("\nMean Average by Hometown")
display(m_hometown)
```


```
#C
fig, axes = plt.subplots(1, 3, figsize=(18, 5), sharey=True)
fig.suptitle('Mean of Board Exam Average by Category', fontsize=16, fontweight='bold')

axes[0].bar(m_track['Track'], m_track['Average'], color='#2b5c8f')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average Score')
axes[0].set_ylim(0, 100)

axes[1].bar(m_gender['Gender'], m_gender['Average'], color='#2e7d32')
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average Score')

axes[2].bar(m_hometown['Hometown'], m_hometown['Average'], color='#e65100')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average Score')

plt.tight_layout()
plt.show()
```


```
#D
highest_track = m_track.loc[m_track['Average'].idxmax(), 'Track']
highest_gender = m_gender.loc[m_gender['Average'].idxmax(), 'Gender']
highest_hometown = m_hometown.loc[m_hometown['Average'].idxmax(), 'Hometown']

print("\n  Statement:")
print(f"1. Among the tracks, the {highest_track} track obtained the highest sample mean for Average.")
print(f"2. Between genders, {highest_gender} students achieved the highest sample mean for Average.")
print(f"3. Across the hometown regions, students from {highest_hometown} recorded the highest sample mean for Average.")
```


Output: The output aligned with the required result:

- Displayed the three category mean tables:

<img width="197" height="455" alt="image" src="https://github.com/user-attachments/assets/651a1289-1ac5-4cff-98ed-4c3e8f8691e7" />


- Displayed bar charts comparing mean board exam averages across Track, Gender, and Hometown:
  
<img width="1102" height="290" alt="image" src="https://github.com/user-attachments/assets/243d3e84-98c4-4617-a996-31a1c1f8eb23" />


- Printed interpretation statements:

```
Statement:
1. Among the tracks, the Communication track obtained the highest sample mean for Average.
2. Between genders, Male students achieved the highest sample mean for Average.
3. Across the hometown regions, students from Luzon recorded the highest sample mean for Average.
```
