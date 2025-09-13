# wk7-Assignment
# Create a figure with 4 subplots
fig, axes = plt.subplots(2, 2, figsize=(15, 12))

# 1. Line chart (using index as pseudo-time series)
axes[0, 0].plot(df_clean.index, df_clean['sepal length (cm)'], label='Sepal Length')
axes[0, 0].plot(df_clean.index, df_clean['petal length (cm)'], label='Petal Length')
axes[0, 0].set_title('Trend of Sepal and Petal Length Measurements')
axes[0, 0].set_xlabel('Observation Index')
axes[0, 0].set_ylabel('Length (cm)')
axes[0, 0].legend()

# 2. Bar chart showing average sepal length by species
species_means = df_clean.groupby('species')['sepal length (cm)'].mean()
axes[0, 1].bar(species_means.index, species_means.values, color=['skyblue', 'lightgreen', 'lightcoral'])
axes[0, 1].set_title('Average Sepal Length by Species')
axes[0, 1].set_xlabel('Species')
axes[0, 1].set_ylabel('Sepal Length (cm)')

# 3. Histogram of petal length
axes[1, 0].hist(df_clean['petal length (cm)'], bins=15, color='lightgreen', edgecolor='black')
axes[1, 0].set_title('Distribution of Petal Length')
axes[1, 0].set_xlabel('Petal Length (cm)')
axes[1, 0].set_ylabel('Frequency')

# 4. Scatter plot of sepal length vs petal length
colors = {'setosa': 'red', 'versicolor': 'green', 'virginica': 'blue'}
for species in df_clean['species'].unique():
    species_data = df_clean[df_clean['species'] == species]
    axes[1, 1].scatter(species_data['sepal length (cm)'], 
                       species_data['petal length (cm)'], 
                       label=species, 
                       alpha=0.7,
                       color=colors[species])
axes[1, 1].set_title('Sepal Length vs Petal Length')
axes[1, 1].set_xlabel('Sepal Length (cm)')
axes[1, 1].set_ylabel('Petal Length (cm)')
axes[1, 1].legend()

plt.tight_layout()
plt.show()

# Additional visualization using seaborn for better style
plt.figure(figsize=(12, 8))
sns.scatterplot(data=df_clean, x='sepal length (cm)', y='petal length (cm)', 
                hue='species', style='species', s=100)
plt.title('Sepal vs Petal Length by Species (Seaborn Style)')
plt.show()
