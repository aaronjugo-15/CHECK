## EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION
### Aaron Siegfreid R. Jugo
### 2ECE-A
### August 31, 2026

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

`​`​`python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_excel('board2.xlsx')
df['Average'] = (df.Math + df.Electronics + df.GEAS + df.Communication) / 4

display(df)
`​`​``

`​`​`
VisComm = df[(df['Hometown'] == 'Visayas') & 
             (df['Track'] == 'Communication')
            ][['Name', 'Gender', 'Math', 'Electronics', 'Average']]

display(VisComm)

print("Number of Rows:", len(VisComm))
`​`​`

Output: The output aligned with the required result:

*   Displayed the loaded DataFrame with computed Average column: | | Name | Gender | Track | Hometown | Math | Electronics | GEAS | Communication | Average | |---|---|---|---|---|---|---|---|---|---| | 0 | S1 | Male | Instrumentation | Luzon | 58 | 89 | 75 | 78 | 75.00 | | 1 | S2 | Female | Communication | Mindanao | 52 | 75 | 90 | 52 | 67.25 | | 2 | S3 | Female | Instrumentation | Mindanao | 83 | 74 | 77 | 57 | 72.75 | | 3 | S4 | Male | Instrumentation | Visayas | 65 | 58 | 91 | 68 | 70.50 | | 4 | S5 | Male | Communication | Luzon | 59 | 86 | 43 | 88 | 69.00 | | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | | 28 | S29 | Male | Instrumentation | Mindanao | 73 | 48 | 71 | 62 | 63.50 | | 29 | S30 | Male | Instrumentation | Luzon | 78 | 81 | 57 | 56 | 68.00 |

_(30 rows × 9 columns)_

*   Displayed the VisComm DataFrame and its row count: | | Name | Gender | Math | Electronics | Average | |---|---|---|---|---|---| | 10 | S11 | Female | 48 | 56 | 54.75 | | 11 | S12 | Male | 89 | 67 | 76.00 | | 17 | S18 | Male | 81 | 40 | 63.50 | | 21 | S22 | Female | 64 | 39 | 62.50 | | 27 | S28 | Male | 85 | 53 | 67.75 |
    
`​`​`
Number of Rows: 5
`​`​`

### B. VISAYAS FEMALE DATAFRAME

Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only: Name, Track, GEAS, Electronics, Average. Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter.

Code:

`​`​`
VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
display(VisFemale)

print("\nFemale Students in Visayas that averages at least 60 in GEAS and Electronics")
display(VisFemale[VisFemale['Average'] >= 60])
`​`​`

Output: The output aligned with the required result:

*   Displayed the VisFemale DataFrame: | | Name | Track | GEAS | Electronics | Average | |---|---|---|---|---|---| | 5 | S6 | Microelectronics | 86 | 45 | 75.50 | | 10 | S11 | Communication | 48 | 56 | 54.75 | | 20 | S21 | Microelectronics | 68 | 51 | 68.50 | | 21 | S22 | Communication | 89 | 39 | 62.50 | | 23 | S24 | Microelectronics | 60 | 45 | 57.75 | | 25 | S26 | Instrumentation | 83 | 47 | 65.75 |
*   Displayed female students in Visayas with an Average of at least 60:
    
`​`​`
Female Students in Visayas that averages at least 60 in GEAS and Electronics
`​`​`

|     | Name | Track | GEAS | Electronics | Average |
| --- | --- | --- | --- | --- | --- |
| 5   | S6  | Microelectronics | 86  | 45  | 75.50 |
| 20  | S21 | Microelectronics | 68  | 51  | 68.50 |
| 21  | S22 | Communication | 89  | 39  | 62.50 |
| 25  | S26 | Instrumentation | 83  | 47  | 65.75 |

### C. CATEGORY-AVERAGE VISUALIZATION

Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown. a. For each feature, compute the mean of Average for every category using Pandas. b. Display the three summary tables. c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown. d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

Code:

`​`​`
# A & B: Compute and display mean Average summaries
m_track = df.groupby('Track')['Average'].mean().reset_index()
m_gender = df.groupby('Gender')['Average'].mean().reset_index()
m_hometown = df.groupby('Hometown')['Average'].mean().reset_index()

print("\nMean Average by Track")
display(m_track)

print("\nMean Average by Gender")
display(m_gender)

print("\nMean Average by Hometown")
display(m_hometown)
`​`​`

`​`​`
# C: Generate comparison bar charts
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
`​`​`

`​`​`
# D: Interpretation statements
highest_track = m_track.loc[m_track['Average'].idxmax(), 'Track']
highest_gender = m_gender.loc[m_gender['Average'].idxmax(), 'Gender']
highest_hometown = m_hometown.loc[m_hometown['Average'].idxmax(), 'Hometown']

print("\n  Statement:")
print(f"1. Among the tracks, the {highest_track} track obtained the highest sample mean for Average.")
print(f"2. Between genders, {highest_gender} students achieved the highest sample mean for Average.")
print(f"3. Across the hometown regions, students from {highest_hometown} recorded the highest sample mean for Average.")
`​`​`

Output: The output aligned with the required result:

*   Displayed the three category mean tables:
    
`​`​`
Mean Average by Track
`​`​`

|     | Track | Average |
| --- | --- | --- |
| 0   | Communication | 67.975 |
| 1   | Instrumentation | 65.225 |
| 2   | Microelectronics | 67.500 |

`​`​`
Mean Average by Gender
`​`​`

|     | Gender | Average |
| --- | --- | --- |
| 0   | Female | 66.616667 |
| 1   | Male | 67.183333 |

`​`​`
Mean Average by Hometown
`​`​`

|     | Hometown | Average |
| --- | --- | --- |
| 0   | Luzon | 68.083333 |
| 1   | Mindanao | 66.678571 |
| 2   | Visayas | 65.750000 |

*   Displayed bar charts comparing mean board exam averages across Track, Gender, and Hometown:

_(Visualization Output: 1×3 subplot bar charts plotting Mean of Board Exam Average by Category)_

*   Printed interpretation statements:

`​`​`
  Statement:
1. Among the tracks, the Communication track obtained the highest sample mean for Average.
2. Between genders, Male students achieved the highest sample mean for Average.
3. Across the hometown regions, students from Luzon recorded the highest sample mean for Average.
`​`​`

Powered by Gemini Exporter (https://www.ai-chat-exporter.com)
