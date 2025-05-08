# Chick-fil-A Supply: Network Theory & Distribution Center Analysis  
University of Notre Dame — MSBA Program  
**Course**: Network Theory & Analysis  
**Date**: April 29, 2025  

This project applies network theory to analyze the rapid expansion of **Chick-fil-A Supply**, a logistics-focused subsidiary of Chick-fil-A. Using clustering algorithms and centrality metrics, we evaluated whether the company’s distribution center (DC) placements align with store density and geographic efficiency. By modeling store relationships as a network, we uncovered structural patterns in Chick-fil-A’s supply chain and explored opportunities for strategic expansion. This analysis was completed as part of the **MSBA Network Theory & Analysis** course at the University of Notre Dame.

---

## Team

- **Alex Heck** – [@aheck3](https://github.com/aheck3)  
- **Cooper Foster** – [@coopfos](https://github.com/coopfos)  
- **Grace Robinson**

---

## Objective

1. Can clustering analysis explain where Chick-fil-A has placed their existing distribution centers?  
2. Where should Chick-fil-A strategically place new centers based on store geography?  

---

## Background

Chick-fil-A Supply launched in **2019** to vertically integrate and streamline the brand’s growing logistics needs. The subsidiary currently operates **13 confirmed DCs** to support over **3,200+ store locations** nationwide.

![History and First DC](images/cfa-atlanta-history.jpg)

---

## What is Chick-fil-A Supply?

Chick-fil-A Supply is a logistics-focused subsidiary launched in 2019 to streamline the brand’s vertically integrated supply chain. The company operates distribution centers (DCs) that serve hundreds of restaurants across the United States. As of 2025, there are 13 confirmed DCs — 10 operational and 3 in development.

![Current Distribution Centers](images/cfa-current-supply.jpg)
*Figure: Geographic locations of existing Chick-fil-A Supply distribution centers.*


## Network Structure

- **Nodes**: All U.S. Chick-fil-A restaurant locations (scraped from Chick-fil-A’s website)  
- **Edges**: Pairwise geographic distances between stores (calculated using the `geosphere` package in R)

![Store Locations](images/cfa-resturant-locations.jpg)

---

## Methodology

1. **Scraped Chick-fil-A store location data** using Python
2. **Calculated pairwise geographic distances** between stores using the `geosphere` package in R  
3. Removed duplicate vertices and cleaned store/location data  
4. Constructed an **undirected graph** where nodes are stores and edges are distances  
5. Applied the **Louvain clustering algorithm** to detect store communities  
6. Tested distance-based edge cutoffs (50km–500km) to find optimal cluster structure  
7. Calculated **closeness centrality** to assess how well-positioned each DC is within its community

---

### Clustering and Initial Cutoffs

We began by testing three logical distance thresholds — 200 km, 300 km, and 500 km — to define network boundaries and observe how store communities form under different assumptions.

To better understand what these distances look like geographically, we used **Google Earth** to visualize the radius around three operating distribution centers. This helped us confirm that our chosen cutoffs were reasonable based on regional store density.

- **200 km**: 30 communities – Cartersville, GA  
- **300 km**: 15 communities – Weston, FL  
- **500 km**: 7 communities – Kansas City, MO  

These initial tests helped us understand how network density varies by region and informed our later decision to search for an optimal cutoff.

![Clustering Cutoff Selection](images/clustering-cutoff-selection.jpg)

---

## Optimal Cutoff Selection

We ran Louvain clustering across cutoffs from 50–500 km to compare actual DC coverage to cluster size. The **75 km** cutoff yielded the lowest error and highest modularity (0.91), identifying 98 meaningful communities.

![75KM Community Mapping](images/cfa-75km-community-cluster.jpg)

---

## Identifying Expansion Opportunities

Clusters showed **gaps** in the West Coast and Northeast regions. We recommend new DCs in high-density zones like **Los Angeles**, **Bay Area**, and **New York City**.

![Expansion Suggestions](images/cfa-expansion-areas.jpg)

---

## DC Centrality Analysis

Using **closeness centrality**, we evaluated how centrally positioned each DC is within its local community. Several DCs ranked well, while others had room for optimization.

![Closeness Centrality Map](images/cfa-75km-closeness-centrality.jpg)

---

## Key Takeaways

- Distance-based clustering explains many current DC placements  
- High-density regions without nearby DCs signal strong opportunities for expansion  
- Simple network models can offer valuable insights for complex logistics systems  

---

## Files Included

- `chickfila-supply-network-analysis-code.Rmd` – Full R Markdown file with all modeling code  
- `cfa_edges.rda` / `cfa_nodes.rda` – Raw network input data  
- `cfa_w_clusters.csv` – Node list with cluster assignments  
- `dc_ref.csv` – DC-to-cluster lookup table for evaluation  
- `uszips.csv`, `zip_list.csv` – Zip code to lat/lng mapping for distance calculations  
- `images/` – Visuals used throughout this README  
- 📄 [Presentation Slides (PDF)](chickfila-supply-presentation.pdf)

---

## Visual Summary

| Store Network | Supply Chain Footprint | Expansion Zones |
|---------------|------------------------|-----------------|
| ![Stores](images/cfa-resturant-locations.jpg) | ![Current Supply](images/cfa-current-supply.jpg) | ![Expansion](images/cfa-expansion-areas.jpg) |

---

## Acknowledgments

Thanks to my teammates:  
- **Grace Robinson** – MSBA  
- **Cooper Foster** – [@coopfos](https://github.com/coopfos)

And thank you to **Professor Margaret Traeger** for an engaging and practical exploration of network theory in business analytics.

---
