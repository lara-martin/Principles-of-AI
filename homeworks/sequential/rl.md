---
layout: default
img: 
img_link: 
caption: 
title: Reinforcement Learning in GridWorld & Pac-Man
type: Homework
number: 3
active_tab: homework
release_date: 2023-10-26
due_date: 2023-11-14 23:59:00EST
materials:
    - 
        name: GridWorld/Pac-Man files (zip)
        url: https://laramartin.net/Principles-of-AI/homeworks/sequential/hw3-pacman-files.zip

readings:
    -
        title: AIMA Chapter 22
        authors: Peter Norvig and Stuart J. Russell

submission_link: https://blackboard.umbc.edu/ultra/courses/_76209_1/grades/assessment/test/_6357100_1?courseId=_76209_1

---

<h2>Homework 3: Reinforcement Learning in GridWorld & Pac-Man (10%)</h2>

<div class="alert alert-warning" markdown="1">
<b>IMPORTANT:</b> Please list any outside resources (i.e., beyond the textbook, instructor, or TA). If you did not use any outside resources, please state this clearly when you submit your assignment. If we do not see any such statement, we will take off 1 point (out of 20).<br><br>
Due {{page.due_date | date: "%B %-d, %Y at %r"}}
on <a href="{{page.submission_link}}">Blackboard</a>.<br><br>
Materials: 
{% for material in page.materials %}
<a href="{{material.url}}">{{material.name}}</a><br>
{% endfor %}
<br><br>
Related Readings:
{% for reading in page.readings %}
{{reading.title}} by {{reading.authors}}<br>
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
    <li>Synthesize a policy by running value iteration</li>
    <li>Implement a Q-learning agent</li>
    <li>Perform epsilon-greedy action selection</li>
</ul>

<h3>Introduction</h3>

<p>In this homework, you will implement value iteration and Q-learning. You will test your agents first on GridWorld (from class), then apply them to a simulated robot controller (Crawler) and Pac-Man.</p>
<p>Like homework 1, this homework includes an autograder for you to grade your solutions on your machine. This can be run on all questions with the command:</p>
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
    <td>Q-learning agents for GridWorld, Crawler and Pac-Man.</td>
  </tr>
  <tr>
    <td><code><a href="code/analysis.py">analysis.py</a></code></td>
    <td>A file to put your answers to questions given in the homework</td>
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
    <td>The GridWorld implementation.</td>
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
    <td>GridWorld graphical display.</td>
  </tr>
  <tr>
    <td><code><a href="code/graphicsUtils.py">graphicsUtils.py</a></code></td>
    <td>Graphics utilities.</td>
  </tr>
  <tr>
    <td><code><a href="code/textGridworldDisplay.py">textGridworldDisplay.py</a></code></td>
    <td>Plug-in for the GridWorld text interface.</td>
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
    <td>Homework autograder</td>
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

<p><strong>Evaluation:</strong> Your code will be autograded for technical
correctness, using the same autograder and test cases you are provided with. Please <em>do not</em> change the names of any provided functions or classes within the code, or you will wreak havoc on the autograder. You should ensure your code passes all the test cases before submitting the solution, as we will not give any points for any questions if not all the test cases for it pass. <em>However</em>, the correctness of your implementation -- not the autograder's judgements -- will be the final judge of your score. Even if your code passes the autograder, we reserve the right to check it for mistakes in implementation, though this should only be a problem if your code takes too long or you disregarded announcements regarding the homework.
</p>

<p><strong>Collaboration:</strong> You <em>are</em> allowed to collaborate in pairs on this homework. Please make sure both of your names are in the zip file name and that you are in a group together for the assignment on Blackboard.</p>

<p><strong>Academic Dishonesty:</strong> We will be checking your code against other submissions in the class for logical redundancy. If you copy someone
else/another pair's code and submit it with minor changes, we will know. We trust you all to
submit your own work only; <em>please</em> don't let us down. Likewise, <em>do not</em> attempt to write your code specifically to pass the autograder's tests. Either copying or trying to cheat the autograder will be considered violations of the student honor code.

