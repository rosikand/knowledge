# Shuffle arrays in unison 


Use `np.random.permutation`! 

```python
import numpy as np 

X = np.array(data)
y = np.array(target)

perm = np.random.permutation(len(X))
X = X[perm]
y = y[perm]
```


