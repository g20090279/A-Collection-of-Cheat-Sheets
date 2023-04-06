- Key Words: Information Theory Cheat Sheet
- Last Revised: Apr. 5, 2023

---

| Comment | Equations |
|:---|:---|
|discrete/continuous random variable| $X$ |
|the set of its values | $\mathcal{X}$ |
|probability distribution| $\{p_X(x)\}_{x\in\mathcal{X}}$, $p_X(x)\in[0,1]$.|
|normalization condition | $\sum_{x\in\mathcal{X}}p_X(x)=1$; $\int_{x\in\mathcal{X}}p_X(x)\ dx$ |
|an event $A$| $A\subseteq\mathcal{X}$|
|the probability of $A$| $\mathbb{P}(A)$ |
|the expectation of a real-valued function of the random variable $X$| $\mathbb{E}[f]=\sum_{x\in\mathcal{X}}p_X(x)f(x)$; $\mathbb{E}[f]=\int_{x\in\mathcal{X}}p_X(x)f(x)\ dx$ |
|entropy (average of uncertainty) of $X$| $H_X=-\sum_{x\in\mathcal{X}}p(x)\log_2p(x)=\mathbb{E}\left[\log_2\left(\frac{1}{p(X)}\right)\right]$; $H_X=-\int_{x\in\mathcal{X}}p(x)\log_2p(x)\ dx$. Define by continuity $0\log_20=0$. |
||Entropy for continuous PDF is also called differential entropy. The differential entropy can be negative, since the continuous PDF can be larger than 1.|
||(units of entropy) logarithm to the base 2: bits; logarithm to the base $e$: nats.|
|the Kullback-Leibler (KL) divergence between two probability distributions $p(x)$ and $q(x)$ over the same finite space $\mathcal{X}$| $D(p\Vert q)=\sum_{x\in\mathcal{X}}p(x)\log\frac{p(x)}{q(x)}$ |
||KL divergence is nonnegative, i.e. $D(p\Vert q)\geq0$ (Gibbs' Inequality) (P1). It equals zero if and only if $q(x)=p(x)$.|
||Very often we want to replace a complex distribution $q(x)$ with a simpler distribution $p(x)$. KL divergence measures how much information is lost from the origin PDF to the new PDF.|
|total entropy of $x\in\mathcal{X}$ and $y\in\mathcal{Y}$| $H_{X,Y}=-\sum_{x\in\mathcal{X},y\in\mathcal{Y}}p(x,y)\log_2p(x,y)$; $H_{X,Y}=-\int_{x\in\mathcal{X},y\in\mathcal{Y}}p(x,y)\log_2p(x,y)\ dxdy$ |
|| In general, $H_{X,Y}\leq H_X+H_y$. If $X$ and $Y$ are independent, the equality meets. |
|conditional entropy of $Y\in\mathcal{Y}$ given $X\in\mathcal{X}$ (note that need to average over $X$)| $H_{Y\vert X}=-\sum_{x\in\mathcal{X}}p(x)\sum_{y\in\mathcal{Y}}p(y\vert x)\log_2p(y\vert x)$; $H_{Y\vert X}=\int_{x\in\mathcal{X}}p(x)\int_{y\in\mathcal{Y}}p(y\vert x)\log_2p(y\vert x)\ dydx$ |
|| $H_{X,Y}=H_X+H_{Y\vert X}$ (P2) |
|mutual entropy (the correlation) of $X\in\mathcal{X}$ and $Y\in\mathcal{Y}$| $I_{X,Y}=\sum_{x\in\mathcal{X},y\in\mathcal{Y}}p(x,y)\log_2\frac{p(x,y)}{p(x)p(y)}$ |
|| $I_{X,Y}=H_Y-H_{Y\vert X}=H_X-H_{X\vert Y}$, which shows that $I_{X,Y}$ measures the reduction in the uncertainty of $X$ due to the knowledge of $Y$. |
||$I(X,Y)\geq0$. Equality satisfies if $X$ and $Y$ are independent.|

# Proof

## P1

Use the inequality $\ln x\leq x-1$ for the whole domain $x>0$. This essential inequality can be easily proved by calculate the derivative of $x-1-\ln x$, which gives the minimum point at $x=1$ with minimum value $0$.

Then, the Kullback-Leibler divergence has

$$\begin{aligned}D(p\Vert q)&=-\sum_{x\in\mathcal{X}}p(x)\ln\frac{q(x)}{p(x)}\geq-\sum_{x\in\mathcal{X}}p(x)\left(\frac{q(x)}{p(x)}-1\right)\\&=-\sum_{x\in\mathcal{X}}q(x)+\sum_{x\in\mathcal{X}}p(x)=0.\end{aligned}$$

## P2

$$\begin{aligned}H_{X,Y}&=-\sum_{x\in\mathcal{X},y\in\mathcal{Y}}p(x,y)\log_2p(x,y)\\&=-\sum_{x\in\mathcal{X},y\in\mathcal{Y}}p(y|x)p(x)\log_2\left[p(y|x)p(x)\right]\\&=-\sum_{x\in\mathcal{X},y\in\mathcal{Y}}p(y|x)p(x)\log_2p(y|x)-\sum_{x\in\mathcal{X},y\in\mathcal{Y}}p(y|x)p(x)\log_2p(x)\\&=-\sum_{x\in\mathcal{X}}p(x)\sum_{y\in\mathcal{Y}}p(y|x)\log_2p(y|x)-\sum_{y\in\mathcal{Y}}p(y|x)\sum_{x\in\mathcal{X}}p(x)\log_2p(x)\\&=H_{Y|X}+1\cdot H_X\end{aligned}$$