</p><p><strong>Getting Help:</strong> You are not alone!  If you find yourself stuck on something, contact the course staff for help.  Office hours and Slack are there for your support; please use them.  If you can't make our office hours, let us know and we will schedule more.  We want these homeworks to be rewarding and instructional, not frustrating and demoralizing.  But, we don't know when or how to help unless you ask.
    
</p>


<h3> MDPs</h3>
  <p>To get started, run GridWorld in manual control mode, which uses the arrow keys:</p>
  <pre>python gridworld.py -m</pre>
  <p>You will see the two-exit layout from class. The blue dot is the agent. Note that when you press <em>up</em>, the agent only actually moves north 80% of the time. Such is the life of a GridWorld agent!</p>
  <p>You can control many aspects of the simulation. A full list of options is available by running:</p>
  <pre>python gridworld.py -h</pre>
  <p>The default agent moves randomly</p>
  <pre>python gridworld.py -g MazeGrid</pre>
  <p>You should see the random agent bounce around the grid until it happens upon an exit. Not the finest hour for an AI agent.</p>
  <p><em>Note:</em> The GridWorld MDP is such that you first must enter a pre-terminal state (the double boxes shown in the GUI) and then take the special 'exit' action before the episode actually ends (in the true terminal state called <code>TERMINAL_STATE</code>, which is not shown in the GUI). If you run an episode manually, your total return may be less than you expected, due to the discount rate (<code>-d</code> to change; 0.9 by default).</p>
  <p>Look at the console output that accompanies the graphical output (or use <code>-t</code> for all text). You will be told about each transition the agent experiences (to turn this off, use <code>-q</code>).</p>
  <p>As in Pac-Man, positions are represented by <code>(x,y)</code> Cartesian coordinates and any arrays are indexed by <code>[x][y]</code>, with <code>'north'</code> being the direction of increasing <code>y</code>, etc. By default, most transitions will receive a reward of zero, though you can change this with <code>-r</code>.</p>

<h3><a name="Q1"></a>Question 1 (6 points): Value Iteration</h3>
<p>Write a value iteration agent in <code>ValueIterationAgent</code>, which has been partially specified for you in <code>valueIterationAgents.py</code>. Your value iteration agent is an offline planner, not a reinforcement learning agent, and so the relevant training option is the number of iterations of value iteration it should run (option <code>-i</code>) in its initial planning phase. <code>ValueIterationAgent</code> takes an MDP on construction and runs value iteration for the specified number of iterations before the constructor returns.</p>
<p>Value iteration computes k-step estimates of the optimal values, V<sub>k</sub>. In addition to running value iteration, implement the following methods for <code>ValueIterationAgent</code> using V<sub>k</sub>.</p>
<ul>
<li><code>computeActionFromValues(state)</code> computes the best action according to the value function given by <code>self.values</code>.</li>
<li><code>computeQValueFromValues(state, action)</code> returns the Q-value of the (state, action) pair given by the value function given by <code>self.values</code>.</li>
</ul>
<p>These quantities are all displayed in the GUI: values are numbers in squares, Q-values are numbers in square quarters, and policies are arrows out from each square.</p>
<!--<p><em>Important:</em> Use the "batch" version of value iteration where each vector V<sub>k</sub> is computed from a fixed vector V<sub>k-1</sub> (like in lecture), not the "online" version where one single weight vector is updated in place. This means that when a state's value is updated in iteration k based on the values of its successor states, the successor state values used in the value update computation should be those from iteration k-1 (even if some of the successor states had already been updated in iteration k). The difference is discussed in the Sutton &amp; Barto AI textbook in the 6th paragraph of chapter 4.1.</p>-->
<p><em>Note:</em> A policy synthesized from values of depth k (which reflect the next k rewards) will actually reflect the next k+1 rewards (i.e. you return 
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>&#x03C0;<!-- π --></mi>
    <mrow class="MJX-TeXAtom-ORD">
      <mi>k</mi>
      <mo>+</mo>
      <mn>1</mn>
    </mrow>
  </msub>
</math>). Similarly, the Q-values will also reflect one more reward than the values (i.e. you return Q<sub>k+1</sub>).</p>
<p>You should return the synthesized policy
    <math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mi>&#x03C0;<!-- π --></mi>
    <mrow class="MJX-TeXAtom-ORD">
      <mi>k</mi>
      <mo>+</mo>
      <mn>1</mn>
    </mrow>
  </msub>
