## 📐 Probabilitas Transisi Instan dalam Rantai Markov Waktu Kontinu (CTMC)

### 🔍 Definisi Formal

Misalkan $\{X(t), t \geq 0\}$ adalah sebuah **rantai Markov waktu kontinu (CTMC)** dengan **himpunan state diskret** $S = \{0, 1, 2, \dots\}$ dan **generator matrix** $Q = [q_{ij}]$.

- Elemen $q_{ij}$ (untuk $i \neq j$) menyatakan **laju transisi (rate)** dari state $i$ ke state $j$.
- Elemen diagonal $q_{ii} = -\sum_{j \neq i} q_{ij}$, yang merupakan **negatif dari total rate keluar** dari state $i$.

---

### 🎲 Rumus Probabilitas Transisi Instan

Jika dari state $i$ terdapat **lebih dari satu kemungkinan** transisi keluar, maka probabilitas berpindah dari $i$ ke $j$ **setelah waktu tunggu berakhir** (bukan pada waktu tertentu $t$) diberikan oleh:

$$
P_{ij}^{\text{instan}} = \frac{q_{ij}}{-q_{ii}} = \frac{q_{ij}}{\sum_{k \neq i} q_{ik}}, \quad \text{untuk } j \neq i
$$

**Makna:**  
Setelah menunggu waktu eksponensial dengan rate total keluar dari $i$, probabilitas bahwa transisi berikutnya adalah ke $j$ adalah proporsional terhadap laju transisi ke $j$.

---

### 📌 Catatan Penting

- $\sum_{j \neq i} P_{ij}^{\text{instan}} = 1$, karena semua transisi dari $i$ harus menuju salah satu $j \neq i$.
- Probabilitas transisi instan **tidak melibatkan waktu eksplisit** seperti $t$; ini adalah probabilitas **kondisional pada saat transisi terjadi**.

---

### ⏱️ Kapan Menggunakan Probabilitas Transisi Instan?

Gunakan **probabilitas transisi instan** ketika:

✅ Anda hanya ingin tahu **arah mana** yang akan dipilih **ketika proses keluar dari suatu state**.

✅ Umumnya digunakan dalam:
- Penyederhanaan model CTMC
- Perhitungan generator matrix
- Simulasi lintasan CTMC (misalnya algoritma Gillespie)
- Soal seperti: “Setelah keluar dari state $i$, ke mana proses akan pergi?”

Contoh:

Jika dari state $i$, transisi ke:
- $j$ dengan rate 2
- $k$ dengan rate 3

Maka probabilitas transisi instan ke $j$:
$$
P_{ij}^{\text{instan}} = \frac{2}{2 + 3} = \frac{2}{5}
$$

---

### 📉 Kapan **Tidak** Menggunakan Probabilitas Instan?

Gunakan **probabilitas transisi waktu-$t$** (biasa ditulis $p_{ij}(t)$) ketika:

❌ Anda ingin tahu **peluang proses berada di state $j$ pada waktu tertentu $t$**, dengan kondisi awal di state $i$.

$$
p_{ij}(t) = \Pr(X(t) = j \mid X(0) = i)
$$

Cara hitung:
- Dengan menyelesaikan sistem persamaan diferensial Kolmogorov:
  - Kolmogorov maju: $\frac{d}{dt}P(t) = P(t)Q$
  - Kolmogorov mundur: $\frac{d}{dt}P(t) = QP(t)$
- Atau: $P(t) = e^{Qt}$ (matriks eksponensial)

---

### 📚 Kesimpulan

| Konteks                               | Jenis Probabilitas yang Digunakan | Bentuk |
|--------------------------------------|-----------------------------------|--------|
| Ke mana proses pergi setelah keluar? | **Transisi instan**               | $P_{ij}^{\text{instan}} = \frac{q_{ij}}{-q_{ii}}$ |
| Di mana proses berada pada waktu $t$?| **Transisi waktu-$t$**            | $p_{ij}(t) = \Pr(X(t) = j \mid X(0) = i)$ |

Transisi instan bersifat **lokal dan kondisional**, sementara transisi waktu-$t$ mencakup **evolusi sistem seiring waktu** dan bisa melibatkan **multiple langkah** dari state awal.


## ⚙️ Penurunan Matriks Generator (Q) untuk Soal 2 – Dua Mesin dan Teknisi

### 📄 Ringkasan Masalah

