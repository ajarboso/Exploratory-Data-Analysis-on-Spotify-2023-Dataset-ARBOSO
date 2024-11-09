# Exploratory-Data-Analysis-on-Spotify-2023-Dataset-ARBOSO
<div id="header" align="center">
  <img src="https://media.giphy.com/media/M9gbBd9nbDrOTu1Mqx/giphy.gif" width="100"/>
</div>

<h3>
By: Adrian Jomer V. Arboso
</h3>
<h3>
Section: 2ECE-D
</h3>
<h3>
University: University of Santo Tomas
</h3>
<h3 align="center">
 Hello! <img src="https://media.giphy.com/media/hvRJCLFzcasrR4ia7z/giphy.gif" width="30px"/>
</h3>
<div align="center">
  <img src="https://media.giphy.com/media/dWesBcTLavkZuG35MI/giphy.gif" width="600" height="300"/>
</div>

## :man_technologist: About:
This analysis was conducted as part of an academic project for understanding data analysis techniques in the field of music streaming. By utilizing Python-based libraries for data manipulation and visualization, this project offers insights into musical trends, artist popularity, and platform-specific preferences. The dataset analyzed here represents a snapshot of Spotify tracks, and findings from this project may be useful for streaming platforms, music producers, and marketing professionals.

-------------------------
## 📖: GENERAL GUIDELINES:

:one: Begin by familiarizing yourself with the structure of the dataset. Check for missing values and data types, and perform an initial exploration to understand the different features available.

:two: Provide summary statistics to give an overview of key metrics such as the number of streams, release dates, and musical attributes (e.g., BPM, danceability).

:three: Use appropriate visualizations (e.g., bar charts, histograms, scatter plots) to uncover trends and patterns in the data. Ensure that your plots are well-labeled and easy to interpret.

:four: Investigate correlations between different variables and provide insights based on your findings. Explore relationships between streams and other musical characteristics like tempo, energy, or playlists.

:five: Based on your analysis, offer any insights or recommendations regarding the tracks, artists, or musical trends that could be useful for understanding what makes a track popular.

## :file_cabinet: Dataset:

:arrow_right: "spotify_data.csv"
:arrow_right_hook:  Contains information about various Spotify tracks, including popularity metrics, genre information, danceability, and other audio features.

-------------------------

## 🖥️: Codes and Explanations:

##### Importing Libraries and Loading the Dataset:
```
import pandas as pd 
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np 

df = pd.read_csv('spotify-2023.csv',encoding='ISO-8859-1')
df
```
- This cell imports essential libraries for data analysis and visualization
- Reads the Spotify dataset from a CSV file and stores it in a DataFrame (df) for analysis.
-------------------------

## 🔡 Information of the dataFrame and Fixing all the missing Values and Data Types:

```df.info()

numeric_columns = ['streams', 'in_deezer_playlists', 'in_shazam_charts']

#Convert columns to numeric with error handling, making them  integers
for column in numeric_columns:
    df[column] = pd.to_numeric(df[column], errors='coerce').astype('Int64')

    df[column].replace([np.inf, -np.inf], np.nan, inplace=True)
    df[column] = df[column].fillna(0).astype('Int64')
```

