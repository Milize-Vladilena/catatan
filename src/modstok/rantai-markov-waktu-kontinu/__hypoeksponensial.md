### 5.2.4 Konvolusi dari variabel acak eksponensial

Misal $X_i, i = 1, \ldots, n$, adalah variabel acak eksponensial independen dengan rates masing-masing $\lambda_i, i = 1, \ldots , n$ dan asumsikan $\lambda_i \neq \lambda_j$ untuk $i \neq j$. Variabel acak $\sum_{i=1}^n X_i$ dikatakan variabel acak *hypoeksponensial*. 

Untuk hitung fungsi padatan probabilitas, pertama mulai pada kasus $n=2$. Sekarang,

$$
\begin{aligned}
f_{X_1+X_2} &= \int_0^t f_{X_1}(s) f_{X_2}(t-s)ds \\
&= \int_0^t \lambda_1e^{-\lambda_1s}\lambda_2e^{-\lambda_2(t-s)} ds \\
&= \lambda_1 \lambda_2 e^{-\lambda_2t} \int_0^t e^{-(\lambda_1 - \lambda_2)s} ds \\
&= \frac{\lambda_1}{\lambda_1 -\lambda_2} \lambda_2 e^{-\lambda_2t}(1-e^{-(\lambda_1 - \lambda_2)t}) \\
&= \frac{\lambda_1}{\lambda_1 - \lambda_2} \lambda_2 e^{-\lambda_2 t} + \frac{\lambda_2}{\lambda_2 - \lambda_1} \lambda_1 e^{-\lambda_1t}
\end{aligned}
$$ 

dengan cara yang sama untuk $n=3$, yakni

$$
\begin{aligned}
f_{X_1+X_2+X_3} &= \int_0^t f_{X_1 + X_2}(s)f_{X_3}(t-s)ds \\
&= \int_0^t \left( \frac{\lambda_1}{\lambda_1 - \lambda_2} \lambda_2 e^{-\lambda_2 s} + \frac{\lambda_2}{\lambda_2 - \lambda_1} \lambda_1 e^{-\lambda_1s} \right) \lambda_3e^{-\lambda_3(t-s)} ds \\
&= \int_0^t \left( \frac{\lambda_1}{\lambda_1 - \lambda_2} \lambda_2 e^{-\lambda_2 s} + \frac{\lambda_2}{\lambda_2 - \lambda_1} \lambda_1 e^{-\lambda_1s} \right) \lambda_3e^{\lambda_3s} e^{-\lambda_3t} ds \\
&= \int_0^t \left( \frac{\lambda_1}{\lambda_1 - \lambda_2} \lambda_2 \lambda_3 e^{-(\lambda_2 - \lambda_3)s} + \frac{\lambda_2}{\lambda_2 - \lambda_1} \lambda_1 \lambda_3 e^{-(\lambda_1-\lambda_3)s} \right)e^{-\lambda_3t} ds \\
&= e^{-\lambda_3t} \left(\int_0^t \frac{\lambda_1}{\lambda_1 - \lambda_2} \lambda_2 \lambda_3 e^{-(\lambda_2 - \lambda_3)s} ds + \int_0^t \frac{\lambda_2}{\lambda_2 - \lambda_1} \lambda_1 \lambda_3 e^{-(\lambda_1-\lambda_3)s} ds \right)\\
&= e^{-\lambda_3t} \left(
    \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   \int_0^t e^{-(\lambda_2 - \lambda_3)s} ds +
    \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}  \int_0^t e^{-(\lambda_1-\lambda_3)s} ds \right)\\
&= e^{-\lambda_3t} \left(
    \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
    \frac{1}{\lambda_2 - \lambda_3} \left(
    1- e^{-(\lambda_2 - \lambda_3)t}
    \right) +
    \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
    \frac{1}{\lambda_1 - \lambda_3}\left(
     1 - e^{-(\lambda_1 - \lambda_3)t}
     \right)
    \right)\\
&= \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_3t}}{\lambda_2 - \lambda_3} \left(
    1- e^{-(\lambda_2 - \lambda_3)t}
    \right) +
    \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
    \frac{e^{-\lambda_3t}}{\lambda_1 - \lambda_3}\left(
    1 - e^{-(\lambda_1 - \lambda_3)t}
    \right) \\
&= \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}  
   \frac{e^{-\lambda_3t}}{\lambda_2 - \lambda_3} - 
   \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_2t}}{\lambda_2 - \lambda_3} +
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_3t}}{\lambda_1 - \lambda_3} -
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_1t}}{\lambda_1 - \lambda_3} \\
   \\
&= \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_3t}}{\lambda_2 - \lambda_3} - 
   \underbrace{
   \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}  
   \frac{e^{-\lambda_2t}}{\lambda_2 - \lambda_3}
    }_{\text{ada }\lambda_2\text{ pembilang \& penyebut}} +
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_3t}}{\lambda_1 - \lambda_3} -
   \underbrace{
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_1t}}{\lambda_1 - \lambda_3}
   }_{\text{ada }\lambda_1\text{ pembilang \& penyebut}} \\
   \\
