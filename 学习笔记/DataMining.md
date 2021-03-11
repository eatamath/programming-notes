# Data Mining

## Lecture notes

çŽćłçć§č˝äšćŻĺˇĽä¸éćą

ć°ćŽĺćĺćŹ

- inspecting
- cleaning
- transforming
- modeling

ć šćŽ bias ĺ variance ćĽčŻäź°ĺč°ć´ć¨Ąĺ

ĺŠç¨ĺ¤ä¸Şć¨ĄĺçĺšłĺćĽĺĺ°čŻŻĺˇŽ

large bias small var -> model is too simple

small training bias large valid var -> overfitting

large var -> using regularization

### čçąťć¨Ąĺ

čŽ¤çĽć°ćŽçťćĺč§ĺ

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200403113241842.png" alt="image-20200403113241842" style="zoom:33%;" />

#### ĺąćŹĄčçąť

single linkage -- nearest

complete linkage -- furtherest



#### Kmeans

čŽžç˝Žĺć­˘ćĄäťśďźĺŻäťĽćŻĺ¤ä¸ŞĺłĺżçćĄäťś

éç¨éćşçŽćłćžĺ¨ĺąćäźďźĺŚä˝żç¨éĺłäźĺçŽćłäźĺčśĺć°

çŽćłçźşçšďź

- categorical feature
- outlier vulnerability
- data shape presumption
- belong to single cluster

#### EM Algorithm

model based

guassain distribution assumption

- initialize $\mu_i$ and $\sigma_i$
- expectation
  - allocate each $x_i$ to cluster $i$ according to $\mu_i,\sigma_i$
- maximization
  - update all $\mu_i,\sigma_i$ for each cluster $i$

#### DBSCAN

density based

### Linear Regression

A more complex model yields lower error on training data.
If we can truly find the best function.

overfitting: A more complex model does not always lead to better performance on testing data

Training error: larger đ, considering the training error less

A more complex model does not always lead to better performance on testing data.

ćł¨ććšĺˇŽäź°čŽĄéćŻćĺçčżćŻć ĺçäź°čŽĄ

Simpler model is less influenced by the sampled data

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200403112724112.png" alt="image-20200403112724112" style="zoom:33%;" />

large var: more data, regularization



### Outlier Detection

noise removal

outlier detection vs. novelty detection







## Reading Notes

### EM Algorithm

#### prerequisite

$f$ is a convex function if $f^{\prime \prime}(x) \geq 0$ (for all $x \in \mathbb{R}$ )

##### Theorem

Let $f$ be a convex function, and let $X$ be a random variable. Then:
$$
\mathrm{E}[f(X)] \geq f(\mathrm{E} X)
$$
Moreover, if $f$ is strictly convex, then $\mathrm{E}[f(X)]=f(\mathrm{E} X)$ holds true if and only if $X=\mathrm{E}[X]$ with probability 1 (i.e., if $X$ is a constant).

#### Derivation

Suppose we have an estimation problem in which we have a training set $\left\{x^{(1)}, \ldots, x^{(m)}\right\}$ consisting of $m$ independent examples. We wish to fit the parameters of a model $p(x, z)$ to the data, where the likelihood is given by
$$
\begin{aligned}
\ell(\theta) &=\sum_{i=1}^{m} \log p(x ; \theta) \\
&=\sum_{i=1}^{m} \log \sum_{z} p(x, z ; \theta)
\end{aligned}
$$
In such a setting, the EM algorithm gives an efficient method for maximum likelihood estimation. Maximizing $\ell(\theta)$ explicitly might be difficult, and our strategy will be to instead repeatedly construct a lower-bound on $\ell$ (E-step), and then optimize that lowel-bound (M-step).

For each $i,$ let $Q_{i}$ be some distribution over the $z$ 's $\left(\sum_{z} Q_{i}(z)=1, Q_{i}(z) \geq\right.$
0). Consider the following: $^{1}$
$$
\begin{aligned}
\sum_{i} \log p\left(x^{(i)} ; \theta\right) &=\sum_{i} \log \sum_{z^{(i)}} p\left(x^{(i)}, z^{(i)} ; \theta\right) \\
&=\sum_{i} \log \sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right) \frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)} \\
& \geq \sum_{i} \sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}
\end{aligned}
$$
The last step of this derivation used Jensen's inequality.

