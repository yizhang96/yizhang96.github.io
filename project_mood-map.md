---
layout: post
title: Mood Map | UX Research & Design
---

**Role:** UX Researcher, Front-End Developer  
**Duration:** July – August 2025  
**Tools:** React, Tailwind CSS, Supabase  
**Partner Organization:** Flourish Science  

---

## Table of Contents
* [Introduction](#introduction)
* [Research](#research)
* [Design Iteration](#design-iteration)
* [Prototype Demo](#prototype-demo)
* [Outcomes & Reflection](#outcomes--reflection)
* [Credits](#credits)

---

## Introduction
**Why**: Being able to label one's emotions is a skill essential for well-being, yet most emotion trackers limit users to fixed emotion labels (happy, sad) and focus on solitary reflection. *Mood Map* reimagines emotional awareness as a shared, interactive experience—helping people visualize and exchange emotions within teams and groups.

**What**: Mood Map is a browser-based prototype built on the [*Circumplex Model of Affect*](https://psu.pb.unizin.org/psych425/chapter/circumplex-models/). It enables users to log emotions on a two-dimensional space (valence-arousal) using predefined or custom labels. All users' moods are visualized simulteneously.

**How**: Digitized Flourish Science’s physical mood map into a React-based web tool with Supabase backend. Two rounds of usability testing (≈5 users each) led to refinements such as labeled mood blocks, clearer visuals, and the ability to share mood board with teammates, which increased user experience and engagement.

---

## User Research
To gather users' feedback on the initial version of the Mood Map and improve the ease of interaction with the emotion-mapping interface, I ran two rounds of informal usability testing (5 users each), and iterated through two designs.  

**Key Insights:**  
- Users found the valence–arousal axes confusing without clear anchors (the entered labels often don't align with the valence & arousal values).  
- Predefined emotion labels improved orientation while maintaining flexibility.
- The ability to customize and share mood boards sets the product apart from the existing physical mood map.  

---

## Design Iteration

<div style="display: flex; flex-wrap: wrap; gap: 16px; justify-content: center; align-items: flex-start;">

  <div style="flex: 1; min-width: 300px; text-align: center;">
    <img src="/assets/image/mood-map/mood-map-v1.png" alt="Mood Map V1" style="width:100%; border-radius:10px;">
    <p>Mood Map Version 1</p>
  </div>

  <div style="flex: 1; min-width: 300px; text-align: center;">
    <img src="/assets/image/mood-map/mood-map-v2.png" alt="Mood Map V2" style="width:100%; border-radius:10px;">
    <p>Mood Map Version 2</p>
  </div>

</div>

**V1 — Open-Ended Exploration**  
The first prototype let users double-click anywhere on the grid to label their mood freely.
While this design is highly flexibility, many users found it unclear how to interpret the valence and arousal axes or where to place emotions accurately.
As a result, some entries didn’t match the intended emotional dimensions—for instance, “sad” was sometimes labeled as a positive-valence emotion.

**V2 — Guided but Flexible**  
To improve clarity, I added labeled axes and optional predefined emotion examples that help orient users while still allowing personalization.
Users can now either choose a predefined emotion or enter their own label.
V2 also introduced the ability to create and share mood boards with teammates, extending the tool’s use to collaborative or group settings.
Finally, I enhanced visual contrast, hover feedback, and layout responsiveness across devices, making the interaction smoother and more consistent overall.

---

## Prototype Demo
Here’s the digital mood map prototype. Feel free to interact with it directly in your browser:

<iframe src="https://yizhang96.github.io/mood-map/v2/" width="100%" height="600px" style="border:none;"></iframe>

If the embedded view doesn’t load, you can also [open it in a new tab](https://yizhang96.github.io/mood-map/v1/).

---

## Outcomes & Reflection
- The digital prototype has been adopted into Flourish Science’s internal product ecosystem and is being prepared for public integration.  
- By combining iterative usability testing with psychological theories, *Mood Map* turned a conceptual framework into a functional, user-centered tool and demonstrated how theory-informed design and make emotional reflection both intuitive and shareable.  
- Future updates will include onboarding guidance to help users better understand the logic behind the Circumplex model of emotion. In addition, more testing will be done in group settings (e.g. morning check-ins or icebreaking) to evaluate the potential of Mood Map for promoting social connection and emotional bonding.

---

## Credits
This project was inspired by the [*physical mood board*](https://www.myflourish.ai/mood-map) developed by **Julie** and **Xuan** at Flourish Science. Their early design concept and team discussions provided the foundation for the digital adaptation.  

**Built with:** React, Tailwind CSS, Supabase  
View the full source code on [GitHub](https://github.com/yizhang96/mood-map).