- Terdapat **dua mesin** yang berfungsi masing-masing dengan waktu eksponensial (rate $\mu_1$ dan $\mu_2$).
- Bila rusak, mesin akan **diperbaiki oleh satu teknisi** dengan waktu perbaikan eksponensial (rate $\mu$).
- Teknisi hanya bisa memperbaiki **satu mesin pada satu waktu**.

---

### 🔢 Definisi State

Kita definisikan **state CTMC** sebagai jumlah mesin yang **rusak** dan **apakah sedang diperbaiki atau tidak**.

Mari gunakan notasi:

| State ID | Notasi | Deskripsi                                                              |
|----------|--------|--------------------------------------------------------------------------|
| 0        | (0)    | Kedua mesin berfungsi                                                   |
| 1        | (1)    | Satu mesin rusak dan belum diperbaiki *(teknisi idle → langsung mulai)* |
| 2        | (1*)   | Satu mesin sedang dalam perbaikan                                       |
| 3        | (2)    | Dua mesin rusak, satu sedang diperbaiki, satu menunggu                 |

---

### 📥 Transisi Antar State

Kita asumsikan:
- $\lambda_i$ adalah laju kerusakan mesin ke-$i$
- Misalnya diasumsikan: $\mu_1 = \mu_2 = \lambda$, untuk penyederhanaan

💡 Transisi hanya terjadi karena:
- Mesin rusak (rate: $\lambda_i$ atau total kerusakan)
- Mesin diperbaiki (rate: $\mu$)

---

### 🔁 Semua Transisi yang Mungkin

| Dari State | Ke State | Penjelasan                          | Rate Transisi |
|------------|----------|-------------------------------------|----------------|
| 0          | 2        | Salah satu mesin rusak              | $\lambda_1 + \lambda_2 = 2\lambda$ |
| 2          | 0        | Mesin selesai diperbaiki            | $\mu$          |
| 2          | 3        | Mesin lainnya rusak saat satu diperbaiki | $\lambda$   |
| 3          | 2        | Satu mesin selesai diperbaiki       | $\mu$          |

> Tidak ada transisi dari 1 karena kita asumsikan bahwa begitu ada mesin rusak dan teknisi menganggur, perbaikan dimulai **seketika**, sehingga kita lewati state itu (digabung dalam 2).

---

### 🧱 Matriks Generator Q

Susunan state: $[0, 2, 3]$

$$
Q =
\begin{bmatrix}
-2\lambda & 2\lambda & 0 \\
\mu & -(\lambda + \mu) & \lambda \\
0 & \mu & -\mu
\end{bmatrix}
$$

**Penjelasan setiap baris:**

#### Baris 1 – State 0 (semua mesin berfungsi)

- Keluar ke state 2 karena salah satu mesin rusak: rate $2\lambda$
- Tidak ada masuk dari state lain
- Total keluar: $q_{00} = -2\lambda$

#### Baris 2 – State 2 (1 mesin diperbaiki)

- Keluar ke state 0: mesin selesai diperbaiki → rate $\mu$
- Keluar ke state 3: mesin lain rusak → rate $\lambda$
- Total keluar: $q_{22} = -(\lambda + \mu)$

#### Baris 3 – State 3 (dua mesin rusak, satu diperbaiki)

- Keluar ke state 2: satu mesin selesai diperbaiki → rate $\mu$
- Total keluar: $q_{33} = -\mu$

---

### ⚠️ Catatan Alternatif: Termasuk State 1

Jika kita ingin lebih eksplisit dan **tidak menggabungkan** state “1 mesin rusak, belum diperbaiki”, maka matriks akan berukuran 4×4 dan memuat:

- Transisi dari state 1 ke state 2 dengan rate instan (atau sangat besar)
- Ini kurang realistis untuk CTMC, karena **perubahan instan** menyebabkan singularitas dalam matriks $Q$

Maka penggabungan state rusak → langsung diperbaiki adalah pendekatan umum dan valid.

---

### ✅ Kesimpulan

- Matriks generator CTMC dibentuk dari **semua laju keluar dari suatu state**, dan transisi ke state lainnya.
- **Diagonal $q_{ii}$ adalah negatif jumlah laju keluar dari state $i$**
- **Probabilitas transisi instan** dapat dihitung dari $Q$ jika dibutuhkan:  
  $$
  P_{ij}^{\text{instan}} = \frac{q_{ij}}{-q_{ii}}
  $$

Matriks $Q$ secara unik mencerminkan dinamika sistem stokastik dalam waktu kontinu.
