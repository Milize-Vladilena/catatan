## 🔄 Penurunan Sistem Rekursif Ekspektasi Waktu pada CTMC (Soal 3)

### 📄 Masalah

Diberikan proses kelahiran-kematian (birth-death process) dengan:

- Birth rate: $\lambda_i = (i+1)\lambda$
- Death rate: $\mu_i = i\mu$

Soal meminta:  
**Berapa ekspektasi waktu untuk berpindah dari state 2 ke 5?**

---

## 📐 Asal-Usul Sistem Persamaan Rekursif

Misalkan $m(i)$ adalah **ekspektasi waktu** yang diperlukan untuk mencapai state 5 **mulai dari state $i$**, dengan asumsi proses adalah **CTMC** dengan waktu antartransisi eksponensial.

---

### 🧠 Prinsip: *First-Step Analysis* (Analisis Langkah Pertama)

Metode ini didasarkan pada fakta bahwa:
> Waktu total dari $i$ ke 5 = waktu tunggu di $i$ + waktu dari state berikutnya ke 5.

Secara umum, untuk $i \neq 5$:

$$
m(i) = \underbrace{\frac{1}{\lambda_i + \mu_i}}_{\text{waktu tunggu di } i} + 
\underbrace{\frac{\lambda_i}{\lambda_i + \mu_i} m(i+1)}_{\text{ekspektasi jika naik}} +
\underbrace{\frac{\mu_i}{\lambda_i + \mu_i} m(i-1)}_{\text{ekspektasi jika turun}}
$$

- Karena waktu tunggu di CTMC berdistribusi eksponensial dengan rate total keluar.
- Probabilitas transisi instan ke atas: $\lambda_i / (\lambda_i + \mu_i)$
- Probabilitas transisi instan ke bawah: $\mu_i / (\lambda_i + \mu_i)$

Dengan **kondisi batas**:
$$
m(5) = 0
$$

---

### 📋 Contoh untuk Soal 3

Untuk menghitung $m(2)$ menuju 5, bentuk sistem persamaan:

$$
\begin{aligned}
m(4) &= \frac{1}{\lambda_4 + \mu_4} + \frac{\lambda_4}{\lambda_4 + \mu_4} m(5) + \frac{\mu_4}{\lambda_4 + \mu_4} m(3) \\
m(3) &= \frac{1}{\lambda_3 + \mu_3} + \frac{\lambda_3}{\lambda_3 + \mu_3} m(4) + \frac{\mu_3}{\lambda_3 + \mu_3} m(2) \\
m(2) &= \frac{1}{\lambda_2 + \mu_2} + \frac{\lambda_2}{\lambda_2 + \mu_2} m(3) + \frac{\mu_2}{\lambda_2 + \mu_2} m(1)
\end{aligned}
$$

Namun karena kita hanya ingin dari 2 ke 5, biasanya kita cukup bentuk sistem dari $m(2)$ sampai $m(5)$ dan selesaikan numerik atau substitusi.

---

## ❓ Alternatif Metode: **Chain Conditioning / Transient Path**

Jika **rekursi sulit atau tidak diperlukan** (misalnya jika $\mu_i = 0$, hanya ada kenaikan), maka kita bisa gunakan:

### 🎯 Penjumlahan Ekspektasi Langkah Tunggal

Jika kita **hanya memperbolehkan transisi naik** (misalnya $2 \to 3 \to 4 \to 5$), maka:

$$
\mathbb{E}[T_{2 \to 5}] = \sum_{k=2}^{4} \frac{1}{\lambda_k}
$$

Karena waktu antartransisi adalah eksponensial dan **independen**.

Cocok digunakan jika:

- Transisi turun (kematian) diabaikan atau tidak signifikan.
- Kita hanya ingin *approximate shortest path*.
- Soal menyebut proses “murni birth”.

---

## 🧮 Alternatif Lebih Umum: **Sistem Linear Kolmogorov Backward**

Jika ingin solusi **komputasional dan umum**, bisa gunakan:

- Matriks generator $Q$
- Sistem linear dari backward equations:

$$
Q \vec{m} = -\vec{1}
$$

Dengan $\vec{m}_5 = 0$ sebagai boundary condition.

Cocok untuk:
- Sistem besar
- Analisis numerik
- Implementasi dalam Python/Matlab/Maple

---

## ✅ Kesimpulan

| Metode                   | Kapan digunakan                                  | Contoh Soal |
|--------------------------|--------------------------------------------------|-------------|
| Rekursif (first-step)    | Jalur campuran naik/turun, sedikit state         | Soal 3      |
| Jumlah waktu naik saja   | Hanya transisi naik, aproksimasi                 | Soal 3 (pendekatan cepat) |
| Sistem linear Kolmogorov | Umum, numerik, implementasi komputasional        | CTMC besar  |

Semua metode berasal dari prinsip dasar:  
> Ekspektasi waktu = waktu tunggu sekarang + ekspektasi waktu dari state berikutnya.