</math>.</p>
<p><em>Hint:</em> Use the <code>util.Counter</code> class in <code>util.py</code>, which is a dictionary with a default value of zero. Methods such as <code>totalCount</code> should simplify your code. However, be careful with <code>argMax</code>: the actual argmax you want may be a key not in the counter!</p>
<p><em>Note:</em> Make sure to handle the case when a state has no available actions in an MDP (think about what this means for future rewards).</p>
<p>To test your implementation, run the autograder:</p>
<pre>python autograder.py -q q1</pre>
<p>The following command loads your <code>ValueIterationAgent</code>, which will compute a policy and execute it 10 times. Press a key to cycle through values, Q-values, and the simulation. You should find that the value of the start state (<code>V(start)</code>, which you can read off of the GUI) and the empirical resulting average reward (printed after the 10 rounds of execution finish) are quite close.</p>
<pre>python gridworld.py -a value -i 100 -k 10</pre>
<p><em>Hint:</em> On the default BookGrid, running value iteration for 5 iterations should give you this output:</p>
<pre>python gridworld.py -a value -i 5</pre>
<center><img src="./value.png" width="50%" alt="value iteration with k=5"></center>
<p><em>Grading:</em> Your value iteration agent will be graded on a new grid. We will check your values, Q-values, and policies after fixed numbers of iterations and at convergence (e.g. after 100 iterations).</p>


<h3><a name="Q2"></a>Question 2 (1 point): Bridge Crossing Analysis</h3>
<p><code>BridgeGrid</code> is a grid world map with the a low-reward terminal state and a high-reward terminal state separated by a narrow "bridge", on either side of which is a chasm of high negative reward. The agent starts near the low-reward state. With the default discount of 0.9 and the default noise of 0.2, the optimal policy does not cross the bridge. Change only ONE of the discount and noise parameters so that the optimal policy causes the agent to attempt to cross the bridge. Put your answer in <code>question2()</code> of <code>analysis.py</code>. (Noise refers to how often an agent ends up in an unintended successor state when they perform an action.) The default corresponds to:</p>
<pre>python gridworld.py -a value -i 100 -g BridgeGrid --discount 0.9 --noise 0.2</pre>
<center><img src="./value-q2.png" width="50%" alt="value iteration with k=100"></center>
<p><em>Grading:</em> We will check that you only changed one of the given parameters, and that with this change, a correct value iteration agent should cross the bridge. To check your answer, run the autograder:</p>
<pre>python autograder.py -q q2</pre>

