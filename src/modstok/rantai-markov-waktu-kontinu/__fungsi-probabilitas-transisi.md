## 6.4 Fungsi Probabilitas Transisi

Misalkan $$P_{ij}(t) = \mathbb{P}\{X(t + s) = j \mid X(s) = i\}$$ denotasikan probabilitas bahwa **proses** ada di keadaan $i$ akan berada di keadaan $j$ setelah $t$ waktu. Kuantitas ini yang sering disebut probabilitas transisi dari rantai markov waktu kontinu.

Kita dapat secara eksplisit menentukan $P_{ij}(t)$ dalam proses kasus kelahiran murni yang memiliki rate kelahiran *distinct*. Untuk sebuah proses, misal $X_k$ dinotasikan lama waktu **proses** menghabiskan di keadaan $k$ sebelum berpindah ke keadaan $k+1$, $k \geq 1$. Asumskan **proses** ada di keadaan $i$ dan misalkan $j> i$. Maka, ketika $X_i$ adalah lama waktu yang dihabiskan di keadaan $i$ sebelum bergerak ke keadaan $i+1$, dan $X_{i+1}$ adalah lama waktu yang dihabiskan di keadaan $i+1$ sebelum bergerak ke keadaan $i+2$, dan seterusnya, mengikuti $$\sum_{k=i}^{j-1} X_k = X_i + X_{i+1} + X_{i+2} + \cdots + X_{j-1}$$ adalah lama waktu yang dibutuhkan sebelum **proses** masuk ke keadaan $j$. Sekarang, jika **proses** belum masuk ke keadaan $j$ pada waktu $t$, maka itu sama aja bilang keadaan $t$ lebih kecil dari $j$, dan sebaliknya. Atau kalo secara matematis ditulisnya. $$X(t)<j \iff X_i + \cdots + X_{j-1} > t$$
Oleh karenanya, untuk $i<j$ proses kelahiran murni, kita punya
$$
\begin{align*}
\mathbb{P}\{X(t) < j \mid X(0) = i\} &= \mathbb{P}\left\{ \sum_{k=i}^{j-1} X_k > t \right\} \\
&= \mathbb{P}\left\{ X_i + X_{i+1} + X_{i+2} + \cdots + X_{j-1} > t\right\}
\end{align*}
$$


Akan tetapi