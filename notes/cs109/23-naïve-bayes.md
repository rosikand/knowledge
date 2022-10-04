# 🐻 Lecture 23: Naïve Bayes

Yea yea... we have talked about estimating parameters for a parametric probability distribution. But now let's actually do real ML: making predictions! We will do this in the context of three datasets: 
- Hearts 
- Ancestry 
- Netflix 

All three problems on the pset where you implement classifiers for all of them using both Logistic regression and Bayes' nets! 

We will be working with supervised classification specifically. 

![](attachments/Pasted%20image%2020220310020042.png)

**Classification**: 

![](attachments/Pasted%20image%2020220310021220.png)

Note: regression is same thing except numbers aren't binary! 

![](attachments/Pasted%20image%2020220310021248.png)


So how do we program an algorithm for classification? Our first insight might be to brute force Bayes'. 

### Brute force Bayes' 

- 