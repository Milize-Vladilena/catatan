## 6.4 Fungsi Probabilitas Transisi

Misalkan $$P_{ij}(t) = \mathbb{P}\{X(t + s) = j \mid X(s) = i\}$$ denotasikan probabilitas bahwa **proses** ada di keadaan $i$ akan berada di keadaan $j$ setelah $t$ waktu. Kuantitas ini yang sering disebut probabilitas transisi dari rantai markov waktu kontinu.

Kita dapat secara eksplisit menentukan $P_{ij}(t)$ dalam proses kasus kelahiran murni yang memiliki rate kelahiran *distinct*. Untuk sebuah proses, misal $X_k$ dinotasikan lama waktu **proses** menghabiskan di keadaan $k$ sebelum berpindah ke keadaan $k+1$, $k \geq 1$. Asumsikan **proses** ada di keadaan $i$ dan misalkan $j> i$. Maka, ketika $X_i$ adalah lama waktu yang dihabiskan di keadaan $i$ sebelum bergerak ke keadaan $i+1$, dan $X_{i+1}$ adalah lama waktu yang dihabiskan di keadaan $i+1$ sebelum bergerak ke keadaan $i+2$, dan seterusnya, mengikuti $$\sum_{k=i}^{j-1} X_k = X_i + X_{i+1} + X_{i+2} + \cdots + X_{j-1}$$ adalah lama waktu yang dibutuhkan sebelum **proses** masuk ke keadaan $j$. Sekarang, jika **proses** belum masuk ke keadaan $j$ pada waktu $t$, maka itu sama aja bilang keadaan $t$ lebih kecil dari $j$, dan sebaliknya. Atau kalo secara matematis ditulisnya. $$X(t)<j \iff X_i + \cdots + X_{j-1} > t$$
Oleh karenanya, untuk $i<j$ proses kelahiran murni, kita punya
$$
\begin{aligned}
\mathbb{P}\{X(t) < j \mid X(0) = i\} &= \mathbb{P}\left\{ \sum_{k=i}^{j-1} X_k > t \right\} \\
&= \mathbb{P}\left\{ X_i + X_{i+1} + X_{i+2} + \cdots + X_{j-1} > t\right\}
\end{aligned}
$$


Akan tetapi, sebab $X_i, \ldots,X_{j-1}$ adalah variabel acak eksponensial dengan masing-masing ratesnya $\lambda_i, \ldots, \lambda_{j-1}$, kita dapat peroleh dari **Konvolusi Variabel Acak Eksponensial** yang mana fungsi distribusi ekor dari $\sum_{k=i}^{j-1} X_k$, itu
$$
\mathbb{P}\{X(t) < j \mid X(0) = i\} = \sum_{k=i}^{j-1} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j-1} \frac{\lambda_r}{\lambda_r - \lambda_k}
$$

:::{.callout-note title="kalo lu lupa fungsi distribusi ekor dari konvolusi eksponensial" collapse=true}

{{< include rantai-markov-waktu-kontinu/__hypoeksponensial.md >}}

:::

Ganti $j$ dengan $j+1$ diperoleh 

$$
\mathbb{P}\{X(t) < j+1 \mid X(0) = i\} = \sum_{k=i}^{j} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j} \frac{\lambda_r}{\lambda_r - \lambda_k}
$$

Ingat lagi, karena parameter waktunya kontinu. Tapi ruang keadaannya tetap **diskrit**. Maka,

$$
\mathbb{P}\{X<x\}=\mathbb{P}\{X<x+1\} - \mathbb{P}\{X<x\}
$$

yakni
$$
\begin{split}
\mathbb{P}\{X(t) = j \mid X(0) = i\} = \mathbb{P}\{X(t) < j+1 \mid X(0) = i\} \\
- \mathbb{P}\{X(t) < j \mid X(0) = i\}
\end{split}
$$

dan karena $P_{ii}(t) = \mathbb{P}\{X_i > t\} = e^{-\lambda_i t}$. Maka, sifat ini mengikuti.

### Proposition 6.1  
Untuk **proses** kelahiran murni yang memiliki $\lambda_i \ne \lambda_j$ ketika $i \ne j$:

$$
P_{ij}(t) = \sum_{k=i}^{j} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j} \frac{\lambda_r}{\lambda_r - \lambda_k} - \sum_{k=i}^{j-1} e^{-\lambda_k t} \prod_{\substack{r=i \\ r \ne k}}^{j-1} \frac{\lambda_r}{\lambda_r - \lambda_k}, \quad i < j
$$

$$
P_{ii}(t) = e^{-\lambda_i t}
$$

