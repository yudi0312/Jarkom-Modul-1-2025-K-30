# Jarkom Modul 1 2025 K-30

| Nama                          | NRP        |
|-------------------------------|------------|
| Putu Yudi Nandanjaya Wiraguna | 5027241080 |
| Ananda Widi Alrafi            | 5027241067 |

## The Ainulindalë

Sebuah kisah awal mula pembentukan dunia telah dibuka. Eru Ilúvatar atau yang nantinya disebut Eru adalah sang pencipta. Eru menciptakan roh-roh abadi yang disebut Ainur. Mereka adalah "anak-anak dari buah pikirannya". Eru meminta para Ainur untuk menciptakan musik agung bersama-sama. Melalui musik ini, sebuah visi tentang dunia yang akan datang (alam semesta) muncul. Ainu terkuat, Melkor, menjadi sombong dan memasukkan tema-tema sumbang dan egois ke dalam musik, menciptakan disonansi. Ini adalah asal mula kejahatan di alam semesta. Manwë Súlimo yang nantinya disebut Manwe adalah Ainu yang paling memahami kehendak Eru. Selama Musik Penciptaan, dialah yang menjadi konduktor utama untuk tema-tema dari Eru, sering kali berkonflik langsung dengan disonansi yang diciptakan Melkor. Ainur lainnya yang terlibat dalam pembentukan alam semesta dan turun ke Arda (Bumi) yaitu Varda Elentári (Varda) dan Ulmo.

### TOPOLOGI JARINGAN

<img width="771" height="682" alt="image" src="https://github.com/user-attachments/assets/f86f9586-b783-4619-bcd8-0cd7e10faeec" />

### 1. Eru membuat dua switch dan setiap switch membuat 2 client.
Untuk mempersiapkan pembuatan entitas selain mereka, Eru yang berperan sebagai Router membuat dua Switch/Gateway. Dimana Switch 1 akan menuju ke dua Ainur 		yaitu Melkor dan Manwe. Sedangkan Switch 2 akan menuju ke dua Ainur lainnya yaitu Varda dan Ulmo. Keempat Ainur tersebut diberi perintah oleh Eru untuk 		menjadi Client.

Langkah-langkah : 
- Jalankan ip `10.15.43.32` di browser dan masuk ke dalam folder project sesuai nama kelompok (wajib menggunakan jaringan lokal ITS).
- Siapkan Router dengan nama Eru, siapkan 2 switch, dan siapkan 4 client yang bernama Melkor, Manwe, Varda, dan Ulmo.
- Sambungkan dengan add link satu sama lainnya.

### 2. Eru tersambung ke internet
Awalnya Arda (Bumi) masih terisolasi dan tidak terhubung dengan dunia luar. Agar komunikasi dapat berlangsung secara global, Eru perlu dihubungkan ke internet melalui router/gateway. Dengan sambungan ini, Eru dapat mengakses jaringan eksternal, memungkinkan pertukaran data dengan sistem di luar Arda serta membuka konektivitas bagi para Ainur yang berperan sebagai client.

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.226.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.226.2.1
	netmask 255.255.255.0
up apt update
up apt install -y iptables
up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.226.0.0/16
```
Konfigurasi di atas membuat Eru berfungsi sebagai router sekaligus gateway internet, di mana **eth0** memperoleh IP secara DHCP dari jaringan luar/VPN ITS agar dapat terkoneksi ke internet, sedangkan **eth1** dan **eth2** masing-masing diberi alamat statis **192.226.1.1/24** dan **192.226.2.1/24** untuk melayani dua segmen jaringan lokal (Switch 1 dan Switch 2). Perintah tambahan `up apt update` dan `up apt install -y iptables` memastikan paket iptables terpasang saat sistem dinyalakan, lalu aturan `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.226.0.0/16` mengaktifkan NAT sehingga seluruh client dalam jaringan **192.226.x.x** dapat menerjemahkan alamat privatnya menjadi alamat publik Eru agar bisa mengakses internet secara langsung.

### 3. Ainur dapat terhubung dengan yang lain
- Melkor
  ```
  	auto eth0
	iface eth0 inet static
		address 192.226.1.2
		netmask 255.255.255.0
		gateway 192.226.1.1
  ```
- Manwe
	```
	auto eth0
	iface eth0 inet static
		address 192.226.1.3
		netmask 255.255.255.0
		gateway 192.226.1.1
  	``` 
- Varda
  ```
  auto eth0
  iface eth0 inet static
	address 192.226.2.2
	netmask 255.255.255.0
	gateway 192.226.2.1
  ```
- Ulmo
  ```
  auto eth0
	iface eth0 inet static
	address 192.226.2.3
	netmask 255.255.255.0
	gateway 192.226.2.1
  ```
Konfigurasi di atas mengatur IP statis untuk masing-masing Ainur agar mereka bisa saling terhubung melalui router Eru. **Melkor** dan **Manwe** ditempatkan dalam jaringan **192.226.1.0/24** dengan alamat **192.226.1.2** dan **192.226.1.3**, menggunakan **192.226.1.1** (eth1 milik Eru) sebagai gateway. Sementara itu, **Varda** dan **Ulmo** berada dalam jaringan **192.226.2.0/24** dengan alamat **192.226.2.2** dan **192.226.2.3**, menggunakan **192.226.2.1** (eth2 milik Eru) sebagai gateway. Dengan pembagian subnet seperti ini, komunikasi antar-Client dalam satu jaringan langsung dilakukan melalui switch masing-masing, sedangkan komunikasi antar-jaringan (misalnya Melkor ke Varda) akan dilewatkan melalui Eru sebagai router, sehingga seluruh Ainur dapat saling berhubungan meski berada di segmen yang berbeda.

### 4. Eru ingin agar setiap Ainur (Client) dapat mandiri
Setelah berhasil terhubung, sekarang Eru ingin agar setiap Ainur (Client) dapat mandiri. Oleh karena itu pastikan agar setiap Client dapat tersambung ke internet.

Agar setiap client dapat mengakses internet, tambahkan konfigurasi DNS dengan menjalankan perintah
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```

