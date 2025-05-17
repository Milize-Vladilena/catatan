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

### Theorem 6.1 (Kolmogorov’s Backward Equations)

For all states $i, j$, and times $t \geq 0$,
$$
\frac{d}{dt} P_{ij}(t) = \sum_{k \ne i} q_{ik} P_{kj}(t) - \nu_i P_{ij}(t)
$$

---

### Example 6.10  
**The backward equations for the pure birth process become:**
$$
\frac{d}{dt} P_{ij}(t) = \lambda_i P_{i+1,j}(t) - \lambda_i P_{ij}(t)
$$

**The backward equations for the birth and death process become:**

For $i = 0$:
$$
\frac{d}{dt} P_{0j}(t) = \lambda_0 [P_{1j}(t) - P_{0j}(t)]
$$

For $i > 0$:
$$
\frac{d}{dt} P_{ij}(t) = \lambda_i P_{i+1,j}(t) + \mu_i P_{i-1,j}(t) - (\lambda_i + \mu_i) P_{ij}(t) \tag{6.9}
$$

---

### Example 6.11 (A Continuous-Time Markov Chain Consisting of Two States)  

Consider a machine that works for an exponential amount of time with mean $1/\lambda$ before breaking down; and suppose that it takes an exponential amount of time with mean $1/\mu$ to repair the machine.

Let state 0 = "working", and state 1 = "under repair".

**Parameters:**
- $\lambda_0 = \lambda$, $\mu_1 = \mu$
- $\lambda_i = 0$ for $i \ne 0$, $\mu_i = 0$ for $i \ne 1$

From the backward equations:
- Equation (6.10):
  $$
  \frac{d}{dt} P_{00}(t) = \lambda [P_{10}(t) - P_{00}(t)]
  $$
- Equation (6.11):
  $$
  \frac{d}{dt} P_{10}(t) = \mu P_{00}(t) - \mu P_{10}(t)
  $$

Multiply (6.10) by $\mu$, and (6.11) by $\lambda$, then add:
$$
\mu \frac{d}{dt} P_{00}(t) + \lambda \frac{d}{dt} P_{10}(t) = 0
$$

Integrating:
$$
\mu P_{00}(t) + \lambda P_{10}(t) = \mu \tag{6.12}
$$

From this,
$$
\lambda P_{10}(t) = \mu[1 - P_{00}(t)]
$$

Substitute into (6.10):
$$
\frac{d}{dt} P_{00}(t) = \mu[1 - P_{00}(t)] - \lambda P_{00}(t) = \mu - (\mu + \lambda) P_{00}(t)
$$

Let $h(t) = P_{00}(t) - \frac{\mu}{\mu + \lambda}$, then:
$$
h'(t) = -(\mu + \lambda) h(t) \Rightarrow h(t) = K e^{-(\mu + \lambda)t}
$$

Use initial condition $P_{00}(0) = 1$:
$$
P_{00}(t) = \frac{\lambda}{\mu + \lambda} e^{-(\mu + \lambda)t} + \frac{\mu}{\mu + \lambda}
$$

From (6.12), we also get:
$$
P_{10}(t) = \frac{\mu}{\mu + \lambda} \left(1 - e^{-(\mu + \lambda)t} \right)
$$

Thus, the probability that the machine is working at time $t = 10$ is:
$$
P_{00}(10) = \frac{\lambda}{\mu + \lambda} e^{-10(\mu + \lambda)} + \frac{\mu}{\mu + \lambda}
$$

---

### Kolmogorov’s Forward Equations

From the Chapman–Kolmogorov equations:
$$
P_{ij}(t + h) - P_{ij}(t) = \sum_{k \ne j} P_{ik}(t) P_{kj}(h) - [1 - P_{jj}(h)] P_{ij}(t)
$$

Divide by $h$ and take the limit:
$$
\frac{d}{dt} P_{ij}(t) = \sum_{k \ne j} q_{kj} P_{ik}(t) - \nu_j P_{ij}(t)
$$

