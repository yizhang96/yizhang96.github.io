---
layout: post
title: Social Media Comment Map
---

**Role:** Researcher, Designer, and Front-End Developer<br>
**Duration:** February 2026 - Present<br>
**Tools:** Python, OpenAI Embeddings, UMAP, HDBSCAN, Plotly

---

## Table of Contents

* [Project Overview](#project-overview)
* [The Prototype](#the-prototype)
* [Demo](#demo)
* [Method](#method)
* [Findings and Implications](#findings-and-implications)
* [Selected References](#selected-references)

---

## Project Overview

When people scroll social media, comment sections often become a central part of how they interpret the original post. Comments provide social context: they signal what other users agree or disagree with, what kinds of reactions gain visibility, and what forms of expression appear socially approved.

Yet what we see in comment sections is rarely a neutral sample of public opinion. It is shaped by opaque ranking algorithms, engagement metrics, and visibility dynamics that amplify certain voices over others. As a result, readers may overestimate extreme views, misjudge the distribution of opinions, or misperceive social norms (Muchnik et al., 2013).

This project asks:

**Can we make collective voices visible without flattening individual ones?**

Social Media Comment Map is an exploratory public-facing prototype that offers an alternative way of visualizing comment sections. Instead of presenting comments as a linear list ranked by engagement, it uses language-model embeddings and clustering methods to organize comments as a semantic space while preserving access to individual comments.


### Why Comment Spaces Matter

Comment sections are a major site of social inference. People form impressions of what "most people think" based on what they can see, and that visibility is platform-mediated.

Comments matter because they provide more than isolated viewpoints. They show how people respond to one another: what gets endorsed, amplified, ignored, or challenged. Comment sections may therefore be an important environment for social-norm learning, shaping not only what people think others believe, but also what they infer about which forms of interaction are common, acceptable, or socially rewarded.

Research on social media ranking has largely focused on the main feed. Comment sections have received less attention, even though they are often central to how users interpret social media content. This design problem is also a social cognition problem.

---

## The Prototype

I built an interactive prototype that transforms a comment thread into a semantic map.

Each comment is embedded using a language model and projected into a two-dimensional space. Comments with similar meanings appear closer together, forming clusters that reflect recurring themes, framings, or narrative styles.

Crucially, this map does not summarize away individual voices. Users can click any point to view:

* the full original comment
* number of likes
* timestamp
* cluster affiliation

Instead of simply replacing comments with AI summaries, this approach makes the *structure* of the comments visible.

By allowing users to explore both individual comments and broader patterns, the prototype offers one way to study how different forms of comment presentation may shape what people infer from online discussions.

---

## Demo

<iframe
  src="https://yizhang96.github.io/social-media-comment-map/d/xhs_2026-02-07_studyabroad/"
  width="100%"
  height="720"
  style="border: 0;"
  loading="lazy"
  title="Social Media Comment Map Demo"
></iframe>

[Alternatively, open the interactive map in a new tab](https://yizhang96.github.io/social-media-comment-map/d/xhs_2026-02-07_studyabroad/)

---

## Method

This system uses a lightweight NLP and visualization pipeline:

1. Data Collection  
Comment threads are exported as csv/excel files (currently from Xiaohongshu and Reddit-style formats).
2. Text Embedding  
Sentence-level embeddings are generated using OpenAI embedding models.
3. Dimensionality Reduction  
UMAP projects high-dimensional embeddings into a 2D semantic space.
4. Clustering  
HDBSCAN identifies dense thematic clusters without predefining cluster counts.
5. Interactive Visualization  
Plotly renders an interactive scatterplot where each point represents a comment.

---

## Findings and Implications

Across multiple datasets, several patterns emerged:

* More narrative-driven responses created larger, diffuse semantic regions.
* In some cases, what appeared to be polarized discussions visually resembled continuous landscapes rather than sharply separated camps.
* TF-IDF-based maps produced sharper separations around keyword repetition, while embedding-based maps revealed deeper semantic continuity.

These observations suggest that comment sections often contain patterns that are hard to see in a standard ranked feed. A typical interface highlights what is recent, popular, or engaging. A semantic map instead makes relationships among comments more visible: which comments are similar, which themes appear most often, and which perspectives fall between more prominent positions.

From a research perspective, the map can serve as a testbed for studying how comment presentation shapes perceived social norms, perceived polarization, perceived toxicity, and willingness to express minority views.

From a product perspective, it raises design questions: Could alternative representations reduce misperception and polarization? Could visible distribution maps improve deliberative quality? How might platforms expose diversity without suppressing engagement?

From a policy perspective, transparency in how comment spaces are ranked and represented could be part of broader conversations about algorithmic accountability.

---

## Selected References

* Muchnik, L., Aral, S., & Taylor, S. J. (2013). Social influence bias: A randomized experiment. *Science, 341*(6146), 647-651.
* Brady, W. J., & Crockett, M. J. (2024). Norm psychology in the digital age: How social media shapes the cultural evolution of normativity. *Perspectives on Psychological Science, 19*(1), 62-64.
* Kubin, E., Merz, P., Wahba, M., Davis, C., Gray, K., & von Sikorski, C. (2024). Understanding news-related user comments and their effects: A systematic review. *Frontiers in Communication, 9*, 1447457.
* Piccardi, T., Saveski, M., Jia, C., Hancock, J., Tsai, J. L., & Bernstein, M. S. (2025). Reranking partisan animosity in algorithmic social media feeds alters affective polarization. *Science, 390*(6776), eadu5584.
