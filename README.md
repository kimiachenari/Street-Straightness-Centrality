# 🚦 **Street Straightness-Centrality Visualization Using Momepy** 🚦

This project visualizes **street straightness-centrality** for the road network in **Mashhad, Iran** using the **Momepy** library. The visualization highlights the straightness of the streets in the network, helping to understand the geometric properties of the urban area. **Straightness-centrality** measures the degree to which streets deviate from a straight path and can be used to analyze the efficiency of the urban transportation network.

For more information on **Momepy**, visit the [Momepy Documentation](http://docs.momepy.org/).

---

## 🚀 **Key Features**

- **Straightness-Centrality Calculation**: Use **Momepy** to calculate street straightness-centrality, which measures how straight each street segment is in comparison to a straight line.
- **OSM Data**: Data is sourced from **OpenStreetMap** (OSM) using **OSMnx** to extract the street network for **District 11, Mashhad, Iran**.
- **Visualization**: Visualize street straightness using color gradients and quantiles, helping to identify straight and curved streets in the network.
- **Basemap Integration**: Add a **contextual basemap** using **Contextily** to provide spatial context to the straightness-centrality plot.
- **Scalebar**: Add a **scalebar** to the map for better spatial reference.

---

## 🧑‍🔬 **Getting Started**

### 1. **Install Required Libraries**

Ensure that you have the following libraries installed:

```bash
pip install geopandas momepy osmnx matplotlib contextily matplotlib-scalebar
```

### 2. **Run the Script**

1. **Prepare the Data**: The script fetches street network data from **OpenStreetMap** for **District 11, Mashhad, Iran**.
2. **Execute the Script**: Run the script to calculate **straightness-centrality** and generate the visualization.

---

## 🔧 **How It Works**

### 1. **Import Libraries**

The script imports essential libraries such as **GeoPandas**, **Momepy**, **OSMnx**, **Matplotlib**, and **Contextily** for data processing and visualization:

```python
import geopandas as gpd
import momepy
import osmnx as ox
import matplotlib.pyplot as plt
import matplotlib as mpl
import contextily
from matplotlib_scalebar.scalebar import ScaleBar
```

### 2. **Get Street Network Data**

The street network data for **District 11, Mashhad, Iran** is fetched from **OSMnx**, which uses **OpenStreetMap** data:

```python
streets_graph = ox.graph_from_place('District 11, Mashhad, Iran', network_type='drive')
streets_graph = ox.projection.project_graph(streets_graph)
```

The network is then converted into **GeoDataFrames** for easier manipulation and visualization:

```python
streets = ox.graph_to_gdfs(ox.get_undirected(streets_graph), nodes=False, edges=True, node_geometry=False, fill_edge_geometry=True)
```

### 3. **Calculate Street Straightness-Centrality**

**Momepy** is used to calculate the **straightness-centrality** of the street network, which quantifies how straight each street segment is compared to a straight line:

```python
primal = momepy.gdf_to_nx(edges, approach='primal')
primal = momepy.straightness_centrality(primal)
```

### 4. **Visualize Street Straightness**

The calculated **straightness-centrality** is visualized using a **color map** (`Spectral_r`), with **quantiles** for classification:

```python
nodes.plot(ax=ax, column='straightness', cmap='Spectral_r', scheme='quantiles', k=15, alpha=0.6)
ax.set_title('Straightness')
```

A second plot is created using the **Fisher-Jenks classification** to provide a more detailed view:

```python
ax = nodes.plot("straightness", scheme="fisherjenkssampled", markersize=0.5, legend=True, figsize=(12, 12))
```

### 5. **Add Basemap and Scalebar**

A **dark basemap** from **Contextily** is added for spatial context, and a **scalebar** is included for reference:

```python
contextily.add_basemap(ax, crs=nodes.crs, source=contextily.providers.CartoDB.DarkMatterNoLabels)

scalebar = ScaleBar(1, box_alpha=0, location="lower right", color='white', length_fraction=0.25, font_properties={"size": 12})
ax.add_artist(scalebar)
```

### 6. **Save the Final Plot**

The final map is saved as a **PNG** image for further use:

```python
fig.savefig("straightness_centrality_mashhad.png", dpi=300)
```

---

## 📊 **Outputs**

- **Straightness-Centrality Map**: A map that visualizes **street straightness** for the road network in **District 11, Mashhad**, with color coding indicating straightness values.
- **Basemap**: A **dark basemap** for spatial context.
- **Scalebar**: A **scalebar** added to the map for reference.

---

## 📈 **Future Enhancements**

- **Interactive Maps**: Create interactive maps using **Folium** or **Plotly** to explore the straightness-centrality of different areas.
- **Network Analysis**: Combine straightness-centrality with other network analysis techniques, such as **betweenness-centrality** or **closeness-centrality**, to get a fuller understanding of the road network.
- **Comparison of Regions**: Extend the analysis to compare straightness-centrality across different regions or cities.

---

![straightness_mhs_j](https://github.com/user-attachments/assets/15266889-45bf-4af7-8c31-8416ab3b36e9)
