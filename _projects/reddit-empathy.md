---
layout: default
title: "How does empathic support unfold in Reddit conversations?"
type: "research"
year: 2026
tags: ["Empathy", "Social Support", "LLM", "NLP"]
status: "In progress"
status_color: "#f59e0b"   # orange
thumb: "/assets/image/reddit-empathy/support-flow-sankey.png"
summary: "How do people seek and receive support online? This project uses Reddit conversations to examine whether commenters adapt their responses to what posters are asking for, and whether better-matched support leads to more positive replies from the original poster."
link: "/projects/reddit-empathy/"
links:
  report: "/assets/pdf/reddit-empathy-report.pdf"
---

<section class="case-hero reddit-case-hero">
  <p class="case-eyebrow">Computational social science case study</p>
  <h1>How does support unfold in Reddit conversations?</h1>
  <p class="case-lede">
    This project studies online support as an interaction: what the original poster appears to need,
    how commenters respond, and whether the original poster comes back with gratitude, elaboration,
    questions, or pushback.
  </p>
  <div class="case-metrics">
    <div>
      <strong>2,765</strong>
      <span>annotated interaction units</span>
    </div>
    <div>
      <strong>24</strong>
      <span>support and advice subreddits</span>
    </div>
    <div>
      <strong>3</strong>
      <span>annotation layers</span>
    </div>
    <div>
      <strong>Human audit</strong>
      <span>used to refine prompts and labels</span>
    </div>
  </div>
</section>

## Project overview

<div class="case-snapshot-grid">
  <div class="case-snapshot-card">
    <h3>Research question</h3>
    <p>Do support responses fit what posters are asking for, and does that fit predict more positive original-poster uptake?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Data</h3>
    <p>A stratified sample of Reddit post-comment-OP reply units from support and advice communities.</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Methods</h3>
    <p>LLM-assisted annotation, human-in-the-loop validation, LIWC checks, and mixed-effects modeling.</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Core finding</h3>
    <p>Responses often tracked the poster's needs, and better-matched support was associated with OP gratitude and elaboration.</p>
  </div>
</div>

---

## Modeling the dynamics of online social support

What constitutes successful social support online? Previous work tends to focus on the language of the support-provider and has identified a wide range of factors associated with effective support, including linguistic synchrony (Doré & Morris, 2018), use of specific pronounds (e.g., "you" rather than "I"; Munin et al., 2025; Alghamdi et al., 2025), and templates of empathy, including validation, paraphrasing, and reappraisal (Gueorguieva et al., 2026).

However, when people seek support online, they are not all asking for the same thing: some want advice, validation, sensemaking, or space to disclose emotion. We know less about whether support providers adapt these tactics to what the seeker appears to need, and whether this fit predicts how support is received by the seeker.

Rather than treating social support as a property of one comment in isolation, this project models support as a three-part exchange.

<div class="interaction-flow" aria-label="Research logic from support seeking to response strategy to OP uptake">
  <div>
    <span>1</span>
    <h3>What did the OP seek?</h3>
    <p>Advice, emotional disclosure, validation, sense-making, high-stakes help, or another support need.</p>
  </div>
  <div>
    <span>2</span>
    <h3>How did commenters respond?</h3>
    <p>Validation, interpretation, emotional acknowledgment, advice, questions, self-disclosure, or challenge.</p>
  </div>
  <div>
    <span>3</span>
    <h3>How did the OP respond?</h3>
    <p>Gratitude, elaboration, answering a question, follow-up questions, or pushback.</p>
  </div>
</div>

<figure class="deployment-figure case-figure">
  <iframe class="case-iframe" src="/assets/interactive/reddit-empathy/support-flow.html" title="Interactive Sankey diagram of support-seeking needs, comment strategies, and OP uptake"></iframe>
  <figcaption class="deployment-caption">Interactive Sankey chart from the analysis report, showing how support-seeking needs connect to response strategies and OP uptake in the annotated sample.</figcaption>
</figure>

---

## LLM annotation workflow

To model support-seeking and provision in naturalistic conversations. I used human annotation with LLM-assistance: I created a gold set containing the key construct labels and, after validation, used LLM to scale annotation to all 2765 posts/comments.

<div class="workflow-rail">
  <div><span class="workflow-step">1</span><strong>Raw conversations</strong><span>Reddit posts, level-1 comments, and OP replies</span></div>
  <div><span class="workflow-step">2</span><strong>Stratified sampling</strong><span>OP-replied, high-engagement, question-like, and information-rich cases</span></div>
  <div><span class="workflow-step">3</span><strong>Codebook design</strong><span>Support-seeking needs, response strategies, and OP uptake</span></div>
  <div><span class="workflow-step">4</span><strong>GPT-5-mini annotation</strong><span>Multi-label codes for each interaction unit</span></div>
  <div><span class="workflow-step">5</span><strong>Human audit</strong><span>Manual checks against a gold-standard subset</span></div>
  <div><span class="workflow-step">6</span><strong>Modeling and visualization</strong><span>Mixed-effects models, LIWC checks, and communication figures</span></div>
</div>

