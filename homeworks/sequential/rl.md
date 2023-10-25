---
layout: default
img: 
img_link: 
caption: 
title: Reinforcement Learning
type: Homework
number: 3
active_tab: homework
release_date: 2023-10-26
due_date: 2023-11-14 23:59:00EST
materials:
    - 
        name: *new* Pac-Man files (zip)
        url: https://laramartin.net/Principles-of-AI/homeworks/sequential/hw3-pacman-files.zip

readings:
    -
        title: AIMA Chapter 
        authors: Peter Norvig and Stuart J. Russell

submission_link: 
---

<h2>Homework 3: Reinforcement Learning in Pac-Man (10%)</h2>

<div class="alert alert-warning" markdown="1">
<b>IMPORTANT:</b> You are <b>not</b> allowed to use ChatGPT or any other LLMs for this assignment.<br><br>
Due {{page.due_date | date: "%B %-d, %Y at %r"}}
on <a href="{{page.submission_link}}">Blackboard</a>.<br><br>
Materials: 
{% for material in page.materials %}
<a href="{{material.url}}">{{material.name}}</a><br>
{% endfor %}

</div>

<blockquote>
    <center>
      <img src="capsule.png" width="50%"/>
    </center>
      <p><cite></cite></p>
</blockquote>

<h3>Learning Objectives</h3>
In this assignment, you will
<ul>
    <li></li>
</ul>

<h3>Introduction</h3>

<p>In this project, you will implement value iteration and Q-learning. You will test your agents first on Gridworld (from class), then apply them to a simulated robot controller (Crawler) and Pacman.</p>
      <p>Like Project 1, this project includes an autograder for you to grade your solutions on your machine. This can be run on all questions with the command:</p>
      <pre>python autograder.py</pre>
      <p>It can be run for one particular question, such as q2, by:</p>
      <pre>python autograder.py -q q2</pre>
      <p>It can be run for one particular test by commands of the form:</p>
      <pre>python autograder.py -t test_cases/q2/1-bridge-grid</pre>
      <p></p>
      <table class="intro" border="0" cellpadding="10">
        <tbody>
          <tr>
            <td colspan="2"><b>Files you'll edit:</b></td>
          </tr>
          <tr>
            <td><code><a href="code/valueIterationAgents.py">valueIterationAgents.py</a></code></td>
            <td>A value iteration agent for solving known MDPs.</td>
          </tr>
          <tr>
            <td><code><a href="code/qlearningAgents.py">qlearningAgents.py</a></code></td>
            <td>Q-learning agents for Gridworld, Crawler and Pacman.</td>
          </tr>
          <tr>
            <td><code><a href="code/analysis.py">analysis.py</a></code></td>
            <td>A file to put your answers to questions given in the project.</td>
          </tr>
          <tr>
            <td colspan="2"><b>Files you should read but NOT edit:</b></td>
          </tr>
          <tr>
            <td><code><a href="code/mdp.py">mdp.py</a></code></td>
            <td>Defines methods on general MDPs.</td>
          </tr>
          <tr>
            <td><code><a href="code/learningAgents.py">learningAgents.py</a></code></td>
            <td>Defines the base classes <code>ValueEstimationAgent</code> and <code>QLearningAgent</code>, which your agents will extend.</td>
          </tr>
          <tr>
            <td><code><a href="code/util.py">util.py</a></code></td>
            <td>Utilities, including <code>util.Counter</code>, which is particularly useful for Q-learners.</td>
          </tr>
          <tr>
            <td><code><a href="code/gridworld.py">gridworld.py</a></code></td>
            <td>The Gridworld implementation.</td>
          </tr>
          <tr>
            <td><code><a href="code/featureExtractors.py">featureExtractors.py</a></code></td>
            <td>Classes for extracting features on (state,action) pairs. Used for the approximate Q-learning agent (in qlearningAgents.py).</td>
          </tr>
          <tr>
            <td colspan="2"><b>Files you can ignore:</b></td>
          </tr>
          <tr>
            <td><code><a href="code/environment.py">environment.py</a></code></td>
            <td>Abstract class for general reinforcement learning environments. Used by <code><a href="code/gridworld.py">gridworld.py</a></code>.</td>
          </tr>
          <tr>
            <td><code><a href="code/graphicsGridworldDisplay.py">graphicsGridworldDisplay.py</a></code></td>
            <td>Gridworld graphical display.</td>
          </tr>
          <tr>
            <td><code><a href="code/graphicsUtils.py">graphicsUtils.py</a></code></td>
            <td>Graphics utilities.</td>
          </tr>
          <tr>
            <td><code><a href="code/textGridworldDisplay.py">textGridworldDisplay.py</a></code></td>
            <td>Plug-in for the Gridworld text interface.</td>
          </tr>
          <tr>
            <td><code><a href="code/crawler.py">crawler.py</a></code></td>
            <td>The crawler code and test harness. You will run this but not edit it.</td>
          </tr>
          <tr>
            <td><code><a href="code/graphicsCrawlerDisplay.py">graphicsCrawlerDisplay.py</a></code></td>
            <td>GUI for the crawler robot.</td>
          </tr>
          <tr>
            <td><code><a href="code/autograder.py">autograder.py</a></code></td>
            <td>Project autograder</td>
          </tr>
          <tr>
            <td><code><a href="code/testParser.py">testParser.py</a></code></td>
            <td>Parses autograder test and solution files</td>
          </tr>
          <tr>
            <td><code><a href="code/testClasses.py">testClasses.py</a></code></td>
            <td>General autograding test classes</td>
          </tr>
          <tr>
            <td><code>test_cases/</code></td>
            <td>Directory containing the test cases for each question</td>
          </tr>
          <tr>
            <td><code><a href="code/reinforcementTestClasses.py">reinforcementTestClasses.py</a></code></td>
            <td>HW 3 specific autograding test classes</td>
          </tr>
        </tbody>
      </table>
      <p></p>
      <p><strong>Files to Edit and Submit:</strong> You will fill in portions of <code><a href="code/valueIterationAgents.py">valueIterationAgents.py</a></code>, <code><a href="code/qlearningAgents.py">qlearningAgents.py</a></code>, and <code><a href="code/analysis.py">analysis.py</a></code> during the assignment. You should submit these files with your code and comments. Please <em>do not</em> change the other files in this distribution or submit any of our original files other than these files.</p>

