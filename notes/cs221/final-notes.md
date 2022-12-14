# Final Review Document 

## I. Constraint Satisfication Problems 


- If we take that the factors of the factor graph are constraints that result in 0 if not satisfied, then satisfiable assignments will have a weight > 0 because if at least one constraint is not satisfied, then the whole multiplication goes to 0. So the objective of maximizing the weight holds here. 


## II. Markov Networks 

- **Factor graphs**: basically bipartie undirected graphs where there exists nodes representing RV's and nodes representing factors which are functions acting on the RV's they are connected to. Factors are simply functions which spit out some scalar value given assignments to the RV's they take in. Here is an example: 

<p align='center'>
    <img alt="picture 2" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images@main/images/90608e4ad3483f413ba61a67f8d4a9bbda61144c6bfde53e1729e5b0440d6e12.png" width="500" />  
</p>

Some useful terms for factors: 

<p align='center'>
    <img alt="picture 3" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images@main/images/62ea20613bc37dd5b53d921633646909e895be970457db2df2279208700f4be4.png" width="300" />  
</p>


each assignment of values to the RV's has a weight associated to it which involves multiplying the factors together: 

 
:::{.callout-note}
::: {#def-default}

### Assignment weights 
Each assignment $x=\left(x_1, \ldots, x_n\right)$ has a weight:
$$
\operatorname{Weight}(x)=\prod_{j=1}^m f_j(x)
$$
:::
:::
 
#### Transitioning to markov networks 

- Markov networks are just factor graph's but with probability defined to each assignment of the variables rather than weight. Before, we'd have a table that looks like this which specifies a weight for each assignment: 

<p align='center'>
    <img alt="picture 4" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images@main/images/c1160710786b8c3db6c7308f43162a47337088b618bd994d37d0cbd462d00777.png" width="300" />  
</p>

- Now, we can normalize it by dividing each weight by the sum of all weights: 

$$\mathbb{P}(X=x)=\frac{\text { Weight }(x)}{Z}$$ 

where $Z=\sum_{x^{\prime}}$ Weight $\left(x^{\prime}\right)$. We now have: 

<p align='center'>
    <img alt="picture 5" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images@main/images/ea0ff0d2541f63a7ae511a1425e77d18c83c32b8d9ac8a79200aa82cb013c291.png" width="300" />  
</p>


this allows us to represent uncertainty. We can perform inference via taking marginals for example. 

$$
\begin{aligned}
& \mathbb{P}\left(X_2=1\right)=0.15+0.15+0.15+0.15=0.62 \\
& \mathbb{P}\left(X_2=2\right)=0.08+0.31=0.38
\end{aligned}
$$

Note: different than max weight assignment!

### Gibbs Sampling 

- We are interested in computing marginal, conditional, and regular probabilities from the distribution that the markov network represents. Here, we discuss an inference algorithm to *approximate* the marginal calculations (e.g., what is the probability of some random variable $X_2$?). 
- **Marginal probabilities are computed by summing the probabilities over all assignments satisfying the given condition**. Gibbs sampling gives us a computationally efficient approximate. 
  - Note: only given conditional probabilities rather than marginal in the graphs so we must approximate it. 
  - Cond probs are represented by the factors which are often derived when converting bayesian to markov: 
  
  <p align='center'>
    <img alt="picture 6" src="https://cdn.jsdelivr.net/gh/minimatest/vscode-images@main/images/9ab65e611e5dbb1e6f5f8afba4d75178ec382aa5a7af1785d90e1d51ced78f44.png" width="300" />  
  </p>



*Describe algorithm steps here*. 




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

