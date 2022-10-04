# Lecture 20: Algorithmic Analysis 

We will learn how to calculate p-values first. 

## Calculating p-values using bootstrapping 

Say we have two different distributions (lists of scalars). A big question is: what is the difference between the two distributions? We might try finding the difference in means. But there are obvious problems that come along if our sample size isn't enough. For example, we may have samples from the same distribution that just happened to have different means. So we probe a little bit further. 

### Problem set up 

Given two lists: e.g.: 
1. $[1,2,3,4,4,1,2,3,4,5]$
2. $[23,224,24,2,4,2,3]$

These numbers were sampled from some distribution(s). The question is: did we get these samples by sampling from the same distribution or two different distributions? That is what the p-value aims to figure out. 

Calculate the means: 

1. mean: $2.9$. 
2. mean: $40.285714285714$. 

p-value asks: what is the probability that 1 and 2 means were drawn from the *same* distribution. 

> p-values are numbers, between $\mathbf{0}$ and $\mathbf{1}$, that, in
this example, quantify how confident we should be that distribution $\mathbf{1}$ was drawn from a different distribution than the one distribution $\mathbf{2}$ was drawn from just based on the observed data and statistic s(mean in this specific example). 

> if $p$ is close to 0, then we are more confident they are different. 

- Watch [this](https://www.youtube.com/watch?v=vemZtEM63GY) video for a more detailed explanation on the problem setup. 

So hiw to calculate? We can use bootstrapping! 

## Calculating p-values 

We use bootstrapping here via repeated sampling. 

First, take the two distributions and jot down the initial difference between the means (or whatever relevant statistic you are calculating). 
1. Concatenate together the two sample lists to make one universal distribution, $U$. 
2. Iterate at least $10,000$ times and at each iteration, sample from $U$ (appropriate lengths) twice: one for group A and one for group B. 
3. Say you want to calculate the difference in means (called effect size). Take abs(diff between means). Append this to a master list which gets all the effect sizes for the iterations. 
4. Also, at each iteration, calculate whether the effect size between the current sample means is greater than the initial effect size. If so, add to a counter. 
5. At the end, take the counter value and divide it by the total number of iterations. This is your p-value. 

## Algorithmic analysis 

We now get into the heart of this lecture and the last topic in uncertainty theory. Recall that expectation is the weighted average of a rich random variable distribution. Also recall an important fact about expectation:  

> Expectation of sums is sum of expectations: $$E[X+Y]=E[X]+E[Y].$$

- Importantly, the above statement holds regardless of dependency between the components. 
- 