# Final Review Document 

## I. Constraint Satisfication Problems 



## II. Markov Networks 

- Use

## III. Bayesian Networks 

- Form of modeling the world. A BN is simply a directed acyclic graph of random variables where directed edges between nodes represents conditional dependence and causation. 
- Joints are too big in the real world. Can't:
  - Efficiently store all the combinations. We'd have $2^k$ parameters where $k$ is the number of RV's. 
  - Perform useful inference due to the global nature of the joint. 
- Bayes nets allow us to compactly represent the joint via local conditional probability distributions for each RV. And it resolves the second problem by reasoning locally but conditioning globally. This relies on two concepts:
  - conditional independence 
  - chain rule 
  




 
:::{.callout-note appearance='simple'}

#### Bayes net <--> Joint 



The full joint would be to multiply the RV's out: 

$$
P\left(x_1, x_2, \ldots x_n\right)=\prod_{i=1}^n P\left(x_i \mid x_1 \ldots x_{i-1}\right)
$$

this is true for *any* distribution (this is just the chain rule). However, in bayes nets, we assume conditional independence meaning each node is conditionally independent from every node buts its parents. So we reduce the above to: 

$$
P\left(x_i \mid x_1, \ldots x_{i-1}\right)=P\left(x_i \mid \operatorname{parents}\left(X_i\right)\right)
$$


which still gives us a valid joint:


$$
P\left(x_1, x_2, \ldots x_n\right)=\prod_{i=1}^n P\left(x_i \mid\right. \text{parents}\left.\left(X_i\right)\right)
$$

See how much space we save by making the conditional independence assumption? 
:::






#### Conditional Independence 


- Main characteristic that allows us to formulate joints via Bayes' nets. Essentially, conditional independence allows us to condition only on the local parents for each node rather than the ancestor variables. 

Example: 

<p align='center'>
    <img alt="picture 1" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images@main/images/4f6aa56ddd11ad81b38ed4c9fda2a56b59619fa8117396ddddfc272fadb2aeb1.png" width="300" />  
</p>

$x_3$ is independent of $x_2$ given $x_1$. 




### Important points 

- You can **recover** the full joint from a Bayes net via chain rule: 

$$
P\left(x_1, x_2, \ldots x_n\right)=\prod_{i=1}^n P\left(x_i \mid\right. \text{parents} \left.\left(X_i\right)\right)
$$

- **Inference** in a Bayesian network involves computing the probability of a variable, or a set of variables, given some evidence. This involves combining the probabilities of the variables using the chain rule of probability and the conditional probabilities represented in the network. 




#### Questions 

- Why do we assume conditional independence in Bayesian networks? That is, why do we assume that the value of each node depends only on its direct parents rather than the rest of the network and/or its ancestors? 
  - I think this is just the assumption we make when modeling the world using Bayes nets. 
  - We assume the "markov property". 
- 



## IV. Logic 