Also, the term
$$
\sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right)\left[\frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}\right]
$$
in the summation is just an expectation of the quantity $\left[p\left(x^{(i)}, z^{(i)} ; \theta\right) / Q_{i}\left(z^{(i)}\right)\right]$ with respect to $z^{(i)}$ drawn according to the distribution given by $Q_{i} .$ By Jensen's inequality, we have
$$
f\left(\mathrm{E}_{z^{(i)} \sim Q_{i}}\left[\frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}\right]\right) \geq \mathrm{E}_{z^{(i)} \sim Q_{i}}\left[f\left(\frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}\right)\right]
$$
To make the bound tight for a particular value of $\theta,$ we need for the step involving Jensen's inequality in our derivation above to hold with equality. For this to be true, we know it is sufficient that the expectation be taken over a "constant"-valued random variable. I.e., we require that
$$
\frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}=c
$$
for some constant $c$ that does not depend on $z^{(i)} .$ This is easily accomplished by choosing
$$
Q_{i}\left(z^{(i)}\right) \propto p\left(x^{(i)}, z^{(i)} ; \theta\right)
$$
Actually, since we know $\sum_{z} Q_{i}\left(z^{(i)}\right)=1$ (because it is a distribution), this further tells us that
$$
\begin{aligned}
Q_{i}\left(z^{(i)}\right) &=\frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{\sum_{z} p\left(x^{(i)}, z ; \theta\right)} \\
&=\frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{p\left(x^{(i)} ; \theta\right)} \\
&=p\left(z^{(i)} | x^{(i)} ; \theta\right)
\end{aligned}
$$
Thus, we simply set the $Q_{i}$ 's to be the posterior distribution of the $z^{(i)}$ 's given $x^{(i)}$ and the setting of the parameters $\theta$

(E-step) For each $i,$ set
$$
Q_{i}\left(z^{(i)}\right):=p\left(z^{(i)} | x^{(i)} ; \theta\right)
$$
(M-step) Set
$$
\theta:=\arg \max _{\theta} \sum_{i} \sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}
$$

$$
\ell\left(\theta^{(t)}\right)=\sum_{i} \sum_{z^{(i)}} Q_{i}^{(t)}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta^{(t)}\right)}{Q_{i}^{(t)}\left(z^{(i)}\right)}
$$
The parameters $\theta^{(t+1)}$ are then obtained by maximizing the right hand side of the equation above. Thus,
$$
\begin{aligned}
\ell\left(\theta^{(t+1)}\right) & \geq \sum_{i} \sum_{z^{(i)}} Q_{i}^{(t)}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta^{(t+1)}\right)}{Q_{i}^{(t)}\left(z^{(i)}\right)} \\
& \geq \sum_{i} \sum_{z^{(i)}} Q_{i}^{(t)}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta^{(t)}\right)}{Q_{i}^{(t)}\left(z^{(i)}\right)} \\
&=\ell\left(\theta^{(t)}\right)
\end{aligned}
$$
This first inequality comes from the fact that
$$
\ell(\theta) \geq \sum_{i} \sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}
$$
holds for any values of $Q_{i}$ and $\theta,$ and in particular holds for $Q_{i}=Q_{i}^{(t)}$ $\theta=\theta^{(t+1)} .$ To get Equation $(5),$ we used the fact that $\theta^{(t+1)}$ is chosen explicitly to be
$$
\arg \max _{\theta} \sum_{i} \sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}
$$
and thus this formula evaluated at $\theta^{(t+1)}$ must be equal to or larger than the same formula evaluated at $\theta^{(t)} .$ Finally, the step used to get (6) was shown earlier, and follows from $Q_{i}^{(t)}$ having been chosen to make Jensen's inequality hold with equality at $\theta^{(t)}$

#### Remark

If we define
$$
J(Q, \theta)=\sum_{i} \sum_{z^{(i)}} Q_{i}\left(z^{(i)}\right) \log \frac{p\left(x^{(i)}, z^{(i)} ; \theta\right)}{Q_{i}\left(z^{(i)}\right)}
$$
then we know $\ell(\theta) \geq J(Q, \theta)$ from our previous derivation. The EM can also be viewed a coordinate ascent on $J,$ in which the E-step maximizes it with respect to $Q$ (check this yourself), and the M-step maximizes it with respect to $\theta$

### GMM

Suppose that we are given a training set $\left\{x^{(1)}, \ldots, x^{(m)}\right\}$ as usual. since we are in the unsupervised learning setting, these points do not come with any labels.

We wish to model the data by specifying a joint distribution $p\left(x^{(i)}, z^{(i)}\right)=$ $p\left(x^{(i)} | z^{(i)}\right) p\left(z^{(i)}\right) .$ 