&= \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_3t}}{\lambda_2 - \lambda_3} + 
   \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_2t}}{\lambda_3 - \lambda_2} +
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_3t}}{\lambda_1 - \lambda_3} +
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_1t}}{\lambda_3 - \lambda_1} \\
&= \underbrace{
   \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_3t}}{\lambda_2 - \lambda_3} +
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_3t}}{\lambda_1 - \lambda_3}
   }_{\text{kumpulan } \lambda_3} +
   \underbrace{ 
   \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
   \frac{e^{-\lambda_2t}}{\lambda_3 - \lambda_2}
    }_{\text{kumpulan } \lambda_2} +
   \underbrace{
   \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
   \frac{e^{-\lambda_1t}}{\lambda_3 - \lambda_1}
    }_{\text{kumpulan } \lambda_1} \\
\end{aligned}
$$

Oke, sekarang kita akan rapihin kumpulan $\lambda_3$

$$
\begin{aligned}
\text{kumpulan } \lambda_3
&=  \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
    \frac{e^{-\lambda_3t}}{\lambda_2 - \lambda_3} +
    \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_2 - \lambda_1}
    \frac{e^{-\lambda_3t}}{\lambda_1 - \lambda_3} \\
&=  \lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t} 
    \left(
        \frac{1}{(\lambda_1 - \lambda_2)(\lambda_2 - \lambda_3)} +
        \frac{1}{(\lambda_2 - \lambda_1)(\lambda_1 - \lambda_3)}
    \right) \\
&=  \lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t} 
    \left(
        \frac{1}{(\lambda_1 - \lambda_2)(\lambda_2 - \lambda_3)} -
        \frac{1}{(\lambda_1 - \lambda_2)(\lambda_1 - \lambda_3)}
    \right) \\
&=  \lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t} 
    \left(
        \left[\frac{1}{\lambda_1 - \lambda_2}\right]
        \frac{1}{\lambda_2 - \lambda_3} -
        \frac{1}{\lambda_1 - \lambda_3}
    \right) \\
&=  \lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t} 
    \left[\frac{1}{\lambda_1 - \lambda_2}\right]
    \frac{\lambda_1 - \lambda_3 - (\lambda_2 - \lambda_3)}{(\lambda_2 - \lambda_3)(\lambda_1 - \lambda_3)} \\
&=  \lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t} 
    \left[\frac{1}{\lambda_1 - \lambda_2}\right]
    \frac{\lambda_1 - \lambda_2}{(\lambda_2 - \lambda_3)(\lambda_1 - \lambda_3)}\\
&=  \lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t} 
    \frac{1}{(\lambda_2 - \lambda_3)(\lambda_1 - \lambda_3)} \\
&=  \frac{\lambda_1 \lambda_2 \lambda_3 e^{-\lambda_3t}}
    {(\lambda_2 - \lambda_3)(\lambda_1 - \lambda_3)} \\
    \\
&=  \frac{\lambda_1}{\lambda_1 - \lambda_3}
    \frac{\lambda_2}{\lambda_2 - \lambda_3} 
    \lambda_3 e^{-\lambda_3t}\\
\end{aligned}
$$

lalu, untuk kumpulan $\lambda_2$:

$$
\begin{aligned}
\text{kumpulan } \lambda_2
&=  \frac{\lambda_1 \lambda_2 \lambda_3}{\lambda_1 - \lambda_2}   
    \frac{e^{-\lambda_2t}}{\lambda_3 - \lambda_2}\\
&=  \frac{\lambda_1}{\lambda_1 - \lambda_2}
    \frac{\lambda_3}{\lambda_3 - \lambda_2} 
    \lambda_2 e^{-\lambda_2t}\\
\end{aligned}
$$

lalu, untuk kumpulan $\lambda_1$:

$$
\begin{aligned}
\text{kumpulan } \lambda_1
&=  \frac{\lambda_2 \lambda_1 \lambda_3}{\lambda_2 - \lambda_1}
    \frac{e^{-\lambda_1t}}{\lambda_3 - \lambda_1}\\
&=  \frac{\lambda_2}{\lambda_2 - \lambda_1}
    \frac{\lambda_3}{\lambda_3 - \lambda_1} 
    \lambda_1 e^{-\lambda_1t}
\end{aligned}
$$

Jadi, mah intinya

$$
\begin{aligned}
f_{X_1+X_2+X_3} 
&= \frac{\lambda_1}{\lambda_1 - \lambda_3} \frac{\lambda_2}{\lambda_2 - \lambda_3} \lambda_3 e^{-\lambda_3t}\\
&+ \frac{\lambda_1}{\lambda_1 - \lambda_2} \frac{\lambda_3}{\lambda_3 - \lambda_2} \lambda_2 e^{-\lambda_2t}\\
&+ \frac{\lambda_2}{\lambda_2 - \lambda_1}\frac{\lambda_3}{\lambda_3 - \lambda_1} \lambda_1 e^{-\lambda_1t}
\end{aligned}
$$

atau

$$
f_{X_1+X_2+X_3} = \sum_{k=1}^{3} e^{-\lambda_k t} \prod_{\substack{r=1 \\ r \ne k}}^{3} \frac{\lambda_r}{\lambda_r - \lambda_k}
$$

ini ada buktinya pakai induksi matematika, tapi gw nggak akan ngebuktiin disini. Intinya lu tau kalo proses stokastik ini pakai *convolution hypoexponential*.
