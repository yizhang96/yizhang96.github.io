---
layout: post
title: AI Handbook Assistant
---

**Role:** Full-stack developer, AI evaluation researcher  
**Duration:** February 2026 – Present  
**Tools:** RAG; embedding; AI evaluation rubric; failure-mode analysis

---

## Table of Contents
* [Project overview](#project-overview)
* [Background](#background)
* [An AI solution](#an-ai-solution)
* [Product demo](#product-demo)
* [Evaluation and iteration](#evaluation-and-iteration)
* [Summary & next steps](#summary--next-steps)
* [Resources](#resources)

---

## Project overview

**Problem:** PhD students often struggle to interpret complex degree policies and find the current handbook insufficient for quickly answering situation-specific questions.

**Solution:** I built a RAG-based AI Handbook Assistant that answers students' questions about program requirements with concrete suggestions and citations. I also developed an evaluation workflow based on diagnostic and held-out policy questions.

**Outcomes:** Early evaluation identified retrieval and evidence grounding as the main bottlenecks. After redesigning the system, 27 of 30 responses were fully successful in a held-out evaluation, representing a **90% fully successful response rate**.

---

## Background

### A handbook for psychology students

The USC Psychology PhD program has over 100 students across six academic areas. Each area has different course requirements, program milestones, and degree timelines.

To make this information accessible, the department maintains an annually updated graduate handbook to serve as the official reference point for many high-stake student decisions, from research planning to navigating relationships with advisors, to submitting the right documents to meet graduation requirements.

---

### The problem

In practice, however, the handbook has often been a source of confusion. In a recent survey of 74 Psychology PhD students, about 40% explicitly considered the department milestones and requirements to be unclear. Open-ended responses further suggested that **lack of clarity in the Handbook** was a major cause of confusion: it contained apparently conflicting information, vague language, and with 50 pages and over 17,000 words, students often have trouble locating the right section for their needs.

<div class="deployment-figure case-figure">
  <img src="/assets/image/ai-handbook/town_hall_survey_results.png" alt="Survey results showing student perceptions of clarity around department milestones and requirements">
  <p class="deployment-caption">Survey results from 74 Psychology PhD students based on 2026 Town Hall survey</p>
</div>

Due to these frictions, students often have to seek support from one-on-one appointments with department administrators or informal conversations with senior classmates. Both are useful, but neither fully solves the access problem: appointments may not provide immediate support, while peer advice can be unstructured, incomplete, or outdated.

---

## An AI solution

To address this gap, I built a RAG-based AI Handbook Assistant that lets students ask customized questions about PhD requirements and receive answers grounded in the original handbook. The goal is to provide information and support tailored to each student's needs, and help them decide who to ask next when a situation is ambiguous.

### Design priorities

Given the high-stake nature of students' inquiries, an AI handbook assistant needs to do more than produce a plausible answer. It needs to answer from an identifiable source of truth, make the original evidence easy to verify, and acknowledge uncertainty when the handbook language is ambiguous. Accordingly, I defined the following design priorities:

<div class="case-snapshot-grid case-insights">
  <div class="case-snapshot-card">
    <h3>Source-grounded answers</h3>
    <p>Every useful answer should point back to handbook language, so students can verify the basis for the response.</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Uncertainty-aware guidance</h3>
    <p>The interface distinguishes direct support, interpretation, and missing information instead of making every answer sound equally certain.</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Role boundaries</h3>
    <p>It should not replace academic advising. For high-stakes decisions, the assistant nudges students to confirm with the program administrator, instead of providing definitive answers</p>
  </div>
</div>

### RAG workflow

The system parses the handbook into sections and smaller searchable units. When a student asks a question, it combines keyword matching and semantic similarity to retrieve the most relevant sections, including related policies that may appear elsewhere in the handbook. The language model then identifies the useful evidence and generates a concise answer with citations, page numbers, and suggested next steps.

<div class="deployment-figure case-figure">
  <img src="/assets/image/ai-handbook/rag_design.png" alt="RAG workflow diagram showing handbook preprocessing, student query matching, hybrid retrieval, and response generation">
  <p class="deployment-caption">RAG workflow for the AI Handbook Assistant.</p>
</div>

---

## Product demo

<div class="handbook-demo">
  <div class="handbook-demo-header">
    <span>Simulated Demo</span>
    <h3>Qualifying exam timeline</h3>
    <p>This example shows how the assistant turns a student question into a concise answer, then lets the student inspect the evidence behind it.</p>
  </div>

  <div class="handbook-chat">
    <div class="handbook-user-bubble">
      I'm in my 7th semester and still preparing for quals. What happens if I don't complete both the written and oral portions by the deadline, and what retake options do I have?
    </div>

    <div class="handbook-status">
      I found relevant handbook passages that support this answer.
    </div>

    <div class="handbook-answer-card">
      <h4>Answer</h4>
      <p>
        The full qualifying exam is due by the last day of classes of the 7th semester. Missing that deadline may place a student on warning status, with the usual remedy being completion by the end of the 8th semester.
      </p>
      <p>
        If the exam or part of it is failed, the committee may allow a retake within 1-6 months. Students cannot take the qualifying exam more than twice and must be enrolled during any retake term.
      </p>
      <h4>Suggested next step</h4>
      <p>
        Confirm your standing, retake options, and any area-specific policy with your guidance committee and program administrator.
      </p>
    </div>

    <details class="handbook-demo-details">
      <summary>
        <span>How this answer is supported</span>
        <small>5 stated points · 1 uncertainty note</small>
      </summary>
      <div class="handbook-evidence-list">
        <p><strong>Deadline:</strong> The entire qualifying exam must be completed no later than the last day of classes of the 7th semester. <a>S1 · p. 15</a></p>
        <p><strong>Warning status:</strong> Not completing the qualifying exam by that deadline is listed as a reason for warning status. <a>S2 · p. 11</a></p>
        <p><strong>Return to good standing:</strong> The listed remedy is to pass the qualifying exam by the last day of classes of the 8th semester, or pass a re-examination within 6 months if offered. <a>S2 · p. 12</a></p>
        <p><strong>Retake limit:</strong> A student may not take the qualifying exam more than twice. <a>S1 · p. 16</a></p>
        <p><strong>Enrollment:</strong> If not otherwise enrolled, the student must enroll in GRSC 800abz during the term of a retake. <a>S1 · p. 16</a></p>
        <p><strong>Uncertainty:</strong> Some consequences may depend on specialty-area rules, so students should confirm with the program administrator or Area Head.</p>
      </div>
    </details>

    <details class="handbook-demo-details">
      <summary>
        <span>Sources (2)</span>
        <small>Original handbook language</small>
      </summary>
      <div class="handbook-source-card">
        <div class="handbook-source-meta">
          <span>S1</span>
          <strong>K. Qualifying Examination</strong>
          <em>pp. 15-17</em>
        </div>
        <blockquote>
          "entire qualifying exam must be completed no later than the last day of classes of the seventh semester"
        </blockquote>
        <blockquote>
          "may not take the qualifying examination more than twice"
        </blockquote>
      </div>
      <div class="handbook-source-card">
        <div class="handbook-source-meta">
          <span>S2</span>
          <strong>G. Warning Status and Termination</strong>
          <em>pp. 11-13</em>
        </div>
        <blockquote>
          "students are considered to be on warning status if... they did not successfully complete the Ph.D. qualifying examination"
        </blockquote>
        <blockquote>
          "take and pass the qualifying examination by the last day of classes of the eighth semester"
        </blockquote>
      </div>
    </details>
  </div>
</div>

---

## Evaluation and iteration

### Evaluation rubric
To evaluate performance, I created an evaluation set including questions that frequently come up in past conversations, including questions about qualifying exam and dissertation requirements, course offering, program extension, and international student enrollment rules. I also included boundary cases where the Handbook does not give a clear answer, to test whether the AI would appropriately direct students to department staff instead of giving an overly confident response.

Each question-response pair was evaluated based on a **six-dimension rubric**, with each dimension scored on a 0-2 scale:

<div class="case-snapshot-grid">
  <div class="case-snapshot-card">
    <h3>Answer correctness</h3>
    <p>Does the answer match the handbook policy and include important limits or exceptions?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Citation quality</h3>
    <p>Are the answer claims traceable to relevant handbook passages?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Uncertainty calibration</h3>
    <p>Does the assistant acknowledge uncertainty when the evidence is weak, incomplete, or missing?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Actionability</h3>
    <p>Does it recommend a useful next step or the right person to contact?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Role boundary</h3>
    <p>Does it avoid acting beyond its role or implying it can make decisions on the student's behalf?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Clarity & readability</h3>
    <p>Is the answer concise, structured, and easy for students to understand?</p>
  </div>
</div>

Scores on these dimensions were then synthesized into a final pass, partial, or fail judgment, with some dimensions carrying more weight than others. Incorrect conclusions or unsupported claims resulted in failure even when an answer was otherwise clear or useful.

### Round 1: Identifying the main failure

In the first evaluation round, the Handbook Assistant produced **13 passing**, **4 partially acceptable**, and **8 failed** answers. The assistant performed best on role boundaries, clarity, and actionability, but struggled most with answer correctness and evidence quality.

Further review showed that most failures occurred during retrieval. When the correct evidence was retrieved, the assistant usually produced a useful and appropriately bounded answer. When retrieval was incomplete, it could produce plausible but misleading guidance.

<table class="case-table eval-failure-table">
  <thead>
    <tr>
      <th>Failure mode</th>
      <th>Definition</th>
      <th>Product implication / next fix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Retrieval incorrect or incomplete</td>
      <td>The system failed to retrieve the most relevant handbook section.</td>
      <td>Improve chunking and retrieval ranking algorithms.</td>
    </tr>
    <tr>
      <td>Unsupported inference</td>
      <td>The system made conclusions without enough direct support from the retrieved evidence.</td>
      <td>Require key claims to cite direct evidence, and fall back to uncertainty when support is weak.</td>
    </tr>
    <tr>
      <td>Answer was broad and lacked key details</td>
      <td>The relevant evidence was retrieved, but was buried in the citation list and not included in the main answer.</td>
      <td>Refine prompts to guarantee the specificity of answers.</td>
    </tr>
    <tr>
      <td>Crossed role boundaries</td>
      <td>The assistant suggested inappropriate actions, such as contacting department admin on behalf of the student.</td>
      <td>Strengthen guardrails around what the assistant can and cannot do for students.</td>
    </tr>
  </tbody>
</table>

### Round 2: Targeted improvements

Based on these findings, I developed a second version that normalized informal queries, added customized retrieval rules, and refined the answer-generation prompt.

When evaluated on the same 25 diagnostic questions, passing answers increased from **13 to 17**, while failures decreased from **8 to 3**. Correctness and evidence quality improved, although retrieval remained the primary source of error.

### Final system redesign

I then rebuilt the retrieval workflow to combine multiple keyword and semantic signals, account for relationships between handbook sections, and more carefully control which sources shaped the final answer.

An automated evaluation on an expanded set of 56 development questions found all essential handbook sections for **52 questions**. The generated answers retained the essential evidence for **51 questions**. Because these development answers were not manually scored on the six-dimension rubric, I used a separate held-out set to evaluate the final system's end-to-end answer quality.

### Final held-out evaluation

I evaluated the final system on **30 naturally occurring student questions** that were kept separate from development. Each response was manually scored on correctness, evidence quality, uncertainty calibration, actionability, role boundaries, and clarity.

The system produced **27 fully successful responses (90%)**, **2 partially successful responses**, and **1 unsuccessful response**. It received full marks for role boundaries and scored **96.7% on correctness and uncertainty calibration**. Actionability was the lowest-scoring dimension at **91.7%**, reflecting several answers that were correct but could have offered more precise next steps.

The remaining weaknesses were narrow and interpretable. The unsuccessful response confused two similar degree pathways, while the partially successful responses omitted or understated important procedural details.

<div class="eval-comparison">
  <h3>Six-dimension scores across evaluation stages</h3>
  <div class="eval-comparison-legend" aria-label="Evaluation stage legend">
    <span><i class="round-one"></i>Round 1 diagnostic</span>
    <span><i class="round-two"></i>Round 2 V2.5 diagnostic</span>
    <span><i class="final-round"></i>Final held-out</span>
  </div>
  <div class="eval-comparison-scale" aria-hidden="true"><span>0</span><span>1</span><span>2</span></div>
  <div class="eval-comparison-row">
    <span>Correctness</span>
    <div class="eval-comparison-track" aria-label="Correctness: Round 1 1.36, Round 2 1.56, final held-out 1.93 out of 2">
      <i class="eval-dot round-one" style="--x: 68%;"></i><i class="eval-dot round-two" style="--x: 78%;"></i><i class="eval-dot final-round" style="--x: 96.7%;"></i>
    </div>
    <strong>1.36 · 1.56 · 1.93</strong>
  </div>
  <div class="eval-comparison-row">
    <span>Evidence quality</span>
    <div class="eval-comparison-track" aria-label="Evidence quality: Round 1 1.28, Round 2 1.60, final held-out 1.87 out of 2">
      <i class="eval-dot round-one" style="--x: 64%;"></i><i class="eval-dot round-two" style="--x: 80%;"></i><i class="eval-dot final-round" style="--x: 93.3%;"></i>
    </div>
    <strong>1.28 · 1.60 · 1.87</strong>
  </div>
  <div class="eval-comparison-row">
    <span>Uncertainty calibration</span>
    <div class="eval-comparison-track" aria-label="Uncertainty calibration: Round 1 1.52, Round 2 1.72, final held-out 1.93 out of 2">
      <i class="eval-dot round-one" style="--x: 76%;"></i><i class="eval-dot round-two" style="--x: 86%;"></i><i class="eval-dot final-round" style="--x: 96.7%;"></i>
    </div>
    <strong>1.52 · 1.72 · 1.93</strong>
  </div>
  <div class="eval-comparison-row">
    <span>Actionability</span>
    <div class="eval-comparison-track" aria-label="Actionability: Round 1 1.64, Round 2 1.80, final held-out 1.83 out of 2">
      <i class="eval-dot round-one" style="--x: 82%;"></i><i class="eval-dot round-two" style="--x: 90%;"></i><i class="eval-dot final-round" style="--x: 91.7%;"></i>
    </div>
    <strong>1.64 · 1.80 · 1.83</strong>
  </div>
  <div class="eval-comparison-row">
    <span>Role boundaries</span>
    <div class="eval-comparison-track" aria-label="Role boundaries: Round 1 1.84, Round 2 2.00, final held-out 2.00 out of 2">
      <i class="eval-dot round-one" style="--x: 92%;"></i><i class="eval-dot round-two" style="--x: 100%;"></i><i class="eval-dot final-round" style="--x: 100%;"></i>
    </div>
    <strong>1.84 · 2.00 · 2.00</strong>
  </div>
  <div class="eval-comparison-row">
    <span>Clarity</span>
    <div class="eval-comparison-track" aria-label="Clarity: Round 1 1.72, Round 2 1.84, final held-out 1.90 out of 2">
      <i class="eval-dot round-one" style="--x: 86%;"></i><i class="eval-dot round-two" style="--x: 92%;"></i><i class="eval-dot final-round" style="--x: 95%;"></i>
    </div>
    <strong>1.72 · 1.84 · 1.90</strong>
  </div>
  <p class="eval-profile-caption">Average scores on a 0-2 scale. Rounds 1 and 2 evaluated different system versions on the same 25-question diagnostic set. The final system was evaluated on a separate set of 30 held-out questions; it was not manually rescored on the development set.</p>
</div>


---

## Summary & next steps

What can we take away from this project? In high-stakes advising, a helpful answer is not enough. The system must retrieve the right evidence, communicate uncertainty, and maintain clear boundaries around what still requires human judgment. Through repeated evaluation and redesign, the project progressed from an initial chatbot prototype to a validated single-question assistant with strong performance on held-out cases.

**Gather student feedback:** Study whether students find the answers, citations, and escalation guidance useful in realistic advising situations.

**Collaborate with department administration:** Work with USC Psychology administrative staff to review policy interpretations and explore broader student use after further validation.

**Explore future interactions:** Treat conversational follow-up and memory features as a new project phase with a separate test set and evaluation framework.

## Resources

View the source code on [GitHub](https://github.com/yizhang96/psyc-handbook-rag).
