# cognifyz-level1-analysis
Data Analysis Tasks from Level 1 of Cognifyz Internship (Task 2 )

import pandas as pd
import matplotlib.pyplot as plt

# Load the cleaned dataset
df = pd.read_csv("C:/Users/priya/Downloads/Cleaned_Dataset.csv")

# 1. City with the highest number of restaurants
city_counts = df['City'].value_counts()
top_city_by_count = city_counts.idxmax()
top_city_count = city_counts.max()

print(f"City with highest number of restaurants: {top_city_by_count} ({top_city_count} restaurants)")

# 2. Average rating per city
avg_rating_per_city = df.groupby('City')['Aggregate rating'].mean().sort_values(ascending=False)
print("\nAverage Rating Per City:\n", avg_rating_per_city.round(2))

# 3. City with highest average rating
top_city_by_rating = avg_rating_per_city.idxmax()
top_avg_rating = avg_rating_per_city.max()

print(f"\nCity with highest average restaurant rating: {top_city_by_rating} ({top_avg_rating:.2f})")

# 4. Bar chart: Top 10 cities by number of restaurants
top_10_city_counts = city_counts.head(10)

plt.figure(figsize=(10, 6))
top_10_city_counts.plot(kind='bar', color='teal')
plt.title("Top 10 Cities by Number of Restaurants")
plt.xlabel("City")
plt.ylabel("Number of Restaurants")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 5. Bar chart: Average rating in top 10 cities
top_10_cities = top_10_city_counts.index
avg_ratings_top_10 = df[df['City'].isin(top_10_cities)].groupby('City')['Aggregate rating'].mean().loc[top_10_cities]

plt.figure(figsize=(10, 6))
avg_ratings_top_10.plot(kind='bar', color='orange')
plt.title("Average Ratings of Top 10 Cities by Restaurant Count")
plt.xlabel("City")
plt.ylabel("Average Rating")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
