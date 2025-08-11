---
layout: post
title: A digital mood map
---

## Introduction

Emotions can feel complex, fleeting, and hard to capture. Mood Map is an interactive, browser-based tool that helps you log and reflect on your emotions in real time.

The tool is inspired by the [**circumplex model of affect**](https://psu.pb.unizin.org/psych425/chapter/circumplex-models/), a widely used psychological framework that organizes emotions along two dimensions:  
- **Valence**: how pleasant or unpleasant an emotion feels  
- **Arousal**: how activated or calm the emotion is  

Each emotion can be mapped as a point in this two-dimensional space. For example, "joy" is high in both valence and arousal, while "calm" is pleasant but low in arousal. As for negative emotions, "anger" is high in arousal while "sadness" is low in arousal.

## The Physical Mood Map

The idea for this project began during my internship at **Flourish Science**, where the team created [a physical mood map](https://www.myflourish.ai/mood-map) for participants to pin their current emotions.

Seeing its impact on emotional awareness and connection, I wanted to explore whether a **digital version** could serve a similar purpose, especially for individuals reflecting on their feelings in solitude.

## How to Use the Digital Mood Map

Here’s the digital mood map I built. Feel free to interact with it right in your browser:

<iframe src="https://yizhang96.github.io/mood-map/v1/" width="100%" height="800px" style="border:none;"></iframe>

If the embedded view doesn’t load, you can also [open it in a new tab](https://yizhang96.github.io/mood-map/v1/).

To log your mood, simply:

- **Double-click** anywhere on the canvas based on how good/bad and how energetic you currently feel. Double click again to update your previous mood.
- Add a **label** to describe your emotion (e.g., "excited", "tired", "peaceful", or "tired but satisfied"!)
- Hover or tap on a dot to view its emotion label. 

Unlike pre-defined emotion trackers, this map gives you the flexibility to **define your emotions in your own words**.




## Credits

This project was built with:
- **React & Tailwind CSS** for the interactive front-end
- Inspiration and early conversations from Julie and Xuan at **Flourish Science**
- Theoretical guidance from affective science and psychology research

View the full source code on [GitHub](https://github.com/yizhang96/mood-map).
