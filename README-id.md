[English](README.md) | **Bahasa Indonesia**

# SelfCountingSentence
*Self-counting sentences, simplified.*

## Pengantar
SelfCountingSentence adalah pembuat **kalimat merujuk diri** (juga disebut autogram) berbasis peramban (browser) file tunggal: kalimat yang secara benar menyatakan berapa banyak huruf yang dikandungnya. Dirancang untuk ahli bahasa, penggemar teka-teki, pelajar bahasa formal, dan siapa saja yang ingin tahu tentang rujukan diri, alat ini melengkapi klausa pembuka dengan bilangan terucap yang berlaku untuk kalimat yang sudah selesai.

Antarmuka dan frasa penghitung mendukung **lima belas bahasa**: English, Bahasa Indonesia, Español, العربية, Français, Português, اردو, Русский, Deutsch, Tiếng Việt, Kiswahili, Türkçe, Tagalog, فارسی, dan Italiano.

## Cara Kerja
Anda mengetik klausa pembuka. Generator menambahkan ekor khusus bahasa — bilangan yang dieja plus kata “huruf” dalam bentuk tata bahasa yang benar — lalu mencari bilangan *n* sedemikian rupa sehingga kalimat lengkap mengandung tepat *n* huruf.

1. **Hitungan huruf**: Hanya huruf Unicode (`\p{L}`) yang dihitung. Spasi, tanda baca, tanda hubung, dan tanda gabung (misalnya harakat Arab) diabaikan, sehingga *thirty-one* menyumbang sembilan huruf, bukan sepuluh.
2. **Ekor bahasa**: Setiap bahasa memiliki pengeja bilangan sendiri dan aturan kesesuaian sendiri untuk nomina yang dihitung (tunggal/jamak, gender, *tamyīz* Arab, bentuk 2–4 Rusia, dan seterusnya).
3. **Pencarian titik tetap**: Jika klausa pembuka memiliki *b* huruf dan ekor untuk *n* memiliki *t(n)* huruf, solusi adalah setiap *n* yang memenuhi *n = b + t(n)*. Pencarian hanya perlu memeriksa jendela yang sedikit lebih lebar daripada ekor terpanjang yang mungkin (sekitar 48 kandidat, diperluas jika perlu, dibatasi keras pada 400).
4. **Kestabilan**: *n* pertama yang memenuhi identitas dikembalikan, beserta berapa banyak kandidat yang diperiksa. Jika tidak ada di rentang yang mungkin, alat ini melaporkan bahwa kalimat stabil tidak dapat dihasilkan.

Karena klausa pembuka tidak berubah selama pencarian, masukan dihitung sekali dan hanya ekor pemenang yang dirakit menjadi kalimat utuh.

## Mulai Cepat
1. Unduh `SelfCountingSentence.html`.
2. Buka di peramban modern apa pun (Chrome, Edge, Firefox, Safari).
3. Secara opsional buka **Pengaturan** untuk memilih bahasa dan tema (Otomatis, Terang, atau Gelap).
4. Ketik klausa pembuka, atau klik **Contoh** untuk memakai frasa bawaan bahasa saat ini.
5. Klik **Buat kalimat**, atau tekan Enter.
6. Baca kalimat yang sudah lengkap dan jumlah iterasinya.

Contoh terverifikasi dari frasa bawaan:

- English: *This sentence has thirty-one letters.*
- Bahasa Indonesia: *Kalimat ini memiliki tiga puluh enam huruf.*
- Español: *Esta oración tiene treinta y cinco letras.*
- Français: *Cette phrase compte trente lettres.*
- Deutsch: *Dieser Satz hat dreißig Buchstaben.*
- Kiswahili: *Sentensi hii ina herufi thelathini.*
- Türkçe: *Bu cümlede yirmi bir harf.*
- Tagalog: *Ang pangungusap na ito ay may apatnapu't apat na titik.*
- فارسی: *این جمله دارای بیست و دو حرف.*
- Italiano: *Questa frase contiene trentasette lettere.*

