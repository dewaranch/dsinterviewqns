# Probability Basics

Probability theory is the mathematical framework that allows us to analyze chance events in a logically sound manner. The probability of an event is a number indicating how likely that event will occur.

Note that when we say the probability of a head is $1/2$, we are not claiming that any sequence of coin tosses will consist of exactly $50$% heads. If we toss a fair coin ten times, it would not be surprising to observe $6$ heads and $4$ tails, or even $3$ heads and $7$ tails. But as we continue to toss the coin over and over again, we expect the long-run frequency of heads to get ever closer to $50$%. In general, it is important in statistics to understand the distinction between theoretical and empirical quantities. Here, the true (theoretical) probability of a head was $1/2$, but any realized (empirical) sequence of coin tosses may have more or less than exactly $50$% heads.

### Common Terminologies

The **sample space is the set of all possible outcomes in the experiment** : for a dice $Ω = {1, 2, 3, 4, 5, 6}$.

Any **subset of $Ω$ is a valid event**. we can speak of the event $F$ of rolling a $4$, $F = {4}$.

Consider the outcome of a single die roll, and call it $X$. A reasonable question one might ask is “What is the average value of $X$?". We define this notion of “average” as a weighted sum of outcomes. This is called the **expected value**, or expectation of $X$, denoted by $E(X)$, 

$Weighted Average = \frac{1}{6} * (1 + 2 + 3 + 4 + 5 + 6) = 3.5$

If you play the game $ \infty $ times the average value becomes $E(X)$

The **variance** of a random variable $X$ is a nonnegative number that summarizes on average how much $X$ differs from its mean, or expectation.
The square root of the variance is called the **standard deviation.**

$Var(X) = \frac{(1−3.5)^2+(2−3.5)^2+(3−3.5)^2+(4−3.5)^2+(5−3.5)^2+(6−3.5)^2}{6} = \frac{17.5}{6}$

### Set

A set, broadly defined, is a collection of objects. In the context of probability theory, we use set notation to specify compound events. For example, we can represent the event "roll an even number" by the set {2, 4, 6}.


### Permutation and Combination

It can be surprisingly difficult to count the number of sequences or sets satisfying certain conditions. This is where **Premutation and Combination** comes in. For example, consider a bag of marbles in which each marble is a different color. If we draw marbles one at a time from the bag without replacement, how many different ordered sequences (permutations) of the marbles are possible? How many different unordered sets (combinations)? 

- Permutation($AB \neq BA$ , order matters) = $nPr = \frac{n!}{(n-r)!}$
- Combination($AB = BA$ , order does not matter) = $nCr = \frac{n!}{r!(n-r)!}$





### Joint & Conditional Probability

- Joint Probability is the probability of 2 independent events occuring : $P(A \cap B) = P(A)*P(B)$
- Conditional probability tells the probability of B given A has occured, it allow us to account for information we have about our system of interest: $P(B|A) = \frac{P(A \cap B)}{P(A)}$

If both are same then A and B are independent events.

```{figure} ../Statistics/images/image1.PNG
---
height: 150px
name: image1
---
Baye's Theorem
```

$P(Banana|Long,Sweet,Yellow) = \frac{P(Long|Banana)*P(Sweet|Banana)*P(Yellow|Banana)*P(Banana)}{P(Long)*P(Sweet)*P(Yellow)}$


### Questions

```{admonition} Problem: Dice in increasing order
:class: tip, dropdown

**Asked By - UBER**

We throw 3 dice one by one. What is the probability that we obtain 3 points in strictly increasing order?

```

```{admonition} Solution:
:class: dropdown

Suppose we get $4$ in the first roll then,

Total Probability = $P(4) * P(5) * P(6) = 1/6 * 1/6 * 1/6 = 1/216$

Similarly for $3$,    $P(3) * P(4,5 | 4,6 | 5,6) = 1/6 * (1/36 + 1/36 + 1/36) = 3/216$

Taking into consideration $P(1)$ and $P(2)$ we have the total as $= 10/216 + 6/216 + 3/216 + 1/216 = 20/216$ 

```


```{admonition} Problem: Cards without replacement
:class: tip, dropdown

**Asked By - STATE FARM**

Pull $2$ cards from a deck without replacement what is probability that both are of different colors.

There can be many variants to this question.

```

```{admonition} Solution:
:class: dropdown
 
$52$ cards = $26$ Red + $26$ Black

- Different Color Without Replacement $= 26/52 * 26/51$
- Different Color With Replacement    $= 26/52 * 26/52$
- Same Color Without Replacement 	  $= 26/52 * 25/51$
- Same Color With Replacement    	  $= 26/52 * 25/52$
```

```{admonition} Problem: N Dice
:class: tip, dropdown

**Asked By - FACEBOOK**

Suppose you're playing a dice game. You have 2 die.

- What's the probability of rolling at least one 3?
- What's the probability of rolling at least one 3 given N die?
```

```{admonition} Solution:
:class: dropdown

P(at least 1 three) $=$ P(exactly 1 three) $+$  P(2 three) $= 1/6 * 5/6 + 5/6 * 1/6 + 1/36 = 11/36$

The second part of the question is a little tricky, let's start by generalizing the above equation:

P(at least 1 three) $= 2*(5^1/6^2) + 5^0/6^2$

Now for N dice: P(at least 1 three) $=$ P(exactly 1 three) $+$  P(2 three) $+$  P(3 three) ... $+$  P(N three)

Combining both $= N * \frac{5^{N-1}}{6^N} + N * \frac{5^{N-2}}{6^N} + N * \frac{5^{N-3}}{6^N} + ... + N * \frac{5^0}{6^N} = \frac{N}{6^N}(5^{N-1} + 5^{N-2} + .. + 1)$

```