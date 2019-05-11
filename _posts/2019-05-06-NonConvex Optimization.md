---
layout:     post
title:      Summary on Non-Convex Optimization
subtitle:    
date:       2019-04-29
author:     Tintin
header-img: img/post-bg-swift.jpg
catalog: true
tags:
    - Optimization
---

<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>

**Empirical Risk Minimization:**

$$ \min_{x\in R^d}\{f(x):=\sum_{i=1}^{n} \frac{1}{n}f_i(x)\}$$

There are three categories of non-convex problem solvers :

* Transforming the non-convex function into convex function ;
* One point convexity ;
* Approximate stationary point or Local minima.


In the following, I will only focus one the third category.

### 1.Stationary Point 
**Goal 1 : find an approximate “stationary point” with $$||\triangledown f(x)||^2 <\epsilon$$.**

**Known Result**

|$$SGD$$  |$$GD$$ | $$SVRG$$ |
|:------:  | :------: |   :------: |  
|$$T\propto O(\frac{1}{\epsilon^2})$$ |$$T\propto O(\frac{1}{\epsilon})$$| |
		
Other result under small assumption:
* [2017 Zeyuan-Allen Zhu Natasha ](https://arxiv.org/abs/1702.00763): $$f$$ is strongly non-convex;
* [2017 Carmon-Duchi](https://arxiv.org/abs/1611.00756):$$f$$ is 2nd-order smoothness

### 2.Local Minima

**Goal 2 : find an approximate “local minima” with** $$\|\triangledown f(x)\|^2 <\epsilon$$ and $$\|\triangledown f(x)\|^2 \geq -\delta I$$.

Since the function is non-convex, a stationary point can be saddle point or local minima. So the second goal is finding an approximate local minima with an additional condition that the Hessian Eigenvector must greater than a negative small constan $$\delta$$.

The step of solving Goal 2 is firstly applying Goal 1 to find a stationary point. Then find the most negative Eigenvector which should be smaller than $$\delta$$. 

There are two types of methods for finding an approximate local minima: do not use Hessian and use Hessian. 

##### 2.1 Do not use Hessian
This type of methods proved that SGD can escape from saddle point and automatically find the local minima. Thus, it is not necessary to use the Hessian. This is first proposed by Ge rong et al. 

#### 2.1 Use Hessian