<h3><a name="Q3"></a>Question 3 (5 points): Policies</h3>
<p>Consider the <code>DiscountGrid</code> layout, shown below. This grid has two terminal states with positive payoff (in the middle row), a close exit with payoff +1 and a distant exit with payoff +10. The bottom row of the grid consists of terminal states with negative payoff (shown in red); each state in this "cliff" region has payoff -10. The starting state is the yellow square. We distinguish between two types of paths: (1) paths that "risk the cliff" and travel near the bottom row of the grid; these paths are shorter but risk earning a large negative payoff, and are represented by the red arrow in the figure below. (2) paths that "avoid the cliff" and travel along the top edge of the grid. These paths are longer but are less likely to incur huge negative payoffs. These paths are represented by the green arrow in the figure below.</p>
<center><img src="./discountgrid.png" width="50%" alt="DiscountGrid"></center>
<p>In this question, you will choose settings of the discount, noise, and reward parameters for this MDP to produce optimal policies of several different types. Your setting of the parameter values for each part should have the property that, if your agent followed its optimal policy without being subject to any noise, it would exhibit the given behavior. If a particular behavior is not achieved for any setting of the parameters, assert that the policy is impossible by returning the string <code>'NOT POSSIBLE'</code>.</p>
<p>Here are the optimal policy types you should attempt to produce:</p>
<ol type="a"><ol type="a">
<li>Prefer the close exit (+1), risking the cliff (-10)</li>
<li>Prefer the close exit (+1), but avoiding the cliff (-10)</li>
<li>Prefer the distant exit (+10), risking the cliff (-10)</li>
<li>Prefer the distant exit (+10), avoiding the cliff (-10)</li>
<li>Avoid both exits and the cliff (so an episode should never terminate)</li>
</ol></ol>
<p></p>
<p>To check your answers, run the autograder:</p>
<pre>python autograder.py -q q3</pre>
<p><code>question3a()</code> through <code>question3e()</code> should each return a 3-item tuple of (discount, noise, reward) in <code>analysis.py</code>.</p>
<p><em>Note:</em> You can check your policies in the GUI. For example, using a correct answer to 3(a), the arrow in (0,1) should point east, the arrow in (1,1) should also point east, and the arrow in (2,1) should point north.</p>
<p><em>Note:</em> On some machines you may not see an arrow. In this case, press a button on the keyboard to switch to qValue display, and mentally calculate the policy by taking the arg max of the available qValues for each state.</p>
<p><em>Grading:</em> We will check that the desired policy is returned in each case.</p>

 <h3><a name="Q4"></a>Question 4 (5 points): Q-Learning</h3>
<p>Note that your value iteration agent does not actually learn from experience. Rather, it ponders its MDP model to arrive at a complete policy before ever interacting with a real environment. When it does interact with the environment, it simply follows the precomputed policy (e.g. it becomes a reflex agent). This distinction may be subtle in a simulated environment like a GridWorld, but it's very important in the real world, where the real MDP is not available.</p>
<p>You will now write a Q-learning agent, which does very little on construction, but instead learns by trial and error from interactions with the environment through its <code>update(state, action, nextState, reward)</code> method. A stub of a Q-learner is specified in <code>QLearningAgent</code> in <code>qlearningAgents.py</code>, and you can select it with the option <code>'-a q'</code>. For this question, you must implement the <code>update</code>, <code>computeValueFromQValues</code>, <code>getQValue</code>, and <code>computeActionFromQValues</code> methods.</p>
<p><em>Note:</em> For <code>computeActionFromQValues</code>, you should break ties randomly for better behavior. The <code>random.choice()</code> function will help. In a particular state, actions that your agent <em>hasn't</em> seen before still have a Q-value, specifically a Q-value of zero, and if all of the actions that your agent <em>has</em> seen before have a negative Q-value, an unseen action may be optimal.</p>
<p>With the Q-learning update in place, you can watch your Q-learner learn under manual control, using the keyboard:</p>
<pre>python gridworld.py -a q -k 5 -m</pre>
<p>Recall that <code>-k</code> will control the number of episodes your agent gets to learn. Watch how the agent learns about the state it was just in, not the one it moves to, and "leaves learning in its wake." Hint: to help with debugging, you can turn off noise by using the <code>--noise 0.0</code> parameter (though this obviously makes Q-learning less interesting). If you manually steer Pac-Man north and then east along the optimal path for four episodes, you should see the following Q-values: </p>
<center><img src="./q-learning.png" width="50%" alt="QLearning"></center>
<p></p>
<p><em>Grading:</em> We will run your Q-learning agent and check that it learns the same Q-values and policy as our reference implementation when each is presented with the same set of examples. To grade your implementation, run the autograder:</p>
<pre>python autograder.py -q q4</pre>

