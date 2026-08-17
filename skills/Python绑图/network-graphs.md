# Network and Graph Visualization

## When to Use

- Visualizing network structures in academic papers
- Plotting citation networks, social graphs, or collaboration graphs
- Displaying knowledge graphs, ontologies, or hierarchical structures
- Showing community detection results or centrality measures
- Illustrating communication or information flow networks

## Tools and Libraries

```
pip install networkx matplotlib numpy scipy
pip install pyvis  # optional: interactive HTML visualization
```

## Step-by-Step Instructions

### 1. Configure Network Visualization Defaults

```python
import networkx as nx
import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
import numpy as np
from matplotlib.lines import Line2D

# Publication defaults
plt.rcParams.update({
    'font.family': 'serif',
    'font.serif': ['Times New Roman', 'DejaVu Serif'],
    'font.size': 10,
    'figure.dpi': 300,
    'savefig.dpi': 600,
    'savefig.bbox': 'tight',
    'savefig.pad_inches': 0.05,
})

# Color palette for communities / node types
COMMUNITY_COLORS = ['#0072B2', '#D55E00', '#009E73',
                    '#CC79A7', '#E69F00', '#56B4E9']
EDGE_COLOR = '#888888'
NODE_BORDER = '#333333'
```

### 2. Layout Selection Guide

```python
LAYOUTS = {
    'spring': nx.spring_layout,         # Force-directed, general purpose
    'kamada': nx.kamada_kawai_layout,   # Good for small graphs (< 200 nodes)
    'circular': nx.circular_layout,     # Cycle/ring structures
    'shell': nx.shell_layout,           # Concentric circles
    'spectral': nx.spectral_layout,     # Based on graph Laplacian
    'fruchterman': nx.fruchterman_reingold_layout,  # Force-directed variant
}

def choose_layout(G):
    """Choose layout based on graph properties."""
    n = G.number_of_nodes()
    if n < 50:
        return 'kamada'
    elif n < 200:
        return 'spring'
    else:
        return 'fruchterman'
```

## Code Templates

### Template 1: Citation Network Visualization

```python
def plot_citation_network(G, paper_labels=None, citations=None,
                           filename='citation_network.pdf',
                           figsize=(5.0, 4.0)):
    """
    Visualize a citation network with node size proportional to citation count.

    Parameters
    ----------
    G : nx.DiGraph
        Directed graph (citing paper -> cited paper).
    paper_labels : dict, optional
        {node_id: label_string}.
    citations : dict, optional
        {node_id: citation_count}. If None, uses in-degree.
    """
    fig, ax = plt.subplots(figsize=figsize)

    if citations is None:
        citations = dict(G.in_degree())

    # Normalize node sizes
    max_cite = max(citations.values()) if citations else 1
    node_sizes = [100 + 900 * (citations.get(n, 0) / max_cite)
                  for n in G.nodes()]

    # Color by citation count
    cite_values = np.array([citations.get(n, 0) for n in G.nodes()])
    norm = plt.Normalize(vmin=cite_values.min(), vmax=cite_values.max())

    pos = nx.spring_layout(G, k=1.5 / np.sqrt(G.number_of_nodes()),
                           seed=42, iterations=50)

    # Draw edges
    nx.draw_networkx_edges(G, pos, ax=ax, edge_color=EDGE_COLOR,
                           alpha=0.3, width=0.5,
                           arrows=True, arrowsize=8,
                           arrowstyle='->', connectionstyle='arc3,rad=0.1')

    # Draw nodes
    nodes = nx.draw_networkx_nodes(G, pos, ax=ax, node_size=node_sizes,
                                    node_color=cite_values, cmap='YlOrRd',
                                    edgecolors=NODE_BORDER, linewidths=0.5)

    # Labels
    if paper_labels:
        nx.draw_networkx_labels(G, pos, paper_labels, ax=ax,
                                font_size=6, font_family='serif')

    cbar = plt.colorbar(nodes, ax=ax, shrink=0.8)
    cbar.set_label('Citation Count', fontsize=9)
    cbar.ax.tick_params(labelsize=8)

    ax.set_axis_off()
    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

# Usage
if __name__ == '__main__':
    G = nx.DiGraph()
    papers = ['Transformer', 'BERT', 'GPT', 'RoBERTa', 'T5',
              'ViT', 'CLIP', 'LLaMA']
    edges = [
        ('BERT', 'Transformer'), ('GPT', 'Transformer'),
        ('RoBERTa', 'BERT'), ('T5', 'Transformer'),
        ('ViT', 'Transformer'), ('CLIP', 'ViT'),
        ('LLaMA', 'GPT'), ('LLaMA', 'Transformer'),
        ('CLIP', 'BERT'), ('RoBERTa', 'Transformer'),
    ]
    G.add_edges_from(edges)
    citations = {p: G.in_degree(p) * 500 + np.random.randint(100, 1000)
                 for p in papers}
    plot_citation_network(G, paper_labels={p: p for p in papers},
                          citations=citations)
```

