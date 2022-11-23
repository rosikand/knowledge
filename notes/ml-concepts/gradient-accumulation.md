---
date: 11/22/22
---

# Gradient accumulation 

- Only update params every $n$ steps. 
- Essentially replicates (is (almost) statistically the same) the notion of batching in stochastic gradient descent.  
  - Thus, allows one to train a model on a smaller machine but simulate a bigger batch size to avoid out-of-memory errors. 



## gradient accumulation in PyTorch 

See [here](https://kozodoi.me/python/deep%20learning/pytorch/tutorial/2021/02/19/gradient-accumulation.html) for more and how to do this in PyTorch (or see CS 330 HW3). 


## gradient accumulation in Jax 

