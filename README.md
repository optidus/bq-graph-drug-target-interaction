# BigQuery Graph Analytics — Drug-Target Interaction Network

A hands-on demo showcasing BigQuery's Property Graph and GQL (`GRAPH_TABLE`) capabilities for Life Sciences drug discovery. The notebook walks through building a synthetic drug-target interaction dataset in BigQuery, defining a property graph over it, and running GQL queries that would be significantly more complex to express in standard SQL.

---

## 📓 Notebook

`BQ Graph_Drug Target interaction.ipynb`

Designed to run end-to-end in **Google Colab** against your own BigQuery project.

---

## 🧬 Use Case — Drug-Target Interaction Network

**Business question:** What is the full blast radius of a compound — which targets does it bind, which biological pathways are affected, and what disease areas are implicated?

**Tables:**

| Table | Description |
|---|---|
| `compounds` | Drug molecules with mechanism of action and development stage |
| `targets` | Protein targets with gene names and UniProt IDs |
| `interactions` | Compound-target binding affinity (primary targets + off-targets) |
| `pathways` | Biological pathways with disease area associations |
| `target_pathways` | Junction table linking targets to the pathways they participate in |

**Property graph model:**
```
(Compound)-[BINDS_TO {affinity_nm, ic50_nm, interaction_type}]->(Target)
(Target)-[PARTICIPATES_IN {role, importance_score}]->(Pathway)
```

---

## 🔍 Demo Queries

Each query is shown in GQL alongside its SQL equivalent for direct comparison.

| Query | What it shows |
|---|---|
| Q1: Target binding profile | 1-hop traversal — compound to all primary and off-targets |
| Q2: hERG cardiac risk detection | 2-hop traversal — compound → hERG target → cardiac pathway |
| Q3: Shared-target compound pairs | Bidirectional match — two compounds converging on the same target node |
| Q4: Disease pathway blast radius | 2-hop aggregation — full pathway and disease area coverage per compound |
| Q5: Safe compound selection | Compounds with high oncology coverage but no hERG cardiac liability |

---

## 🚀 Getting Started

### Prerequisites
- A GCP project with BigQuery enabled and Editor role
- Google Colab or a Jupyter environment with the BigQuery client library

### Running the notebook

1. Open `BQ Graph_Drug Target interaction.ipynb` in Google Colab
2. Update the `PROJECT` variable in the Setup cell to your GCP project ID
3. Run steps 1–7 sequentially to create the dataset, tables, and property graph
4. Run the GQL query cells — each includes a SQL equivalent for side-by-side comparison
5. Visualisation cells use `%%bigquery --graph display_only` and render inline in Colab

---

## 📝 Further Reading

- [BigQuery Graph blog](https://medium.com/google-cloud/bigquery-graph-series-part-1-from-dark-data-to-knowledge-graphs-5a37f052d043))
- [BigQuery Graph Analytics video presentation](https://www.youtube.com/watch?v=ylUaoy1musw&t=481s)
- [Spanner Graph documentation](https://cloud.google.com/spanner/docs/graph/overview) — for real-time operational graph use cases