This leads to the next theorem.

---

### Theorem 6.2 (Kolmogorov’s Forward Equations)

Under suitable regularity conditions,
$$
\frac{d}{dt} P_{ij}(t) = \sum_{k \ne j} q_{kj} P_{ik}(t) - \nu_j P_{ij}(t) \tag{6.13}
$$

---

We now solve the forward equations for the **pure birth process**. For this case, (6.13) becomes:
$$
\frac{d}{dt} P_{ij}(t) = \lambda_{j-1} P_{i,j-1}(t) - \lambda_j P_{ij}(t)
$$

Since $P_{ij}(t) = 0$ when $j < i$, we can write:
$$
\frac{d}{dt} P_{ii}(t) = -\lambda_i P_{ii}(t) \\
\frac{d}{dt} P_{ij}(t) = \lambda_{j-1} P_{i,j-1}(t) - \lambda_j P_{ij}(t), \quad j \ge i+1 \tag{6.14}
$$

---

### Proposition 6.4  
For a pure birth process:
$$
P_{ii}(t) = e^{-\lambda_i t}, \quad i \ge 0
$$
$$
P_{ij}(t) = \lambda_{j-1} e^{-\lambda_j t} \int_0^t e^{\lambda_j s} P_{i,j-1}(s) \, ds, \quad j \ge i + 1
$$

**Proof sketch:** Integrate both sides of (6.14) using the integrating factor $e^{\lambda_j t}$ and initial condition $P_{ij}(0) = 0$.

---

### Example 6.12 (Forward Equations for Birth and Death Process)

Using Eq. (6.13), for the birth-death process we get:

For $j = 0$:
$$
\frac{d}{dt} P_{i0}(t) = \mu_1 P_{i1}(t) - \lambda_0 P_{i0}(t) \tag{6.15}
$$

For $j \ge 1$:
$$
\frac{d}{dt} P_{ij}(t) = \lambda_{j-1} P_{i,j-1}(t) + \mu_{j+1} P_{i,j+1}(t) - (\lambda_j + \mu_j) P_{ij}(t) \tag{6.16}
$$


## 6.5 Limiting Probabilities

In analogy with a basic result in discrete-time Markov chains, the probability that a continuous-time Markov chain will be in state $j$ at time $t$ often converges to a limiting value that is independent of the initial state. That is, if we call this value $P_j$, then
$$
P_j \equiv \lim_{t \to \infty} P_{ij}(t)
$$
where we assume the limit exists and is independent of the initial state $i$.

To derive a set of equations for the $P_j$, consider the forward equations:
$$
\frac{d}{dt} P_{ij}(t) = \sum_{k \ne j} q_{kj} P_{ik}(t) - \nu_j P_{ij}(t) \tag{6.17}
$$

Letting $t \to \infty$ and assuming we can interchange the limit and summation:
$$
\lim_{t \to \infty} \frac{d}{dt} P_{ij}(t) = \sum_{k \ne j} q_{kj} P_k - \nu_j P_j
$$

But since $P_{ij}(t)$ is a bounded function, its derivative must converge to 0:
$$
0 = \sum_{k \ne j} q_{kj} P_k - \nu_j P_j
$$

That is,
$$
\nu_j P_j = \sum_{k \ne j} q_{kj} P_k, \quad \text{for all states } j \tag{6.18}
$$

Along with the normalization condition:
$$
\sum_j P_j = 1 \tag{6.19}
$$

This system can be used to solve for the limiting probabilities.

---

**Remarks:**

