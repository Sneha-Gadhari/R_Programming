# Experiment 5 — Social Network Analysis with R

## Files

| File | Description |
|---|---|
| `R_Prog_Experiment_5_23102B0055.ipynb` | R notebook (Colab, `igraph`) — full implementation |
| `R_Prog_Experiment-5_23102B0055_Sneha_Gadhari.pdf` | Lab report / write-up |
| `centrality_measures.csv` | Node-level centrality results (degree, closeness, betweenness, hub, authority) |
| `network_degree_plot.png` | Network graph sized & colored by node degree |
| `community_plot.png` | Detected communities (edge-betweenness) |

## Objective

Study relationships between entities using R, model them as a node-edge network, apply `igraph` to compute structural measures, identify influential nodes, and detect communities.

## Description

The notebook builds the analysis step by step:

- **Setup:** install and load `igraph`.
- **Toy graphs:** small undirected and directed graphs to demonstrate node/edge representation.
- **Toy measures:** degree (in/out/all), diameter, density, reciprocity, closeness, betweenness, transitivity, assortativity computed on the toy graph.
- **Real dataset:** edge list imported from a public GitHub CSV, built into a directed graph `net`.
- **Degree distribution:** histogram and summary statistics of node degree.
- **Network measures:** diameter, density, reciprocity, closeness, betweenness, transitivity, assortativity on the real network.
- **Visualization:** raw network plot, degree-sized/colored plot, degree heat-map.
- **Hub/Authority scores:** `hub_score()` for connector nodes, `authority.score()` for popular/pointed-to nodes.
- **Centrality table:** combines degree, in/out-degree, closeness, betweenness, hub, and authority scores; ranks top nodes.
- **Community detection:** edge-betweenness and Louvain clustering, modularity compared between methods.
- **Outputs:** centrality table saved as CSV, key plots saved as PNG.

## Key Results

- Network has 52 nodes.
- Highest-degree node: **CA** (degree 62, in-degree 50, out-degree 12) — the most connected node overall.
- Other high-degree hubs: **CC** (50), **CD** (40), **DD** (36).
- Highest hub score: **CC** (1.0) — points to the most nodes, acting as the top connector.
- Highest authority score: **CA** (1.0) — the node most pointed to by others.
- **CD** has the highest betweenness (375.99), making it the strongest broker linking otherwise separate parts of the network.
- Community detection (edge-betweenness) splits the network into multiple distinct clusters, visible as separate colored regions in `community_plot.png`.

## Conclusion

The network shows a hub-and-spoke degree pattern, with a small number of high-degree nodes (CA, CC, CD, DD) acting as key connectors and brokers. Centrality measures and hub/authority scores consistently identify the same nodes as most influential. Community detection reveals distinct sub-groups within the network, confirming that `igraph` is effective for representing, analyzing, and visualizing social network structure end to end.

## How to Run

1. Open `R_Prog_Experiment_5_23102B0055.ipynb` in Google Colab.
2. Set runtime to **R**.
3. Run all cells top to bottom — the dataset is fetched automatically from GitHub.
4. Outputs (CSV + PNGs) are saved to an `outputs/` folder in the Colab session.
