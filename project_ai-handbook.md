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

**Outcomes:** Round 1 showed that the main bottleneck was retrieval and evidence grounding, not answer clarity. After round 2 updates, the rates of acceptable answers increased from 68% to 88% on the original diagnostic set and reached 80% on a held-out test set.

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

Scores on these dimensions were then synthesized to make a final pass/partial/fail judgment, with some dimensions more important than others. For example, incorrect conclusions or unsupported claims would lead to automatic failure even when an answer was otherwise clear or useful.

### Round 1 findings

In the first evaluation round, the Handbook Assistant produced **13 passing**, **4 partially acceptable**, and **8 failed** answers. The assistant performed best on role boundaries, clarity, and actionability, but struggled most with answer correctness and evidence quality.

<div class="eval-profile">
  <h3>Round 1 average scores</h3>
  <div class="eval-profile-row">
    <span>Role boundary</span>
    <div class="eval-profile-track"><div class="eval-profile-fill" style="--w: 92%;"></div></div>
    <strong>1.84 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Clarity & readability</span>
    <div class="eval-profile-track"><div class="eval-profile-fill" style="--w: 86%;"></div></div>
    <strong>1.72 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Actionability</span>
    <div class="eval-profile-track"><div class="eval-profile-fill mid" style="--w: 82%;"></div></div>
    <strong>1.64 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Uncertainty calibration</span>
    <div class="eval-profile-track"><div class="eval-profile-fill mid" style="--w: 76%;"></div></div>
    <strong>1.52 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Answer correctness</span>
    <div class="eval-profile-track"><div class="eval-profile-fill low" style="--w: 68%;"></div></div>
    <strong>1.36 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Citation quality</span>
    <div class="eval-profile-track"><div class="eval-profile-fill low" style="--w: 64%;"></div></div>
    <strong>1.28 / 2</strong>
  </div>
  <p class="eval-profile-caption">Average score for each rubric dimension across 25 questions, using a 0-2 scale.</p>
</div>

Further review of the logs suggested that most failures happened at the **retrieval stage**: When retrieval was correct, the assistant usually produced high-quality answers; when retrieval was incorrect or incomplete, it sometimes produced plausible but misleading guidance.

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

### Round 2 update

Based on these findings, I made targeted updates, including normalizing queries (e.g., turning "quals" to "qualifying exam"), refining rules for section retrieval, and refined prompts. I then re-evaluated the product using both the original diagnostic set and a held-out test set.

On the original 25-question diagnostic set, performance improved from **13 to 17 passing answers**, with failures dropping from **8 to 3**. On a 15-question held-out set, the assistant produced **9 passing**, **3 partially acceptable**, and **3 failed** answers.

<div class="eval-profile">
  <h3>Round 2 average scores</h3>
  <div class="eval-profile-row">
    <span>Role boundary</span>
    <div class="eval-profile-track"><div class="eval-profile-fill" style="--w: 100%;"></div></div>
    <strong>2.00 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Clarity & readability</span>
    <div class="eval-profile-track"><div class="eval-profile-fill" style="--w: 92%;"></div></div>
    <strong>1.84 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Actionability</span>
    <div class="eval-profile-track"><div class="eval-profile-fill" style="--w: 90%;"></div></div>
    <strong>1.80 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Uncertainty calibration</span>
    <div class="eval-profile-track"><div class="eval-profile-fill" style="--w: 86%;"></div></div>
    <strong>1.72 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Answer correctness</span>
    <div class="eval-profile-track"><div class="eval-profile-fill mid" style="--w: 78%;"></div></div>
    <strong>1.56 / 2</strong>
  </div>
  <div class="eval-profile-row">
    <span>Citation quality</span>
    <div class="eval-profile-track"><div class="eval-profile-fill mid" style="--w: 80%;"></div></div>
    <strong>1.60 / 2</strong>
  </div>
  <p class="eval-profile-caption">Average score for each rubric dimension across 25 questions, using a 0-2 scale.</p>
</div>


---

## Summary & next steps

What can we take away from this project? In AI-mediated advising, a helpful answer is not enough. The assistant also needs to show where the answer comes from, acknowledge uncertainty, and guide students toward the right human support when the handbook is ambiguous. Moving forward, I plan to focus on three areas:

**Further improve retrieval and evidence-grounding:** The next iteration will continue to help the system find more relevant handbook sections. I will re-run the evaluation workflow after implementing the proposed changes.

**Gather more student feedback:** I am deploying the product with current PhD students at different program stages and asking them to test it with more questions, helping ensure the assistant is reliable in real use settings.

**Collaborate with department administration:** After further validation and refinement, I will work with USC Psychology administrative staff to explore whether the tool could reduce repetitive first-pass advising questions, reducing friction for students and lowering repetitive advising workload for staff.

## Resources

View the source code on [GitHub](https://github.com/yizhang96/psyc-handbook-rag).