Here, $z^{(i)} \sim$ Multinomial $(\phi)$ (where $\phi_{j} \geq 0, \sum_{j=1}^{k} \phi_{j}=1$
and the parameter $\phi_{j}$ gives $p\left(z^{(i)}=j\right),$ and $x^{(i)} | z^{(i)}=j \sim \mathcal{N}\left(\mu_{j}, \Sigma_{j}\right) .$ We let $k$ denote the number of values that the $z^{(i)}$ 's can take on. 

Thus, our model posits that each $x^{(i)}$ was generated by randomly choosing $z^{(i)}$ from $\{1, \ldots, k\},$ and then $x^{(i)}$ was drawn from one of $k$ Gaussians depending on $z^{(i)} .$ This is called the mixture of Gaussians model. 

Also, note that the $z^{(i)}$ 's are latent random variables, meaning that they're hidden/unobserved. This is what will make our estimation problem difficult.

#### main idea

The EM algorithm is an iterative algorithm that has two main steps. Applied to our problem, in the E-step, it tries to "guess" the values of the $z^{(i)}$ 's. In the M-step, it updates the parameters of our model based on our guesses. since in the M-step we are pretending that the guesses in the first part were correct, the maximization becomes easy. Here's the algorithm:

Repeat until convergence: \{
									(E-step) For each $i, j,$ set
$$
w_{j}^{(i)}:=p\left(z^{(i)}=j | x^{(i)} ; \phi, \mu, \Sigma\right)
$$
â									(M-step) Update the parameters:
$$
\begin{aligned}
\phi_{j} &:=\frac{1}{m} \sum_{i=1}^{m} w_{j}^{(i)} \\
\mu_{j} &:=\frac{\sum_{i=1}^{m} w_{j}^{(i)} x^{(i)}}{\sum_{i=1}^{m} w_{j}^{(i)}} \\
\Sigma_{j} &:=\frac{\sum_{i=1}^{m} w_{j}^{(i)}\left(x^{(i)}-\mu_{j}\right)\left(x^{(i)}-\mu_{j}\right)^{T}}{\sum_{i=1}^{m} w_{j}^{(i)}}
\end{aligned}
$$
}

In the E-step, we calculate the posterior probability of our parameters the $z^{(i)}$ 's, given the $x^{(i)}$ and using the current setting of our parameters. I.e., using Bayes rule, we obtain:
$$
p\left(z^{(i)}=j | x^{(i)} ; \phi, \mu, \Sigma\right)=\frac{p\left(x^{(i)} | z^{(i)}=j ; \mu, \Sigma\right) p\left(z^{(i)}=j ; \phi\right)}{\sum_{l=1}^{k} p\left(x^{(i)} | z^{(i)}=l ; \mu, \Sigma\right) p\left(z^{(i)}=l ; \phi\right)}
$$
Here, $p\left(x^{(i)} | z^{(i)}=j ; \mu, \Sigma\right)$ is given by evaluating the density of a Gaussian with mean $\mu_{j}$ and covariance $\Sigma_{j}$ at $x^{(i)} ; p\left(z^{(i)}=j ; \phi\right)$ is given by $\phi_{j},$ and so on. The values $w_{j}^{(i)}$ calculated in the E-step represent our "soft" guesses $^{2}$ for the values of $z^{(i)}$

Also, you should contrast the updates in the M-step with the formulas we had when the $z^{(i)}$ 's were known exactly. They are identical, except that instead of the indicator functions " $1\left\{z^{(i)}=j\right\}$ " indicating from which Gaussian each datapoint had come, we now instead have the $w_{j}^{(i)}$ s.

#### remark

The EM-algorithm is also reminiscent of the K-means clustering algorithm, except that instead of the "hard" cluster assignments $c(i),$ we instead have the "soft" assignments $w_{j}^{(i)} .$ Similar to K-means, it is also susceptible to local optima, so reinitializing at several different initial parameters may be a good idea.



### 推荐系统

CB应该算是最早被使用的推荐方法吧，它根据用户过去喜欢的**产品**（本文统称为 **item**），为用户推荐和他过去喜欢的产品相似的产品。例如，一个推荐饭店的系统可以依据某个用户之前喜欢很多的烤肉店而为他推荐烤肉店。 CB最早主要是应用在信息检索系统当中，所以很多信息检索及信息过滤里的方法都能用于CB中。

   CB的过程一般包括以下三步：

1. **Item Representation**：为每个item抽取出一些特征（也就是item的content了）来表示此item；

2. **Profile Learning**：利用一个用户过去喜欢（及不喜欢）的item的特征数据，来学习出此用户的喜好特征（profile）；

3. **Recommendation Generation**：通过比较上一步得到的用户profile与候选item的特征，为此用户推荐一组相关性最大的item。

中对于上面的三个步骤给出一张很细致的流程图（第一步对应着Content Analyzer，第二步对应着Profile Learner，第三步对应着Filtering Component）：

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200612141639516.png" alt="image-20200612141639516" style="zoom:50%;" />

#### TF-IDF算法

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200612141756920.png" alt="image-20200612141756920" style="zoom:50%;" />

最终带k个词在文档j中的权重由下面的公式获得。
$$
w_{k, j}=\frac{\mathrm{TF}-\mathrm{IDF}\left(t_{k}, d_{j}\right)}{\sqrt{\sum_{s=1}^{|T|} \mathrm{TF}-\mathrm{IDF}\left(t_{s}, d_{j}\right)^{2}}}
$$

#### 协同过滤

参考

[协同过滤推荐算法](https://zhuanlan.zhihu.com/p/80069337)
$$
\sin (u, s)=\sum_{s_{i} \in S} \operatorname{score}\left(u, s_{i}\right) * \operatorname{sim}\left(s_{i}, s\right)
$$
