# Constraint satisfaction problems

> This note covers the units in CS 221 for the CSP unit. 


## I. Overview 

> Search but incorporating problem structure into the model and focusing on modeling instead of inference. 

- Start of the variable-based models. 
- Heart is object called a **factor graph**. 
  - Will formally introduce them next lecture, but here is the general idea: 

 
::: {#def-default}
**(factor graphs (high-level overview))**: We are given a graphical model consisting of variables $X_1,...,X_n$ and factors (functions) $f_1,...,f_m$ where the factors defines how the variables relate to each other (in a graphical way): 
<p align='center'>
    <img alt="picture 1" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/1c1f4adf14a6be608537a8a6e00b7928dbb14b36f0b27079866946645e8992d6.png" width="300" />  
</p>

A solution to a variable-based model problem is an assignment to the variables (discrete or continious). 
:::

 

Here is an example: 

 
::: {#exm-default}
**(Map coloring)**: Given a map of Australia, color each of the provinces in red, green, or blue such that (the *constraint*) no two adjacent provinces have the same color. 

<p align='center'>
    <img alt="picture 2" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/32f641bcd187d2334296a037f9a5ca7efa327540545ba73feca3964ab5b600a6.png" width="300" />  
</p>
:::
 

To motivate factor graphs and CSP models, think about how we can solve this as a search problem. We can do it like this: 

<p align='center'>
    <img alt="picture 3" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/3ca33e985b3877691d8ae1fdf8a5363c77660f33d5a57cd03cc811c1f75bccb2.png" width="80%" />  
</p>

where each leaf node defines if it satisfies the conditions and each branch explores a potential solution path. 

 
 
:::{.callout-note appearance='simple'}
**Key realization**: the search problem doesn't encompass useful information about the problem structure. For example, in this case: 

- Variable ordering doesn't affect correctness, can optimize
- Variables are interdependent in a local way, can decompose. That is, we can solve Tasmania in isolation cuz its in the ocean and then re-combine at the end to solve the entire problem. Decompose problem into subproblems.

The key realization is that by incorporating the problem structure into our solution (which search fails to incorporate), we can *speed up* the algorithm solution. 
:::

### Variable-based models

- Algorithms:
  - Constraint satisfaction problems
  - Markov networks
  - Bayesian networks
- Key uniting factor:
  - Idea of a **variable**. 
- Variable-based models is just another term for probabilistic graphical models! 
- Theory is that variables are a higher-level (Python to assembly comparison) way to model a problems ❓. 
  - Ok... this is what this means: we focus on modeling and devote the cumbersome work to the inference algorithms which allows us to focus more on modeling (unlike search). Makes more of a general framework to solve different types of problems unlike search. 
  
<p align='center'>
    <img alt="picture 4" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/40ad2fb586b5444a3f648cbe537b932414218d301ae05a599720e72eaa343f0f.png" width="80%" />  
</p>


So just to summarize, the idea behind state-based models is that we model the problem as a factor graph (modeling) and then assign values to the variables (inference). 

**Example problems:**

- Vehicle routing: how to assign packages to trucks to deliver to customers. 
- Scheduling: when to schedule sports team to meet to minimize things like travel, availability of TV networks, etc. 
- School class scheduling 

The thing that is ubiqitious about this is that we aim to solve an isolated problem but with a set of constraints (hence, CSP). As you might imagine, CSP's are therefore very useful. 


**Roadmap**: 

<p align='center'>
    <img alt="picture 5" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/cc06b914f1d327a8f37c22f5171d2b6eb88ccfde7d54c9187508b1cdef86de3c.png" width="60%" />  
</p>


- Definitions
- Algorithms to solve CSP's 
- Approximations to speed up the exponential cost 


## II. Definitions 

From R&N: 

<p align='center'>
    <img alt="picture 6" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/abad59d0a4b3ad83c86242d7ccf009ff3019a06d202b098185c3eab82722b9ef.png" width="90%" />  
</p>


To-do: cover weights.

Note: weights make you think *globally* (due to products in calculations) while factors represent local dependencies! 

Note: factors == constraints. 

Definitions (from slides):  

<p align='center'>
    <img alt="picture 9" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/39325f5f0060ad48edbab5b07b9ec6fba417c4227815abdbaa1d0815bf1c3394.png" width="50%" />  
</p>

<p align='center'>
     <img alt="picture 8" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/6f512d11c74c3c39619c1aa4bb4b26850c79e85d476c0aaf3ac300d01cafdb47.png" width="35%" />  
</p>

<p align='center'>
    <img alt="picture 7" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images/images/5ba81fefb4e1162851a742e3b0624eae0d859b2b7a2839a6a116166c2de7bdda.png" width="60%" />  
</p>


## III. Examples

- LSAT logic puzzle 
- Event scheduling 
- Program verification 

 
::: {#def-default}
**(indicator function)**: (useful for defining constraints/factors). 

Can think of it as a python function that returns a boolean if the specified condition is true. 
:::
 

> Basic idea is to formulate your problem in terms of variables (desired quantities to be assigned) and factors (your constraints for these variable values). A CSP will assign values to these variables that are supposed to satisfy the constraints. Moreover, define factors as indicator functions that check whether the specified condition (i.e., the constraint) is true. 


## IV. Dynamic Ordering 

- We covered modeling, now let's get to inference (how to solve CSP's!)
- To understand how to solve CSP, must understand idea behind weights. 

Each assignment $x=\left(x_1, \ldots, x_n\right)$ has a weight:
$$
\operatorname{Weight}(x)=\prod_{j=1}^m f_j(x)
$$

(notice how it depends on the factors!) So essentially, what we are saying is that we set a weight for each factor/constraint and the outcome/result is what is being weighted. Then, we can mathematically define the objective: 

$$
\arg \max _x \text { Weight }(x)
$$

that is, find the max $x$ for the assignments. 

❓I guess the idea is that the solutions will have a bigger weight than non-solutions? What to do in tie? Where to draw line of solution and non-solution? 

### Backtracking search 

- Blueprint for DO (dynamic ordering)
- Cut-off when condition isn't satisfied
- Explore all paths
- Take highest weighted path at end as solution if satisfies conditions 

We can probe this idea further to motivate DO. 

- Idea: **partial assignment weights**
  - Recall that the weight of an assignment (solution!) is the product of all the factors.
  - We define the weight of a partial assignment to be the product of all the factors that we can evaluate, namely those whose scope includes only assigned variables.
  - For example, if only $WA$ and $NT$ are assigned, the weight is just value of the single factor between them.
  - When we assign a new variable a value, the weight of the new extended assignment is the old weight times all the factors that depend on the new variable and only previously assigned variables.