### Template 2: Collaboration Graph with Communities

```python
def plot_collaboration_graph(G, communities, filename='collab_graph.pdf',
                              figsize=(5.0, 4.0)):
    """
    Collaboration network with community coloring.

    Parameters
    ----------
    G : nx.Graph
        Undirected collaboration graph.
    communities : dict
        {node_id: community_id}.
    """
    fig, ax = plt.subplots(figsize=figsize)

    # Node colors by community
    unique_comms = sorted(set(communities.values()))
    comm_colors = {c: COMMUNITY_COLORS[i % len(COMMUNITY_COLORS)]
                   for i, c in enumerate(unique_comms)}
    node_colors = [comm_colors[communities[n]] for n in G.nodes()]

    # Node sizes by degree centrality
    centrality = nx.degree_centrality(G)
    max_c = max(centrality.values()) if centrality else 1
    node_sizes = [80 + 600 * (centrality[n] / max_c) for n in G.nodes()]

    # Edge widths by weight
    weights = [G[u][v].get('weight', 1) for u, v in G.edges()]
    max_w = max(weights) if weights else 1
    edge_widths = [0.3 + 2.0 * (w / max_w) for w in weights]

    pos = nx.spring_layout(G, k=2.0 / np.sqrt(G.number_of_nodes()),
                           seed=42)

    nx.draw_networkx_edges(G, pos, ax=ax, edge_color=EDGE_COLOR,
                           alpha=0.25, width=edge_widths)

    nx.draw_networkx_nodes(G, pos, ax=ax, node_size=node_sizes,
                            node_color=node_colors, edgecolors=NODE_BORDER,
                            linewidths=0.5, alpha=0.9)

    nx.draw_networkx_labels(G, pos, ax=ax, font_size=6)

    # Legend for communities
    legend_elements = [
        Line2D([0], [0], marker='o', color='w',
               markerfacecolor=comm_colors[c],
               markersize=8, label=f'Community {c}')
        for c in unique_comms
    ]
    ax.legend(handles=legend_elements, loc='upper left',
              framealpha=0.9, fontsize=8)
    ax.set_axis_off()
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 3: Knowledge Graph / Ontology

```python
def plot_knowledge_graph(triples, node_types=None, filename='kg.pdf',
                          figsize=(6.0, 4.5)):
    """
    Visualize a knowledge graph from (subject, predicate, object) triples.

    Parameters
    ----------
    triples : list of (str, str, str)
        [(subject, predicate, object), ...].
    node_types : dict, optional
        {node_name: type_string} for coloring.
    """
    G = nx.DiGraph()
    edge_labels = {}
    for s, p, o in triples:
        G.add_edge(s, o)
        edge_labels[(s, o)] = p

    fig, ax = plt.subplots(figsize=figsize)

    if node_types:
        type_colors = {}
        for t in set(node_types.values()):
            idx = len(type_colors) % len(COMMUNITY_COLORS)
            type_colors[t] = COMMUNITY_COLORS[idx]
        node_colors = [type_colors[node_types.get(n, 'default')]
                       for n in G.nodes()]
    else:
        node_colors = COMMUNITY_COLORS[0]

    pos = nx.spring_layout(G, k=1.8 / np.sqrt(G.number_of_nodes()), seed=42)

    nx.draw_networkx_edges(G, pos, ax=ax, edge_color=EDGE_COLOR,
                           alpha=0.4, width=0.8, arrows=True,
                           arrowsize=10, arrowstyle='-|>',
                           connectionstyle='arc3,rad=0.1')

    nx.draw_networkx_nodes(G, pos, ax=ax, node_size=600,
                            node_color=node_colors, edgecolors=NODE_BORDER,
                            linewidths=0.8, node_shape='o')

    nx.draw_networkx_labels(G, pos, ax=ax, font_size=7)

    # Edge labels with curved offset
    nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels,
                                  ax=ax, font_size=6,
                                  font_color='#444444',
                                  bbox=dict(boxstyle='round,pad=0.2',
                                           facecolor='white',
                                           edgecolor='none', alpha=0.8))

    if node_types:
        legend_elements = [
            Line2D([0], [0], marker='o', color='w',
                   markerfacecolor=type_colors[t],
                   markersize=8, label=t)
            for t in sorted(type_colors.keys())
        ]
        ax.legend(handles=legend_elements, loc='upper left',
                  framealpha=0.9, fontsize=8)

    ax.set_axis_off()
    fig.savefig(filename, format='pdf')
    plt.close(fig)

