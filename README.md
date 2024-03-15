# London bike rides dasboard
Developed a Tableau dashboard to analyze London Bike Sharing data, employing Python and Pandas for data processing. Showcases skills in data analysis, manipulation, and advanced visualization techniques, illustrating proficiency in creating dynamic, insightful dashboards.

### Project Overview
1. Gather data from Kaggle's London Bike Sharing dataset.
2. Use Python and Pandas for data exploration, assessment, and manipulation.
3. Export the processed data to an Excel format for Tableau.
4. In Tableau, connect to the Excel dataset and craft visualizations: total rides, moving average, temperature vs. wind speed heatmap, and tooltips showing rides by weather and hour.
5. Utilize dynamic parameters and set actions in Tableau to create an interactive dashboard.
6. Format and finalize the dashboard for presentation.

### Data Source
https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset

### Tools
- Jupyther Notebook
- Excel
- Tableau

### Data Cleaning/Preparation

```python
# explore the data
bikes.info()
```
```python
bikes.shape
```
```python
# count the unique values in the weather_code column
bikes.weather_code.value_counts()
```
```python
# count the unique values in the season column
bikes.season.value_counts()
```
```python
# specifying the column names that I want to use
new_cols_dict ={
    'timestamp':'time',
    'cnt':'count', 
    't1':'temp_real_C',
    't2':'temp_feels_like_C',
    'hum':'humidity_percent',
    'wind_speed':'wind_speed_kph',
    'weather_code':'weather',
    'is_holiday':'is_holiday',
    'is_weekend':'is_weekend',
    'season':'season'
}

# Renaming the columns to the specified column names
bikes.rename(new_cols_dict, axis=1, inplace=True)
```
```python
# changing the humidity values to percentage (i.e. a value between 0 and 1)
bikes.humidity_percent = bikes.humidity_percent / 100
```
```python
# creating a season dictionary so that we can map the integers 0-3 to the actual written values
season_dict = {
    '0.0':'spring',
    '1.0':'summer',
    '2.0':'autumn',
    '3.0':'winter'
}

# creating a weather dictionary so that we can map the integers to the actual written values
weather_dict = {
    '1.0':'Clear',
    '2.0':'Scattered clouds',
    '3.0':'Broken clouds',
    '4.0':'Cloudy',
    '7.0':'Rain',
    '10.0':'Rain with thunderstorm',
    '26.0':'Snowfall'
}

# changing the seasons column data type to string
bikes.season = bikes.season.astype('str')
# mapping the values 0-3 to the actual written seasons
bikes.season = bikes.season.map(season_dict)

# changing the weather column data type to string
bikes.weather = bikes.weather.astype('str')
# mapping the values to the actual written weathers
bikes.weather = bikes.weather.map(weather_dict)
```
```python
# checking our dataframe to see if the mappings have worked
bikes.head()
```
```python
# writing the final dataframe to an excel file that we will use in our Tableau visualisations. The file will be the 'london_bikes_final.xlsx' file and the sheet name is 'Data'
bikes.to_excel('london_bikes_final.xlsx', sheet_name='Data')
```
### Recommandations
1. **Adjusting Fleet Size Based on Usage Patterns:** Increase the number of bikes during peak hours and in popular seasons to meet demand.
2. **Implementing Dynamic Pricing Models:** Adjust prices during peak times to manage demand and encourage usage during off-peak hours.
3. **Enhancing Bike Maintenance Schedule:** Use data on usage patterns to schedule maintenance, ensuring high availability and reliability of bikes.
4. **Promoting Off-Peak Usage:** Develop targeted marketing campaigns to encourage bike usage during less busy times, balancing the demand across the day.