<table class="case-table">
  <thead>
    <tr>
      <th>Annotation layer</th>
      <th>What it captures</th>
      <th>Example labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Support-seeking needs</td>
      <td>What kind of response the original post appears to invite.</td>
      <td>Advice, emotional disclosure, validation/appraisal, sense-making.</td>
    </tr>
    <tr>
      <td>Comment strategies</td>
      <td>What the level-1 reply does in response to the OP.</td>
      <td>Validation, emotional acknowledgment, interpretation, question, advice, self-disclosure.</td>
    </tr>
    <tr>
      <td>OP uptake</td>
      <td>How the original poster responds when they return to the thread.</td>
      <td>Gratitude, elaboration, answering, follow-up question, pushback.</td>
    </tr>
  </tbody>
</table>

---

## Statistical modeling

I used logistic mixed-effects models to test three linked questions: whether support-seeking needs predicted comment response strategies, whether response strategies predicted OP uptake, and whether specific need-response fit indicators predicted OP gratitude or pushback. Where possible, models accounted for clustering among comments within posts and subreddits, with simpler random-effects structures used when needed for stable model fitting.

---

## Key findings

### Finding 1: Commenters responded to what posters appeared to seek.

Advice-seeking posts received more advice, emotional disclosure received more acknowledgment and validation, and sense-making posts received more interpretation and questions.

  <figure class="deployment-figure case-figure">
    <img src="/assets/image/reddit-empathy/need-response-model-effects.png" alt="Mixed-effects model coefficients showing support-seeking needs predicting comment response strategies">
    <figcaption class="deployment-caption">Mixed-effects models showed theoretically coherent links between support-seeking needs and response strategies.</figcaption>
  </figure>

### Finding 2: Different response strategies predicted different OP reactions.

Questions predicted answering and elaboration; validation was associated with gratitude and lower pushback; challenge predicted pushback.

  <figure class="deployment-figure case-figure">
    <img src="/assets/image/reddit-empathy/response-uptake-model-effects.png" alt="Mixed-effects model coefficients showing comment response strategies predicting original-poster uptake">
    <figcaption class="deployment-caption">Response strategies predicted different forms of OP uptake, including answering questions, elaboration, gratitude, and pushback.</figcaption>
  </figure>

### Finding 3: Better-matched support predicted OP uptake.

Specific forms of need-response fit were associated with how original posters replied. For example, advice-seeking posts that received advice and emotional disclosure posts that received acknowledgment or validation predicted more OP gratitude, whereas sense-making posts that received interpretation or questions predicted more OP pushback.

  <figure class="deployment-figure case-figure">
    <img src="/assets/image/reddit-empathy/fit-uptake-gratitude-pushback.png" alt="Mixed-effects model coefficients showing need-response fit predicting original-poster gratitude and pushback">
    <figcaption class="deployment-caption">Specific need-response fit indicators predicted OP gratitude and pushback in the mixed-effects models.</figcaption>
  </figure>

### Cross-checking the meaning of support comments with LIWC

LIWC results showed that different response categories had distinct language profiles. For example, emotional acknowledgment, advice, questions, interpretation, validation, and self-disclosure differed in their overall tone, as well as the use of affective, cognitive, social, and self-focused words. This provides a descriptive check that the annotation labels capture meaningful differences in how people provide support.

<figure class="deployment-figure case-figure">
  <img src="/assets/image/reddit-empathy/liwc-profile.png" alt="LIWC language profiles by comment response move">
  <figcaption class="deployment-caption">The LLM-coded response strategies differed in overall tone.</figcaption>
</figure>

<figure class="deployment-figure case-figure">
  <img src="/assets/image/reddit-empathy/liwc-correlation-heatmap.png" alt="Heatmap of correlations between LIWC linguistic features and comment response categories">
  <figcaption class="deployment-caption">The response strategies showed distinct patterns of association with LIWC features</figcaption>
</figure>

---

## Contribution and next steps

Unlike past work, which tends to focus primarily on the support message and their effectiveness, the present project simultaneously models three components of online social support: what support-seekers ask for, what the commenter provides, and how the support-seeker. This makes it possible to study support *fit* rather than treating empathy as a stand-alone property of a single reply.

As a next step, I plan to scale the annotation to the full dataset after further validation. Additionally, the current dataset provides a useful human baseline for social support provision and can contribute to the evaluation of LLMs in providing goal-sensitive, calibrated social support in online settings.

---

## References

Alghamdi, Z., Kumarage, T., Agrawal, G., Karami, M., Almuteb, I., & Liu, H. (2025). RedditESS: A Mental Health Social Support Interaction Dataset -- Understanding Effective Social Support to Refine AI-Driven Support Tools. *arXiv*. https://arxiv.org/abs/2503.21888

Doré, B. P., & Morris, R. R. (2018). Linguistic synchrony predicts the immediate and lasting impact of text-based emotional support. Psychological Science, 29(10), 1716-1723.

Gueorguieva, E., Zhan, H., Suh, J., Hernandez, J., Lau, T., Li, J. J., & Ong, D. C. (2026). AI generates well-liked but templatic empathic responses. *arXiv*. https://arxiv.org/abs/2604.08479

Munin, S., Jurkiewicz, O., Gueorguieva, E. S., Oveis, C., & Ong, D. C. (2025). What can I say to help you? Language associated with successful extrinsic emotion regulation. *Emotion*.