![image](https://github.com/user-attachments/assets/05739cb9-2499-4eaa-92f8-110c38814658)

The purpose of this code is to convert specified DataFrame columns from object types to integers. It handles non-numeric or infinite values by converting them to NaN, then fills any missing values with zero. This ensures the columns are consistently formatted as integers, with errors and outliers managed, and changes any object data types to integer types.

  ----------------------------

## 📘 Updated fixed dataFrame:

![image](https://github.com/user-attachments/assets/13d0bb86-9936-4faf-a3df-f5def5cc7fae)

--------------------------------

## 📈 Summary statistics:

``` df.describe() ```

![image](https://github.com/user-attachments/assets/fd18e374-b441-4d5b-ac0e-e311778f7936)

- The output from df.describe() provides a summary of the statistical properties of each numeric column in the DataFrame.
----------------------------

## 📝 Correlations between different variable:
```
numeric_columns = [
    'streams', 'bpm', 'danceability_%', 'valence_%', 'energy_%', 
    'acousticness_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%',
    'in_spotify_playlists', 'in_apple_playlists', 'in_deezer_playlists'
]

for column in numeric_columns:
    df[column] = pd.to_numeric(df[column], errors='coerce')

# Drop any rows with NaN values to clean up the data for correlation analysis
df_cleaned = df[numeric_columns].dropna()

# Calculate the correlation matrix
correlation_matrix = df_cleaned.corr()


# Plot heatmap for visual analysis of correlations
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title("Correlation Heatmap between Streams and Musical Characteristics")
#Display
plt.show()
```

![image](https://github.com/user-attachments/assets/02a556c8-7dae-4924-82fe-e0879d5b0027)

- The heatmap shows the correlation between "streams," various musical characteristics, and playlist metrics. Strong positive correlations appear between "streams" and both "in_spotify_playlists" and "in_apple_playlists," suggesting that songs featured in these playlists are streamed more. Musical traits like "danceability_%" and "valence_%" also show a moderate positive correlation, indicating that songs that are more danceable tend to have a more positive mood. There’s a negative correlation between "energy_%" and "acousticness_%," meaning that high-energy songs are less likely to be acoustic. Overall, the heatmap reveals how streaming numbers relate to playlist features and certain musical qualities.

  ----------------------------

## 📟 Overview of Dataset:

####  rows and columns in the the dataset:
```
#Getting  rows and columns of the dataset
df_shape = df.shape
print("Number of rows:", df_shape[0])
print("Number of columns:", df_shape[1])
```
output:
![image](https://github.com/user-attachments/assets/760a9cd6-b49f-49ac-bb43-dee51e22c4c4)

#### Data types and Missing values in each column:
```
print("Data types of each column:")
#To get data types of each column
print(df.dtypes)

# Check for missing values in each column
print("\nMissing values in each column:")
print(df.isnull().sum())
```
- This code checks the dataset's structure by displaying each column's data type and the count of missing values in each column.
Output:

![image](https://github.com/user-attachments/assets/763ffe86-fcb4-4879-8fe4-0f5cd792d9f8)

![image](https://github.com/user-attachments/assets/cc772701-4edc-422d-9661-a476c253820f)

----------------------------
## 📈 Basic Descriptive Statistics: 

####  Mean, Median, and Standard deviation of the streams column:

```
#Data Frame for mean,median and sd
streams_stats = pd.DataFrame({
    "Mean": [df['streams'].mean()],
    "Median": [df['streams'].median()],
    "Standard Deviation": [df['streams'].std()]
})

# Display
streams_stats
```
- The code calculates the mean, median, and standard deviation of the streams column in the DataFrame df and stores these statistics in a new DataFrame called streams_stats.

Output:

![image](https://github.com/user-attachments/assets/4f5759b4-8b8d-46fb-9ed0-ad41ab855921)


#### Distribution of released_year, artist_count and trends or outliers:

```
plt.figure(figsize=(13, 6))

# Distribution of released_year
plt.subplot(1, 2, 1)
plt.hist(df['released_year'], bins=15, color='pink')
plt.title('Graph for Distribution of Released Year')
plt.xlabel('Year')
plt.ylabel('Frequency')

# Distribution of artist_count
plt.subplot(1, 2, 2)
plt.hist(df['artist_count'], bins=15, color='skyblue')
plt.title('Graph for Artist Count')
plt.xlabel('Artist Count')
plt.ylabel('Frequency')

#Display
plt.show()
```

- This code performs basic descriptive statistics and visualizations on the dataset. It first calculates the mean, median, and standard deviation of the streams column and stores these in a DataFrame for easy display. Then, it creates histograms to show the distributions of released_year and artist_count, highlighting any patterns in the years songs were released and the number of artists per track. This approach provides a quick overview of the central tendency, spread, and distribution of key variables.

![image](https://github.com/user-attachments/assets/fbd29ebd-a629-48ce-a1c0-dfb211acdae1)

----------------------------
## 🎭 Top Performers:

#### top 5 most streamed tracks:
```
#find the top 5 most-streamed tracks with artist names
top_5_tracks = df.nlargest(5, 'streams').reset_index(drop=True)[['track_name', 'artist(s)_name', 'streams']]

# Display
top_5_tracks
```
Output:
![image](https://github.com/user-attachments/assets/5d751e6a-b80b-4cce-b8ef-00ddff39c7be)

```
# Plot the top 5 most streamed tracks
plt.figure(figsize=(10, 6))
plt.barh(top_5_tracks['track_name'], top_5_tracks['streams'], color='khaki')
plt.xlabel('Streams')
plt.title('Top 5 Most Streamed Tracks')

#Display
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/ffdd67a4-f542-41ce-8c92-723f9fb23507)

- Those codes displays the top most streamed tracks

####  Top 5 most frequent artists based on the number of tracks in the dataset:

```
# top 5 most frequent artists based on the number of tracks
top_artists = df['artist(s)_name'].value_counts().head(5).reset_index()
top_artists.columns = ['Artist', 'Number of Tracks']
top_artists
```
Output:
![image](https://github.com/user-attachments/assets/8df2249d-eb29-4571-b848-ac7d601215c4)


```
#barh for top 5 most frequent artists based on the number of tracks
plt.figure(figsize=(10, 6))
top_artists.plot(kind='barh', color='navajowhite')
plt.title('Top 5 Artists by Number of Tracks')
plt.xlabel('Artist')
plt.ylabel('Number of Tracks')
plt.xticks(rotation=45)
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/06b2090f-5914-4283-a238-47f9e1653b82)

- This code finds the track with the highest number of streams and displays the top 5 most streamed tracks in a table. Also alculates the top 5 artists based on the number of tracks they have in the dataset and displays this in a bar chart. You can see in the graph who and Data Frame who is the top 5's.

----------------------------
## 📈 Temporal Trends:

####  Trends in the number of tracks released over time:

```
#display count the number of tracks released each year
tracks = df['released_year'].value_counts().sort_index().reset_index()
tracks.columns = ['Year', 'Track Count']
tracks
```

- This code counts the number of tracks released each year in the df DataFrame and organizes this information in a new DataFrame called tracks. It first counts occurrences of each unique year in the released_year column using value_counts(), giving the number of tracks released per year. The counts are then sorted in ascending order by year using sort_index(), which arranges the data chronologically. After sorting, reset_index() is applied to convert the result into a DataFrame with a default integer index. Finally, the columns are renamed to Year and Track Count for clarity. The resulting tracks DataFrame provides a clear view of the number of tracks released each year, with each row showing a specific year and the corresponding track count.

Output:
![image](https://github.com/user-attachments/assets/80ae7296-ccab-41b3-a575-457ed3333d45) ![image](https://github.com/user-attachments/assets/a0392fde-b4e8-479b-802c-e17732b9a21a)

- The analysis of the tracks DataFrame shows how the number of tracks released has changed over time. By plotting the Year against Track Count, we can observe trends such as increases or decreases in music releases over the years. Here's a code to create the plot:

#### Plotted tracks released per year:

```
# Plot the number of tracks released per year
plt.figure(figsize=(12, 6))
plt.plot(tracks['Year'], tracks['Track Count'], marker='*', color='plum')
plt.xlabel('Year')
plt.ylabel('Number of Tracks Released')
plt.title('Number of Tracks Released Per Year')

plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/c393c1f0-36e3-4236-907b-380f7a8e8771)


#### Number of tracks released each month:
```
# Group by month to count the number of tracks released each month
tracks_month = df['released_month'].value_counts().sort_index().reset_index()
tracks_month.columns = ['Month', 'Track Count']
tracks_month
```
- This code groups the tracks by the month of release, counts the number of tracks released in each month, and organizes the result into a new DataFrame called tracks_month. Using value_counts() on the released_month column, it calculates the number of releases for each month, then sorts the months in ascending order using sort_index() to ensure the months are in order. Finally, it renames the columns to Month and Track Count for clarity

Output:
![image](https://github.com/user-attachments/assets/da3add75-4645-4fc7-b342-f43c79aa56b7)

#### Plotted number of tracks released each month:
```
- To analyze patterns, you can observe if certain months consistently have more releases than others. For example, a particular month might show a peak in releases, indicating a trend. Here's a code to plot the results and see which month has the most releases:

# Plot the number of tracks released per month
plt.figure(figsize=(10, 6))
plt.bar(tracks_month['Month'], tracks_month['Track Count'], color='palegreen')
plt.xlabel('Month')
plt.ylabel('Number of Tracks Released')
plt.title('Number of Tracks Released Per Month')
# label for months
plt.xticks(range(1, 13))  

plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/7819d395-17c6-4935-bc1d-16d8a9ba47f5)

The plot shows patterns in track releases by month. For example, if December has the highest number of releases, it suggests a trend of increased music production for the holiday season. 


----------------------------
## 🎵 Genre and Music Characteristics:

####  Correlation between streams and musical attributes
```
#Asigning specific attributes
attributes = ['streams', 'bpm', 'danceability_%', 'valence_%', 'energy_%', 
              'acousticness_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']
#geeting there Correlation
correlation = df[attributes].corr()['streams'][1:]  

# Convert to DataFrame
correlation_df = correlation.reset_index()
correlation_df.columns = ['Attribute', 'Streams Correlation']
correlation_df = correlation_df.sort_values(by='Streams Correlation', ascending=False)

# Display
correlation_df
```
- This code calculates the correlation between streams and various musical attributes (e.g., bpm, danceability_%, energy_%) to identify which attributes are most associated with higher stream counts. By finding and sorting these correlations in a new DataFrame (correlation_df), it reveals the attributes with the strongest positive or negative impact on streams.

Output:
![image](https://github.com/user-attachments/assets/4e182537-b6a0-4755-9f0d-cc80c842bdc0)

#### Plot bar chart for each attribute's correlation with streams:

```plt.figure(figsize=(10, 6))
plt.barh(correlation_df['Attribute'], correlation_df['Streams Correlation'], color='lavender')
plt.xlabel('Streams')
plt.title('Correlation of Streams with Each Musical Attribute')

plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/006be23e-a318-4a34-ae39-b7018b557eec)

- Based on the output, Mode appears to influence streams the most, showing the highest correlation with the number of streams. 

#### # Scatter plot for valence_% and acousticness_%,  valence_% and acousticness_%:

```
plt.figure(figsize=(12, 5))

# Scatter plot for danceability_% and energy_%
plt.subplot(1, 2, 1)
sns.scatterplot(data=df, x='danceability_%', y='energy_%', color='coral')
plt.title('Correlation between Danceability % and Energy %')
plt.xlabel('Danceability %')
plt.ylabel('Energy %')


# Scatter plot for valence_% and acousticness_%
plt.subplot(1, 2, 2)
sns.scatterplot(data=df, x='valence_%', y='acousticness_%', color='teal')
plt.title('Correlation between Valence % and Acousticness %')
plt.xlabel('Valence %')
plt.ylabel('Acousticness %')

#display
plt.tight_layout()
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/c9efacbc-5858-4925-86fc-79e79c3ea0e6)\

Based on the scatter plots
- Danceability % and Energy %: There appears to be a positive correlation between danceability and energy. Tracks with higher danceability scores also tend to have higher energy levels, which makes sense as both features often describe more lively, upbeat music.
- Valence % and Acousticness %: The relationship between valence and acousticness is less clear and seems weak, if present at all. The data points are more spread out, suggesting little to no correlation. Valence (positivity) and acousticness (how "acoustic" a track is) may not be directly related in this dataset.

----------------------------
## 📺  Platform Popularity:

#### Platform to favor the most popular tracks:

```# Group by each platform column to count the number of tracks in each
playlist_counts = df[['in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].sum().reset_index()
playlist_counts.columns = ['Platform', 'Track Count']

- The code calculates the number of tracks present in each playlist platform by summing the values in the columns for in_spotify_playlists, in_deezer_playlists, and in_apple_playlists. The result is stored in a DataFrame called playlist_counts, where each row represents a platform and the total count of tracks within its playlists.

# Display
playlist_counts
```
Output:
![image](https://github.com/user-attachments/assets/afdd83fb-475c-46e7-9dfc-57f48b0cfc5a)

#### Plot a bar chart to compare track counts across platforms:
```
plt.figure(figsize=(12, 6))
plt.bar(playlist_counts['Platform'], playlist_counts['Track Count'], color=['powderblue', 'mistyrose', 'lightsalmon'])
plt.xlabel('Platform')
plt.ylabel('Number of Tracks')
plt.title('Comparison of Track Counts Across Spotify Playlists, Spotify Charts, and Apple Playlists')
#Dsiplay
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/e313c389-b055-4874-adda-073c9be42994)

- Seeing in the Bar Chart, Spotify playlists contain the highest number of tracks, indicating that Spotify likely emphasizes including a broader range of popular music to appeal to a large audience. Deezer and Apple follow behind, with Deezer having a balanced number of tracks, suggesting it caters to a mix of popular and niche audiences, and Apple showing a more selective approach, possibly focusing on high-demand or curated music. Overall, Spotify appears to favor popular tracks the most, positioning itself as the platform with the widest selection for mainstream listeners.

----------------------------
## 👨‍🏫  Advanced Analysis

#### Patterns among tracks with the same key or mode:
```
#Group by for key and mode 
streams_by_key_mode = df.groupby(['key', 'mode'])['streams'].mean().reset_index()
streams_by_key_mode.columns = ['Key', 'Mode', 'Average Streams']

# Display the DataFrame
streams_by_key_mode
```
- The code groups the data by musical key and mode (where mode 1 represents Major and 0 represents Minor) and calculates the average number of streams for each combination. This results in a DataFrame, streams_by_key_mode, with columns for Key, Mode, and Average Streams, allowing us to analyze streaming patterns based on musical characteristics.

Output:
![image](https://github.com/user-attachments/assets/955eab5c-0964-4a3e-98d3-4311e45beb04)

#### Plot for Average Streams by Key
```
streams_by_key = df.groupby('key')['streams'].mean().reset_index()
plt.figure(figsize=(10, 6))
plt.bar(streams_by_key['key'], streams_by_key['streams'], color='rosybrown')
plt.xlabel('Musical Key')
plt.ylabel('Average Streams')
plt.title('Average Streams by Musical Key')

#Display
plt.show()
```
Output: 
![image](https://github.com/user-attachments/assets/7d0c10f4-7d59-4db5-a7ff-6a9081d807f7)

- Analyzing the streams data reveals that certain keys seem to attract higher average streams. Tracks in the key of C, in particular, tend to have the highest average streams, suggesting that this key resonates strongly with listeners. 

#### Plot for Average Streams by Mode:
```
streams_by_mode = df.groupby('mode')['streams'].mean().reset_index()
plt.figure(figsize=(6, 5))
plt.bar(streams_by_mode['mode'], streams_by_mode['streams'], color=['#e69597', '#ceb5b7'])
plt.xlabel('Mode')
plt.ylabel('Average Streams')
plt.title('Average Streams by Mode')

#Display
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/56038ce3-ba60-43df-af81-0921766b4217)

- Analyzing the streams data reveals that certain keys and modes seem to attract higher average streams. Tracks in Major mode (mode 1) tend to have higher average streams compared to those in Minor (mode 0), suggesting a preference for Major-mode tracks, which are often perceived as more uplifting or accessible. 

#### Artists consistently appear in more playlists or charts:

```
# Sum up the number of tracks
track_counts = df.groupby('artist(s)_name')[['in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].sum()

# Get the top 5 artists with the most tracks in specifc playlist
top_spotify_tracks = track_counts.nlargest(5, 'in_spotify_playlists')
top_deezer_tracks = track_counts.nlargest(5, 'in_deezer_playlists')
top_apple_tracks = track_counts.nlargest(5, 'in_apple_playlists')
```
- The code groups the data by artist name and sums up the number of times each artist appears in Spotify, Deezer, and Apple playlists. It then identifies the top 5 artists with the highest track count in each playlist platform individually

#### Plot top 5 artists by number of tracks in Spotify playlists
```
plt.figure(figsize=(10, 5))
plt.bar(top_spotify_tracks.index, top_spotify_tracks['in_spotify_playlists'], color='#fdffb6')
plt.xlabel('Artist')
plt.ylabel('Number of Tracks')
plt.title('Top 5 Artists by Number of Tracks in Spotify Playlists')
plt.show()
```

Output: 
![image](https://github.com/user-attachments/assets/005b694d-4e89-44b1-a4b8-337775f1c822)

#### Plot top 5 artists by number of tracks in Deezer playlists
```
plt.figure(figsize=(10, 5))
plt.bar(top_deezer_tracks.index, top_deezer_tracks['in_deezer_playlists'], color='#caffbf')
plt.xlabel('Artist')
plt.ylabel('Number of Tracks')
plt.title('Top 5 Artists by Number of Tracks in Deezer Playlists')
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/c67002aa-5ac7-474e-ad5b-59548ade91ff)

#### Plot top 5 artists by number of tracks in Apple playlists
```
plt.figure(figsize=(10, 5))
plt.bar(top_apple_tracks.index, top_apple_tracks['in_apple_playlists'], color='#9bf6ff')
plt.xlabel('Artist')
plt.ylabel('Number of Tracks')
plt.title('Top 5 Artists by Number of Tracks in Apple Playlists')
plt.show()
```
Output:
![image](https://github.com/user-attachments/assets/b3e747e1-777d-48c3-a47a-05437ecfb003)

- It reveals that certain artists consistently appear across playlists on Spotify, Deezer, and Apple, indicating their popularity and strong presence across these platforms. Artists in the top 5 for each platform are likely mainstream or well-known, as they have significant playlist representation, helping them reach wider audiences. While the top artists might vary slightly by platform, popular artists appear across multiple playlists, with Spotify often showing the most frequent representation due to its extensive user base and playlist diversity.

-----------------------
## 🖋️ Revisions:
:one: Replaced Matplot to Seaborn for Correlations between different variables with the help of Chat GPT.

:two: Coloring all of the Graphs into Pastel Colors

:three: Changing the kind of Graphs for more efficient visualization.

-----------------------
## 📰 References and Materials Used: 
:one: https://matplotlib.org/stable/gallery/color/named_colors.html

:two: https://www.sitepoint.com/github-profile-readme/

:three: https://chatgpt.com

-----------------------


<div  align="center">
  <img src="https://media.giphy.com/media/Z0YRcYVJqXyavIR9t6/giphy.gif?cid=ecf05e47cvi1mp4rrftjv18c1iilyoz7h202utbub89phu1n&ep=v1_gifs_search&rid=giphy.gif&ct=g" width="600" height="300"/>
</div>















