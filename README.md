# Forest Fire Model Replication on Patent Citation Networks

This repository explores the temporal evolution of complex networks, specifically analyzing densification laws and shrinking diameters as networks grow over time. Based on the foundational paper *“Graphs over Time: Densification Laws, Shrinking Diameters and Possible Explanations”* by Jure Leskovec, Jon Kleinberg, and Christos Faloutsos, this project evaluates whether the **Forest Fire model** effectively replicates real-world network characteristics using a curated U.S. patent citation dataset.

---

## Problem Statement

Does the Forest Fire model effectively replicate the observed trends of densification, diameter reduction, and heavy-tailed degree distributions evident in the evolutionary trajectory for the chosen dataset?

---

## Dataset

The study utilizes data sourced from the **NBER Patent Data Project**, encompassing comprehensive records of U.S. patents issued between 1976 and 2006. 

* **Attributes Focused:** `Patent` (Citing patent ID), `Cit_Year` (Year the citation was recorded), and `Citation` (Unique identifier of the cited patent).
* **Scale:** Preprocessed, cleaned, and constrained to a systematic subset of 10,000 rows to optimize computational runtime while fully preserving critical citation mechanics and relationships.

---

## The Forest Fire Model

The Forest Fire model builds structural connections organically without predefining community structures. It utilizes a random ambassador node and a recursive, probabilistic "burning" process across forward and backward links using geometric distributions.

### Process Breakdown
1. **Initialize:** Start with a directed graph $G_1$ from the citation subset.
2. **Ambassador Selection:** Add a new node $v$ and link it to a uniformly selected random ambassador node $w$.
3. **Burn Forward Links:** Generate a random number $x$ from a geometric distribution with mean $\frac{1}{1-p}$. Select $x$ out-links and form recursive edges from $v$ to those targets.
4. **Burn Backward Links:** Generate a random number $y$ from a geometric distribution with mean $\frac{1}{1-rp}$. Select $y$ in-links and form recursive edges from $v$ to those sources.
5. **Recursive Step:** For each selected link, apply the burning process recursively until the fire dies out.

---

## Observations

* **Heavy-Tailed Degree Distributions:** The model yields a highly skewed, heavy-tailed in-degree distribution (where fundamental patents hold massive citations, while most hold very few) alongside a more constrained, naturally skewed out-degree distribution.
* **Network Densification:** The edge count grows at a significantly faster rate than the node count (the red line outpaces the blue line). This step-wise acceleration proves that the network becomes strictly more interconnected and dense over time.
* **Shrinking Effective Diameter:** Rather than expanding indefinitely with network size, the effective diameter undergoes alternating expansion and contraction phases, eventually flattening to exhibit a stable, highly connected core with an average path length of approximately `4.176`.
* **Emergent Scale-Free Properties:** Comparison benchmarks against Barabási-Albert modeling highlight a clear rich-get-richer phenomenon where highly interconnected foundational hubs naturally structure the center of the network, while niche or newer patents reside on the peripheral ring.

---

## Conclusion

Our study of graph evolution over time reveals significant patterns, including the Densification Power Law and shrinking diameters. By implementing the Forest Fire Model using only two key parameters ($p$ and $r$), we successfully generated realistic graphs that organically replicate heavy-tailed in- and out-degrees, network densification, and a shrinking effective diameter without hardcoding community structures.
