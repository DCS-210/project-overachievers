# data

Place data file(s) in this folder.

Codebooks (variables, and their descriptions) for our data file(s).

## world-happiness folder, 2015.csv dataset 

For the 2015 World Happiness Report dataset, we have the following variables: 

- `Country`: Country 
- `Region`: The region in which the country belongs to
- `Happiness Rank`: Rank of the country based on happiness score
- `Happiness Score`: A metric measured in 2015 by asking the sampled people the question: "How would you rate your happiness on a scale of 0 to 10 where 10 is the happiest."
- `Standard Error`: The standard error of the happiness score.
- `Economy (GDP per Capita)`: The extent to which GDP contributes to the calculation of the Happiness Score.
- `Family`: The extent to which Family contributes to the calculation of the Happiness Score.
- `Health (Life Expectancy)`: The extent to which Life expectancy contributed to the calculation of the Happiness Score.
- `Freedom`: The extent to which Freedom contributed to the calculation of the Happiness Score.
- `Trust (Government Corruption)`: The extent to which Perception of Corruption contributes to Happiness Score.
- `Generosity`: The extent to which Generosity contributed to the calculation of the Happiness Score.
- `Dystopia Residual`: The extent to which Dystopia Residual contributed to the calculation of the Happiness Score.

**dimensions:** 158 rows x 12 columns

## pharmaceutical-drug folder, pharmaceutical_data_csv.csv dataset

For the Pharmaceutical Drug Spending by Country dataset, we have the following variables:

- `LOCATION`: Country represented by 3-letter abbreviation.
- `TIME`: Year in which the data was collected.
- `PC_HEALTHXP`: Percent of health spending = drug spending / total healthcare spending * 100%.
- `PC_GDP`: Percent of GDP = drug spending / total GDP = (drug spending / healthcare spending) * (healthcare spending / GDP) = PC_HEALTHXP * (healthcare spending / GDP).
- `USD_CAP`: US dollars per capita.
- `FLAG_CODES`: flag codes. (This will not be necessary).
- `TOTAL_SPEND`: Total spending on pharmaceutical drugs.

**dimensions:** 1036 rows x 7 columns

