---
layout: default
img: wampa-world.png
img_link: 
caption: Wampa World
title: Logical Agents
type: Homework
number: 2
active_tab: homework
release_date: 2023-09-31
due_date: 2023-10-10 23:59:00EST
materials:
    - 
        name: HW2-LogicalAgents.ipynb
        url: https://laramartin.net/Principles-of-AI/homeworks/logic/HW2-LogicalAgents.ipynb

readings:
    -
        title: AIMA Chapter 7
        authors: Peter Norvig and Stuart J. Russell

submission_link: https://blackboard.umbc.edu/ultra/courses/_76209_1/outline/assessment/test/_6357099_1?courseId=_76209_1
---

<h2>Homework 2: Hunt the Wampa (10%)</h2>

<div class="alert alert-warning" markdown="1">
Due {{page.due_date | date: "%B %-d, %Y at %r"}}
on <a href="{{page.submission_link}}">Blackboard</a>.<br><br>
Materials: 
{% for material in page.materials %}
<a href="{{material.url}}">{{material.name}}</a><br>
{% endfor %}

</div>


<h3>Learning Objectives</h3>
In this assignment, you will:
<ul>
    <li>
    Combine propositional logic rules to create an inference algorithm that can successfully guide the agent (the robot R2-D2) toward its goal</li>
    <li>Implement a way to populate the agent's knowledge base
   <li> Analyze the consequences of different propositional logic rules on the agent's decision-making process</li>
   <li> Evaluate the effectiveness of your inference algorithm in guiding the agent's behavior in different Wampa World scenarios</li>
</ul>

### Part 1: Implement the agent
1.    [3 points] Implement the knowledgeBase() function in the Agent class
2.    [10 points] Implement the inferenceAlgorithm() function in the Agent class
3.    For a successful path for each scenario, report
      a. [5 points] the agent's actions & percepts
      b. [10 points] the logic at each step

### Part 2: Analyze it (Answer in natural language)
4. [3 points] For any of the scenarios, were there any steps where the agent could have used a different logic rule and have still succeeded? If so, would the path have differed? If not, why not?
5. [2 points] Which scenario required the most actions to solve?
6. [2 points] How efficient was your agent? Was there a shorter path available that it didn't take?
7. [1 point] Were there any points where the agent was navigating "blindly" (i.e., without any information about a particular square)? Where?
8. [3 points] Where might you use a logical agent like this in the real world?
9. [5 points] How does a logical agent like this compare to a search agent?
10. [5 points] Could you integrate a search algorithm into this agent? If so, how? If not, why not?

### Part 3: Feedback (Answer in natural language)
11. [1 point] Approximately how long did you spend on this assignment?
12. [1 point] Which aspects of this assignment did you find most challenging? Were there any significant stumbling blocks?
13. [1 point] Which aspects of this assignment did you like? Is there anything you would have changed?

 
<h3> What to Submit </h3>
   Create a zip with your ipynb file and a pdf with the answers to Questions 3-13 <b> named with the first letter of your first name, your last name, and homework number</b> (example: lmartin_hw1.zip) and submit it on Blackboard before the due date. If you are submitting as a pair, please label the file with both of your last names and the homework number (example: martin_ayanzadeh_hw1.zip).
    <br>
    <a href="{{page.submission_link}}">Submission link</a>
  


<div class="alert alert-warning" markdown="1">
<h3> Grading Summary</h3>
- Part 1 - 28 points
- Part 2 - 21 points
- Part 3 - 3 points

</div>



