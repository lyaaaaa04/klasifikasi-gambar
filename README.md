# Mammals Image Classification – Deep Learning Project

## Penjelasan Proyek
Proyek ini merupakan submission akhir yang dikerjakan dalam modul Belajar Fundamental Deep Learning dalam platform Dicoding. Proyek ini mengimplementasikan deep learning untuk klasifikasi gambar yang berupa mamalia.

## Dataset yang Digunakan
Data yang digunakan dalam proyek ini adalah mengenai Animal-5 Mammal yang diperoleh dari sumber Kaggle. Jumlah dataset yang digunakan adalah sebanyak 14.997.

## Pratinjau Data Gambar
Dalam dataset yang digunakan, terdapat 5 jenis hewan mamalia yaitu :
- Dog: 2927 data
- Cat: 3037 data
- Lion: 2984 data
- Horse: 3009 data
- Elephant: 3040 data

<img width="988" height="395" alt="image" src="https://github.com/user-attachments/assets/f288e8e8-faba-42a2-8b6a-0367df565552" />


## Distribusi Gambar
Untuk setiap kelas hewan, masing-masing terdiri atas banyak dimensi yang beragam. 


## Model yang Digunakan

### 1. MobileNetV2 Pre-trained (Transfer Learning)
Model menggunakan **MobileNetV2** yang telah dilatih pada dataset ImageNet sebagai feature extractor.  
Top layer dihapus (`include_top=False`) sehingga hanya bagian ekstraksi fitur yang digunakan.  
Ukuran input model adalah **(224, 224, 3)**.

---

### 2. Fine-Tuning Layer
- Sebagian besar layer awal dibekukan untuk mempertahankan fitur umum dari ImageNet.  
- **30 layer terakhir dibuka (trainable)** agar model dapat menyesuaikan dengan dataset klasifikasi hewan.  
- Pendekatan ini membantu meningkatkan akurasi tanpa kehilangan generalisasi.

---

### 3. Custom CNN Head (Layer Tambahan)
Model dilengkapi dengan layer tambahan untuk meningkatkan kemampuan klasifikasi:
- `Conv2D` (64 filter, kernel 3x3, ReLU, padding='same')  
- `MaxPooling2D` (2x2)  
- `Conv2D` (128 filter, kernel 3x3, ReLU, padding='same')  
- `MaxPooling2D` (2x2)  

---

### 4. Feature Aggregation & Regularization
- `GlobalAveragePooling2D` digunakan untuk merangkum fitur dan mengurangi jumlah parameter.  
- `Dropout` (rate = 0.4) digunakan untuk mencegah overfitting dan meningkatkan generalisasi model.

---

### 5. Fully Connected Layer
- `Dense` (128 unit, ReLU) untuk pembelajaran fitur lanjutan  
- `Dense` (5 unit, Softmax) sebagai output layer untuk klasifikasi multi-kelas (5 kelas hewan)

---

## Nilai Akurasi dan Loss
<img width="1189" height="490" alt="image" src="https://github.com/user-attachments/assets/9017107f-e2fc-4671-a244-ee584e0686a7" />

---

Model MobileNetV2 Pre-trained yang digunakan menunjukkan hasil yang sangat baik selama proses pelatihan. Nilai terbaik diperoleh pada:
Akurasi Training Terbaik    : 95.07% (Epoch ke-20)
Akurasi Validasi Terbaik    : 95.38% (Epoch ke-18)

---

<img width="788" height="701" alt="image" src="https://github.com/user-attachments/assets/9086339a-c0dd-4962-979e-cc1eac930e43" />

