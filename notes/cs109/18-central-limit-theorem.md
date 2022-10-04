# Lecture 18: Central Limit Theorem 


We now begin study of the "fundamental theorem of probability"... one so important that we dedicate an entire lecture to it. The main premise that the summation of iid random variables forms a normal distribution no matter what the original distribution was for the random variables. Specifically, the sum of many iid random variables is itself a random variable that can take on different values at different probabilities (i.e. it is a random variable). Plotting this specific distribution will look normal. Astounding! 

- **Application example:** say we are given a problem where it involves summing/multiple iterations of something and we are asked the probability of something about that something. This should immediatly scream CLT (when you see a sum of *iid* random variables) no matter what the individual iid RVs were. 
	- **Example:** see slide 11 on lecture 18 slides 
	- It allows us to answer questions when we are summing up many different random variables. 

- Note that the CLT is extended to **average**: that is, the averages (expectation) of many random variables will follow a normal distribution. 


One day I plan to study the proof of this. Because it is quite an amazing result when you think of it. 

Note (**Inverse $\phi$**): often times you'll be asked to calculate the probability of things--fairly standard. But some times you might be asked to calculate a value for something that equates to a certain probability. This is just an equation where you must rearrange the PMF/PDF around. Specifically, it should be a system of one unknown and one equation. So why discuss this? Well for the CDF of a normal, you'll be left with the $\phi$ function. So we need to invert it somehow. This is given to us but I thought I'd make note that this is indeed a possible thing to do. 


## Sampling 

When we talk about sampling, what we mean is that we "instantiate" a random variable: we draw a sample from the dsitribution that is based on the probabilities of drawing each value the random variable can take on. 

Different types of sampling: 

![](attachments/Pasted%20image%2020220304034540.png)

- Data science is the science of making rigouros conclusions from dsitrubtions of samples. 

