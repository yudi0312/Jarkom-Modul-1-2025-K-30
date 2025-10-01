# Jarkom Modul 1 2025 K-30

| Nama                          | NRP        |
|-------------------------------|------------|
| Putu Yudi Nandanjaya Wiraguna | 5027241080 |
| Ananda Widi Alrafi            | 5027241067 |

## The Ainulindalë

Sebuah kisah awal mula pembentukan dunia telah dibuka. Eru Ilúvatar atau yang nantinya disebut Eru adalah sang pencipta. Eru menciptakan roh-roh abadi yang disebut Ainur. Mereka adalah "anak-anak dari buah pikirannya". Eru meminta para Ainur untuk menciptakan musik agung bersama-sama. Melalui musik ini, sebuah visi tentang dunia yang akan datang (alam semesta) muncul. Ainu terkuat, Melkor, menjadi sombong dan memasukkan tema-tema sumbang dan egois ke dalam musik, menciptakan disonansi. Ini adalah asal mula kejahatan di alam semesta. Manwë Súlimo yang nantinya disebut Manwe adalah Ainu yang paling memahami kehendak Eru. Selama Musik Penciptaan, dialah yang menjadi konduktor utama untuk tema-tema dari Eru, sering kali berkonflik langsung dengan disonansi yang diciptakan Melkor. Ainur lainnya yang terlibat dalam pembentukan alam semesta dan turun ke Arda (Bumi) yaitu Varda Elentári (Varda) dan Ulmo.

### 14. Melkor melancarkan serangan brute force terhadap  Manwe. 

Setelah gagal mengakses FTP, Melkor melancarkan serangan brute force terhadap  Manwe. Analisis file capture yang disediakan dan identifikasi upaya brute force Melkor. 
(link file) nc 10.15.43.32 3401. 

1. Hal pertama yang kami lakukan, yaitu melakukan unzip untuk file yang diberikan.
   
   <img width="1919" height="344" alt="image" src="https://github.com/user-attachments/assets/0f41c282-8c42-49e1-98ba-bd7bea87b524" />

2. Setelah melakukan unzip, kami mendapatkan file dengan nama **shortbf.pcapng**, kami langsung membuka file tersebut di wireshark dan menjalankan `nc 10.15.43.32 3401` di terminal kali-linux.
   
   <img width="1919" height="1016" alt="image" src="https://github.com/user-attachments/assets/87380657-9036-42d1-a113-ca16cd9519b8" />

3. Ketika kami menjalankan `nc 10.15.43.32 3401`, terdapat beberapa pertanyaan yang dilontarkan :
   - **How many packets are recorded in the pcapng file?** Format: int
     
     Kami langsung mendapatkan paket yang terekam pada file tersebut sebanyak **500358**.
   
     <img width="1918" height="1024" alt="Screenshot 2025-09-30 235546" src="https://github.com/user-attachments/assets/93ec5901-7fac-44ec-9369-3af7372f6136" />
4. Setelah kami menjawab pertanyaan tersebut, kami mendapat pertanyaan lagi :
   - **What are the user that successfully logged in?** Format: user:pass
     
     Kami mencoba untuk menemukan user yang berhasil login dengan langkah pertama melakukan filter terhadap `http` dan mencari paket secara manual di bagian akhir.
     
     <img width="1922" height="1021" alt="Screenshot 2025-09-30 235940" src="https://github.com/user-attachments/assets/24a21e90-b8cf-4243-b18f-877287bf944c" />

     Setelah mendapatkan paket yang kami curigai berisi user dan pass, kami melakukan Follow TCP Stream dan ternyata benar, di dalam paket tersebut berisi user dan pass yang kami cari untuk menjawab soal tersebut.
     
     USER : **n1enna**
     
     PASS : **y4v4nn4_k3m3nt4r1**

     <img width="1918" height="1006" alt="Screenshot 2025-10-01 000050" src="https://github.com/user-attachments/assets/0ea220e7-c4c3-4922-b6b2-fe04dfe7e04f" />

5. User dan Pass yang sudah kami dapatkan membuat kami mendapat pertanyaan lanjutan :
   - **In which stream were the credentials found?** Format: int

   Pada tahap ini tidak terlalu susah, disini kami disuruh untuk menemukan nomor stream yang kredensial dan kami langsung menemukannya.

   Stream : **41824**

   <img width="1917" height="1012" alt="Screenshot 2025-10-01 000218" src="https://github.com/user-attachments/assets/346a186d-d539-4f4e-a561-12747cc277e7" />

6. Kami tidak berhenti disitu saja, setelah input nomor stream kami mendapatkan soal yang lumayan gampang :
   - **What tools are used for brute force**? Format: Hydra v1.8.0-dev

   Kami diberikan tugas untuk mencari tahu tools apa yang digunakan oleh user tersebut untuk brute force. Kami langsung melakukan Follow TCP Stream lagi untuk mencari tools yang digunakan.

   Tools : **Fuzz Faster U Fool v2.1.0-dev**

   <img width="1918" height="1017" alt="Screenshot 2025-10-01 000315" src="https://github.com/user-attachments/assets/f762ad1b-acd4-4c26-871e-4c9994e8bca9" />

   Akhirnya itu merupakan pertanyaan terakhir yang diberikan dan kami mendapatkan flag.

   FLAG : **KOMJAR25{Brut3_F0rc3_BQiQEdk0UkYCnDvDHTHX581kX}**

   <img width="1914" height="707" alt="Screenshot 2025-10-01 000351" src="https://github.com/user-attachments/assets/f75de848-6eef-403f-a50f-c2546b6c3010" />

### 15. Buka file capture dapatkan password rahasia

Melkor menyusup ke ruang server dan memasang keyboard USB berbahaya pada node Manwe. Buka file capture dan identifikasi pesan atau ketikan (keystrokes) yang berhasil dicuri oleh Melkor untuk menemukan password rahasia.
(link file) nc 10.15.43.32 3402

1. ndnd

   

   



   



