# Automation Exposure Occupations  UK SOC (2010)

## Overview
This repository provides a methodology for analyzing the relationship between technological innovation and occupational tasks. Specifically, it measures how advancements in robotics and artificial intelligence (AI) affect job exposure to automation. By utilizing patent data and semantic analysis, we construct a framework for evaluating the substitution potential of occupational tasks by emerging technologies.

---

## Methodology

### 1. **Identifying Occupational Tasks**
We use the task descriptions from the UK Standard Occupational Classification 2010 (UK SOC 2010), encompassing 363 occupations (ONS, 2010). These descriptions provide granular insights into the inputs required for various job roles. For illustrative purposes, examples of task descriptions for two occupations are included in Table 1.

### 2. **Measuring Innovation with Patent Data**

#### Patent Dataset
We rely on patent data from the Google Patents Public Dataset, focusing on patents granted between 1980 and 2020. The dataset includes approximately 1,300,000 worldwide patents published in English. Patents are classified into two technological categories:

- **Robot family**: Includes patents with titles containing terms like "robot," "mechatronics," "cyber-physical systems," etc.
- **AI family**: Includes patents with terms like "artificial intelligence," "machine learning," "neural network," etc.

#### Labeling Procedure
We adopt Webb’s (2019) approach of quasi-labeling patents using predefined keywords. While the procedure does not ensure unique labels, a qualitative review of verb-noun pairs demonstrates sufficient differentiation between technology categories.

### 3. **Semantic Analysis**

#### Leveraging Large Language Models
To measure the semantic similarity between patents and job tasks, we utilize the Bidirectional Encoder Representations from Transformers (BERT) model (Devlin et al., 2018). BERT’s contextual representation capabilities allow us to compute dense vector embeddings for both patent descriptions and job tasks.

#### Cosine Similarity
We calculate semantic similarity using the cosine similarity metric between the dense vectors. A matrix $X^\tau_{p,j}$ represents the similarity scores between each patent ($p$) and job task ($j$) for a given technology ($\tau$).

$$\text{cosine similarity}(\mathbf{u}, \mathbf{v}) = \frac{\mathbf{u_j} \cdot \mathbf{v_p}}{\|\mathbf{u_j}\| \|\mathbf{v_p}\|}$$

Here, $\mathbf{u}$ and $\mathbf{v}$ are the dense vectors representing the semantic embeddings. The similarity matrix $X^\tau_{p,j}$ represents the similarity scores between each patent ($p$) and job task ($j$) for a given technology ($\tau$), and is computed using cosine similarity for all $p,j$ pairs.

### 4. **Thresholding and Aggregation**

#### Thresholding
Following Autor et al. (2024), we retain the top 15% highest similarity scores, applying the threshold:

$$I^\tau_{p,j} = \begin{cases} 
1 & \text{if } X^\tau_{p,j} \geq \lambda^\tau_t \\
0 & \text{otherwise}
\end{cases}$$

where $\lambda^\tau_t$ represents the similarity distribution threshold for a given technology ($\tau$) and period ($t$).

#### Aggregation
For each occupation $j$ and technology $\tau$, we calculate cumulative exposure to automation:

$$\text{Aut}^\tau_{j,t} = \sum_{p \in \mathcal{P}^\tau} \sum_{j \in \mathcal{O}} I^\tau_{p,j}$$

This measure aggregates exposure across all relevant patents and tasks over time.


---

## Suggested Citation
If you use this repository, please cite:

Martin Lábaj, Tomáš Oleš, Gabriel Procházka. "Impact of Robots and Artificial Intelligence on Labor and Skill Demand: Evidence from the UK." Forthcoming in Eurasian Business Review, 2025.

---

## Repository Structure
- **data/**: Processed datasets, including patent data and occupational task descriptions.
- **figures/**: Visualizations of patent trends, similarity distributions, and exposure scores.

---

## License
This project is licensed under the MIT License. See `LICENSE` for details.

---

## Contributing
We welcome contributions! Please open an issue or submit a pull request for any suggestions or improvements.

