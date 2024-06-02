```python
import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt

# Load the dataset from CSV
df = pd.read_csv("/Users/tvvr/Downloads/ex5-2/costcos-geocoded.csv")

# Spatial chart (scatter plot)
plt.figure(figsize=(10, 8))
plt.scatter(df["Longitude"], df["Latitude"], c='b', alpha=0.5)
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.title('Costco Locations')
plt.grid(True)
plt.show()

# Heat map
world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))
gdf = gpd.GeoDataFrame(df, geometry=gpd.points_from_xy(df.Longitude, df.Latitude))
fig, ax = plt.subplots(figsize=(10, 8))
world.plot(ax=ax, color='lightgrey')
gdf.plot(ax=ax, markersize=20, color='blue', marker='o', alpha=0.5)
plt.title('Costco Locations Heat Map')
plt.show()

# Lollipop chart
plt.figure(figsize=(20,18))
plt.hlines(y=df.index, xmin=0, xmax=df['Longitude'], color='skyblue')
plt.plot(df['Longitude'], df.index, "o")
plt.yticks(df.index, df['Zip Code'])
plt.xlabel('Longitude')
plt.ylabel('Address')
plt.title('Costco Locations Lollipop Chart')
plt.grid(True)
plt.show()

```


    
![png](output_0_0.png)
    


    /var/folders/nl/520j0msd7vvdfj784n0twgxm0000gn/T/ipykernel_4387/1129241124.py:18: FutureWarning: The geopandas.dataset module is deprecated and will be removed in GeoPandas 1.0. You can get the original 'naturalearth_lowres' data from https://www.naturalearthdata.com/downloads/110m-cultural-vectors/.
      world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))



    
![png](output_0_2.png)
    



    
![png](output_0_3.png)
    



```python
# Lollipop chart
plt.figure(figsize=(10,8))
plt.hlines(y=df.index, xmin=0, xmax=df['Longitude'], color='skyblue')
plt.plot(df['Longitude'], df.index, "o")
plt.yticks(df.index[::2], df['Zip Code'][::2], fontsize=8)  # Adjust fontsize and stride for better readability
plt.xlabel('Longitude')
plt.ylabel('Zip Code')
plt.title('Costco Locations Lollipop Chart')
plt.gca().invert_yaxis()  # Invert y-axis to display addresses from top to bottom
plt.grid(True)
plt.tight_layout()  # Adjust layout for better spacing
plt.show()

```


    
![png](output_1_0.png)
    



```python

```
