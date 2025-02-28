# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To determine the most in-demand skills for the top 3 data roles, I identified the top 3 roles by US job posting counts. Then, for each skill, I calculated the percentage of job postings that require that skill (done for each of the top 3 roles).

View my notebook with detailed steps here:
[2_Skills_Count.ipynb](3_Project\2_Skills_Count.ipynb)

### Code for Visualizing the Data

```python
sns.set_theme(style = 'ticks')
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data = df_plot, x = 'skill_percent', y = 'job_skills', ax = ax[i], hue = 'skill_percent', palette = 'dark:b_r')
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0, 80)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va = 'center')
    
    if i < len(job_titles) - 1:
        ax[i].set_xticks([])

ax[2].set_xlabel('Percent of Jobs Requiring the Skill')

fig.suptitle('Top 5 Highest Demand Skills by Job Title', fontsize = 15)
fig.tight_layout()
```

### Results

![Bar Chart of In-Demand Job Skills for Data Roles](3_Project\images\skill_demand.png)

### Insights

SQL is the most in-demand skills for data analysts and data engineers, while python is the most in-demand for data scientists. Data engineer positions also have high demand for python. There is far less demand for python for data analyst positions.

## 2. How are the most in-demand skills for data analyst jobs trending?

To determine trends in high-demand skills for data analyst jobs, I calculated the percentage of data analyst jobs requiring each skill by month. Then, for the top 5 most demanded skills, I plotted the percentages by month to show the trend across the last year.

View my notebook with detailed steps here:
[3_Skills_Trend.ipynb](3_Project\3_Skills_Trend.ipynb)

### Code for Visualizing the Data

```python
sns.set_theme(style = 'ticks')
sns.lineplot(data = df_plot, dashes = False, palette = 'tab10')
sns.despine()
plt.title('Trend of Data Analyst Skill Demand')
plt.xlabel('Month')
plt.ylabel('Percent of Jobs Requiring Skill')
plt.legend().remove()

for i in range(5):
    plt.text(12, df_plot.iloc[-2, i], df_plot.columns[i])

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals = 0))

plt.show()
```
### Results

![Line Chart of Skills Trend for Data Analyst Roles](3_Project\images\skill_trend.png)

### Insights

SQL is consistently the most demanded skill across this 12 month period, however, the demand appears to be declining. SQL was required for approximately 54% of data analyst jobs in January, and this declined to about 46% in December. Excel is the second most demanded skill, but its demand also appears to be declining slightly (approximately 42% in January to 38% in December). Tableau, Python, and SAS are less demanded skills in general, but the demand for these skills appears more consistent across this 12 month period compared to SQL and Excel.