(i) We have assumed that the limiting probabilities $P_j$ exist. A sufficient condition is:
- (a) All states communicate (i.e., from any state $i$ there's positive probability of reaching any $j$).
- (b) The chain is positive recurrent (the mean return time to any state is finite).

If (a) and (b) hold, then $P_j$ exists, satisfies (6.18) and (6.19), and $P_j$ also represents the long-run proportion of time spent in state $j$.

(ii) Eq. (6.18) has a **balance equation** interpretation:  
In the long run, the rate at which transitions **enter** state $j$ equals the rate at which transitions **leave** state $j$:
- Rate leaving state $j$: $\nu_j P_j$
- Rate entering from $k$: $q_{kj} P_k$
Thus:
$$
\sum_{k \ne j} q_{kj} P_k = \nu_j P_j
$$

---

### Limiting Probabilities for a Birth and Death Process

From (6.18), or by balancing rate in = rate out, we obtain:

| State | Leave rate = Enter rate |
|-------|-------------------------|
| 0     | $\lambda_0 P_0 = \mu_1 P_1$ |
| 1     | $(\lambda_1 + \mu_1) P_1 = \mu_2 P_2 + \lambda_0 P_0$ |
| 2     | $(\lambda_2 + \mu_2) P_2 = \mu_3 P_3 + \lambda_1 P_1$ |
| $\cdots$ | $\cdots$ |

Adding each equation to the previous yields:
$$
\lambda_0 P_0 = \mu_1 P_1 \\
\lambda_1 P_1 = \mu_2 P_2 \\
\lambda_2 P_2 = \mu_3 P_3 \\
\vdots
$$

Solving recursively in terms of $P_0$:
$$
P_1 = \frac{\lambda_0}{\mu_1} P_0 \\
P_2 = \frac{\lambda_1}{\mu_2} P_1 = \frac{\lambda_1 \lambda_0}{\mu_2 \mu_1} P_0 \\
\cdots \\
P_n = \frac{\lambda_0 \lambda_1 \cdots \lambda_{n-1}}{\mu_1 \mu_2 \cdots \mu_n} P_0
$$

Using normalization $\sum_{n=0}^\infty P_n = 1$:
$$
P_0 = \left( 1 + \sum_{n=1}^\infty \frac{\lambda_0 \lambda_1 \cdots \lambda_{n-1}}{\mu_1 \mu_2 \cdots \mu_n} \right)^{-1}
$$

So:
$$
P_n = \frac{\lambda_0 \cdots \lambda_{n-1}}{\mu_1 \cdots \mu_n} P_0, \quad n \ge 1 \tag{6.20}
$$

**Existence condition:**  
The limiting probabilities exist if:
$$
\sum_{n=1}^\infty \frac{\lambda_0 \cdots \lambda_{n-1}}{\mu_1 \cdots \mu_n} < \infty \tag{6.21}
$$

---

### Examples:

**Multiserver Exponential Queue (Example 6.6):**

Condition (6.21) reduces to:
$$
\sum_{n=s+1}^\infty \frac{\lambda^n}{(s\mu)^n} < \infty
\quad \Rightarrow \quad \lambda < s\mu
$$

---

**Linear Growth Model with Immigration (Example 6.4):**

Condition (6.21) becomes:
$$
\sum_{n=1}^\infty \frac{\theta(\theta + \lambda) \cdots (\theta + (n - 1)\lambda)}{n! \mu^n}
$$

Apply ratio test:
$$
\lim_{n \to \infty} \frac{\theta + n\lambda}{(n + 1)\mu} = \frac{\lambda}{\mu} < 1
\quad \Rightarrow \text{Converges if } \lambda < \mu
$$

---

### Example 6.13 (Machine Repair Model)

- $M$ machines, one repairman
- Time to fail: $\text{Exp}(1/\lambda)$, repair time: $\text{Exp}(1/\mu)$
- Let state $n$ be the number of failed machines

Parameters:
- $\mu_n = \mu$, $n \ge 1$
- $\lambda_n = (M - n)\lambda$, $n \le M$; $\lambda_n = 0$ otherwise

From (6.20):
- $P_0 = \left(1 + \sum_{n=1}^M \frac{(M\lambda)(M-1)\lambda \cdots (M - n + 1)\lambda}{\mu^n} \right)^{-1}$
- Simplifies to:
  $$
  P_0 = \left(1 + \sum_{n=1}^M \frac{(\lambda/\mu)^n M!}{(M - n)!} \right)^{-1}
  $$
  $$
  P_n = \frac{(\lambda/\mu)^n M!}{(M - n)!} \cdot P_0, \quad n = 0, \dots, M
  $$

**Average number of machines not in use:**
$$
\sum_{n=0}^M n P_n = \frac{\sum_{n=0}^M n (\lambda/\mu)^n M! / (M - n)!}{1 + \sum_{n=1}^M (\lambda/\mu)^n M! / (M - n)!} \tag{6.22}
$$

**Proportion of time a given machine is working:**
$$
1 - \frac{1}{M} \sum_{n=0}^M n P_n
$$

---

### Example 6.14 (The M/M/1 Queue)

- $\lambda_n = \lambda$, $\mu_n = \mu$
- From (6.20):
  $$
  P_n = \frac{(\lambda/\mu)^n}{1 + \sum_{k=1}^\infty (\lambda/\mu)^k} = (\lambda/\mu)^n (1 - \lambda/\mu), \quad n \ge 0
  $$
- Valid only if $\lambda < \mu$.

---

### Example 6.15 (Shoe Shine Shop)

- 3 states: 0, 1, 2 (number of customers)
- Transitions: 2 → 0 possible, not birth-death
- Use balance equations:

| State | Leave rate = Enter rate |
|-------|--------------------------|
| 0     | $\lambda P_0 = \mu_2 P_2$ |
| 1     | $\mu_1 P_1 = \lambda P_0$ |
| 2     | $\mu_2 P_2 = \mu_1 P_1$ |

Solve:
- $P_1 = \frac{\lambda}{\mu_1} P_0$, $P_2 = \frac{\lambda}{\mu_2} P_0$

Normalize:
$$
P_0 = \frac{\mu_1 \mu_2}{\mu_1 \mu_2 + \lambda (\mu_1 + \mu_2)}
$$

So:
$$
P_1 = \frac{\lambda \mu_2}{\mu_1 \mu_2 + \lambda (\mu_1 + \mu_2)}, \quad
P_2 = \frac{\lambda \mu_1}{\mu_1 \mu_2 + \lambda (\mu_1 + \mu_2)}
$$

---

### Example 6.16 (Preemptive Repair with n Components)

- $n$ components, one repairman
- Each component $i$ fails with rate $\lambda_i$, repaired with rate $\mu_i$
- Most recent failure is repaired first (preemption allowed)
- State: ordered list of failed components

Number of states:
$$
\sum_{k=0}^n \binom{n}{k} k! = n! \sum_{i=0}^n \frac{1}{i!}
$$

Let $P(i_1, ..., i_k)$ be the steady-state probability of state $(i_1, ..., i_k)$.

Balance equations:
- Exit rate from $(i_1, ..., i_k)$:
  $$
  \mu_{i_1} + \sum_{\substack{i \ne i_j \\ j=1..k}} \lambda_i
  $$
- Entry:
  - From $(i_2, ..., i_k)$ if $i_1$ fails
  - From $(i, i_1, ..., i_k)$ if $i$ (not in list) is repaired

Let
$$
P(i_1, ..., i_k) = \frac{\lambda_{i_1} \cdots \lambda_{i_k}}{\mu_{i_1} \cdots \mu_{i_k}} P(\varnothing) \tag{6.24}
$$

Normalization:
$$
P(\varnothing) = \left[ 1 + \sum_{i_1,...,i_k} \frac{\lambda_{i_1} \cdots \lambda_{i_k}}{\mu_{i_1} \cdots \mu_{i_k}} \right]^{-1}
$$

**Example with $n = 2$**: states: $\varnothing$, 1, 2, 12, 21

- $P(1) = \frac{\lambda_1}{\mu_1} P(\varnothing)$
- $P(2) = \frac{\lambda_2}{\mu_2} P(\varnothing)$
- $P(1,2) = P(2,1) = \frac{\lambda_1 \lambda_2}{\mu_1 \mu_2} P(\varnothing)$
- Normalize:
  $$
  P(\varnothing) = \left[ 1 + \frac{\lambda_1}{\mu_1} + \frac{\lambda_2}{\mu_2} + 2 \cdot \frac{\lambda_1 \lambda_2}{\mu_1 \mu_2} \right]^{-1}
  $$

**Observation**: given the set of failed components, all orderings are equally likely.

---

When the limiting probabilities exist, we say the chain is **ergodic**. The $P_j$ are also called **stationary probabilities**, because if the chain starts in state $j$ with probability $P_j$, then:
$$
\mathbb{P}(X(t) = j) = P_j, \quad \text{for all } t
$$

**Verification:**
Assume initial state distributed as $\{P_j\}$:
$$
\mathbb{P}(X(t) = j) = \sum_k P_{kj}(t) P_k = \lim_{s \to \infty} \sum_k P_{kj}(t) P_{ik}(s) = \lim_{s \to \infty} P_{ij}(t + s) = P_j
$$
(by Chapman–Kolmogorov and limit properties)

## 6.6 Time Reversibility

Consider a continuous-time Markov chain that is **ergodic**, and let $P_i$ denote its limiting probabilities. If we ignore the time spent in each state and just look at the **sequence of states visited**, it forms a discrete-time Markov chain (called the **embedded chain**) with transition probabilities $P_{ij}$. Let $\pi_i$ be the limiting probabilities of this embedded chain, satisfying:

$$
\pi_i = \sum_j \pi_j P_{ji}, \quad \sum_i \pi_i = 1
$$

Since $\pi_i$ is the proportion of **transitions** into state $i$, and $1/\nu_i$ is the mean time spent in state $i$ per visit, it's intuitive that $P_i$, the proportion of **time** in state $i$, is:

$$
P_i = \frac{\pi_i / \nu_i}{\sum_j \pi_j / \nu_j} \tag{6.25}
$$

This is confirmed via the balance equation:
$$
\nu_i P_i = \sum_{j \ne i} P_j q_{ji} = \sum_j P_j \nu_j P_{ji}
$$

Suppose the chain is observed in **steady state**, and we **reverse** time from some time $T$. The reversed process is also a continuous-time Markov chain, with:
- Sojourn times in each state still exponential with rate $\nu_i$
- Transition probabilities:
$$
Q_{ij} = \frac{\pi_j P_{ji}}{\pi_i}
$$

Thus, the reversed process has same rates and is **time reversible** if:
$$
\pi_i P_{ij} = \pi_j P_{ji}, \quad \forall i, j
$$

Given:
$$
P_i = \frac{\pi_i / \nu_i}{\sum_j \pi_j / \nu_j}
$$

This condition becomes:
$$
P_i q_{ij} = P_j q_{ji} \tag{6.26}
$$

**Interpretation**:  
In time-reversible chains, the **rate** of direct transitions from $i$ to $j$ equals the rate from $j$ to $i$.

---

### Proposition 6.5

**An ergodic birth and death process is time reversible.**

**Proof sketch**: In any interval, the number of transitions from $i$ to $i+1$ differs by at most 1 from transitions from $i+1$ to $i$. Hence, over long time, their rates must be equal.

---

### Corollary 6.6

**In an M/M/s queue with $\lambda < s\mu$, the departure process is a Poisson process with rate $\lambda$ (in steady state).**

**Reason**: The process is time reversible. In forward time, arrivals are Poisson. So in reverse, "arrivals" are actually departures in forward time ⇒ Poisson.

---

### Example 6.17 (Queue Occupancy Interpretation)

Let C be a customer in an **M/M/1** queue with arrival rate $\lambda$ and service rate $\mu$ ($\lambda < \mu$). Given that C spends time $t$ in the system, what's the distribution of the number of others present at their arrival?

**Solution**:  
By reversibility, number of departures in $(s, s+t)$ is equal in distribution to number of **arrivals** in that interval in the reversed process. Thus, this number is **Poisson($\lambda t$)**.

### Proposition 6.7  
Suppose that an ergodic continuous-time Markov chain has transition rates $q_{ij}$ and limiting probabilities $P_i$. If
$$
P_i q_{ij} = P_j q_{ji} \quad \text{for all } i, j \tag{6.27}
$$
then the process is **time reversible**.

**Proof sketch**:  
From this condition, it's easy to verify that the reversed process has the same dynamics as the forward process. Specifically, the reversed transition rates $q_{ij}^*$ become:
$$
q_{ij}^* = \frac{P_j q_{ji}}{P_i} = q_{ij}
$$
Thus, the reversed process has the same generator matrix $Q$, hence same law.

---

### Example 6.18 (Two-Server Queue)  
A two-server queue has a maximum of three customers. Arrivals follow a Poisson process with rate $\lambda$ and service is exponential with rate $\mu$ per server.

States: 0, 1, 2, 3 (number of customers)

Transition diagram:
- $0 \xrightarrow{\lambda} 1$
- $1 \xrightarrow{\lambda} 2$, $1 \xrightarrow{\mu} 0$
- $2 \xrightarrow{\lambda} 3$, $2 \xrightarrow{2\mu} 1$
- $3 \xrightarrow{2\mu} 2$

Let’s check time reversibility:
- Solve for stationary probabilities:
  $$
  P_1 = \frac{\lambda}{\mu} P_0,\quad
  P_2 = \frac{\lambda}{2\mu} P_1 = \frac{\lambda^2}{2\mu^2} P_0,\quad
  P_3 = \frac{\lambda}{2\mu} P_2 = \frac{\lambda^3}{4\mu^3} P_0
  $$

Normalization:
$$
P_0 = \left(1 + \frac{\lambda}{\mu} + \frac{\lambda^2}{2\mu^2} + \frac{\lambda^3}{4\mu^3}\right)^{-1}
$$

Now check detailed balance:
$$
P_0 \cdot \lambda = P_1 \cdot \mu \quad \text{✓} \\
P_1 \cdot \lambda = P_2 \cdot 2\mu \quad \text{✓} \\
P_2 \cdot \lambda = P_3 \cdot 2\mu \quad \text{✓}
$$

Thus, the process is **time reversible**.

---

### Example 6.19 (Jackson Network)

Let a network consist of $n$ service stations. Customers:
- arrive from outside to station $i$ at rate $r_i$,
- get served (service rate $\mu_i$),
- then with probability $P_{ij}$ go to station $j$, or
- with probability $1 - \sum_j P_{ij}$ leave the system.

Let $\lambda_i$ be the **total arrival rate** to station $i$ (external + internal). Then:
$$
\lambda_i = r_i + \sum_{j=1}^n \lambda_j P_{ji}
$$

This is a system of **traffic equations**. Once solved, define the **utilization** of station $i$:
$$
\rho_i = \frac{\lambda_i}{\mu_i}
$$

If all $\rho_i < 1$, then in steady state the queue at station $i$ behaves like an M/M/1 queue.

The network has **product-form solution**:
$$
P(n_1, ..., n_n) = \prod_{i=1}^n (1 - \rho_i) \rho_i^{n_i}
$$

This process is **not** time reversible in general (because the routing matrix $P_{ij}$ may not be symmetric), but the **stationary distribution** still exists and has a nice form.

---

### Summary: Time Reversibility

- A continuous-time Markov chain is **time reversible** if:
  $$
  P_i q_{ij} = P_j q_{ji}, \quad \text{for all } i, j
  $$
- Time-reversible chains have a particularly simple form of the **balance equations**
- Common reversible examples:
  - Birth–death processes
  - M/M/s queues
  - Some queueing networks with symmetric routing

## 6.7 Applications of Continuous-Time Markov Chains

We now consider some practical applications of the theory of continuous-time Markov chains.

---

### Example 6.20 (Switching Between Two Machines)

A factory has two machines, A and B. Only one is operated at a time. When A is operating, it breaks down at rate $\lambda_1$, and when B is operating, it breaks down at rate $\lambda_2$. When a machine breaks, the other is repaired and operation switches to that one. The time to repair is negligible.

**State description**:  
Let the state be the currently running machine: state 1 = A, state 2 = B.

**Transition rates**:
- From state 1 to 2: $\lambda_1$
- From state 2 to 1: $\lambda_2$

This forms a two-state continuous-time Markov chain.

**Limiting probabilities**:
- Let $P_1$ and $P_2$ be the steady-state probabilities.

From balance:
$$
\lambda_1 P_1 = \lambda_2 P_2
$$

With $P_1 + P_2 = 1$:
$$
P_1 = \frac{\lambda_2}{\lambda_1 + \lambda_2}, \quad P_2 = \frac{\lambda_1}{\lambda_1 + \lambda_2}
$$

So the **long-run proportion of time** that machine A is operating is $P_1$.

---

### Example 6.21 (System Availability)

A two-unit system operates as long as **at least one unit is operational**.  
Each unit:
- fails with rate $\lambda$
- is repaired with rate $\mu$

If both are operational, the failure of either results in a transition to one unit working. If only one is working and it fails, system is down.

**States**:
- 2: both working  
- 1: one working  
- 0: both failed  

**Transitions**:
- $2 \to 1$ with rate $2\lambda$
- $1 \to 0$ with rate $\lambda$
- $1 \to 2$ with rate $\mu$
- $0 \to 1$ with rate $\mu$

**Balance equations**:
Let $P_0$, $P_1$, $P_2$ be steady-state probabilities.

From flow balance:
- $\lambda P_1 = \mu P_0$
- $2\lambda P_2 = \mu P_1$
- $P_0 + P_1 + P_2 = 1$

Solve:
1. $P_0 = \frac{\lambda}{\mu} P_1$
2. $P_2 = \frac{\mu}{2\lambda} P_1$

Substitute into normalization:
$$
\frac{\lambda}{\mu} P_1 + P_1 + \frac{\mu}{2\lambda} P_1 = 1 \Rightarrow P_1 \left( \frac{\lambda}{\mu} + 1 + \frac{\mu}{2\lambda} \right) = 1
$$

Solve for $P_1$, then:
$$
P_{\text{up}} = P_1 + P_2 = 1 - P_0
$$

This gives **long-run availability** of the system.

---

### Example 6.22 (Computer Virus Spread)

A network of $n$ computers. Any infected computer can infect any uninfected one at rate $\lambda$, and any infected computer gets cleaned at rate $\mu$.

Let $X(t)$ be the number of infected computers at time $t$. Then $\{X(t)\}$ is a **birth–death process** on states $0$ to $n$, with:

- $\lambda_i = \lambda i (n - i)$: $i$ infected can infect $(n - i)$ others
- $\mu_i = \mu i$: each infected gets cleaned

**Goal**: find the **expected time to infection extinction** starting from $i$ infected computers.

Let $m_i = \mathbb{E}[\text{time until absorption at 0} \mid X(0) = i]$

Recursion:
$$
m_0 = 0 \\
m_i = \frac{1}{\lambda_i + \mu_i} + \frac{\lambda_i}{\lambda_i + \mu_i} m_{i+1} + \frac{\mu_i}{\lambda_i + \mu_i} m_{i-1}, \quad i = 1, \dots, n-1 \\
m_n = \frac{1}{\mu_n} + m_{n-1}
$$

This is a standard way to compute **expected hitting times** in birth–death processes.

---

### Application Notes

The above examples illustrate:
- Modeling with CTMCs by carefully defining **states** and **transition rates**
- Using **limiting probabilities** for long-run behavior
- Using **first-step analysis** and recurrence relations to solve for expectations
- Relevance to systems reliability, networking, queueing, and more

## 6.7 Applications of Continuous-Time Markov Chains

We now consider some practical applications of the theory of continuous-time Markov chains.

---

### Example 6.20 (Switching Between Two Machines)

A factory has two machines, A and B. Only one is operated at a time. When A is operating, it breaks down at rate $\lambda_1$, and when B is operating, it breaks down at rate $\lambda_2$. When a machine breaks, the other is repaired and operation switches to that one. The time to repair is negligible.

**State description**:  
Let the state be the currently running machine: state 1 = A, state 2 = B.

**Transition rates**:
- From state 1 to 2: $\lambda_1$
- From state 2 to 1: $\lambda_2$

This forms a two-state continuous-time Markov chain.

**Limiting probabilities**:
- Let $P_1$ and $P_2$ be the steady-state probabilities.

From balance:
$$
\lambda_1 P_1 = \lambda_2 P_2
$$

With $P_1 + P_2 = 1$:
$$
P_1 = \frac{\lambda_2}{\lambda_1 + \lambda_2}, \quad P_2 = \frac{\lambda_1}{\lambda_1 + \lambda_2}
$$

So the **long-run proportion of time** that machine A is operating is $P_1$.

---

### Example 6.21 (System Availability)

A two-unit system operates as long as **at least one unit is operational**.  
Each unit:
- fails with rate $\lambda$
- is repaired with rate $\mu$

If both are operational, the failure of either results in a transition to one unit working. If only one is working and it fails, system is down.

**States**:
- 2: both working  
- 1: one working  
- 0: both failed  

**Transitions**:
- $2 \to 1$ with rate $2\lambda$
- $1 \to 0$ with rate $\lambda$
- $1 \to 2$ with rate $\mu$
- $0 \to 1$ with rate $\mu$

**Balance equations**:
Let $P_0$, $P_1$, $P_2$ be steady-state probabilities.

From flow balance:
- $\lambda P_1 = \mu P_0$
- $2\lambda P_2 = \mu P_1$
- $P_0 + P_1 + P_2 = 1$

Solve:
1. $P_0 = \frac{\lambda}{\mu} P_1$
2. $P_2 = \frac{\mu}{2\lambda} P_1$

Substitute into normalization:
$$
\frac{\lambda}{\mu} P_1 + P_1 + \frac{\mu}{2\lambda} P_1 = 1 \Rightarrow P_1 \left( \frac{\lambda}{\mu} + 1 + \frac{\mu}{2\lambda} \right) = 1
$$

Solve for $P_1$, then:
$$
P_{\text{up}} = P_1 + P_2 = 1 - P_0
$$

This gives **long-run availability** of the system.

---

### Example 6.22 (Computer Virus Spread)

A network of $n$ computers. Any infected computer can infect any uninfected one at rate $\lambda$, and any infected computer gets cleaned at rate $\mu$.

Let $X(t)$ be the number of infected computers at time $t$. Then $\{X(t)\}$ is a **birth–death process** on states $0$ to $n$, with:

- $\lambda_i = \lambda i (n - i)$: $i$ infected can infect $(n - i)$ others
- $\mu_i = \mu i$: each infected gets cleaned

**Goal**: find the **expected time to infection extinction** starting from $i$ infected computers.

Let $m_i = \mathbb{E}[\text{time until absorption at 0} \mid X(0) = i]$

Recursion:
$$
m_0 = 0 \\
m_i = \frac{1}{\lambda_i + \mu_i} + \frac{\lambda_i}{\lambda_i + \mu_i} m_{i+1} + \frac{\mu_i}{\lambda_i + \mu_i} m_{i-1}, \quad i = 1, \dots, n-1 \\
m_n = \frac{1}{\mu_n} + m_{n-1}
$$

This is a standard way to compute **expected hitting times** in birth–death processes.

---

### Application Notes

The above examples illustrate:

- Modeling with CTMCs by carefully defining **states** and **transition rates**
- Using **limiting probabilities** for long-run behavior
- Using **first-step analysis** and recurrence relations to solve for expectations
- Relevance to systems reliability, networking, queueing, and more
