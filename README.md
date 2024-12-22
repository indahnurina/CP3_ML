# CP3_ML
Capstone Project: Bank Marketing Campaign

# Bank Marketing Campaign

## A. Context

Salah satu instrumen keuangan yang sudah dikenal masyarakat secara luas adalah term deposit. Pada term deposit, nasabah menitipkan sejumlah uang di bank dan uang tersebut baru dapat dicairkan setelah jangka waktu tertentu, sesuai kesepakatan di awal. Sebagai imbalannya, bank akan memberikan bunga tetap sesuai dengan jumlah nominal uang yang dititipkan. Sebagai perusahaaan yang bergerak di industri yang cukup kompetitif, untuk meningkatkan jumlah penerbitan term deposit, bank perlu memahami perilaku nasabah sehingga marketing campaign sebagai salah satu media untuk menarik minat para nasabah dapat dilaksanakan secara efektif dan optimal. 

## B. Problem Statement
Marketing campaign tentunya membutuhkan banyak sumberdaya, baik dari sisi keuangan, SDM dan juga waktu. Tanpa adanya kejelasan target (segmentasi) dan metode pemasaran yang optimal, maka marketing campaign menjadi sebuah gambling (mungkin sukses, mungkin gagal tanpa adanya kontrol). Untuk itu, apabila perusahaan mengharapkan kenaikan rate penerbitan deposito dengan adanya marketing campaign, maka perusahaan perlu mengurangi risiko kegagalan marketing campaign dengan cara membuat model prediksi penerbitan deposito berjangka berdasarkan profil nasabah dan metode marketing campaign yang digunakan.

Sumberdaya yang dikeluarkan untuk marketing campaign dapat direpresentasikan dalam bentuk nominal biaya pemasaran. Estimasi biaya pemasaran per nasabah/customer disebut dengan Customer Acquisition Cost dan dihitung dengan formula berikut:

CAC = Total Spend on Sales or Marketing ÷ Customers Acquired

Nilai CAC berbeda berdasarkan distribution channel, dimana terdapat 2 tipe distribution channel sebagai berikut:
|Channel| Description |
|---|---|
|Organic (Earned Traffic)| These channels include SEO, social media, email marketing, and other forms of marketing where it does not cost incrementally more money to gather more ad impressions.|
|Paid (Bought Traffic) |These channels include Google & Meta Ads, radio ads, TV ads, print ads, and other forms of marketing where to reach more people, more money must be spent in a generally linear fashion|

Berdasarkan data di bawah ini, biaya marketing melalui bought traffic untuk sertifikat deposito adalah sebesar **USD 176**.

sumber: https://focus-digital.co/average-banking-customer-acquisition-cost/#location

