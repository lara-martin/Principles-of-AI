---
layout: default
img: estimating_time.png
caption: Don't Panic
img_link: https://xkcd.com/1658/   
title: Project Proposal
type: Project Milestone
number: 1
active_tab: homework
release_date: 2023-11-03
due_date: 2023-10-16 23:59:00EST
---

<!-- Check whether the assignment is ready to release -->
{% capture today %}{{'now' | date: '%s'}}{% endcapture %}
{% capture release_date %}{{page.release_date | date: '%s'}}{% endcapture %}
{% if release_date > today %} 
<div class="alert alert-danger">
Warning: this assignment is out of date.  It may still need to be updated for this year's class.  Check with your instructor before you start working on this assignment.
</div>
{% endif %}
<!-- End of check whether the assignment is up to date -->


<!-- Check whether the assignment is up to date -->
{% capture this_year %}{{'now' | date: '%Y'}}{% endcapture %}
{% capture due_year %}{{page.due_date | date: '%Y'}}{% endcapture %}
{% if this_year != due_year %} 
<div class="alert alert-danger">
Warning: this assignment is out of date.  It may still need to be updated for this year's class.  Check with your instructor before you start working on this assignment.
</div>
{% endif %}
<!-- End of check whether the assignment is up to date -->


<div class="alert alert-info">
This assignment is due on {{ page.due_date | date: "%A, %B %-d, %Y" }} before {{ page.due_date | date: "%I:%M%p" }}. 
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


{{page.type}} {{page.number}}: {{page.title}}
=============================================================

The project is a chance for you to delve into one of the topics we have covered in class. You can **choose between two directions**: creating a novel AI system or answering a research question. For the direction that you choose, write a project proposal that answers the questions below. 

If you are trying to decide between multiple project ideas, or if you're struggling to come up with something, we highly encourage you to come to office hours and discuss it with the staff. We are experienced researchers and should be able to help you narrow down which ideas of yours are the most feasible + interesting.

## Build a novel AI system
Use the techniques we have learned in class to build a novel AI system. By the end of the semester, you should have a demo that runs either in Colab or a website showcasing your system.

Write a project proposal that includes the following sections:
1. __Project Description__(3 points): What novel AI system do you propose to design?
  - Give an example mockup of what the user experience will look like.
2. __Proposed Method__(3 points): How will you be using algorithms from class in order to create your system? Will you need to train an agent?
  - Write 2-3 paragraphs explaining your proposed method.
3. __Data__(3 points): What data will be needed to build your system?
  - Does the needed data already exist?  If so, how much data is available?
4. __Related work__(3 points): Do similar systems exist to the one you propose to create?
  - Give pointers to them and explain how you think they relate to your project idea.
5. __Team members__(1 point): Give a list of the students who will participate in this project, and what contribution you expect each person to make to the project.


## Attempt to answer an AI research question
By the end of the semester, you should have an academic paper that describes the research question, the experiments you ran to try and answer it, and an analysis of the experimental results.

Write a project proposal that includes the following sections:
1. __Project Description__ (3 points): What research question or problem are you trying to solve?
  - Write a problem definition (1 to 2 paragraphs)
  - Give an illustrative example of the problem and/or your proposed solution.
2. __Data__ (3 points): What kind of data will you need to train and evaluate your method?
  - Does the needed data already exist?  If so, how much data is available?
3. __Evaluation__ (3 points): What evaluation metrics do you plan to use to answer your research question?
4. __Related work__ (3 points): What previous research has been done on this research question?
  - Give pointers to several research papers that you think are relevant along with short explanations of how you think they relate to your project idea.
5. __Team members__ (1 point): Give a list of the students who will participate in this project, and what contribution you expect each person to make to the project.

# What to Submit
Submit to Gradescope:
* `proposal.pdf` which contains your project proposal. To make grading easier, your proposal should include section headers corresponding to each of the bulleted points as well. Latex is preferred but not required.


# Grading
<div class="alert alert-warning" markdown="1">
* Project Description - 3 points
* Proposed Method or Evaluation - 3 points
* Data - 3 points
* Related Work - 3 points
* Team Members - 1 point
</div>