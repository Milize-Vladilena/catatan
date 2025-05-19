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
\mathbb{P}\{X=x\}=\mathbb{P}\{X<x+1\} - \mathbb{P}\{X<x\}
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

### Contoh 6.8

Ingat lagi **proses Yule** dimana proses kelahiran murni yang masing-masing individu di populasi itu independen yang memberikan rate kelahiran $\lambda$, dan begitu juga untuk $\lambda_n = n\lambda, n \geq 1$. Misalkan $i=1$, kita peroleh dari proposisi 6.1:

$$
P_{1j}(t) = \sum_{k=1}^{j} e^{-k\lambda t} \prod_{\substack{r=1 \\ r \ne k}}^{j} \frac{r}{r - k} - \sum_{k=1}^{j-1} e^{-k\lambda t} \prod_{\substack{r=1 \\ r \ne k}}^{j-1} \frac{r}{r - k}
$$

Ini disederhanakan menjadi:
$$
P_{1j}(t) = e^{-j\lambda t} \prod_{r=1}^{j-1} \frac{r}{r - j} + \sum_{k=1}^{j-1} e^{-k\lambda t} \left( \prod_{\substack{r=1 \\ r \ne k}}^{j} \frac{r}{r - k} - \prod_{\substack{r=1 \\ r \ne k}}^{j-1} \frac{r}{r - k} \right)
$$

Lebih lanjut kita dapat sederhanakan menjadi:
$$
\frac{k}{j-k} \prod_{\substack{r=1 \\ r \ne k}}^{j-1} \frac{r}{r - k} = \frac{(j-1)!}{(1-k)(2-k)\cdots(k-1-k)(j-k)!} = (-1)^{k-1} \binom{j-1}{k-1}
$$

Sehingga:
$$
P_{1j}(t) = \sum_{k=1}^{j} \binom{j-1}{k-1} e^{-k\lambda t} (-1)^{k-1}
$$

Misalkan $i = j-k$, dan menyederhanakan index menjadi:
$$
P_{1j}(t) = e^{-\lambda t} \sum_{i=0}^{j-1} \binom{j-1}{i} e^{-i\lambda t} (-1)^i = e^{-\lambda t} (1 - e^{-\lambda t})^{j-1}
$$

Oleh karenanya, dimulai dari individu tunggal, ukuran populasi dimulai dari waktu $t$ memiliki **distribusi geometrik** dengan rerata $e^{\lambdat}$. Jika populasi dimulai dari individu $i$, kita dapat pertimbangkan masing-masing individu dimulai dari **proses Yule independen** sendiri, dan begitu populasi pada waktu $t$ akan dijumlahkan dari independen $i$ dan variabel acak distribusi geometrik identik dengan parameter $e^{-\lambdat}.

Sehingga, ukuran populasi di waktu $t$ memiliki **distribusi binomial negatif** dengan parameter $i$ dan $e^{\lambdat}$, jadi:

$$
P_{ij}(t) = \binom{j-1}{i-1} e^{-i\lambda t} (1 - e^{-\lambda t})^{j-i}, \quad j \ge i \ge 1
$$

### Contoh 6.9
Sebuah gentong mengandung satu bola tipe 1 dan satu bola tipe 2. 