# Usage
if __name__ == '__main__':
    triples = [
        ('BERT', 'is_a', 'Language Model'),
        ('BERT', 'published_by', 'Google'),
        ('GPT', 'is_a', 'Language Model'),
        ('GPT', 'published_by', 'OpenAI'),
        ('BERT', 'based_on', 'Transformer'),
        ('GPT', 'based_on', 'Transformer'),
        ('Transformer', 'is_a', 'Architecture'),
        ('Attention', 'part_of', 'Transformer'),
    ]
    node_types = {
        'BERT': 'Model', 'GPT': 'Model', 'Transformer': 'Architecture',
        'Google': 'Organization', 'OpenAI': 'Organization',
        'Attention': 'Component',
        'Language Model': 'Concept', 'Architecture': 'Concept',
    }
    plot_knowledge_graph(triples, node_types)
```

### Template 4: Interactive Network with Pyvis

```python
from pyvis.network import Network

def create_interactive_network(G, communities=None,
                                filename='network.html'):
    """
    Create an interactive HTML network visualization.
    """
    net = Network(height='600px', width='100%', bgcolor='#ffffff',
                  font_color='black', notebook=False)
    net.barnes_hut(gravity=-3000, central_gravity=0.3)

    for node in G.nodes():
        color = COMMUNITY_COLORS[communities[node] % len(COMMUNITY_COLORS)] \
                if communities else COMMUNITY_COLORS[0]
        net.add_node(str(node), label=str(node), color=color,
                     size=10 + G.degree(node) * 2)

    for u, v in G.edges():
        net.add_edge(str(u), str(v), color='#cccccc', width=0.5)

    net.save_graph(filename)
    print(f"Saved: {filename}")
```

## Style Specifications

| Element | Value |
|---------|-------|
| Node size range | 80 – 800 (scaled by centrality) |
| Node border width | 0.5 pt |
| Node border color | #333333 |
| Edge color | #888888 |
| Edge width range | 0.3 – 2.5 pt |
| Edge alpha | 0.25 – 0.5 |
| Label font size | 6 – 8 pt |
| Layout seed | Always set `seed` for reproducibility |
| DPI (raster) | 300 for draft, 600 for submission |

## Common Pitfalls

1. **Non-reproducible layouts**: Always set `seed=N` in layout functions
2. **Node labels overlapping**: Reduce font size or use `adjustText` library
3. **Edge clutter in dense graphs**: Use lower alpha or threshold edges by weight
4. **Large graphs (>500 nodes)**: Use edge bundling or filter to top-k edges
5. **Arrow size in directed graphs**: Tune `arrowsize` to avoid oversized arrows
6. **Colorbar in multi-panel figures**: Use shared colorbar with `plt.colorbar(mappable, ax=[ax1, ax2])`
7. **Graph disconnected**: Check `nx.is_connected(G)` and consider layout per component

## Journal-Specific Tips

- **IEEE**: Embed as PDF/EPS in LaTeX; keep node labels ≥ 6 pt
- **Nature Complex Systems**: Prefer adjacency matrix visualization for large graphs
- **PNAS**: Use consistent node shapes across subfigures
- **General**: Provide adjacency matrix or edge list as supplementary data
- **PLOS**: Minimum 300 dpi; describe layout algorithm in figure caption