<h3><a name="Q5"></a>Question 5 (3 points): Epsilon Greedy</h3>
<p>Complete your Q-learning agent by implementing epsilon-greedy action selection in <code>getAction</code>, meaning it chooses random actions an epsilon fraction of the time, and follows its current best Q-values otherwise. Note that choosing a random action may result in choosing the best action - that is, you should not choose a random sub-optimal action, but rather <i>any</i> random legal action.</p>
<pre>python gridworld.py -a q -k 100 </pre>
<p>Your final Q-values should resemble those of your value iteration agent, especially along well-traveled paths. However, your average returns will be lower than the Q-values predict because of the random actions and the initial learning phase.</p>
<p>You can choose an element from a list uniformly at random by calling the <code>random.choice</code> function. You can simulate a binary variable with probability <code>p</code> of success by using <code>util.flipCoin(p)</code>, which returns <code>True</code> with probability <code>p</code> and <code>False</code> with probability <code>1-p</code>.</p>
<p>To test your implementation, run the autograder:</p>
<pre>python autograder.py -q q5</pre>
<p>With no additional code, you should now be able to run a Q-learning crawler robot:</p>
<pre>python crawler.py</pre>
<p>If this doesn't work, you've probably written some code too specific to the <code>GridWorld</code> problem and you should make it more general to all MDPs.</p>
<p>This will invoke the crawling robot from class using your Q-learner. Play around with the various learning parameters to see how they affect the agent's policies and actions. Note that the step delay is a parameter of the simulation, whereas the learning rate and epsilon are parameters of your learning algorithm, and the discount factor is a property of the environment.</p>

<h3><a name="Q6"></a>Question 6 (1 point <b>extra credit</b>): Bridge Crossing Revisited</h3>
<p>First, train a completely random Q-learner with the default learning rate on the noiseless BridgeGrid for 50 episodes and observe whether it finds the optimal policy.</p>
<pre>python gridworld.py -a q -k 50 -n 0 -g BridgeGrid -e 1</pre>
<p>Now try the same experiment with an epsilon of 0. Is there an epsilon and a learning rate for which it is highly likely (greater than 99%) that the optimal policy will be learned after 50 iterations? <code>question6()</code> in <code>analysis.py</code> should return EITHER a 2-item tuple of <code>(epsilon, learning rate)</code> OR the string <code>'NOT POSSIBLE'</code> if there is none. Epsilon is controlled by <code>-e</code>, learning rate by <code>-l</code>.</p>
<p><em>Note:</em> Your response should be not depend on the exact tie-breaking mechanism used to choose actions. This means your answer should be correct even if for instance we rotated the entire bridge grid world 90 degrees.</p>
<p>To grade your answer, run the autograder:</p>
<pre>python autograder.py -q q6</pre>

