# Lecture 17: Adding Random Variables 

> Goals: 
> - Learn how to add random variables from the same parametric distribution. 
> - Derive from first principle how to add random variables more generally. 

We start with a new definition: 

> - **Definition (i.i.d. random variables):** Consider $n$ random variables $X_{1}, X_{2}, \ldots X_{n}$. These random variables are considered iid if each random variable has the same probability distribution (same PMF or PDF) as the others and are all mutually independent. This implies expectation and variance are the same. 

- Special note: by "same PDF/PMF", we literally mean that the written out form must be identical. Specifically, the must all come from the same parametric distribution family and on top of that, have the *exact same parameters*. 
- Why is this important: because we may have some real world scenario where we need to have a ton of different RVs but they should all be the same distribution (and so they can all take on different values when the experiment is brought to life). 
- Making this assumption is vital and allows us to solve more complicated problems efficiently. Used in ML a lot! 
- **Example of iid**: Let $X_{i} \sim \operatorname{Exp}(\lambda)$ where each $X_{i}$ is independent of the other random variables. 
- **Example (1) of non-iid**: Let $X_{i} \sim \operatorname{Exp}\left(\lambda_{i}\right)$ where each $X_{i}$ is independent of the other random variables. Notice how the RVs have different parameters?! So they are not iid. 
- **Example (2) of non-iid**: Let $X_{i} \sim \operatorname{Exp}(\lambda)$ where $X_{1}=X_{2}=\cdots=X_{n}$. Not iid because each RV is conditionally dependent on the other. So all RVs that are equal to each other are not in fact not iid. 

Now we begin our real study of uncertainty theory. We start out by asking "how do we add random variables"? 

## Adding random variables from first principle 

Note: the variables must be **independent** to add them. Question: do they need to be from the same family as well then?  

Let us derive from first principles how one might add two random variables. Let $X$ and $Y$ be iid discrete random variables. We want to find $\mathrm{P}(X+Y=n)$. We start by realizing that this is equivalent to $\mathrm{P}(X=i, Y=n-i)$ for some $i \in \mathbb{N}$. How so? For example, let $i=3$ for  $\mathrm{P}(X+Y=n)$. Plugging in, we obtain this: $3+Y=n \rightarrow Y = n - 3$. Now we can repeat this idea for any $i$ and obtain the whole PMF for $X+Y$!: 

$$
\mathrm{P}(X+Y=n)=\sum_{i=-\infty}^{\infty} \mathrm{P}(X=i, Y=n-i).
$$

This repeated process is called a **convolution** (see [here](https://www.youtube.com/watch?v=zbu8KQx9bqM) and [here](https://www.youtube.com/watch?v=kwtf4WxjPKA&list=PLeB45KifGiuHesi4PALNZSYZFhViVGQJK&index=24&t=204s) for more discussion) of discrete random variables. So convolution corresponds to addition which, by extenson, allows us to form linear combinations (linear transforms). 

The continious version of this is defined as 

$$
f(X+Y=n)=\int_{i=-\infty}^{\infty} f(X=n-i, Y=i) d i.
$$ 

## Adding parametric random variables 

We are in luck. In practice, we generally won't need to compute the convolution between two distributions if the RVs are from the families of distributions we know about: these families already have their sums derived! 

See the course reader for the equations. 

I will add some of my own thoughts and examples here. 

- **Example:** here is an intuitive example. We have two groups of people
	- P1: 50 people, each independently infected with $p=0.1$
	- P2: 100 people, each independently infected with $p=0.4$ 
	- Question: Probability of more than 40 infections?
		- Solution: your first thought is probably to define two binomial random variables and just add them. Let $P_1 \sim bin(50,0.1)$ and let $P_1 \sim bin(100,0.4)$. But we have a problem. We can't add binomials with different probability parameters (see course reader equation definitions)! So what we do now? We **approximate the binomials with normals**!!!  
		- The key point here is that you should try to rearrange your problem to get it in terms of something you know how to work with. 
		- Though remember to perform continuinty correction when tranforming from the discrete to continious realm. 
- I want to stress that adding RVs is an important problem solving strategy. When given questions of the form above, you can try to break it down and solve it from first principles. But if you just realize that you can split it up into two RVs and sum them up, it becomes easier. This gives us some nostolgia from when we first discussed RVs; why did we introduce them to begin with? Because it made it significantly easier to work with some core probability problems! 


- **Remark:** Say we have some random variable, $X$. What is $2X$? Hold your horses. It is not like what we did above. In fact, this is an invalid expression. Can you picture why? Because $X$ is not independent from itself! So instead, we must use a **linear transform**. 
- **Remark:** subtraction is just addition by linear transforming the second part of the expression with -1 first. So $X-Y=X+(-1Y)=X+(-Y)$. 