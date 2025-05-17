## 6.4 The Transition Probability Function $P_{ij}(t)$

Let  
$$P_{ij}(t) = \mathbb{P}\{X(t + s) = j \mid X(s) = i\}$$  
denote the probability that a process presently in state $i$ will be in state $j$ a time $t$ later. These quantities are often called the transition probabilities of the continuous-time Markov chain.

We can explicitly determine $P_{ij}(t)$ in the case of a pure birth process having distinct birth rates. For such a process, let $X_k$ denote the time the process spends in state $k$ before making a transition into state $k+1$, $k \geq 1$. Suppose that the process is presently in state $i$, and let $j > i$. Then, as $X_i$ is the time it spends in state $i$ before moving to state $i+1$, and $X_{i+1}$ is the time it then spends in state $i+1$ before moving to state $i+2$, and so on, it follows that  
$$\sum_{k=i}^{j-1} X_k$$  
is the time it takes until the process enters state $j$. Now, if the process has not yet entered state $j$ by time $t$, then its state at time $t$ is smaller than $j$, and vice versa. That is,  
$$X(t) < j \iff X_i + \cdots + X_{j-1} > t$$

Therefore, for $i < j$, we have for a pure birth process that  
$$
\mathbb{P}\{X(t) < j \mid X(0) = i\} = \mathbb{P}\left\{ \sum_{k=i}^{j-1} X_k > t \right\}
$$

However, since $X_i, \ldots, X_{j-1}$ are independent exponential random variables with respective rates $\lambda_i, \ldots, \lambda_{j-1}$, we obtain from the preceding and Eq. (5.9), which gives the tail distribution function of $\sum_{k=i}^{j-1} X_k$, that  
$$
\mathbb{P}\{X(t) < j \mid X(0) = i\} = \sum_{k=i}^{j-1} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j-1} \frac{\lambda_r}{\lambda_r - \lambda_k}
$$

Replacing $j$ by $j+1$ in the preceding gives  
$$
\mathbb{P}\{X(t) < j+1 \mid X(0) = i\} = \sum_{k=i}^{j} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j} \frac{\lambda_r}{\lambda_r - \lambda_k}
$$

Since  
$$
\mathbb{P}\{X(t) = j \mid X(0) = i\} = \mathbb{P}\{X(t) < j+1 \mid X(0) = i\} - \mathbb{P}\{X(t) < j \mid X(0) = i\}
$$  
and since $P_{ii}(t) = \mathbb{P}\{X_i > t\} = e^{-\lambda_i t}$, we have shown the following.

### Proposition 6.1  
For a pure birth process having $\lambda_i \ne \lambda_j$ when $i \ne j$:

$$
P_{ij}(t) = \sum_{k=i}^{j} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j} \frac{\lambda_r}{\lambda_r - \lambda_k} - \sum_{k=i}^{j-1} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j-1} \frac{\lambda_r}{\lambda_r - \lambda_k}, \quad i < j
$$

$$
P_{ii}(t) = e^{-\lambda_i t}
$$

### Example 6.8  
Consider the **Yule process**, which is a pure birth process in which each individual in the population independently gives birth at rate $\lambda$, and so $\lambda_n = n\lambda$, $n \geq 1$. Letting $i = 1$, we obtain from Proposition 6.1:

$$
P_{1j}(t) = \sum_{k=1}^{j} e^{-k\lambda t} \prod_{\substack{r=1 \\ r \ne k}}^{j} \frac{r}{r - k} - \sum_{k=1}^{j-1} e^{-k\lambda t} \prod_{\substack{r=1 \\ r \ne k}}^{j-1} \frac{r}{r - k}
$$

This simplifies to:  
$$
P_{1j}(t) = e^{-j\lambda t} \prod_{r=1}^{j-1} \frac{r}{r - j} + \sum_{k=1}^{j-1} e^{-k\lambda t} \left( \prod_{\substack{r=1 \\ r \ne k}}^{j} \frac{r}{r - k} - \prod_{\substack{r=1 \\ r \ne k}}^{j-1} \frac{r}{r - k} \right)
$$