</p><p><strong>Evaluation:</strong> Your code will be autograded for technical
correctness, using the same autograder and test cases you are provided with. Please <em>do not</em> change the names of any provided functions or classes within the code, or you will wreak havoc on the autograder. You should ensure your code passes all the test cases before submitting the solution, as we will not give any points for any questions if not all the test cases for it pass. <em>However</em>, the correctness of your implementation -- not the autograder's judgements -- will be the final judge of your score. Even if your code passes the autograder, we reserve the right to check it for mistakes in implementation, though this should only be a problem if your code takes too long or you disregarded announcements regarding the homework.

</p>

<p><strong>Collaboration:</strong> You <em>are</em> allowed to collaborate in pairs on this homework Please make sure both of your names are in the zip file name and that you are in a group together for the assignment on Blackboard.</p>

<p><strong>Academic Dishonesty:</strong> We will be checking your code against other submissions in the class for logical redundancy. If you copy someone
else/another pair's code and submit it with minor changes, we will know. We trust you all to
submit your own work only; <em>please</em> don't let us down. Likewise, <em>do not</em> attempt to write your code specifically to pass the autograder's tests. Either copying or trying to cheat the autograder will be considered violations of the student honor code.

</p><p><strong>Getting Help:</strong> You are not alone!  If you find yourself stuck on something, contact the course staff for help.  Office hours and Slack are there for your support; please use them.  If you can't make our office hours, let us know and we will schedule more.  We want these homeworks to be rewarding and instructional, not frustrating and demoralizing.  But, we don't know when or how to help unless you ask.
    
</p>


<h3> MDPs</h3>


 
<h3> What to Submit </h3>
    <p> Zip only the files you altered for this assignment as a .zip <b> named with the first letter of your first name, your last name, and homework number</b> (example: lmartin_hw1.zip) and submit it on Blackboard before the due date. If you are submitting as a pair, please label the file with both of your last names and the homework number (example: martin_ayanzadeh_hw1.zip).
    <br>
    <a href="{{page.submission_link}}">Submission link</a>
    </p>

    <p> <i>Important:</i> Please re-download your submission and ensure all files run as intended. We will not entertain regrade requests for submitting the wrong files.</p>
    
    





<div class="alert alert-warning" markdown="1">
<h3> Grading Summary</h3>
- Question 1 - 2 points
- Question 2 - 2 points
- Question 3 - 2 points
- Question 4 - 3 points
- Question 5 - 2 points
- Extra credit - 2 points max

</div>