## Fitur Utama
- **Lima belas bahasa**: Inggris, Indonesia, Spanyol, Arab, Prancis, Portugis, Urdu, Rusia, Jerman, Vietnam, Swahili, Turki, Tagalog, Persia, dan Italia — masing-masing dengan pengeja bilangan asli.
- **Kesesuaian tata bahasa**: Numeralia feminin dalam bahasa Spanyol, Prancis, Italia, dan Portugis; tunggal Jerman setelah numeralia yang berakhiran *ein*; Rusia *буква / буквы / букв*; *tamyīz* Arab lengkap; penutup kalimat Urdu *۔*; perangkai ligatur Tagalog (*-ng* / *-g* / *na*); urutan nomina Swahili (*herufi ...*); nomina tunggal Turki dan Persia (*harf* / *حرف*).
- **Penghitungan sadar Unicode**: Huruf dari aksara apa pun dihitung; tanda gabung tidak.
- **Tata letak RTL**: Arab, Urdu, dan Persia membalik seluruh antarmuka, bukan hanya hasilnya.
- **Tema Gelap/Terang**: Pilihan tema otomatis atau manual.
- **Tombol Contoh**: Mengisi frasa pemula khusus bahasa dan langsung menghasilkan kalimat.
- **File HTML tunggal**: Tidak perlu instalasi, tidak ada dependensi, bekerja sepenuhnya offline.
- **Desain responsif**: Bekerja dengan baik di desktop, tablet, dan perangkat seluler.

## Kasus Penggunaan
- **Teka-teki dan permainan kata**: Membangun autogram dan kalimat deskriptif-diri.
- **Pengajaran bahasa**: Mendemonstrasikan kata bilangan dan kesesuaian nomina.
- **Linguistik**: Membandingkan cara bahasa yang berbeda mengkodekan nomina terhitung.
- **Pendidikan**: Mengenalkan pencarian titik tetap dan rujukan diri dengan contoh konkret yang dapat dicek.

## Memahami Pencarian
Kalimat selalu berbentuk:

    <klausa pembuka> + " " + <kata bilangan> + " " + <kata-huruf> + <penutup>

Hanya ekor yang bergantung pada *n*, sehingga:

    huruf(kalimat) = huruf(klausa) + huruf(ekor(n))

Solusi adalah titik tetap dari fungsi tersebut. Sebagian besar klausa pembuka memiliki satu solusi; beberapa (misalnya fragmen Inggris yang sangat pendek yang panjang ekornya melewati total yang diperlukan) tidak memiliki solusi, dan alat ini mengatakannya daripada mengembalikan hitungan yang salah.

Ekor di-memo per bahasa, sehingga beralih bahasa atau menekan Buat lagi memakai ulang hitungan sebelumnya.

## Bahasa yang Didukung

| Bahasa | Contoh pemula | Nomina terhitung |
| --- | --- | --- |
| English | This sentence has | letter / letters |
| Bahasa Indonesia | Kalimat ini memiliki | huruf |
| Español | Esta oración tiene | letra / letras (numeralia feminin) |
| العربية | هذه الجملة فيها | حرف / حرفان / أحرف / حرفًا |
| Français | Cette phrase compte | lettre / lettres (numeralia feminin) |
| Português | Esta frase tem | letra / letras (numeralia feminin) |
| اردو | اس جملے میں | حرف / حروف |
| Русский | В этом предложении | буква / буквы / букв |
| Deutsch | Dieser Satz hat | Buchstabe / Buchstaben |
| Tiếng Việt | Câu này có | chữ cái |
| Kiswahili | Sentensi hii ina | herufi |
| Türkçe | Bu cümlede | harf |
| Tagalog | Ang pangungusap na ito ay may | titik (dengan ligatur -ng / -g / na) |
| فارسی | این جمله دارای | حرف |
| Italiano | Questa frase contiene | lettera / lettere (numeralia feminin) |

## Privasi & Data
Semua perhitungan terjadi secara lokal di peramban Anda. Tidak ada data yang dikirim ke server mana pun. Alat ini sepenuhnya offline setelah dimuat.

## Lisensi
Lisensi MIT. Lihat LICENSE untuk detailnya.

## Kontribusi
Kontribusi, masalah, dan saran dipersilakan. Silakan buka *issue* untuk mendiskusikan ide atau kirimkan PR.