We can further simplify using:  
$$
\frac{k}{j-k} \prod_{\substack{r=1 \\ r \ne k}}^{j-1} \frac{r}{r - k} = \frac{(j-1)!}{(1-k)(2-k)\cdots(k-1-k)(j-k)!} = (-1)^{k-1} \binom{j-1}{k-1}
$$

Hence:  
$$
P_{1j}(t) = \sum_{k=1}^{j} \binom{j-1}{k-1} e^{-k\lambda t} (-1)^{k-1}
$$

Letting $i = j - k$, and simplifying the index:  
$$
P_{1j}(t) = e^{-\lambda t} \sum_{i=0}^{j-1} \binom{j-1}{i} e^{-i\lambda t} (-1)^i = e^{-\lambda t} (1 - e^{-\lambda t})^{j-1}
$$

Thus, starting with a single individual, the population size at time $t$ has a **geometric distribution** with mean $e^{\lambda t}$. If the population starts with $i$ individuals, then we can regard each of these individuals as starting her own independent Yule process, and so the population at time $t$ will be the sum of $i$ independent and identically distributed geometric random variables with parameter $e^{-\lambda t}$.

Hence, the population size at time $t$ has a **negative binomial distribution** with parameters $i$ and $e^{-\lambda t}$, so:

$$
P_{ij}(t) = \binom{j-1}{i-1} e^{-i\lambda t} (1 - e^{-\lambda t})^{j-i}, \quad j \ge i \ge 1
$$

### Example 6.9  
An urn initially contains one type 1 and one type 2 ball. At each stage, a ball is chosen from the urn, with the chosen ball being equally likely to be any of the balls in the urn. If a type $i$ ball is chosen, then an experiment that is successful with probability $p_i$ is performed; if it is successful then the ball chosen along with a new type $i$ ball are put in the urn, and if it is unsuccessful then only the ball chosen is put in the urn, $i = 1, 2$. We then move to the next stage.

We are interested in determining the mean numbers of type 1 and type 2 balls in the urn after $n$ stages.

**Solution:**  
To determine the mean numbers, for $i = 1,2$, let $m_i(j,k:r)$ denote the mean number of type $i$ balls in the urn after the $n$ stages have elapsed, given that there are currently $j$ type 1 and $k$ type 2 balls in the urn, with a total of $r$ additional stages remaining. Also, let

$$
m(j,k:r) = (m_1(j,k:r), m_2(j,k:r))
$$

We need to determine $m(1,1:n)$. To start, we derive recursive equations for $m(j,k:r)$ by conditioning on the first ball chosen and whether the resulting experiment is successful. This yields:

$$
m(j,k:r) = \frac{j}{j+k} [p_1 m(j+1,k:r-1) + 
q_1 m(j,k:r-1)] + 
\frac{k}{j+k} [p_2 m(j,k+1:r-1) + 
q_2 m(j,k:r-1)]
$$

where $q_i = 1 - p_i$, $i = 1,2$.

Using the base case:
$$
m(j,k:0) = (j, k)
$$

we can use the recursion to determine the values of $m(j,k:r)$ for $r = 1$, then $r = 2$, and so on, up to $r = n$.

---

We can also derive an **approximation** for the mean numbers of type 1 and type 2 balls in the urn after $n$ stages by using a *Poissonization* trick.

Imagine that each ball in the urn, independently of the others, "lights up" at times distributed as a Poisson process with rate $\lambda = 1$. Suppose that each time a type $i$ ball lights up, we conduct the experiment that is successful with probability $p_i$, and add a new type $i$ ball to the urn if it is successful.

