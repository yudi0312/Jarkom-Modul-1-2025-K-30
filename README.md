# Jarkom Modul 1 2025 K-30

| Nama                          | NRP        |
|-------------------------------|------------|
| Putu Yudi Nandanjaya Wiraguna | 5027241080 |
| Ananda Widi Alrafi            | 5027241067 |

## The Ainulindalë

Sebuah kisah awal mula pembentukan dunia telah dibuka. Eru Ilúvatar atau yang nantinya disebut Eru adalah sang pencipta. Eru menciptakan roh-roh abadi yang disebut Ainur. Mereka adalah "anak-anak dari buah pikirannya". Eru meminta para Ainur untuk menciptakan musik agung bersama-sama. Melalui musik ini, sebuah visi tentang dunia yang akan datang (alam semesta) muncul. Ainu terkuat, Melkor, menjadi sombong dan memasukkan tema-tema sumbang dan egois ke dalam musik, menciptakan disonansi. Ini adalah asal mula kejahatan di alam semesta. Manwë Súlimo yang nantinya disebut Manwe adalah Ainu yang paling memahami kehendak Eru. Selama Musik Penciptaan, dialah yang menjadi konduktor utama untuk tema-tema dari Eru, sering kali berkonflik langsung dengan disonansi yang diciptakan Melkor. Ainur lainnya yang terlibat dalam pembentukan alam semesta dan turun ke Arda (Bumi) yaitu Varda Elentári (Varda) dan Ulmo.

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

1. 









   

   



   



