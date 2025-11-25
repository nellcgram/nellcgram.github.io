---
title: Help Center Article
parent: Samples
nav_order: 1
layout: default
---

# Help Center Article
<h2><a href="https://nellcgram.github.io/html/hc_scribbler_gram_sample.html" target="_blank" rel="noopener noreferrer">How to use Story Board view in Scribbler</a></h2>

<h2>About</h2>
<p>I wrote this sample Help Center article for a fictional writing app called Scribbler in the style of the structured documentation I write for Google Play.
</p>

<h2>Why I chose this project</h2>
<p>I initially explored writing about the real app Scrivener, but decided to fictionalize the steps since Scrivener is so complex. I describe a similar user interface to Scrivener with some of the same names.</p>
<p>I focused tightly on the Story Board view used to outline projects rather than writing about the entire Scribbler application. As a person who's enthusiastic about information organization and discoverability in my own projects, I wanted to demonstrate the ability to customize the app for a user who cares about those things (like how to set colors for different content types to make cards, or what types of custom metadata the user can create).</p>

<h2>Content strategy</h2>
<p><a href="https://nellcgram.github.io/pdf/hc_scribbler.pdf" target="_blank" rel="noopener noreferrer">This article includes IA annotations</a> showing a content model used for single-source publishing in a Content Management System. Content is structured into reusable blocks (instructions, definitions, tips, etc.) that can be published across multiple platforms and localized into other languages.</p>
<p>I chose a Help Center "How to / About" content model, a common model I would use when drafting for Google. Specifically, this starts with a "Benefits" block (how Story Board benefits the user), moves to task, tip, and important blocks, then ends with related resources so users can learn more about how to use Scribbler.</p>
<p>I organized the article structure from beginning to advanced customization for users who might want different things; for example, a card's color label is simple, custom metadata less so.</p>

<h2>Writing and design approach</h2>
    
<p><strong>Style standards (based on Google’s style guide):</strong></p>
 <ul>
<li>Tone: friendly, empathetic, conversational (contraction use is OK)</li>
<li>Clarity: 7th grade reading level, active voice, front-loaded sentences</li>
<li>Formatting: Sentence case for titles, title case for UI, breadcrumb navigation</li>
</ul>
<p><strong>Design decisions:</strong></p>
<p>Google uses bold (the "strong" HTML tag) text for UI and limits use of "code" font for public-facing, less technical documentation. But I differentiated between the three types of tags I used to create visual hierarchy and improve accessibility: I used "kbd" tags for keyboard shortcuts, "code" for UI elements, and "strong" for conceptual emphasis.</p>

<p>I changed from title to sentence case for UI elements (First Draft, Revised Draft) since this is not a Google app. I designed  two distinct callout boxes for scannability and to emphasize information:
  <ul>
<li>Tip (blue for information adding context)</li>
<li>Important (yellow for warning)</li>
  </ul>

<p>I created the article with HTML and added CSS over time, purposefully echoing my GitHub website "Just the Docs" theme because of its readability.</p>

---

<a href="https://nellcgram.github.io" target="_blank" rel="noopener noreferrer">Homepage</a>