Setelah itu lakukan pengecekan koneksi menggunakan ping google.com. Jika ping berhasil, berarti client sudah terhubung ke internet. Terakhir, pastikan setiap perangkat telah menggunakan alamat IP yang sesuai dengan melakukan pengecekan melalui perintah ip a.

### 5. Eru dan para Ainur lainnya meminta agar semua konfigurasi tidak hilang 
Ainur terkuat Melkor tetap berusaha untuk menanamkan kejahatan ke dalam Arda (Bumi). Sebelum terjadi kerusakan, Eru dan para Ainur lainnya meminta agar semua konfigurasi tidak hilang saat semua node di restart.

<img width="1919" height="809" alt="image" src="https://github.com/user-attachments/assets/a7023734-ccbb-4970-b920-41a68d968c37" />

Lakukan pengeditan pada file **/root/.bashrc** dan tambahkan perintah seperti `apt update`, `apt install`, atau perintah lain yang diperlukan. Dengan cara ini, setiap kali sistem dijalankan ulang, paket yang sudah terpasang tetap tersedia dan konfigurasi tidak hilang.

### 6. Pada soal nomer 6 setelah ainur terhubung ke internet, Melkor mencoba masuk ke komunikasi antara manwe dan eru

Nah langkah pertama di sini kami memasukan file berupa file traffic.zip ke dalam sistem Manwe

1. Melakukan ``wget --no-check-certificate -O traffic.zip "https://drive.google.com/uc?export=download&id=1bE3kF1Nclw0VyKq4bL2VtOOt53IC7lG5"`` ke dalam manwe

<img width="934" height="679" alt="Screenshot 2025-10-03 103544" src="https://github.com/user-attachments/assets/c4538bbd-b144-46de-8a8d-72ff5d87dc9e" />


2. Setelah traffic.zip terinstall langkah selanjutnya ada melakukan unzip terhadap file traffic.zip tersebut ``apt update`` dan ``apt install unzip -y``

<img width="404" height="66" alt="Screenshot 2025-10-03 103742" src="https://github.com/user-attachments/assets/d0964835-6263-474a-a190-d05232828138" />


3. Setelah melakukan unzip akan muncul file bernamakan traffic.sh, setelah itu langsung saja di dalam manwe dijalnkan file traffic.sh tersebut ``./traffic.sh``

<img width="654" height="114" alt="Screenshot 2025-10-03 103842" src="https://github.com/user-attachments/assets/d793e5c7-c031-4d61-9d26-e071b51697b8" />


4. Setelah itu buka wireshark untuk melihat mendapatkan file capture di wireshark tersebut

### 7 Pada nomor demi meningkatkan keamanan eru, lakukan konfigurasi FTP Server pada node eru dengan membuat dua user baru ainur dan melkor, ainur dengan hak akses write & read dan melkor tanpa hak akses sama sekali ke direktori shared

1. Langkah pertama, lakukan command ``apt update apt install vsftpd -y`` untuk menginstall vsftpd

[BUKTI FOTO]

2. Setelah itu, masuk ke dalam ``nano /etc/vsftpd.conf`` untuk melakukan pengeditan pada beberapa baris berikut
local_enable=YES
write_enable=YES
chroot_local_user=YES
listen=YES
listen_ipv6=NO

[BUKTI FOTO]

3. make directory untuk user yaitu ``mkdir -p /srv/ftp/shared``

[BUKTI FOTO]

4. masukan user ainur dan melkor dan masukan pula password pada kedua user tersebut ``adduser ainur`` ``adduser melkor``

[BUKTI FOTO]

5. Mengubah kepemilikan owner terhadap ainur dengan melakukan
``chown ainur:ainur /srv/ftp/shared``
``chmod 770 /srv/ftp/shared``
``chmod 700 /srv/ftp/shared``

[BUKTI FOTO]

6. Masukan file test.txt dengan melakukan command ``echo "File tes FTP" > test.txt

[BUKTI FOTO]

