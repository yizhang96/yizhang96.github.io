---
layout: post
title: AI Handbook Assistant
---

**Role:** Full-stack developer, AI evaluation researcher  
**Duration:** February 2026 – Present  
**Tools:** Retrieval-augmented generation (RAG); LLM embedding  

---

## Table of Contents
* [Project overview](#project-overview)
* [Background](#background)
* [An AI solution](#an-ai-solution)
* [Product demo](#product-demo)
* [Evaluation: Round 1 findings](#evaluation-round-1-findings)
* [Summary & next steps](#summary--next-steps)
* [Resources](#resources)

---

## Project overview

**Problem:** PhD students often struggle to interpret complex degree policies and find the current handbook insufficient for quickly answering situation-specific questions.

**Solution:** I built a RAG-based AI Handbook Assistant that answers student questions about degree requirements using retrieved handbook text, citations, and concrete suggestions.

**Outcomes:** Initial evaluation showed the assistant answered 14/25 cases appropriately and revealed retrieval accuracy—not response generation—as the primary failure mode.

---

## Background

### A handbook for psychology students

The USC Psychology PhD program has over 100 students, each navigating different course requirements, annual milestones, committee rules, and other degree requirements.

To make this information accessible, the department maintains an annually updated graduate handbook to serve as the official reference point for many high-stake student decisions, from research planning to navigating relationships with advisors, to submitting the right documents to meet graduation requirements.

---

### The problem

In practice, however, the handbook has often been a source of confusion. In a survey of 74 Psychology PhD students, about 40% explicitly considered the department milestones and requirements to be unclear. Open-ended responses further suggested that lack of clarity in the Handbook was a major cause of confusion: it contained apparently conflicting information, vague language, and with 50 pages and over 17,000 words, students often have trouble locating the right section for their needs.

<div class="deployment-figure case-figure">
  <img src="/assets/image/ai-handbook/town_hall_survey_results.png" alt="Survey results showing student perceptions of clarity around department milestones and requirements">
  <p class="deployment-caption">Survey results from 74 Psychology PhD students based on 2026 Town Hall survey</p>
</div>

Due to these frictions, support often shifts to one-on-one appointments with department administrators or informal conversations with senior classmates. Both are useful, but neither fully solves the access problem: appointments may not provide immediate support, while peer advice can be unstructured, incomplete, or outdated.

---

## An AI solution

To address this gap, I built a RAG-based AI Handbook Assistant that lets students ask customized questions about PhD requirements and receive concise answers grounded in the original handbook. The goal is to provide information and support tailored to each student's needs, and help them decide who to ask next when a situation is ambiguous.

### Design priorities

Given the often high-stake nature of students' questions, an AI handbook assistant needs to do more than produce a plausible answer. It needs to answer from an identifiable source of truth, make the original evidence easy to verify, and acknowledge uncertainty when the handbook language is ambiguous. I therefore defined the following design priorities, which differentiate the product from a general-purpose AI chatbot that relies on broad model knowledge and does not provide detailed citation references.

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
    <h3>Escalation built in</h3>
    <p>For high-stakes decisions, the assistant nudges students to confirm with the program administrator, DGS, advisor, or area head.</p>
  </div>
</div>

### RAG workflow

The system parses the handbook into sections and stores each section as an embedding. When a student asks a question, it uses both query embeddings and keyword matching to retrieve the most relevant handbook chunks. These chunks are then passed to the LLM to generate a concise answer with evidence, page numbers, and citations.

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
        The full qualifying exam should be completed by the last day of classes of the 7th semester. If the exam is not completed on time, the student may be placed on warning status and should confirm the exact consequence with their Area Head or program administrator.
      </p>
      <p>
        If a qualifying exam or part of it is failed, the committee may allow a retake within 1-6 months. Students cannot take the qualifying exam more than twice, and must be enrolled during the term of any retake.
      </p>
      <h4>Suggested next step</h4>
      <p>
        Contact your guidance committee and program administrator now to confirm your deadline, standing, and whether any area-specific policy applies.
      </p>
    </div>

    <details class="handbook-demo-details">
      <summary>
        <span>How this answer is supported</span>
        <small>3 stated points · 1 uncertainty note</small>
      </summary>
      <div class="handbook-evidence-list">
        <p><strong>Deadline:</strong> The entire qualifying exam must be completed no later than the last day of classes of the 7th semester. <a>S1 · p. 15</a></p>
        <p><strong>Retake limit:</strong> A student may not take the qualifying exam more than twice. <a>S1 · p. 16</a></p>
        <p><strong>Enrollment:</strong> If not otherwise enrolled, the student must enroll in GRSC 800abz during the term of a retake. <a>S1 · p. 16</a></p>
        <p><strong>Uncertainty:</strong> Some consequences may depend on specialty-area rules, so students should confirm with the program administrator or Area Head.</p>
      </div>
    </details>

    <details class="handbook-demo-details">
      <summary>
        <span>Sources (1)</span>
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
    </details>
  </div>
</div>

---

## Evaluation: Round 1 findings

To evaluate performance, I created an evaluation set including questions that frequently come up in past conversations, including questions about qualifying exam and dissertation requirements, course offering, program extension, and international student enrollment rules. I also included boundary cases where the Handbook does not give a clear answer, to test whether the AI would appropriately direct students to department staff instead of giving an overly confident response.

In high-stakes advising, a good answer must not only be correct, but also be verifiable, uncertainty-aware, and actionable. Accordingly, my initial evaluation round focused on the following metrics:

<div class="case-snapshot-grid">
  <div class="case-snapshot-card">
    <h3>Answer quality</h3>
    <p>Is the answer unacceptable, acceptable but improvable, or good?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Evidence grounding</h3>
    <p>Can the answer be traced back to original handbook text?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Uncertainty handling</h3>
    <p>Does the assistant say when the evidence is insufficient?</p>
  </div>
  <div class="case-snapshot-card">
    <h3>Action quality</h3>
    <p>Does it recommend the right next contact, such as an advisor, department administrator, or international student office?</p>
  </div>
</div>

In the first evaluation round, the prototype produced good answers for **14 of 25 cases**, partial but directionally useful answers for **7 cases**, and failed or substantively wrong answers for **4 cases**. The main failure mode involved retrieval and ranking rather than answer generation: when the correct handbook section was selected, the generated answer was usually reasonable, but some precise policy sections were outranked or filtered out before generation.

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
      <td>Wrong section retrieved</td>
      <td>The system selected a broad or adjacent handbook section instead of the section that directly answered the question.</td>
      <td>Split large handbook chunks and prioritize passage-level matches.</td>
    </tr>
    <tr>
      <td>Relevant evidence filtered out</td>
      <td>The right source appeared during retrieval, but was removed before the answer was generated.</td>
      <td>Fine-tune threshold for keeping vs. dropping candidate sections before answer generation.</td>
    </tr>
    <tr>
      <td>Student wording under-modeled</td>
      <td>The system missed connections between everyday student language (e.g., "quals") and formal handbook terminology ("qualifying exam").</td>
      <td>Add dictionary for common shorthand, synonyms, and insider phrases before retrieval.</td>
    </tr>
  </tbody>
</table>

---

## Summary & next steps

What can we take away from this project? In AI-mediated advising, a helpful answer is not enough. The assistant also needs to show where the answer comes from, acknowledge uncertainty, and guide students toward the right human support when the handbook is ambiguous. Moving forward, I plan to focus on three areas:

**Improve retrieval accuracy:** The next iteration will focus on helping the system find shorter but more relevant handbook sections, especially when broad sections contain overlapping keywords.

**Gather real user feedback:** I will deploy the product with current PhD students in the department and ask them to test it with questions from different program stages, helping ensure the assistant is reliable in real use settings.

**Collaborate with department administration:** After further validation, I will work with USC Psychology administrative staff to explore whether the tool could reduce repetitive first-pass advising questions, reducing friction for students and lowering repetitive advising workload for staff.  

## Resources

View the source code on [GitHub](https://github.com/yizhang96/psyc-handbook-rag).
