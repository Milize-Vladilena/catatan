## 🧮 Perhitungan Ekspektasi Waktu dengan Sistem Linear Kolmogorov Backward

### 📌 Masalah

Pada Soal 3, kita ingin menghitung:

> Ekspektasi waktu untuk berpindah dari **state 2 ke 5** dalam proses **birth-death**, di mana:

- $\lambda_i = (i+1)\lambda$
- $\mu_i = i\mu$
- Untuk $i = 0, 1, 2, 3, 4$ (hingga state tujuan 5)

Kita misalkan:
- $m(i)$ = ekspektasi waktu untuk mencapai **state 5** mulai dari **state $i$**

---

### 🧠 Prinsip Kolmogorov Backward Equation

Jika kita definisikan vektor $m = [m(0), m(1), m(2), m(3), m(4)]^T$, maka sistem persamaan ekspektasi waktu dapat ditulis:

$$
Q \cdot m = -\vec{1}
$$

Dengan:
- $Q$: submatriks generator untuk state 0–4 (state 5 dianggap absorbing $\Rightarrow m(5) = 0$)
- $\vec{1}$: vektor berisi angka 1

---

### 🧱 Langkah-langkah Penyusunan Matriks $Q$

Kita hanya butuh **submatriks generator** untuk state 0 sampai 4, karena target adalah state 5 (absorbing).

Untuk proses kelahiran-kematian, baris ke-$i$ pada $Q$ adalah:

$$
Q_{i,i-1} = \mu_i, \quad Q_{i,i} = -(\lambda_i + \mu_i), \quad Q_{i,i+1} = \lambda_i
$$

Dengan asumsi $\lambda_i = (i+1)\lambda$, $\mu_i = i\mu$

---

### 🧮 Matriks $Q$ untuk State 0–4

Misalnya kita gunakan $\lambda = 1$, $\mu = 1$ untuk penyederhanaan.

$$
Q =
\begin{bmatrix}
 -1 & 1 & 0 & 0 & 0 \\
 1 & -3 & 2 & 0 & 0 \\
 0 & 2 & -5 & 3 & 0 \\
 0 & 0 & 3 & -7 & 4 \\
 0 & 0 & 0 & 4 & -9 \\
\end{bmatrix}
$$

Dan kita ingin menyelesaikan sistem:

$$
Q \cdot m = -\begin{bmatrix}1\\1\\1\\1\\1\end{bmatrix}
$$

---

### 📐 Contoh Implementasi Manual: Metode Substitusi

Sistem:

$$
\begin{aligned}
-1 m_0 + 1 m_1 &= -1 \\
1 m_0 - 3 m_1 + 2 m_2 &= -1 \\
2 m_1 - 5 m_2 + 3 m_3 &= -1 \\
3 m_2 - 7 m_3 + 4 m_4 &= -1 \\
4 m_3 - 9 m_4 &= -1 \\
\end{aligned}
$$

Kita bisa selesaikan ini secara numerik (eliminasi Gauss, substitusi balik) atau menggunakan software seperti Python/Numpy.

---

### 🔎 Fokus Hasil

Dari sistem ini, kita akan peroleh nilai $m(2)$ sebagai bagian dari solusi. Itulah **ekspektasi waktu** untuk mencapai state 5 mulai dari state 2.

---

### ✅ Keunggulan Metode Kolmogorov Backward

- ⚡ Cepat untuk sistem besar (bisa diselesaikan dengan solver matriks)
- 📐 Formal dan akurat
- 🧠 Menyediakan kerangka umum untuk berbagai fungsi ekspektasi: hitting time, occupation time, dll.

---

### 💡 Tips Implementasi

Di Python:

```python
import numpy as np

Q = np.array([
    [-1, 1, 0, 0, 0],
    [1, -3, 2, 0, 0],
    [0, 2, -5, 3, 0],
    [0, 0, 3, -7, 4],
    [0, 0, 0, 4, -9]
], dtype=float)

b = -np.ones(5)
m = np.linalg.solve(Q, b)

print("Ekspektasi waktu dari state 2 ke 5:", m[2])
```

---

### 🧾 Kesimpulan

- Metode Kolmogorov Backward menyusun sistem **linear** berdasarkan generator matrix $Q$.
- Dapat digunakan untuk menghitung ekspektasi waktu ke state target (absorbing state).
- Solusinya memberikan $m(i)$: **ekspektasi waktu dari state $i$ ke state target**.