7. masuk ke dalam server ftp dengan command ``service vsftpd start`` ``ftp 192.226.1.1`` dan mencoba seluruh akses ainur
``ftp 192.226.1.1``
``login ke user ainur``
``ftp > ascii``
``ftp > cd shared``
``ftp> put test.txt``
``ftp> ls``
``ftp> get test.txt``

[BUKTI FOTO]

8. Terakhir untuk mencoba akses yang dibatasi yaitu user melkor, langsung saja masuk dengan cara yang sama
``ftp 192.226.1.1``
``login ke user ainur``
``ftp > ascii``
``ftp > cd shared``
``ftp > put test.txt``

hasil akan membuat melkor tidak memiliki akses untuk directory shared (lokal)

[BUKTI FOTO]

### 8 Ulmo perlu mengirimkan data ramalan cuaca ke node eru, lakukan koneksi sebagai client dari node ulmo ke ftp server eru menggunakan user ainur, upload file cuaca.zip dan analisis proses ini menggunakan wireshark dan identifikasi perintah FTP yang digunakan 

1. Langkah pertama, masuk ke client Ulmo dan lakukan ``wget --no-check-certificate "https://drive.usercontent.google.com/u/0/uc?id=11ra_yTV_adsPIXeIPMSt0vrxCBZu0r33&export=download" -O cuaca.zip`` untuk menginstall cuaca.zip di ulmo

[BUKTI FOTO]

2. Lakukan unzip cuaca.zip tersebut

[BUKTI FOTO]

3. Install terlebih dahulu vsftpd terlebih dahulu
``service vsftpd start``
``apt update``
``apt install vsftpd -y``

[BUKTI FOTO]

4. masuk ke dalam vsftpd server dan install ftp
``service vsftpd start``
``apt update``
``apt install ftp -y``

[BUKTI FOTO]

5. Masuk ke dalam ftp server, karena ulmo berada di switch 2 maka masukan
``ftp 192.226.2.1``
``login ainur``
``ftp > cd shared``
``ftp > put cuaca.txt``
``ftp > put mendung.jpg``
**DISCLAIMER SEBELUM MELAKUKAN ANALISIS, BISA BUKA WIRESHARK TERLEBIH DAHULU**

[BUKTI FOTO LOGIN DAN WIRESHARK]

### 9 Eru ingin membagikan "Kitab penciptaan" file kitab_penciptaan.zip kepada Manawe. Dari FTP server eru mendownload file tersebut ke node manwe. Karena Eru merasa kitab tersebut sangat penting maka ia mengubah akses user ainur menjadi read-only, setelah itu gunakan wireshark untuk memonitor koneksi, identifikasi perintah FTP yang digunakan, dan uji akses user ainur

1. Pada langkah awal, lakukan instalasi kitab_penciptaan.zip terlebih dahulu dengan ``wget --no-check-certificate "https://drive.google.com/uc?export=download&id=11ua2KgBu3MnHEIjhBnzqqv2RMEiJsILY" -O kitab_penciptaan.zip``

[BUKTI FOTO]

2. unzip kitab_penciptaan.zip langsung

[BUKTI FOTO]

3. Jalankan server ftp dan restart server ftp dengan ``service vsftpd restart`` supaya memastikan layanan FTP aktif kembali setelah perubahan konfigurasi atau izin file

[BUKTI FOTO]

4. masuk ke dalam server dan kirim file oleh eru ke server ftp yaitu dengan ``ftp 192.226.1.1`` setelah itu ``ftp>put kitab_penciptaan.txt``

[BUKTI FOTO]

5. langkah selanjutnya masuk dengan Manwe dan install file kitab dari FTP server
``ftp 192.226.1.1``
``login manwe``
``ftp>get kitab_penciptaan.txt``

[BUKTI FOTO]

6. Nah kita harus membatasi akses untuk user ainur, caranya adalah
``chmod 555 /srv/ftp/shared``
``sevice vstfpd restart``

nah sehingga folder /srv/ftp/shared jadi read-only

7. Langsung saja dicoba dengan user ainur yaitu dengan memasukan
``ftp 192.226.1.1``
``login ainur``
``ftp> put test.txt``
Hasil harus gagal, karena permission sudah diubah menjadi read-only

[BUKTI FOTO]

8. Masuk ke dalam wireshark dan saat upload bisa cek command STOR filename (untuk put), saat download cek command RETR filename (untuk get)

### 10 Melkor yang marah karena tidak diberi akses mencoba melakukan serangan dengan mengirimkan banyak sekali request ke server Eru dengan menggunakan command ping dari node Melkor ke node eru dengan jumlah paket yang tidak biasa (spam ping misalnya 100 paket)

1. Caranya langsung saja melakukan ping ke pada Eru dengan command ``ping 192.122.1.1 -c 100``

[BUKTI FOTO]

### 14. Melkor melancarkan serangan brute force terhadap  Manwe. 

