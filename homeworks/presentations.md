---
layout: default
title: Paper Presentation (10%)
active_tab: homework
release_date: 2023-09-03 
submission_link: https://blackboard.umbc.edu/ultra/courses/_76209_1/outline/assessment/test/_6357062_1?courseId=_76209_1

---

<div class="alert alert-info">
The summary assignment is due before 3PM ET the day before your presentation. 
</div>

{% if page.materials %}
<div class="alert alert-info">
You can download the materials for this assignment here:
<ul>
{% for item in page.materials %}
<li><a href="{{item.url}}">{{ item.name }}</a></li>
{% endfor %}
</ul>
</div>
{% endif %}


{{page.title}}
=============================================================

This assignment is to show you the modern uses of older AI methods and give you an entry point for how to critically read an academic paper.

## Learning Objectives
In this assignment, you will
- find reputible research articles from a specific AI area that you find interesting
- recognize & synthesize key points of a research paper
- communicate key findings from a research paper

## Instructions
- Pick a Module from 1-4: [sign-up sheet](https://docs.google.com/forms/d/e/1FAIpQLSfaVh0jst-vw9b7iJlOqKQ23550p1Qk9Xpn7K7QVfWY25dLLQ/viewform?usp=sf_link)
  - Modules will be assigned to be as evenly distributed across the class as possible, keeping in mind your preferences.
  - Once you are assigned a Module, you will be told the approximate date when your presentation will be. (Since the lecture material moves around as the course progresses, the presentation dates might move as well.) 
- [1 pt] **Find a recent paper** (published within the past 5 years) from a reputable AI conference or journal. Your selection should be submitted to Lara & Aydin a week before your presentation & summary are due so that we can verify that your choice is a peer-reviewed article that is relevant to the Module. When you submit your selection, you will provide 1) the name of the article, 2) the authors of the article, 3) the link where the article can be found online, and 4) what class topic (i.e., lesson title) the article is relevant to.
- [5 pts] **Summarize** the paper in a 1-page report. Please include, _in your own words_:
  - what are the main findings of the paper?
  - how does the paper relate to the class?
  - what are the strengths of the paper?
  - what are the weaknesses of the paper?
  - are there any ethical concerns that people should consider if they were to replicate the paper or use any of the methods/data/etc. that are introduced in the paper?
  - (no points but required at the end of the summary) the names of anyone you talked to about the paper and/or how you used LLMs (if you did). Please see the [Generative AI Policy](#generative-ai-policy) for more information on how to cite LLM use. If you did not receive any help, please state that instead.
- [1 pt] **Present what you learned from the paper** to small groups in class. You're welcome to create a few slides to help you present to your group, but this is not required. We will take abou 10 minutes talking in separate groups and then 5 minutes coming together to share with the whole class.
- 7 points total

### Generative AI Policy

If you use ChatGPT (or similar chatbots or AI-based generation tools), you must describe exactly how you used it, including providing the prompt, the original generation, and your edits. This applies to prose, code, or any form of content creation. Not disclosing is an academic integrity violation. If you do disclose, your answer may receive anywhere from 0 to full credit, depending on the extent of substantive edits, achievement of the [learning objectives](#learning-objectives), and overall circumvention of those objectives.

Use of AI/automatic tools for grammatical assistance (such as spell-checkers or Grammarly) or small-scale predictive text (e.g., next word prediction, tab completion) is okay. Provided the use of these tools does not change the substance of your work, use of these tools may be, but is not required to be, disclosed.

### What to Submit

1. [Fill out this form](https://docs.google.com/forms/d/e/1FAIpQLSfaVh0jst-vw9b7iJlOqKQ23550p1Qk9Xpn7K7QVfWY25dLLQ/viewform?usp=sf_link), choosing what Module(s) you would like to present from --- due 9/8 at 11:59PM ET for everyone in the class.
2. The summary, due 3PM the night before your presentation day. [Submission link](https://blackboard.umbc.edu/ultra/courses/_76209_1/outline/assessment/test/_6357062_1?courseId=_76209_1)
3. No submission, but: Be prepared to discuss what you learned in class on your assigned presentation day.


{% if page.readings %} 
## Recommended Readings
{% for reading in page.readings %}
* {{ reading.authors }}, <a href="{{ reading.url }}">{{ reading.title }}</a>.  <i>{{ reading.note }}</i>
{% endfor %}
{% endif %}