![image](https://github.com/user-attachments/assets/17e798c0-9d54-438b-b693-14a9781daa9c)


## C. Goals
Berdasarkan permasalahan yang dipaparkan sebelumnya, maka akan dilakukan beberapa tahapan berikut:
1. Menaganalisis faktor-faktor yang memengaruhi keputusan nasabah untuk membuka term deposit, baik dari sisi profil nasabah maupun metode marketing
1. Mengidentifikasi segmentasi pelanggan yang berpotensi untuk membuka term deposit
1. Membentuk model prediksi pembukaan term deposit berdasarkan profil nasabah dan metode marketing
1. Melakukan simulai what if analysis, yaitu dengan cara membandingkan:
    - Total biaya yang dikeluarkan jika marketing campaign dilaksanakan ***tanpa*** mempertimbangkan prediksi pembukaan term deposit
    - Total biaya yang dikeluarkan jika marketing campaign dilaksanakan ***dengan*** mempertimbangkan prediksi pembukaan term deposit
1. Mengembangkan marketing campaign yang lebih menarik, optimal, terarah dan lebih efisien.

## D. Data
|Customer profile| Keterangan|Tipe Variabel|
|---|---|---|
|Age|Usia|Explanatory - Numerikal|  
|Job|Pekerjaan|Explanatory - Nominal|
|Balance|Balance|Explanatory - Numerikal|
|Housing|Memiliki atau tidak memiliki pinjaman rumah|Explanatory - Nominal|
|loan|Memiliki pinjaman|Explanatory - Nominal|
|contact|Jalur komunikasi|Explanatory - Nominal|
|month|Bulan akhir dari Last contact|Explanatory - ordinal|
|campaign|Jumlah kontak sepanjang marketing campaign|Explanatory - Numerikal|
|pdays|Lama hari dari kontrak terakhir|Explanatory - Numerikal|
|poutcome|Outcome dari marketing campaign sebelumnya|Explanatory - Nominal|
|deposit|Informasi apakah nasabah membuka deposit atau tidak|Target-Nominal|

## E. Analytic Approach
Berdasarkan tujuan analisis di atas, maka perusahaan ingin mengetahui apakah seseorang akan membuka/tidak membuka deposito berjangka berdasarkan profil nasabah dan metode marketing tertentu.

Response Variable/ Target/ Independent Variable = Deposit

1 : Membuka deposito

0 : Tidak membuka deposito

Oleh karena itu, perlu dilakukan analisis kategori pelanggan. Metode yang tepat untuk digunakan pada analisis ini adalah metode klasifikasi, diantaranya:
1. Logistic Regression
1. KNN (K-Nearest Neighbour)
1. Decision Trees
1. Support Vector Machines (SVM) / Support Vector Classifier (SVC)
1. Ensemble Various Type : Hard Vote dan Stacking
1. Ensemble Single Type : Bagging, Random Forest, Extra Gradient Boosting dan Light Boosting
1. etc.

Adapun proses pembentukan model yang akan dilakukan adalah sbb:
1. 
1. Membentuk 4 base model (logistic Regression, KNN, Decision Tree dan SVM) dengan cara mencari parameter model yang memiliki metric score terbaik untuk masing-masing model.
1. Membentuk ensemble model untuk various type (hard vote dan stacking) berdasarkan 3 dari 4 model dengan metric score terbaik pada poin 1
1. Membentuk ensemble model untuk single type (Bagging, random forest dan boosting). Untuk bagging, estimator dipilih dari 1 model terbaik pada poin 1
1. Melakukan cross validation untuk memastikan bahwa dengan adanya perubahan sampling, metric score masih tetap stabil
1. Melakukan hyperparameter tuning agar memperoleh model terbaik
1. Melakukan analisis kuangan terhadap model yang dihasilkan


## F. Metric Classification
Type 1 Error (False Positive)
  - Diprediksi membuka deposito namun kenyataannya tidak
  - Konsekuensi : kerugian atas sumber daya pemasaran yang dikeluarkan

Type 2 Error (False Negative)
  - Diprediksi tidak membuka deposito namun kenyataannya membuka
  - Konseskuensi : Kehilangan kesempatan pembukaan deposito baru

Dari type error di atas, false positif lebih merugikan daripada false negative, sehingga:
- False positive rate diharapkan mendekati nol
- Positive prediction diharapkan sangat akurat

Oleh karena itu metric yang akan digunakan adalah **precision**

precision = (TP)/(TP+FP)

Model akan dipilih berdasarkan nilai precision terbesar.
## H. Final Model
1. Berdasarkan proses pemodelan sebelumnya, diperoleh model terbaik,yaitu decision tree dengan depth 4 dan criterion log_loss yang memiliki nilai Mean Precision tertinggi yaitu 0.7208 dan sdev precision yang cukup rendah, yaitu sebesar 0.0171.
1. Target/dependent variable yang didefinisikan pada model adalah kolom deposito, dimana:
    - 0: No/Tidak membuka deposito
    - 1: Yes/Membuka deposito
1. Kolom selain deposit dipilih sebagai feature apabila memiliki asosiasi yang cukup kuat dengan target variable. Asosiasi diukurur menggunakan chi square test untuk feature categorical dan spearman rho untuk feature numerik.
1. Feature/explanatory variable/independent variable yang terpilih dan digunakan dalam model prediksi meliputi 7 variable, yaitu: job, balance, housing, loan, contact, campaign, pdays. 
1. Pada proses pemodelan, sebelum dilakukan proses fitting model, tahap preprocessing telah dilakukan terhadap feature, yaitu:
    - Mengimplementasikan One Hot Encoder pada feature housing,loan,contact
    - Mengimplementasikan Binary Encoder pada feature job (karena memiliki katagori>5)
    - Menerapkan robustscaller pada feature numerik (balance,campaign,pdays)
1. Setelah dilakukan preprocessing, jumlah kolom feature yang sebelumnya 7 kolom menjadi 11 kolom. Data inilah yang selanjutnya digunakan dalam proses pemodelan
1. Setelah dilakukan tahap pre processing, row data selanjutnya dipisahkan menjadi 2, yaitu data training (80% dari baris data) dan data testing (20% dari baris data).
1. Data training selanjutnya digunakan dalam proses fitting dan data testing digunakan dalam prediksi. 
1. Hasil decision tree dapat divisualisasikan dalam bentuk grafik/bagan (lihat di bagian selanjutnya)

Keseluruhan pipeline dan data setelah proses preprocessing dapat dilihat di bawah ini:
![image](https://github.com/user-attachments/assets/9ec3c836-0d05-4ae2-ad51-30b370514df0)

![image](https://github.com/user-attachments/assets/b9c040dd-d6d1-4ea0-ab27-9ac9f1e4a8c1)

Model decision tree yang terbentuk dapat dilihat pada visualisasi graph di bawah ini. Graph di bawah ini menunjukkan bagaimana model bekerja dalam memprediksi klasifikasi apakah seorang nasabah akan membuka deposito/tidak. Penjelasan untuk salah satu cabang yang terbentuk adalah sebagai berikut:
1. Step 1: Model memisahkan berdasarkan kondisi feature onehot_contact_other
    - Jika  onehot_contact_other<=0.5, maka masuk ke klasifikasi Deposito=0 (No).
    - Dapat dilihat dari 6244 baris xtrain, 1289 bernilai false.
1. Step 2: Setelah step 1, model memisahkan lebih lanjut berdasarkan kondisi scalling__pdays 
    - Jika scalling__pdays≤ 0.641, maka masuk ke klasifikasi Deposito=0 (No).
    - Dapat dilihat dari 1289 baris dari step 1, 11 baris bernilai False.
1. Step 3. Setelah step 2, model memisahkan lebih lanjut berdasarkan scalling__pdays 
    - Jika scalling__pdays≤ 9.713, maka masuk ke klasifikasi Deposit=1 (Yes)
    - Berdasarkan hasil akhir klasifikasi, terdapat 8 data True dan 3 data false. 
    - Jika dilihat dari value yang terbentuk untuk masing-masing klasifikasi:
        - Cabang di sisi kiri menunjukkan value=[0,8], artinya data asli menunjukkan seluruh target bernilai Deposit=1 (Yes)
        - Cabang di sisi kanan menunjukkan value=[3,0], artinya data asli menunjukkan seluruh target bernilai Deposit=0 (False)
        - Value sesuai dengan sample, sehingga dapat disimpulkan pada percabangan ini, seluruh nilai prediksi sesuai dengan nilai aslinya (accuracy 100%)

Note cara membaca graph untuk leaf yang terbawah:
- log_loss = 0.799
- samples = 772
- value = [585, 187]
- class = Deposit 0: No

Artinya: 
Dari sample sebanyak 772 baris dikategorikan sebagai class = Deposit 0: No, namun pada kenyataanya sebanyak 187 data bernilai Deposit 1: Yes / terjadi False Positive. Semakin rendah log_loss, maka hasil prediksi semakin akurat.

## I. Financial Impact Analysis
Analisis kerugian untuk 2 kondisi/opsi berikut:
Opsi A: Jika marketing campaign dilakukan untuk seluruh nasabah 
Opsi B: Jika marketing campaign dilakukan hanya untuk nasabah yang diprediksi akan membuka deposito

Kerugian didefinisikan sebagai total biaya marketing campaign yang sudah dikeluarkan untuk nasabah per tahunnya (CAC) yang pada akhirnya tidak membuka term deposit.

Kerugian = CAC x jumlah nasabah yang tidak membuka deposito tetapi termasuk dalam target campaign

    Kerugian Opsi A = 176 x Jumlah Nasabah dengan Nilai Deposito 0 atau No
                          = 176 x 4075= 717200 USD

    Kerugian Opsi B = 176 x (jumlah nasabah dengan ypred bernilai 1 - jumlah nasabah dengan yactual bernilai 0)
                          = 176  x  664 = 116864 USD

    Penghematan = Kerugian Opsi A - Kerugian Opsi B
                       = 717200 – 116864 = 600,336 USD

## J. Recommendation
1. Gunakan model prediksi untuk memilih nasabah yang menjadi target campaign agar tidak banyak biaya campaign yang terbuang sia-sia
2. Jumlah kontak sepanjang campaign memiliki feature significance yang cukup rendah, sehingga pada saat campaign tidak perlu melakukan kontak secara excessive.
3. Utamakan nasabah yang tidak memiliki loan home dan memiliki jalur komunikasi via telepon atau hp. Jika ingin menghubungi untuk kembali menawarkan, sebaiknya jangan terlalu jauh dengan waktu campaign berakhir.
4. Model ini dapat diimprove dengan menambahkan feature lain, seperti:
- risk appetite nasabah
- historis pembukaan deposito
- Informasi gaji/pendapatan bulanan
- Informasi tujuan utama dalam berinvestasi
- Status pernikahan
- Informasi pendidikan terakhir
  
## K. Model Limitation
1. Model Decision Tree yang digunakan memiliki keterbatasan berikut:
2. Termasuk model yang kurang stabil terhadap perubahan data dan data noise, sehingga model perlu diupdate jika terdapat update data dan data quality perlu ditingkatkan (tidak ada data unknown)
3. Model belum mempertimbangkan imbalance, sehingga apabila terdapat data baru dan menyebabkan terjadi imbalance, maka perlu ditambahkan proses balancing