Setelah gagal mengakses FTP, Melkor melancarkan serangan brute force terhadap  Manwe. Analisis file capture yang disediakan dan identifikasi upaya brute force Melkor. 
[link file](https://drive.google.com/drive/folders/13rf0AlzUrkNhUWbBNt9tIVSimw3njKqd) nc 10.15.43.32 3401. 

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
[link file](https://drive.google.com/drive/folders/1aHSRMoEgQBsA-4I2wWatFxAy3laumcgb) nc 10.15.43.32 3402

1. Kami mendapatkan file dengan nama **hiddenmsg.zip** dan langsung melakukan ekstrak untuk file tersebut. Hasil ekstrak tersebut memberikan satu file yang bernama **hiddenmsg.pcapng**.
   
   <img width="1919" height="455" alt="Screenshot 2025-10-01 005811" src="https://github.com/user-attachments/assets/c0b2205d-515c-4557-9d22-b6dfa72420d0" />

2. Kami membuka file **hiddenmsg.pcapng** dan menjalankan `nc 10.15.43.32 3402` pada terminal linux.

   <img width="1919" height="1014" alt="Screenshot 2025-10-01 005849" src="https://github.com/user-attachments/assets/53cd9a73-52b9-46bc-8482-eb91ac2717b3" />

3. Pada soal pertama, kami diberikan tugas untuk menemukan device apa yang digunakan oleh Melkor. Kami melakukan analisis pada log-log paket yang ada dan kami menemukan sebuah paket yang kami curigai sebagai paket yang bisa kami analisis untuk mendapat device yang digunakan oleh Melkor :
   - **What device does Melkor use?** Format: string
   
   <img width="1915" height="1015" alt="Screenshot 2025-10-01 005909" src="https://github.com/user-attachments/assets/03b73a92-61fb-4d6c-adf1-a1faabf92767" />

Kami mendapatkan USB Keyboard sebagai device yang digunakan oleh Melkor, tetapi ketika kami input USB Keyboard tidak bisa, sedangkan ketika kami input keyboard jawabannya benar. 

Device : **Keyboard**

4. Device sudah kami temukan, tetapi masih ada pertanyaan yang harus kita pecahkan :
   - **What did Melkor write?** Format: string
  
   Kami disini menjalankan **python3** untuk menjalankan script yang digunakan untuk mengekstrak pesan tersembunyi dari file pcap (hasil capture traffic USB  keyboard). Dipakai ketika sebuah paket diketik lewat USB keyboard dan direkam di pcapng.

   ```
   from scapy.all import *
   import base64
   
   hid_map = {
       0x00: ('', ''),
       0x04: ('a', 'A'), 0x05: ('b', 'B'), 0x06: ('c', 'C'), 0x07: ('d', 'D'),
       0x08: ('e', 'E'), 0x09: ('f', 'F'), 0x0a: ('g', 'G'), 0x0b: ('h', 'H'),
       0x0c: ('i', 'I'), 0x0d: ('j', 'J'), 0x0e: ('k', 'K'), 0x0f: ('l', 'L'),
       0x10: ('m', 'M'), 0x11: ('n', 'N'), 0x12: ('o', 'O'), 0x13: ('p', 'P'),
       0x14: ('q', 'Q'), 0x15: ('r', 'R'), 0x16: ('s', 'S'), 0x17: ('t', 'T'),
       0x18: ('u', 'U'), 0x19: ('v', 'V'), 0x1a: ('w', 'W'), 0x1b: ('x', 'X'),
       0x1c: ('y', 'Y'), 0x1d: ('z', 'Z'),
       0x1e: ('1', '!'), 0x1f: ('2', '@'), 0x20: ('3', '#'), 0x21: ('4', '$'),
       0x22: ('5', '%'), 0x23: ('6', '^'), 0x24: ('7', '&'), 0x25: ('8', '*'),
       0x26: ('9', '('), 0x27: ('0', ')'),
       0x28: ('\n', '\n'), 
       0x29: ('[ESC]', '[ESC]'), 
       0x2a: ('[BACKSPACE]', '[BACKSPACE]'),  
       0x2b: ('\t', '\t'),  
       0x2c: (' ', ' '),  
       0x2d: ('-', '_'), 0x2e: ('=', '+'), 0x2f: ('[', '{'), 0x30: (']', '}'),
       0x31: ('\\', '|'), 0x33: (';', ':'), 0x34: ("'", '"'), 0x35: ('`', '~'),
       0x36: (',', '<'), 0x37: ('.', '>'), 0x38: ('/', '?'),
   }
   
   def decode_hid_data(packets):
       """Decode HID keyboard data from packet payloads"""
       result = []
    
    for packet in packets:
        try:
            data = packet.load[-8:]
            modifier = data[0]
            shift_pressed = (modifier & 0x02) or (modifier & 0x20)
            scancode = data[2]
            if scancode in hid_map:
                char = hid_map[scancode][1 if shift_pressed else 0]
                if char:  
                    result.append(char)
                    
        except Exception as e:

            continue
    
    return ''.join(result)

      print("="*60)
      print("HID KEYBOARD DECODER - CTF FLAG EXTRACTOR")
      print("="*60)
      
      packets = rdpcap('hiddenmsg.pcapng')
      print(f"\n[+] Loaded {len(packets)} packets from hiddenmsg.pcapng")
      
      decoded_message = decode_hid_data(packets)
      print(f"[+] Decoded {len(decoded_message)} characters from HID data")
      
      print("\n" + "="*60)
      print("DECODED MESSAGE (Base64):")
      print("="*60)
      print(decoded_message)
      
      try:
          flag = base64.b64decode(decoded_message).decode('utf-8')
          print("\n" + "="*60)
          print("FLAG:")
          print("="*60)
          print(flag)
          print("="*60)
      except Exception as e:
          print(f"\n[!] Error decoding Base64: {e}")
          print("[!] The decoded message might not be valid Base64")
   ```

   <img width="1920" height="1013" alt="Screenshot 2025-10-01 010432" src="https://github.com/user-attachments/assets/09f01789-19dc-48c2-8583-34ae16f8aac4" />

   Setelah kami menjalankan script tersebut, kami mendapatkan apa yang ditulis oleh Melkor.

   Melkor write : **UGx6X3ByMHYxZGVfeTB1cl91czNybjRtZV80bmRfcDRzc3cwcmQ=**

5. Kami telah mendapatkan apa yang ditulis oleh Melkor, tetapi string tersebut sepertinya ada maksud tertentu :
   - **What is Melkor's secret message?** Format: string

   Pada soal ketiga ini kami diberikan tugas untuk mendecode pesan rahasia yang ditulis oleh Melkor. Untuk case ini kami menggunakan tools [CyberChef](https://gchq.github.io/CyberChef/) dan menggunakan operation From Base64.

   <img width="1918" height="1017" alt="Screenshot 2025-10-01 010553" src="https://github.com/user-attachments/assets/5f91302f-63c6-458e-8128-d835f1c9b4d5" />

   Setelah kami mendecode dan benar itu jawabannya, kami mendapatkan flag yang kami cari.

   FLAG : **KOMJAR25{K3yb0ard_W4rr10r_GoeOfj6gQj71urXTlvTxDE7wL}**

   <img width="1919" height="497" alt="Screenshot 2025-10-01 010659" src="https://github.com/user-attachments/assets/9bedf8b3-6954-4f1b-81e3-1443f0918004" />

### 16.  Identifikasi file apa yang diletakkan oleh Melkor.

   Melkor semakin murka ia meletakkan file berbahaya di server milik Manwe. Dari file capture yang ada, identifikasi file apa yang diletakkan oleh Melkor.
	[link file](https://drive.google.com/drive/folders/1aJf_PQGXwr4fxd79df8nd7NzL7SsN6U9) nc 10.15.43.32 3403. 

1. Pertama-tama kami mendownload file yang diberikan dan langsung melakukan unzip dan mendapatkan satu file bernama **MelkorPlan1.pcap**
   
   <img width="1919" height="464" alt="Screenshot 2025-10-01 142450" src="https://github.com/user-attachments/assets/7ea555d4-77cf-452b-a08c-ee8eb82c0a7f" />

2. Setelah kami melakukan unzip pada file tersebut, kami menjalankan file tersebut di wireshark dan menjalankan **nc 10.15.43.32 3403** di terminal kali.

   <img width="1919" height="1021" alt="Screenshot 2025-10-01 144457" src="https://github.com/user-attachments/assets/57c522d5-066b-4219-bbac-483ea3a6c567" />

3. Pada soal pertama, terdapat pertanyaan :
   - **What credential did the attacker use to log in?** Format: user:pass

	Kami disuruh menganalisis untuk mencari kredensial apa yang digunakan penyerang dalam format **user:pass**. 

	<img width="1919" height="1018" alt="Screenshot 2025-10-01 142657" src="https://github.com/user-attachments/assets/2398e062-a10b-4155-a4d9-04eef5099ecc" />

	Kami langsung mencari paket yang mencurigakan, biasanya log in yang sukses itu terdapat di bagian akhir-akhir. Setelah menemukan paketnya, kami melakukan follow TCP Stream pada paket tersebut.

	<img width="1918" height="1018" alt="Screenshot 2025-10-01 142715" src="https://github.com/user-attachments/assets/8763dabd-031b-403e-9093-15c2551b4dd8" />

	Disini kami mendapatkan user dan pass yang digunakan oleh penyerang.

	USER : **ind@psg420.com**
	PASS : **{6r_6e#TfT1p**

4. Selanjutnya kami diberikan tugas untuk mencari beberapa paket yang mungkin terdapat malware.
	- **How many files are suspected of containing malware?** Format: int

	<img width="1916" height="1015" alt="Screenshot 2025-10-01 143037" src="https://github.com/user-attachments/assets/5252be62-00b0-43dd-ab19-708530bb0e2d" />

	<img width="1917" height="1017" alt="Screenshot 2025-10-01 143117" src="https://github.com/user-attachments/assets/095c3c0d-cf52-4572-9d89-f497f87f88f2" />

	Disini terdapat 5 file yang mengandung malware.

	FILE CONTAINING MALWARE : **5**

5. Setelah itu, kami disuruh untuk mencari hash dari beberapa file yang ada.
   - What is the hash of the file (q.exe, w.exe, e.exe, r.exe, t.exe)? Format: sha25

	Untuk mencari hash dari file diatas, kami langsung saja mencari paket yang mengandung q.exe, w.exe, e.exe, r.exe dan t.exe. Setelah itu kami melakukan Follow TCP Stream untuk file tersebut. 

	<img width="1918" height="1018" alt="Screenshot 2025-10-01 143253" src="https://github.com/user-attachments/assets/9ea7e565-bb02-454f-b470-4d5bebb145f7" />

   Setelah melakukan Follow TCP Stream, kami mendownload filenya dalam bentuk raw.

   <img width="1918" height="1017" alt="Screenshot 2025-10-01 143340" src="https://github.com/user-attachments/assets/ce9554b6-d74e-4a19-8f0c-296af42f51d6" />

   Semua file q.exe, w.exe, e.exe, r.exe dan t.exe sudah di simpan dan kami pindah ke terminal kali linux untuk menjalankan `sha256sum [namafile].exe`.
   
	<img width="1918" height="802" alt="Screenshot 2025-10-01 144052" src="https://github.com/user-attachments/assets/b13daaf1-18be-4aa4-b11f-8ca049488685" />

	Hasil hash tersebut di input semua dan kami langsung mendapatkan flag yang kami cari.

	FLAG : **KOMJAR25{Y0u_4r3_4_g00d_4nalyz3r_MTD7eVP68trIhgC4GuGWHA8EJ}**

	<img width="1919" height="961" alt="Screenshot 2025-10-01 144104" src="https://github.com/user-attachments/assets/3d7d88af-05e6-4418-9dc0-b510238b0ff6" />

### 17. Analisis file capture Analisis file capture untuk menggagalkan rencana Melkor

Manwe membuat halaman web di node-nya yang menampilkan gambar cincin agung. Melkor yang melihat web tersebut merasa iri sehingga ia meletakkan file berbahaya agar web tersebut dapat dianggap menyebarkan malware oleh Eru. Analisis file capture untuk menggagalkan rencana Melkor dan menyelamatkan web Manwe.
(link file) nc 10.15.43.32 3404

1. Hal yang pertama kami lakukan, yaitu mendownload file yang diberikan dan melakukan unzip pada file tersebut. Hasil dari unzip tersebut memberikan satu file yang bernama **MelkorPlan2.pcap** dan kami langsung membuka file tersebut menggunakan wireshark dan menjalankan `nc 10.15.43.32 3404` di terminal kali linux.

   <img width="1919" height="762" alt="Screenshot 2025-10-01 150802" src="https://github.com/user-attachments/assets/925ea7b9-8ca4-4e3c-aebb-24edfa8ef9e9" />

	<img width="1918" height="1017" alt="Screenshot 2025-10-01 150826" src="https://github.com/user-attachments/assets/85b7d6f3-f3ca-484d-867e-e2c8a4fe7394" />

2. Soal pertama dan kedua yang kami dapat, yaitu :
   - **What is the name of the first suspicious file?** Format: file.exe
   - **What is the name of the second suspicious file?** Format: file.exe
   Untuk menemukan suspicious file, kami masuk ke dalam export object HTTP dan mendapatkan 2 suspicious file.

	<img width="1917" height="1017" alt="Screenshot 2025-10-01 150934" src="https://github.com/user-attachments/assets/92b4163f-4ffc-4944-a60e-8f5b7f9570dd" />
	
	<img width="1913" height="1016" alt="Screenshot 2025-10-01 151021" src="https://github.com/user-attachments/assets/89173e07-0a66-464d-8b47-2fde7aca13c9" />

	Kami langsung input nama file tersebut dan memang benar bahwa file tersebut suspicious.

	First Suspicious : **Invoice&MSO-Request.doc**

	Second Suspicious : **knr.exe**

3. Setelah kami mendapat file tersebut, kami lanjut ke soal berikutnya :
   - **What is the hash of the second suspicious file (knr.exe)?** Format: sha256

	Kami mendownload file **knr.exe** dan langsung menjalankan ` sha256sum knr.exe` untuk menemukan hash dari knr.exe.

	<img width="1918" height="1022" alt="Screenshot 2025-10-01 151138" src="https://github.com/user-attachments/assets/7a413b48-8e6e-40a5-a711-a8d95c1a2c88" />

	<img width="1918" height="604" alt="Screenshot 2025-10-01 151314" src="https://github.com/user-attachments/assets/27df0631-c56c-46ae-b884-f42c391edba8" />

   Ketika kami input hash dari knr.exe, kami mendapatkan flagnya.

   	FLAG : **KOMJAR25{M4ster_4n4lyzer_1eGyiGRw7rSGqBAGYeiJ2Nztq}**

   <img width="1919" height="730" alt="Screenshot 2025-10-01 151323" src="https://github.com/user-attachments/assets/dfa38aaf-4b4c-4201-9cba-0e00e70b6f65" />

### 18. Melkor meletakkan file berbahaya lagi tetapi dengan metode yang berbeda.
Karena rencana Melkor yang terus gagal, ia akhirnya berhenti sejenak untuk berpikir. Pada saat berpikir ia akhirnya memutuskan untuk membuat rencana jahat lainnya dengan meletakkan file berbahaya lagi tetapi dengan metode yang berbeda. Gagalkan lagi rencana Melkor dengan mengidentifikasi file capture yang disediakan agar dunia tetap aman.
(link file) nc 10.15.43.32 3405

1. File yang kita sudah download tadi kita ekstrak dan menemukan suatu file dengan nama **MelkorPlan3.pcap**. Setelah kita ekstrak, buka file tersebut di wireshark dan jalankan `nc 10.15.43.32 3405` di terminal linux.
   
   <img width="1919" height="514" alt="Screenshot 2025-10-01 153620" src="https://github.com/user-attachments/assets/3b63b084-0288-4815-8805-97e18af59711" />
   
	<img width="1918" height="1021" alt="Screenshot 2025-10-01 153641" src="https://github.com/user-attachments/assets/e4b631fd-6c60-411a-aa31-8e71669b333f" />

2. Setelah kita menjalankan `nc 10.15.43.32 3405`, kita mendapatkan pertanyaan :
   - **How many files are suspected of containing malware?**Format: int

   Untuk pertanyaan ini kami membuka Export Object SMB.

	<img width="1918" height="1017" alt="Screenshot 2025-10-01 153721" src="https://github.com/user-attachments/assets/3ccb5831-18fd-4fde-88d8-577d21bad70d" />

	Pada tools tersebut kami mendapatkan 2 file misterius sesuai dengan gambar. 

	<img width="1917" height="1022" alt="Screenshot 2025-10-01 153753" src="https://github.com/user-attachments/assets/07eb8655-eef9-407a-8ce0-96d2dbd8d2dd" />

   FILES CONTAINING MALWARE : **2**

3. File malware yang kami temukan itu menjawab untuk soal selanjutnya :
   - **What is the name of the first malicious file?** Format: file.exe
   - **Apa nama file berbahaya yang kedua?** Format: file.exe

	Tools tadi sekaligus menjawab pertanyaan diatas, yaitu :

	FILE PERTAMA : **d0p2nc6ka3f_fixhohlycj4ovqfcy_smchzo_ub83urjpphrwahjwhv_o5c0fvf6.exe**
	FILE KEDUA : **oiku9bu68cxqenfmcsos2aek6t07_guuisgxhllixv8dx2eemqddnhyh46l8n_di.EXE**

4. Setelah kita menemukan nama file tersebut, download kedua filenya tersebut dan jalankan `sha256sum [namafile].exe` untuk menemukan hashnya.

   <img width="1919" height="475" alt="image" src="https://github.com/user-attachments/assets/bfad54fc-0869-4947-a142-62b76435f97b" />

	Setelah menginput hashnya, kami mendapatkan flag yang kami cari.

	<img width="1919" height="782" alt="image" src="https://github.com/user-attachments/assets/d7f69e19-9b1a-42a8-9452-2f8f8bcc05e1" />
```c
	FLAG : **KOMJAR25{Y0u_4re_g0dl1ke_ehWoBb7DO3ZP4g9emSeYHYUnq}**
```
### 19. Melkor sipaling jahat langsung melancarkan aksinya yaitu meneror Varda dengan email yang disamarkan
Manwe mengirimkan email berisi surat cinta kepada Varda melalui koneksi yang tidak terenkripsi. Melihat hal itu Melkor sipaling jahat langsung melancarkan aksinya yaitu meneror Varda dengan email yang disamarkan. Analisis file capture jaringan dan gagalkan lagi rencana busuk Melkor.
(link file) nc 10.15.43.32 3406

1. Pertama-tama kami melakukan ekstrak untuk file yang sudah diberikan. Setelah di ekstrak, kami membuka file `MelkorPlan4.pcap` di wireshark dan menjalankan  `nc 10.15.43.32 3406` di terminal linux.
   
<img width="1898" height="491" alt="Screenshot 2025-10-01 183625" src="https://github.com/user-attachments/assets/a9b53e25-a3af-4bfd-bb18-a93aec6a05cd" />

<img width="1912" height="1021" alt="Screenshot 2025-10-01 183707" src="https://github.com/user-attachments/assets/da509f16-ee23-41ce-b753-8122334287f0" />

2. Setelah kami membuka file dan menjalankan netcat, kami mendapat pertanyaan :
   - **Who sent the threatening message?** Format: string (name)
   - **How much ransom did the attacker demand ($)?** Format: int
   - **What is the attacker's bitcoin wallet?** Format: string

   Pertama-tama buka wireshark dan analisis dengan filter tcp. Setelah itu saya Follow TCP Stream. 

   <img width="1918" height="1013" alt="Screenshot 2025-10-01 183946" src="https://github.com/user-attachments/assets/5438323a-970a-4763-96e6-852713681b37" />

	<img width="1918" height="1010" alt="Screenshot 2025-10-01 184245" src="https://github.com/user-attachments/assets/0dd6784a-e15b-4d0b-91ee-bd02e4d3804a" />

	Disini kami mendapatkan semua jawaban yang diperlukan untuk menjawab pertanyaan tersebut.

	```C
	USER : Your Life

	RANSOM : 1600

	BITCOIN WALLET :  1CWHmuF8dHt7HBGx5RKKLgg9QA2GmE3UyL\

	FLAG : KOMJAR25{Y0u_4re_J4rk0m_G0d_YHKBrkPR2OAjVX7xF9Mk0diDf}
   ```
   
### 20. Analisis file capture dan identifikasi kegunaan bantuan yang diberikan oleh Manwe
Untuk yang terakhir kalinya, rencana besar Melkor yaitu menanamkan sebuah file berbahaya kemudian menyembunyikannya agar tidak terlihat oleh Eru. Tetapi Manwe yang sudah merasakan adanya niat jahat dari Melkor, ia menyisipkan bantuan untuk mengungkapkan rencana Melkor. Analisis file capture dan identifikasi kegunaan bantuan yang diberikan oleh Manwe untuk menggagalkan rencana jahat Melkor selamanya.
(link file) nc 10.15.43.32 3407

1. Pertama-tama kami melakukan unzip untuk file yang kami telah download dan membuka file yang sudah diunzip di wireshark dan menjalankan `nc 10.15.43.32 3407`.

   <img width="1910" height="578" alt="Screenshot 2025-10-01 185728" src="https://github.com/user-attachments/assets/420a7992-4d1b-4b0b-829c-7cfc07abd698" />

	<img width="1919" height="1023" alt="Screenshot 2025-10-01 185801" src="https://github.com/user-attachments/assets/d205d02e-ef61-45aa-a7af-6df37efd69cf" />

2. Kami mendapatkan beberapa pertanyaan :
	- **What encryption method is used?** Format: string

	Pada MelkorPlan5, lalu lintas data tidak lagi ditransmisikan dalam bentuk teks biasa (cleartext) seperti pada SMTP/HTTP sebelumnya. Seluruh komunikasi 			berjalan melalui protokol terenkripsi, sehingga kontennya tidak bisa langsung dibaca seperti perintah MAIL FROM/DATA atau HTTP/1.1 GET. Berdasarkan penggunaan 	port tertentu dan payload yang tampak teracak, dapat disimpulkan bahwa teknik enkripsi yang digunakan adalah TLS.

NAME : **TLS**

3. Setelah kita mendapat jawabannya, kami mendapat pertanyaan baru :
   - **What is the name of the malicious file placed by the attacker?** Format: file.exe

   Kami mencoba membuka Export Object HTTP, tetapi tidak bisa melihat file yang ada. 

   <img width="1918" height="1021" alt="Screenshot 2025-10-01 191006" src="https://github.com/user-attachments/assets/9a00e1e9-a58a-4f92-a352-86664980a288" />

   <img width="1919" height="1020" alt="Screenshot 2025-10-01 191103" src="https://github.com/user-attachments/assets/3928312a-ca2e-42df-8fb4-8b87293d14ae" />

   Kami mencoba memasukan file `keyslogfile.txt` ke dalam Edit --> Preference --> Protocol --> TLS, dan setelah itu kembali lagi ke HTTP.

   <img width="1919" height="1021" alt="Screenshot 2025-10-01 191257" src="https://github.com/user-attachments/assets/c8ca7c9f-ac8b-4749-a7ca-77eca4cad72d" />
   
	<img width="1919" height="1009" alt="Screenshot 2025-10-01 191628" src="https://github.com/user-attachments/assets/548490a0-9e7d-42bf-a272-151e1b3228db" />

	Terdapat beberapa file yang ada dan yang berisi malware adalah `invest_20.dll`.

	NAME FILE : **invest_20.dll**

4. Setelah kita mengetahui file yang berisi malware, kita save file tersebut dan kita jalankan `sha256sum invest_20.dll` untuk mengetahui hash yang ditanyakan di soal.
   - **What is the hash of the file containing the malware?** Format: sha256

   <img width="1919" height="472" alt="Screenshot 2025-10-01 191808" src="https://github.com/user-attachments/assets/918d6ddf-87d6-4a80-95bb-b03cd11660d6" />

   <img width="1919" height="616" alt="Screenshot 2025-10-01 191837" src="https://github.com/user-attachments/assets/24d402a6-0fc3-44e5-a4e8-7376cfdeee17" />

   Setelah input jawabannya, kami langsung mendapatkan flagnya :
   ```c
	HAST : 31cf42b2a7c5c558f44cfc67684cc344c17d4946d3a1e0b2cecb8eb58173cb2f
	FLAG : KOMJAR25{B3ware_0f_M4lw4re_tEVhkrmwIfmXMG774JWT27Xbu}
   ```


   


   






   

   



   