Each time a ball lights up, say that a new stage has begun. For an urn with $j$ type 1 and $k$ type 2 balls, the next ball to light up will be of type 1 with probability $\frac{j}{j+k}$. Thus, the numbers of type 1 and type 2 balls in the urn after successive stages are distributed exactly as in the original model.

Whenever there are $j$ type 1 balls, the time until the next type 1 ball lights up is the minimum of $j$ independent exponential random variables with rate 1, which is exponential with rate $j$. Since with probability $p_1$ this results in a new type 1 ball being added, the time until the next type 1 ball is added is exponential with rate $jp_1$.

Therefore, the number of type 1 balls in the urn over time is a **Yule process** with birth parameters:
$$
\lambda_1(j) = jp_1,\quad j \ge 1
$$

Similarly, for type 2:
$$
\lambda_2(j) = jp_2,\quad j \ge 1
$$

These two Yule processes are independent.

Let $N_i(t)$ be the number of type $i$ balls in the urn at time $t$. Then:
$$
N_i(t) \sim \text{Geometric}(1 - e^{-p_i t}) \Rightarrow \mathbb{E}[N_i(t)] = e^{p_i t},\quad i = 1,2
$$

Let $L_i(t)$ be the number of times that a type $i$ ball has lit up by time $t$. Then:
$$
\mathbb{E}[N_i(t)] = p_i \mathbb{E}[L_i(t)] + 1 \Rightarrow \mathbb{E}[L_i(t)] = \frac{e^{p_i t} - 1}{p_i},\quad i = 1,2
$$

Hence, the expected number of stages that have passed by time $t$ is:
$$
\mathbb{E}[L_1(t) + L_2(t)] = \frac{e^{p_1 t} - 1}{p_1} + \frac{e^{p_2 t} - 1}{p_2}
$$

Let $t_n$ be the value of $t$ that makes the above equal $n$, i.e., $t_n$ solves:
$$
\frac{e^{p_1 t_n} - 1}{p_1} + \frac{e^{p_2 t_n} - 1}{p_2} = n
$$

Then we can approximate the expected number of type $i$ balls in the urn after $n$ stages by:
$$
\mathbb{E}[N_i(t_n)] = e^{p_i t_n},\quad i = 1,2
$$

---

**Remarks:**

(i) That $\mathbb{E}[N_i(t)] = p_i \mathbb{E}[L_i(t)] + 1$ is not immediate. The number of light ups affects the probability of success (e.g., larger $L_i(t)$ makes success more likely). So in general,
$$
\mathbb{E}[N_i(t) \mid L_i(t)] \ne p_i L_i(t) + 1
$$
However, the unconditional expectation formula *is* correct and can be proven using **Wald’s equation**, which will be presented in Section 7.3.

(ii) This example has been applied in **drug testing**. Suppose there are two drugs with unknown cure probabilities ($p_1$ and $p_2$). At each stage, a patient receives a drug determined by drawing a ball. If a type $i$ ball is drawn, drug $i$ is used. A successful outcome results in another ball of the same type being added.

(iii) For $p_1 = 0.7$, $p_2 = 0.4$, after $n = 500$ stages:  
- True expected number of type 1 balls: 288.92  
- True expected number of type 2 balls: 36.47  
- Approximate values: 304.09 and 26.23

After 1000 stages:  
- True means: 600.77 and 58.28  
- Approximations: 630.37 and 39.79

---

We shall now derive a set of differential equations that the transition probabilities $P_{ij}(t)$ satisfy in a general continuous-time Markov chain. However, first we need a definition and a pair of lemmas.

For any pair of states $i$ and $j$, let
$$
q_{ij} = \nu_i P_{ij}
$$

Since $\nu_i$ is the rate at which the process makes a transition when in state $i$ and $P_{ij}$ is the probability that this transition is into state $j$, it follows that $q_{ij}$ is the **rate**, when in state $i$, at which the process makes a transition into state $j$. The quantities $q_{ij}$ are called the **instantaneous transition rates**.

