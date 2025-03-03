```python
import pandas as pd

def calculate_demographic_data(print_data=True):
    df = pd.read_csv('adult.data.csv')

    race_count = df['race'].value_counts()

    average_age_men = round(df[df['sex'] == 'Male']['age'].mean(), 1)

    percentage_bachelors = round(df[df['education'] == 'Bachelors'].shape[0] / df.shape[0] * 100, 1)

    q1 = df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])
    q2 = df['salary'] == '>50K'

    higher_education_rich = round((q1 & q2).sum() / q1.sum() * 100, 1)
    lower_education_rich = round((~q1 & q2).sum() / (~q1).sum() * 100, 1)

    min_work_hours = df['hours-per-week'].min()

    q1 = df['hours-per-week'] == min_work_hours

    rich_percentage = round((q1 & q2).sum() / q1.sum() * 100, 1)

    p = (df[q2]['native-country'].value_counts() \
                                / df['native-country'].value_counts() * 100).sort_values(ascending=False)

    highest_earning_country = p.index[0]
    highest_earning_country_percentage = round(p.iloc[0], 1)

    top_IN_occupation = df[(df['native-country'] == 'India') & q2] \
                          ['occupation'].value_counts().index[0]

    if print_data:
        print("Number of each race:\n", race_count) 
        print("Average age of men:", average_age_men)
        print(f"Percentage with Bachelors degrees: {percentage_bachelors}%")
        print(f"Percentage with higher education that earn >50K: {higher_education_rich}%")
        print(f"Percentage without higher education that earn >50K: {lower_education_rich}%")
        print(f"Min work time: {min_work_hours} hours/week")
        print(f"Percentage of rich among those who work fewest hours: {rich_percentage}%")
        print("Country with highest percentage of rich:", highest_earning_country)
        print(f"Highest percentage of rich people in country: {highest_earning_country_percentage}%")
        print("Top occupations in India:", top_IN_occupation)

    return {
        'race_count': race_count,
        'average_age_men': average_age_men,
        'percentage_bachelors': percentage_bachelors,
        'higher_education_rich': higher_education_rich,
        'lower_education_rich': lower_education_rich,
        'min_work_hours': min_work_hours,
        'rich_percentage': rich_percentage,
        'highest_earning_country': highest_earning_country,
        'highest_earning_country_percentage':
        highest_earning_country_percentage,
        'top_IN_occupation': top_IN_occupation
    }

```