<h3><a name="Q7"></a>Question 7 (1 point <b>extra credit</b>): Q-Learning and Pac-Man</h3>
<p>Time to play some Pac-Man! Pac-Man will play games in two phases. In the first phase, <em>training</em>, Pac-Man will begin to learn about the values of positions and actions. Because it takes a very long time to learn accurate Q-values even for tiny grids, Pac-Man's training games run in quiet mode by default, with no GUI (or console) display. Once Pac-Man's training is complete, he will enter <em>testing</em> mode. When testing, Pac-Man's <code>self.epsilon</code> and <code>self.alpha</code> will be set to 0.0, effectively stopping Q-learning and disabling exploration, in order to allow Pac-Man to exploit his learned policy. Test games are shown in the GUI by default. Without any code changes you should be able to run Q-learning Pac-Man for very tiny grids as follows:</p>
<pre>python pacman.py -p PacmanQAgent -x 2000 -n 2010 -l smallGrid </pre>
<p>Note that <code>PacmanQAgent</code> is already defined for you in terms of the <code>QLearningAgent</code> you've already written. <code>PacmanQAgent</code> is only different in that it has default learning parameters that are more effective for the Pac-Man problem (<code>epsilon=0.05, alpha=0.2, gamma=0.8</code>). You will receive full credit for this question if the command above works without exceptions and your agent wins at least 80% of the time. The autograder will run 100 test games after the 2000 training games.</p>
<p><em>Hint:</em> If your <code>QLearningAgent</code> works for <code>gridworld.py</code> and <code>crawler.py</code> but does not seem to be learning a good policy for Pac-Man on <code>smallGrid</code>, it may be because your <code>getAction</code> and/or <code>computeActionFromQValues</code> methods do not in some cases properly consider unseen actions. In particular, because unseen actions have by definition a Q-value of zero, if all of the actions that <em>have</em> been seen have negative Q-values, an unseen action may be optimal. Beware of the argmax function from util.Counter!</p>
<p><em>Note:</em> To grade your answer, run:</p>
<pre>python autograder.py -q q7</pre>
<p><em>Note:</em> If you want to experiment with learning parameters, you can use the option <code>-a</code>, for example <code>-a epsilon=0.1,alpha=0.3,gamma=0.7</code>. These values will then be accessible as <code>self.epsilon, self.gamma</code> and <code>self.alpha</code> inside the agent.</p>
<p><em>Note:</em> While a total of 2010 games will be played, the first 2000 games will not be displayed because of the option <code>-x 2000</code>, which designates the first 2000 games for training (no output). Thus, you will only see Pac-Man play the last 10 of these games. The number of training games is also passed to your agent as the option <code>numTraining</code>.</p>
<p><em>Note:</em> If you want to watch 10 training games to see what's going on, use the command:</p>
<pre>python pacman.py -p PacmanQAgent -n 10 -l smallGrid -a numTraining=10</pre>
<p>During training, you will see output every 100 games with statistics about how Pac-Man is faring. Epsilon is positive during training, so Pac-Man will play poorly even after having learned a good policy: this is because he occasionally makes a random exploratory move into a ghost. As a benchmark, it should take between 1,000 and 1400 games before Pac-Man's rewards for a 100 episode segment becomes positive, reflecting that he's started winning more than losing. By the end of training, it should remain positive and be fairly high (between 100 and 350).</p>
<p>Make sure you understand what is happening here: the MDP state is the <em>exact</em> board configuration facing Pac-Man, with the now complex transitions describing an entire ply of change to that state. The intermediate game configurations in which Pac-Man has moved but the ghosts have not replied are <em>not</em> MDP states, but are bundled in to the transitions.</p>
<p>Once Pac-Man is done training, he should win very reliably in test games (at least 90% of the time), since now he is exploiting his learned policy.</p>
<p>However, you will find that training the same agent on the seemingly simple <code>mediumGrid</code> does not work well. In our implementation, Pac-Man's average training rewards remain negative throughout training. At test time, he plays badly, probably losing all of his test games. Training will also take a long time, despite its ineffectiveness.</p>
<p>Pac-Man fails to win on larger layouts because each board configuration is a separate state with separate Q-values. He has no way to generalize that running into a ghost is bad for all positions. Obviously, this approach will not scale.</p>


<h3> What to Submit </h3>
<p> Zip only the files you altered for this assignment as a .zip <b> named with the first letter of your first name, your last name, and homework number</b> (example: lmartin_hw1.zip) and submit it on Blackboard before the due date. If you are submitting as a pair, please label the file with both of your last names and the homework number (example: martin_ayanzadeh_hw1.zip).
<br>
<a href="{{page.submission_link}}">Submission link</a>
</p>


<div class="alert alert-warning" markdown="1">
<h3> Grading Summary</h3>
- Question 1 - 6 points
- Question 2 - 1 point
- Question 3 - 5 points
- Question 4 - 5 points
- Question 5 - 3 points
- Extra credit - 2 points max
</div>



