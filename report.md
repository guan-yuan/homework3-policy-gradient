# Homework3-Policy-Gradient report
陳冠元(105065530)

## Problem 1: construct a neural network to represent policy   

In this part, I use tf.layers.dense() function to build neural networks for solving the problem. Details as follow:
```
        # YOUR CODE HERE >>>>>>
        l1 = tf.layers.dense(self._observations, hidden_dim, tf.nn.tanh)
        l2 = tf.layers.dense(l1, out_dim)
        probs = tf.nn.softmax(l2)
        # <<<<<<<<
```


## Problem 2: compute the surrogate loss    

In this part, I added 1 line to solve the problem via the given hints.
```
        # YOUR CODE HERE >>>>>>
        surr_loss = tf.reduce_mean((-log_prob)*self._advantages)
        # <<<<<<<<
```

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/p1.PNG" width = "80%" alt=""/>
</div>
    
[Reference](https://github.com/CEDL2017/homework3-policy-gradient/blob/master/Lab3-policy-gradient.ipynb)


## Problem 3    

In this part, I added 1 line to solve the problem via the given hints.
```
         # YOUR CODE HERE >>>>>>
         a = r - b
         # <<<<<<<<
```

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/3.png" width = "80%" alt=""/>
</div>

#### Results:

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/4.png" width = "50%" alt=""/>
</div>


## Problem 4    

From the result, We can find that after removing the baseline term, the variance become higher, even though the avg. return at the same level.  


#### Results:

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/5.png" width = "50%" alt=""/>
</div>


The reasons of why the baseline won't introduce bias can be explained as bellow:

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/2.PNG" width = "80%" alt=""/>
</div>

[Reference](http://rll.berkeley.edu/deeprlcourse/)


## Problem 5: Actor-Critic algorithm (with bootstrapping)    
In this part, we can find when we revise the problem 3 by using the one-step bootstrap for the advantage function, it become very shaky, and it cannot solve the problem within 200 n_iter.

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/6.png" width = "80%" alt=""/>
</div>

#### Results:

<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/9.png" width = "50%" alt=""/>
</div>

## Problem 6: Generalized Advantage Estimation¶     

In this part, I added 1 line to solve the problem via the given hints. Refer to the paper ["High-Dimensional Continuous Control Using Generalized Advantage Estimation"](https://arxiv.org/pdf/1506.02438.pdf). The GAE using the hyperparameter λ,  to trade-off between bias and variance (bias variance dilemma). As the result, the GAE method can solve the problem within 80 n_iter, and have lower variance than the method of Problem 5 (Actor-Critic algorithm (with bootstrapping)).
```
            # YOUR CODE HERE >>>>>>>>
            a = util.discount(a, LAMBDA * self.discount_rate)
            # <<<<<<<
```
<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/7.png" width = "80%" alt=""/>
</div>

#### Results: 
<div align=left>
<img src="https://github.com/guan-yuan/homework3-policy-gradient/blob/master/outputs/8.png" width = "50%" alt=""/>
</div>

## References:
[CS 294: Deep Reinforcement Learning, Fall 2017](http://rll.berkeley.edu/deeprlcourse/)   
   
[CEDL2017](https://github.com/CEDL2017)

[UCL Course on RL](http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching.html)

[Deep RL Bootcamp](https://sites.google.com/view/deep-rl-bootcamp/lectures)