Since
$$
\nu_i = \sum_j \nu_i P_{ij} = \sum_j q_{ij}
$$
and
$$
P_{ij} = \frac{q_{ij}}{\nu_i} = \frac{q_{ij}}{\sum_j q_{ij}},
$$
it follows that specifying the instantaneous transition rates determines the parameters of the continuous-time Markov chain.

---

**Lemma 6.2.**  
(a)  
$$
\lim_{h \to 0} \frac{1 - P_{ii}(h)}{h} = \nu_i
$$

(b)  
$$
\lim_{h \to 0} \frac{P_{ij}(h)}{h} = q_{ij}, \quad \text{when } i \ne j
$$

**Proof.**  
We first note that since the amount of time until a transition occurs is exponentially distributed, it follows that the probability of two or more transitions in a time $h$ is $o(h)$ (i.e., vanishes faster than $h$).

Thus, $1 - P_{ii}(h)$, the probability that a process in state $i$ at time 0 will **not** be in state $i$ at time $h$, equals the probability that a transition occurs within time $h$ plus something small compared to $h$. Therefore,
$$
1 - P_{ii}(h) = \nu_i h + o(h)
$$
and part (a) is proven.

To prove part (b), we note that $P_{ij}(h)$, the probability that the process goes from state $i$ to state $j$ in a time $h$, equals the probability that a transition occurs in this time multiplied by the probability that the transition is into state $j$, plus something small compared to $h$. That is,
$$
P_{ij}(h) = h \nu_i P_{ij} + o(h)
$$
and part (b) is proven. $\blacksquare$

---

**Lemma 6.3.**  
For all $s \ge 0$, $t \ge 0$,
$$
P_{ij}(t + s) = \sum_{k=0}^{\infty} P_{ik}(t) P_{kj}(s) \tag{6.8}
$$

**Proof.**  
In order for the process to go from state $i$ to state $j$ in time $t + s$, it must be somewhere at time $t$, and thus:
$$
P_{ij}(t + s) = \mathbb{P}\{X(t + s) = j \mid X(0) = i\}
$$

By the law of total probability:
$$
= \sum_{k=0}^{\infty} \mathbb{P}\{X(t + s) = j, X(t) = k \mid X(0) = i\}
$$

By conditional probability:
$$
= \sum_{k=0}^{\infty} \mathbb{P}\{X(t + s) = j \mid X(t) = k, X(0) = i\} \cdot \mathbb{P}\{X(t) = k \mid X(0) = i\}
$$

By the **Markov property**:
$$
= \sum_{k=0}^{\infty} \mathbb{P}\{X(t + s) = j \mid X(t) = k\} \cdot \mathbb{P}\{X(t) = k \mid X(0) = i\}
$$
$$
= \sum_{k=0}^{\infty} P_{kj}(s) P_{ik}(t)
$$
and the proof is completed. $\blacksquare$

The set of equations (6.8) is known as the **Chapman–Kolmogorov equations**.

From Lemma 6.3, we obtain:
$$
P_{ij}(h + t) - P_{ij}(t) = \sum_{k \ne i} P_{ik}(h) P_{kj}(t) - [1 - P_{ii}(h)] P_{ij}(t)
$$

Thus,
$$
\frac{P_{ij}(t + h) - P_{ij}(t)}{h} = \sum_{k \ne i} \frac{P_{ik}(h)}{h} P_{kj}(t) - \frac{1 - P_{ii}(h)}{h} P_{ij}(t)
$$

Now, assuming that we can interchange the limit and the summation, and applying Lemma 6.2:
$$
\lim_{h \to 0} \frac{P_{ij}(t + h) - P_{ij}(t)}{h} = \sum_{k \ne i} q_{ik} P_{kj}(t) - \nu_i P_{ij}(t)
$$

It turns out that this interchange can indeed be justified, and hence...
