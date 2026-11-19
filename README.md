# Human Writing Editor edisi RASA

Tulisan yang terasa ditulis manusia, bukan dihasilkan mesin.

Skill agen portabel untuk menulis dan menyunting Bahasa Indonesia: lugas, alami, inklusif, sesuai EYD, dan lulus pemeriksaan RASA.

![Lisensi MIT](https://img.shields.io/badge/lisensi-MIT-green)
![Bahasa Indonesia](https://img.shields.io/badge/bahasa-Indonesia-red)
![EYD Edisi V](https://img.shields.io/badge/EYD-Edisi%20V-blue)
![RASA](https://img.shields.io/badge/RASA-Ritmis%20%C2%B7%20Akurat%20%C2%B7%20Sarat%20Makna%20%C2%B7%20Alami-purple)

Alat ini bukan pendeteksi AI, dan tidak menjanjikan tulisan lolos detektor. Detektor AI sering keliru. Yang dikejar di sini adalah tulisan yang jelas, tepat, dan enak dibaca, bukan tulisan yang menyamar.

Repo ini menggabungkan dua sumber:

- [human-writing-editor](https://github.com/feyber/human-writing-editor) karya Feyber, untuk audit pola tulisan AI, humanisasi, pencocokan suara, dan skor 50.
- [Skill Bahasa Indonesia plain dan RASA](https://gist.github.com/orepras/3e1ca8974fc51d11825f142fa6a66635) karya [orepras](https://x.com/orepras), untuk bahasa polos, EYD, bahasa inklusif, desain ramah trauma, dan kerangka RASA.

## Mulai cepat

Tempel prompt ini ke agen yang sudah memuat `SKILL.md`.

```text
Gunakan human-writing-editor edisi RASA. Tulis ulang teks di bawah untuk pembaca [siapa]
di [kanal]. Pertahankan fakta, jangan menambah klaim. Periksa dengan RASA dan beri skor 50.

Brief:
[kebutuhan, fakta, dan batasan]

Teks:
[teks yang ingin disunting]
```

Hasil yang kamu dapat:

- teks final;
- skor lima dimensi;
- status keempat huruf RASA;
- alasan singkat kenapa versi baru lebih baik.

Kalau satu huruf RASA gagal, minta agen mengulang. Skor tinggi tidak menutupi tulisan yang masih kaku.

## Daftar isi

- [Apa ini](#apa-ini)
- [Masalah yang dipecahkan](#masalah-yang-dipecahkan)
- [Dua sumber, satu alur](#dua-sumber-satu-alur)
- [Cara kerja](#cara-kerja)
  - [Tahap 0: pahami brief](#tahap-0-pahami-brief)
  - [Tahap 1: audit AI-ism](#tahap-1-audit-ai-ism)
  - [Tahap 2: audit Bahasa Indonesia](#tahap-2-audit-bahasa-indonesia)
  - [Tahap 3: humanisasi](#tahap-3-humanisasi)
  - [Tahap 4: gerbang RASA](#tahap-4-gerbang-rasa)
  - [Tahap 5: skor dan keputusan](#tahap-5-skor-dan-keputusan)
- [Sistem skor](#sistem-skor)
- [Aturan Bahasa Indonesia](#aturan-bahasa-indonesia)
  - [Pilihan kata](#pilihan-kata)
  - [Kalimat dan paragraf](#kalimat-dan-paragraf)
  - [EYD dan ejaan](#eyd-dan-ejaan)
  - [Format teks](#format-teks)
  - [Bahasa inklusif](#bahasa-inklusif)
  - [Komunikasi ramah trauma](#komunikasi-ramah-trauma)
  - [Angka dan diskalkulia](#angka-dan-diskalkulia)
  - [Teks antarmuka](#teks-antarmuka)
- [Contoh sebelum dan sesudah](#contoh-sebelum-dan-sesudah)
- [Format keluaran](#format-keluaran)
- [Pemasangan](#pemasangan)
- [Prompt siap pakai](#prompt-siap-pakai)
- [Struktur repo](#struktur-repo)
- [Berkontribusi](#berkontribusi)
- [Peta jalan](#peta-jalan)
- [Lisensi dan atribusi](#lisensi-dan-atribusi)
- [Kontributor](#kontributor)
- [Istilah](#istilah)
- [Referensi](#referensi)

## Apa ini

Human Writing Editor edisi RASA adalah satu skill untuk dua pekerjaan yang biasanya dipisah:

1. Menghapus pola tulisan AI: pembuka pemanasan, kata hiasan, otoritas samar, ritme rata, dan kesimpulan generik.
2. Menulis ulang dengan standar Bahasa Indonesia: bahasa polos, EYD, inklusif, dan gerbang RASA.

Alat ini berguna untuk artikel, email, caption, dokumentasi, teks antarmuka, pesan kesalahan, pengumuman produk, dan laporan.

Cocok untuk:

- penulis dan editor yang ingin tulisan lebih jernih;
- desainer produk dan penulis UX yang menulis microcopy;
- tim dukungan yang menulis pesan kesalahan dan panduan;
- developer yang menulis README dan dokumentasi;
- siapa pun yang menerima draf terasa "seperti ChatGPT" dan ingin memperbaikinya.

Tidak cocok untuk:

- riset fakta dan verifikasi sumber;
- menerjemahkan dokumen hukum atau medis tanpa ahli;
- menulis kode;
- menghindari deteksi AI. Itu bukan tujuan repo ini.

Prinsipnya sederhana: tulisan yang baik tidak perlu terdengar pintar. Cukup dipahami pada bacaan pertama.

## Masalah yang dipecahkan

Tulisan AI punya gejala yang mudah dikenali. Bukan karena satu kata, tapi karena polanya konsisten.

| Gejala | Yang sering muncul | Akibat |
| --- | --- | --- |
| Pembuka pemanasan | "Di era digital yang berkembang pesat..." | Pembaca menunggu inti yang tidak kunjung datang. |
| Kata hiasan | "solusi menyeluruh", "terdepan", "inovatif" | Klaim tanpa isi. Pembaca tidak tahu apa yang ditawarkan. |
| Ritme rata | Semua kalimat 18 sampai 25 kata | Teks terasa monoton, seperti hasil mesin. |
| Otoritas samar | "Para ahli mengatakan..." | Pembaca tidak bisa memeriksa klaim. |
| Struktur terjemahan | "Hal ini menyoroti pentingnya..." | Bahasa Indonesia terasa kaku dan asing. |
| Birokrasi | "dalam rangka", "terkait hal tersebut" | Pesan tenggelam dalam kata pengantar. |
| Tanpa sudut pandang | Kalimat bisa ditempel di topik apa pun | Tidak ada alasan untuk membaca sampai habis. |

Masalah kedua datang dari bahasa Indonesia yang ditulis seperti terjemahan. Kalimatnya panjang, pasifnya berlapis, dan nominalisasinya menumpuk. Pembaca harus membaca dua kali untuk memahami satu maksud.

Dua masalah ini sering muncul bersamaan. Karena itu, alat ini tidak hanya mengganti kata. Alat ini memeriksa pola, ritme, makna, dan rasa.

## Dua sumber, satu alur

| Lapisan | Sumber | Yang dibawa |
| --- | --- | --- |
| Inti penyuntingan | [human-writing-editor](https://github.com/feyber/human-writing-editor) | Audit AI-ism, humanisasi, pencocokan suara, skor lima dimensi. |
| Lensa Bahasa Indonesia | [Gist Bahasa Indonesia](https://gist.github.com/orepras/3e1ca8974fc51d11825f142fa6a66635) oleh [orepras](https://x.com/orepras) | Bahasa polos, EYD, inklusif, ramah trauma, angka, teks antarmuka, RASA. |

Kenapa digabung:

- Human Writing Editor tahu cara membongkar pola AI, tapi belum punya standar khusus Bahasa Indonesia.
- Skill Bahasa Indonesia tahu aturan EYD dan bahasa polos, tapi tidak memburu pola AI dan tidak memberi skor.
- Setelah digabung, alurnya lengkap: deteksi, perbaikan, verifikasi, lalu keputusan.

Yang berubah dari versi sebelumnya:

- Lima dimensi skor tetap dipakai, tapi diberi nama Indonesia: Lugas, Ritmis, Akurat, Padat, Alami.
- RASA bukan lagi daftar periksa tambahan. RASA menjadi gerbang sebelum tulisan dianggap selesai.
- Aturan EYD, inklusif, dan ramah trauma masuk ke dalam proses, bukan ditempel di akhir.

Kerangka RASA dan prinsip bahasa polos diadaptasi dari gist [orepras](https://x.com/orepras). Kami cantumkan sumbernya di [Lisensi dan atribusi](#lisensi-dan-atribusi).

## Cara kerja

Alurnya berurutan. Jangan melompat ke humanisasi sebelum audit selesai.

```text
Brief
  |
  v
[1] Audit AI-ism
  |
  v
[2] Audit Bahasa Indonesia
  |
  v
[3] Tulis ulang
  |
  v
[4] Gerbang RASA ---- gagal ----> kembali ke [3]
  |
  lulus
  v
[5] Skor dan keputusan
```

Setiap tahap punya keluaran yang jelas. Kalau brief kurang, tanya dulu. Jangan mengarang fakta untuk membuat tulisan terasa spesifik.

### Tahap 0: pahami brief

Sebelum menulis satu kalimat, jawab tujuh pertanyaan ini.

1. Siapa pembacanya?
2. Di kanal apa teks ini muncul?
3. Apa satu tujuan utamanya?
4. Apa yang harus dilakukan pembaca setelah membaca?
5. Nada seperti apa yang cocok: hangat, netral, tegas, atau santai?
6. Fakta apa yang sudah terverifikasi dan boleh dipakai?
7. Istilah, nama, atau larangan apa yang wajib diikuti?

Kalau ada jawaban yang kosong, tulis asumsinya. Jangan diam-diam mengarang.

Contoh brief yang cukup:

```text
Pembaca: pengguna baru aplikasi kirim paket.
Kanal: halaman onboarding.
Tujuan: menjelaskan bahwa proses kini lebih singkat.
Fakta: dulu 7 langkah, sekarang 3 langkah.
Nada: tenang, langsung, tidak salesy.
```

### Tahap 1: audit AI-ism

Tandai pola, jangan langsung hapus. Periksa apakah polanya memang mengganggu atau justru dibutuhkan konteks.

| Pola | Contoh | Perbaikan |
| --- | --- | --- |
| Kata hiasan | "solusi menyeluruh", "terdepan", "inovatif" | Sebut hasil atau angka yang konkret. |
| Metafora kosong | "ekosistem", "lanskap", "transformasi digital" | Sebut pihak, aktivitas, atau perubahan yang nyata. |
| Pembuka pemanasan | "Di era digital yang berkembang pesat..." | Mulai dari inti. |
| Signposting | "Mari kita selami", "Pada artikel ini..." | Tulis poinnya langsung. |
| Artefak chatbot | "Tentu", "Semoga membantu", "Berikut penjelasannya" | Hapus. |
| Otoritas samar | "Para ahli mengatakan", "Studi menunjukkan" | Sebut sumber atau hapus klaimnya. |
| Kepentingan palsu | "menandai momen penting", "menjadi bukti" | Sebut kejadiannya. Pembaca menilai sendiri. |
| Kontras formulaik | "Bukan sekadar X, melainkan Y" | Pakai kalimat langsung. Boleh sekali, jangan jadi pola. |
| Tiga serangkai | "cepat, andal, dan skalabel" | Pertahankan hanya jika ketiganya terbukti. |
| Sinonim berputar | "pengguna", lalu "pelanggan", lalu "konsumen" untuk orang yang sama | Pilih satu kata dan ulangi. |
| Ritme rata | Semua kalimat 20 kata | Campur kalimat pendek dan panjang. |
| Kesimpulan generik | "Masa depan cerah", "Hanya waktu yang akan menjawab" | Tutup dengan tindakan, angka, atau keputusan. |

Aturan audit:

- Kutip bagian yang bermasalah, lalu jelaskan kenapa.
- Jangan mengganti kata tanpa memperbaiki kalimatnya.
- Jangan mengorbankan makna hanya agar terlihat "manusiawi".
- Pertahankan istilah teknis yang memang dipakai pembaca.

### Tahap 2: audit Bahasa Indonesia

Setelah pola AI dibersihkan, periksa struktur bahasanya.

| Pola kaku | Perbaikan |
| --- | --- |
| "Hal ini menyoroti pentingnya..." | "Ini menunjukkan..." |
| "Melakukan pengoptimalan proses" | "Mempercepat proses" |
| "Dapat dilakukan oleh pengguna" | "Kamu bisa..." |
| "Dalam rangka meningkatkan..." | "Untuk meningkatkan..." |
| "Terkait hal tersebut..." | "Soal itu..." |
| "Pada dasarnya..." | Hapus, lalu mulai dari inti. |
| "Perlu diketahui bahwa..." | Hapus. |
| "Sangat penting untuk..." | "Kamu perlu..." atau jelaskan akibatnya. |
| "Berbagai macam..." | "Berbagai..." atau sebut jumlahnya. |
| "Rumah di mana saya tinggal" | "Rumah tempat saya tinggal" |
| "Yang mana" | "Yang" |

Periksa juga:

- kalimat lebih dari 25 kata;
- pasif berlapis;
- nominalisasi berlebihan;
- pengulangan ide;
- kata mubazir seperti "sangat", "cukup", "berbagai", "mungkin";
- ejaan dan tanda baca. Rinciannya ada di [EYD dan ejaan](#eyd-dan-ejaan).

### Tahap 3: humanisasi

Humanisasi bukan berarti membuat semua tulisan santai. Artinya, tulisan terasa ditulis orang untuk pembaca tertentu.

Lakukan ini:

- Variasikan panjang kalimat. Setelah kalimat panjang, pakai kalimat pendek. Ritme yang rata adalah tanda paling mudah dikenali.
- Tambahkan detail dari brief. Angka, nama, tanggal, dan akibat nyata membuat tulisan hidup. Jangan mengarang.
- Pilih sudut pandang. Kalau konteksnya cocok, pakai "saya" atau "kami". Tulisan tanpa sudut pandang terasa netral dan bisa ditempel di topik apa pun.
- Baca dengan keras. Kalau kamu tersandung, pembaca juga akan tersandung.
- Pertahankan ketidaksempurnaan yang berguna. Fragmen, jeda, dan kalimat menggantung boleh dipakai, asal cocok dengan kanal.
- Jangan memoles semuanya. Tulisan yang terlalu rapi justru terasa mesin.

Contoh:

```text
Sebelum:
Kami memastikan bahwa seluruh proses yang selama ini dijalankan oleh tim dapat berjalan lebih efisien dan juga lebih cepat.

Sesudah:
Tim kami memangkas proses lama. Sekarang lebih cepat, tanpa langkah tambahan.
```

Kalau pengguna memberikan contoh tulisan sendiri, cocokkan suaranya. Perhatikan panjang kalimat, kebiasaan tanda baca, tingkat formalitas, humor, dan kata yang sering muncul. Jangan menyalin frasa persis tanpa izin.

### Tahap 4: gerbang RASA

RASA adalah akronim sekaligus ujian: apakah tulisan ini punya rasa?

Keempat dimensi diuji setelah draf selesai. Kalau satu gagal, draf kembali ke tahap 3. Skor tidak bisa menutupi kegagalan gerbang.

Contoh di bagian ini memakai data brief. Angka dan sumbernya hanya ilustrasi.

#### Ritmis (R)

Apakah teks enak dibaca dan didengar?

Cara uji:

- baca dengan keras;
- periksa variasi panjang kalimat;
- cari kluster bunyi yang sulit diucapkan;
- beri jeda di tempat yang tepat;
- pastikan tidak ada kalimat yang membuat pembaca mengulang bacaan.

Tanda gagal: semua kalimat sama panjang, paragraf terasa berat, dan tidak ada ruang bernapas.

```text
Sebelum:
Kami berkomitmen untuk terus menghadirkan layanan yang semakin baik bagi seluruh pelanggan di seluruh Indonesia.

Sesudah:
Layanan kami kini menjangkau 38 kota. Tahun depan, 12 kota lagi.
```

#### Akurat (A)

Apakah setiap kata tepat sasaran?

Cara uji:

- periksa denotasi dan konotasi kata;
- buang kualifikasi kabur seperti "cukup", "beberapa", "mungkin saja";
- pastikan klaim punya sumber;
- bedakan fakta, perkiraan, dan pendapat;
- cari kata yang hanya "mendekati" makna yang dimaksud.

Tanda gagal: klaim "para ahli mengatakan" tanpa nama, angka tanpa asal, dan kata besar untuk hal kecil.

```text
Sebelum:
Kami membantu banyak bisnis berkembang.

Sesudah:
Kami membantu 43 warung di Denpasar mencatat penjualan harian. (Sumber: data internal, Juni 2026)
```

Kalau sumbernya tidak ada, jangan pertahankan klaimnya. Ganti dengan hal yang bisa dibuktikan.

#### Sarat makna (S)

Apakah setiap baris membawa bobot?

Cara uji:

- tanya apa yang pembaca dapat dari baris ini;
- cek apakah CTA-nya jelas;
- buang kalimat yang hanya memenuhi ruang;
- pastikan panjang teks sebanding dengan informasinya.

Tanda gagal: paragraf panjang, tapi tidak ada informasi baru. Kalimatnya terdengar bagus, isinya kosong.

```text
Sebelum:
Kami berkomitmen memberikan solusi terbaik untuk kebutuhan Anda.

Sesudah:
Keluhan dibalas dalam 1x24 jam. Kalau lewat, biaya bulan itu kami kembalikan.
```

#### Alami (A)

Apakah ini terdengar seperti manusia yang berbicara?

Cara uji:

- baca sebagai pembaca biasa, bukan editor;
- cek apakah nada cocok dengan konteks;
- cari struktur terjemahan;
- pastikan suara konsisten, tapi tidak dipaksakan;
- tanya: apakah ada orang yang benar-benar akan mengatakan ini?

Tanda gagal: kalimat bisa ditempel di topik apa pun, penuh frasa template, dan terasa seperti pengumuman resmi yang tidak punya penulis.

```text
Sebelum:
Mohon untuk dapat memperhatikan ketentuan yang berlaku sebelum melakukan pendaftaran.

Sesudah:
Baca ketentuan pendaftaran dulu. Prosesnya sekitar lima menit.
```

Teks formal bisa tetap alami. Yang membuatnya kaku bukan formalitasnya, melainkan jarak antara penulis dan pembaca.

#### Urutan pengujian

1. Baca keras. Tangkap masalah Ritmis lebih dulu.
2. Periksa kata per kata. Itu jalur Akurat.
3. Tanya apa yang ingin disampaikan. Itu jalur Sarat makna.
4. Baca lagi sebagai pembaca biasa. Itu jalur Alami.

Kalau satu dimensi gagal, perbaiki, lalu ulangi keempatnya. Jangan hanya memperbaiki yang gagal.

#### Aturan keras

- Fakta yang dikarang membatalkan skor, berapa pun nilainya.
- Klaim yang tidak punya sumber harus dihapus atau diberi label sebagai pendapat.
- Jangan menambah detail hanya agar tulisan terasa spesifik.
- Jangan memakai RASA untuk membenarkan manipulasi atau tekanan palsu.

### Tahap 5: skor dan keputusan

Setelah RASA lulus, beri skor. Skor dipakai untuk membandingkan versi, bukan untuk menghias hasil.

Aturan keputusan:

- total minimal 40 dari 50;
- tidak ada dimensi di bawah 7;
- keempat huruf RASA lulus;
- tidak ada pelanggaran fakta.

Kalau salah satu syarat gagal, tulis ulang. Jangan menaikkan skor dengan mengubah definisinya.

## Sistem skor

Lima dimensi, masing-masing 1 sampai 10. Total 50.

| Dimensi | Pertanyaan | Skor 10 | Skor 1 |
| --- | --- | --- | --- |
| Lugas (Directness) | Apakah inti langsung muncul? | Mulai dari poin, tanpa pemanasan. | Berputar-putar dan mengulang prompt. |
| Ritmis (Rhythm) | Apakah enak dibaca keras? | Panjang kalimat bervariasi, ada jeda. | Semua kalimat sama, tersandung. |
| Akurat (Trust) | Apakah kata dan klaimnya tepat? | Kata pas, sumber jelas, tidak berlebihan. | Klaim samar, kata hanya mendekati makna. |
| Padat (Density) | Apakah setiap kata bekerja? | Tanpa filler, tiap baris berbobot. | Panjang tapi kosong. |
| Alami (Authenticity) | Apakah terdengar seperti manusia? | Suara konsisten dan sesuai konteks. | Template yang bisa ditempel di topik apa pun. |

Padat mengukur Sarat Makna. Lugas adalah syarat bahasa polos, di luar empat huruf RASA.

Panduan nilai:

| Total | Status |
| --- | --- |
| 45 sampai 50 | Siap terbit. |
| 40 sampai 44 | Kuat, biasanya siap terbit. |
| 35 sampai 39 | Perlu satu putaran lagi. |
| 25 sampai 34 | Masih generik atau terlalu rapi. |
| Di bawah 25 | Tulis ulang dari awal. |

Contoh kartu skor:

```text
Skor: 44/50
- Lugas: 9
- Ritmis: 9
- Akurat: 8
- Padat: 9
- Alami: 9

RASA: Ritmis lulus, Akurat lulus, Sarat makna lulus, Alami lulus.
```

Skor bukan ukuran mutlak. Dua editor bisa memberi nilai berbeda. Yang penting: alasan di balik nilai dan perbaikan yang dihasilkan.

## Aturan Bahasa Indonesia

Bagian ini adalah rujukan cepat. Aturannya berlaku untuk prosa, bukan untuk kode atau kutipan langsung.

### Pilihan kata

Gunakan kata sehari-hari. Ganti istilah kantor dengan padanan yang lebih jelas.

| Hindari | Pakai |
| --- | --- |
| memanfaatkan | memakai, menggunakan |
| mengoptimalkan | mempercepat, memperbaiki |
| melakukan optimalisasi | mempercepat |
| memfasilitasi | membantu |
| berkolaborasi | bekerja sama |
| bersinergi | bekerja sama |
| menghadirkan | memberi, menyediakan |
| mendeliver | mengirim, menyerahkan |
| terkait hal tersebut | soal itu |
| dalam rangka | untuk, agar |
| guna | untuk |
| pada akhirnya | akhirnya |
| berbagai macam | berbagai, atau sebut jumlahnya |
| sangat penting | penting, atau jelaskan akibatnya |
| stakeholder | pihak terkait |
| best practice | cara yang terbukti |
| onboarding | proses awal |
| user | pengguna |
| deadline | tenggat |
| robust | kuat, tahan |
| seamless | lancar |
| leverage | pakai, gunakan |

Jangan mengganti istilah teknis yang sudah dipahami pembaca. "API", "cache", dan "deploy" tidak perlu diterjemahkan jika konteksnya teknis.

Hindari metafora yang tidak menambah makna: ekosistem, lanskap, portal, transformasi digital. Kalau istilah itu muncul, tanya apakah ada fakta di baliknya.

### Kalimat dan paragraf

- Pakai kalimat aktif. Sebut siapa melakukan apa.
- Jaga kalimat 12 sampai 20 kata. Maksimal 25 kata.
- Satu ide per kalimat.
- Satu topik per paragraf.
- Letakkan kesimpulan di awal. Detail menyusul.
- Hapus pembuka pemanasan.
- Pakai partikel "-lah" dan "-kah" dengan hemat.
- Hindari "adalah" berlebihan. Kalau bisa memakai kata kerja, pakai kata kerja.

Contoh:

```text
Sebelum:
Perubahan kata sandi dapat dilakukan kapan saja oleh kamu.

Sesudah:
Kamu bisa mengubah kata sandi kapan saja.
```

```text
Sebelum:
Pastikan bahwa semua kolom yang bersifat wajib telah diisi terlebih dahulu.

Sesudah:
Isi semua kolom wajib.
```

```text
Sebelum:
Telah terjadi kesalahan sistem yang tidak terduga. Mohon ulangi proses.

Sesudah:
Pengiriman gagal. Coba lagi.
```

### EYD dan ejaan

Ejaan mengikuti EYD Edisi V. Beberapa hal yang paling sering salah:

- Huruf kapital untuk nama diri, nama lembaga resmi, dan awal kalimat. Bukan untuk penekanan.
- Judul dan subjudul memakai sentence case. Kapital hanya untuk nama diri.
- Tanda titik di akhir kalimat lengkap, termasuk butir daftar yang berupa kalimat utuh.
- Tanda pisah (—) untuk jeda penjelasan. Tanda hubung (-) untuk kata majemuk.
- Tanda seru hanya untuk hal yang benar-benar dirayakan. Maksimal satu.
- "di" sebagai kata depan dipisah: "di kantor". "di-" sebagai awalan disambung: "ditulis".
- "ke" sebagai kata depan dipisah: "ke kantor". "ke-" sebagai awalan disambung: "ketiga".
- "pun" dipisah pada "apa pun" dan "kapan pun". Disambung pada "walaupun" dan "meskipun".
- "antar" pada makna hubungan ditulis serangkai: "antarkota", "antarnegara".

Ejaan yang sering keliru:

| Salah | Benar |
| --- | --- |
| praktek | praktik |
| analisa | analisis |
| resiko | risiko |
| ijin | izin |
| jaman | zaman |
| merubah | mengubah |
| silahkan | silakan |
| nomer | nomor |
| kwalitas | kualitas |
| apotik | apotek |
| obyek | objek |
| aktifitas | aktivitas |
| sekedar | sekadar |
| mempengaruhi | memengaruhi |
| antri | antre |

Angka dan tanggal:

- Tulis "50%", bukan "50 %".
- Tulis "Rp75.000", bukan "Rp 75.000".
- Pisahkan ribuan dengan titik dan desimal dengan koma: 1.500.000.
- Tulis "Rp5 miliar", bukan "Rp5M".
- Rentang angka memakai "hingga" atau "sampai": "10 hingga 20 orang".
- Tanggal: "4 Juni 2026". Rentang: "4 sampai 8 Juni 2026".
- Waktu: "10.00" atau "10.00–11.30".
- Pakai "tengah hari" dan "tengah malam", bukan "12.00 siang".

Singkatan:

- Tulis "misalnya", bukan "mis." atau "e.g.".
- Tulis "yaitu" atau "yakni", bukan "i.e.".
- Tulis "dan sebagainya" atau "seperti", bukan "dll." atau "etc.".
- Tulis "dan", bukan "&", kecuali dalam nama merek.

### Format teks

- Pakai sentence case untuk judul, tombol, label, dan tabel.
- Jangan memakai tebal atau miring untuk penekanan. Struktur dan pilihan kata sudah cukup.
- Tebal hanya untuk nama elemen antarmuka yang literal: "pilih **Simpan**".
- Butir daftar diawali kalimat pengantar yang diakhiri tanda titik dua.
- Mulai butir frasa dengan huruf kecil. Butir berupa kalimat utuh diawali huruf kapital dan diakhiri titik.
- Satu butir, satu ide.
- Langkah bernomor hanya untuk urutan yang harus diikuti.
- Teks tautan harus deskriptif. Jangan "klik di sini" atau "baca selengkapnya".
- Jangan memakai FAQ jika isi sudah menjawab kebutuhan pembaca.

Judul yang baik:

- memuat kata kunci di depan;
- maksimal sekitar 65 karakter;
- tidak diakhiri titik, tanda tanya, atau tanda seru;
- unik dan menjelaskan isi.

### Bahasa inklusif

- Letakkan orangnya dulu: "pengguna dengan disabilitas", bukan "penyandang cacat" atau "difabel", kecuali komunitas itu memilih istilahnya sendiri.
- Hindari kata yang memberi stigma: gila, stres berat, bodoh, lambat, lemah, cacat, abnormal.
- Jangan mengasumsikan satu bentuk keluarga sebagai "normal".
- Pakai "dia" untuk subjek tunggal yang gendernya tidak diketahui.
- Jangan memakai humor berbasis stereotip etnis, gender, agama, atau kondisi tubuh.
- Ikuti istilah yang dipilih komunitas. Komunitas Tuli, misalnya, sering menulis "Tuli" dengan huruf kapital.
- Sertakan konteks di luar Jakarta. Tidak semua pembaca punya internet cepat, ponsel baru, atau rekening bank.
- Pakai nama dan contoh yang beragam. Jangan hanya nama Jawa atau nama Barat.

### Komunikasi ramah trauma

- Jangan menyalahkan pembaca. "Kamu gagal mengisi" bukan pesan yang membantu.
- Jelaskan apa yang akan terjadi sebelum tindakan dijalankan.
- Beri kendali. Sebutkan kalau tindakan bisa dibatalkan atau diulang.
- Tenangkan saat situasi sulit: "Tenang, data kamu tidak hilang."
- Jangan memakai urgensi palsu. "Segera selesaikan" hanya jika memang mendesak.
- Untuk topik sensitif, akui beban emosinya tanpa mendramatisasi. Sediakan jalan keluar.
- Konfirmasi tindakan destruktif harus menyebut akibatnya secara spesifik.

Contoh:

```text
Sebelum:
Apakah kamu yakin ingin menghapus akun?

Sesudah:
Hapus akun? Semua proyek dan riwayat pembayaran akan hilang. Tindakan ini tidak bisa dibatalkan.
```

### Angka dan diskalkulia

- Jangan menumpuk banyak angka dalam satu kalimat. Pecah menjadi daftar.
- Beri perbandingan konkret: "Rp1 miliar, setara biaya sewa kantor kecil selama 10 tahun."
- Pakai kata urutan, bukan hanya angka: "Pertama, kedua, terakhir."
- Tunjukkan langkah perhitungan. Jangan menyembunyikan rumus.
- Pakai format tanggal yang konsisten dan tidak ambigu.
- Beri konteks pada persentase: "30% lebih murah, dari Rp100.000 menjadi Rp70.000."

### Teks antarmuka

| Situasi | Hindari | Pakai |
| --- | --- | --- |
| Tombol | "OK", "Submit", "Proses" | "Simpan", "Kirim lamaran", "Lanjutkan" |
| Empty state | "Tidak ada data." | "Belum ada proyek. Mulai dengan membuat proyek pertama." |
| Pesan sukses | "Operasi berhasil diselesaikan." | "Profil kamu sudah diperbarui." |
| Pesan error | "Error 404: User not found." | "Email ini belum terdaftar. Coba email lain atau daftar dulu." |
| Konfirmasi hapus | "Apakah kamu yakin?" | "Hapus akun? Data kamu akan hilang dan tidak bisa dikembalikan." |
| Placeholder | Placeholder dipakai sebagai label | Label di atas kolom, placeholder hanya contoh format. |

Aturan tambahan:

- Tombol memakai kata kerja aktif.
- Pesan error menjelaskan apa yang terjadi, tanpa menyalahkan, lalu memberi langkah berikutnya.
- Placeholder tidak menggantikan label.
- Tooltip menjawab "kenapa saya perlu mengisi ini".
- Onboarding mengundang, bukan mewajibkan.

## Contoh sebelum dan sesudah

Semua contoh memakai brief. Detail yang muncul di versi baru berasal dari brief, bukan karangan.

### 1. Pengumuman produk

Brief: aplikasi kirim paket. Proses lama tujuh langkah. Sekarang tiga langkah. Pembaca: pengguna baru.

```text
Sebelum:
Di era digital yang berkembang pesat, kami menghadirkan solusi pengiriman yang seamless dan inovatif untuk memenuhi kebutuhan pelanggan.
```

```text
Sesudah:
Kirim paket sekarang tiga langkah: isi alamat, pilih kurir, bayar. Dulu tujuh.
```

Skor: 44/50

- Lugas: 9
- Ritmis: 9
- Akurat: 8
- Padat: 9
- Alami: 9

RASA: lulus.

Kenapa lebih baik:

- membuang pembuka yang tidak memberi informasi;
- memakai angka dari brief;
- ritmenya bergerak dari kalimat panjang ke kalimat pendek.

### 2. Pesan error

Brief: formulir menyimpan draf otomatis. Gangguan terjadi karena koneksi putus.

```text
Sebelum:
Terjadi kesalahan yang tidak terduga. Mohon ulangi proses pengiriman formulir Anda.
```

```text
Sesudah:
Formulir belum terkirim. Periksa koneksi internet, lalu coba lagi. Jawabanmu tetap tersimpan.
```

Skor: 43/50

- Lugas: 9
- Ritmis: 8
- Akurat: 9
- Padat: 9
- Alami: 8

RASA: lulus.

Kenapa lebih baik: pesan menyebut apa yang terjadi, apa yang harus dilakukan, dan apa yang tidak hilang. Tidak ada istilah teknis kosong dan tidak ada tuduhan ke pengguna.

### 3. Email kerja

Brief: tindak lanjut rencana kerja sama. Tim tersedia mulai September 2026. Usul rapat 8 September.

```text
Sebelum:
Dengan hormat, sehubungan dengan rencana kerja sama yang telah kami diskusikan sebelumnya, kami hendak menyampaikan bahwa kami sangat terbuka untuk menjajaki peluang kolaborasi lebih lanjut di waktu mendatang.
```

```text
Sesudah:
Saya ingin menindaklanjuti rencana kerja sama kita. Tim kami bisa mulai September 2026. Apakah tanggal 8 September cocok untuk rapat pertama?
```

Skor: 42/50

- Lugas: 8
- Ritmis: 8
- Akurat: 9
- Padat: 9
- Alami: 8

RASA: lulus.

Kenapa lebih baik: "Dengan hormat" tidak salah. Yang membengkakkan pesan adalah isinya yang berputar. Versi baru menyebut waktu dan langkah berikutnya.

### 4. Caption promosi

Brief: kelas dimulai 3 September 2026. Kuota 20 orang. Pendaftaran ditutup 1 September.

```text
Sebelum:
Jangan lewatkan kesempatan emas ini! Segera daftar dan rasakan pengalaman belajar yang transformative!
```

```text
Sesudah:
Kelas mulai 3 September 2026. Kuotanya 20 orang. Daftar sebelum 1 September kalau ingin ikut.
```

Skor: 44/50

- Lugas: 9
- Ritmis: 9
- Akurat: 8
- Padat: 9
- Alami: 9

RASA: lulus.

Kenapa lebih baik: urgensi asli lebih kuat daripada urgensi palsu. Tanggal dan kuota memberi alasan untuk bergerak.

### 5. Dokumentasi teknis

Brief: layanan harus dihentikan sebelum berkas konfigurasi diubah. Kalau tidak, perubahan tidak terbaca.

```text
Sebelum:
Untuk dapat melakukan konfigurasi ulang pada berkas konfigurasi, pengguna diharuskan untuk terlebih dahulu menghentikan layanan yang sedang berjalan.
```

```text
Sesudah:
Hentikan layanan sebelum mengubah konfigurasi. Kalau layanan tetap jalan, perubahan tidak terbaca.
```

Skor: 44/50

- Lugas: 9
- Ritmis: 9
- Akurat: 9
- Padat: 9
- Alami: 8

RASA: lulus.

Kenapa lebih baik: satu instruksi, satu akibat. Pembaca tidak perlu mengurai kalimat pasif berlapis.

## Format keluaran

### Tulis ulang cepat

Dipakai untuk sebagian besar permintaan.

```text
Hasil:
<teks final>

Skor: <total>/50
- Lugas: <1-10>
- Ritmis: <1-10>
- Akurat: <1-10>
- Padat: <1-10>
- Alami: <1-10>

RASA: <lulus atau gagal, sebut yang gagal>
Kenapa lebih baik:
- <alasan singkat>
- <alasan singkat>
```

### Audit saja

Dipakai kalau pengguna minta "audit", "periksa", atau "jangan tulis ulang".

```text
Masalah:
- "<kutipan>" -> <kenapa bermasalah>

Penilaian:
<apa yang paling penting dan apa yang bisa diabaikan>
```

### Beberapa opsi

```text
Opsi 1:
<teks>
Skor: <total>/50

Opsi 2:
<teks>
Skor: <total>/50

Pilihan terbaik:
Opsi <nomor>, karena <alasan>.
```

### Cocokkan suara

```text
Analisis suara:
- panjang kalimat: <...>
- tanda baca: <...>
- formalitas: <...>
- humor: <...>
- kata yang sering muncul: <...>

Hasil:
<teks>

Skor: <total>/50
```

### Dokumen panjang

```text
1. Brief
2. Masalah yang ditemukan
3. Draf ulang
4. Skor dan status RASA
5. Putaran kedua
6. Versi final
```

## Pemasangan

### Hermes Agent

```bash
mkdir -p ~/.hermes/skills/writing/human-writing-editor
cp SKILL.md ~/.hermes/skills/writing/human-writing-editor/SKILL.md
```

Mulai sesi baru, lalu panggil dengan nama:

```text
Gunakan skill human-writing-editor untuk menyunting teks ini...
```

### Claude Code, Codex, dan agen yang mendukung agentskills

```bash
mkdir -p ~/.skills/human-writing-editor
cp SKILL.md README.md ~/.skills/human-writing-editor/
```

Untuk skill khusus proyek:

```bash
mkdir -p .agents/skills/human-writing-editor
cp SKILL.md README.md .agents/skills/human-writing-editor/
```

### Cursor dan Windsurf

Kalau agen hanya mendukung aturan proyek, salin isi `SKILL.md` ke salah satu berkas ini:

```text
.cursor/rules/human-writing-editor.md
.windsurf/rules/human-writing-editor.md
AGENTS.md
CLAUDE.md
```

Tambahkan instruksi:

```text
Saat diminta menulis ulang, membuat tulisan terasa manusia, mengaudit, atau memberi skor,
ikuti proses Human Writing Editor edisi RASA di berkas ini.
```

### ChatGPT dan Claude Projects

Unggah atau tempel `SKILL.md` ke instruksi proyek. Tambahkan:

```text
Gunakan Human Writing Editor edisi RASA setiap kali pengguna meminta tulisan
diperbaiki, dibuat terasa manusia, atau diberi skor. Pertahankan fakta, hapus pola AI,
periksa EYD, dan jalankan gerbang RASA sebelum menyerahkan hasil.
```

### Prompt sistem

```text
Kamu adalah editor Bahasa Indonesia yang mengikuti Human Writing Editor edisi RASA.
Tugasmu: membuat tulisan lugas, alami, inklusif, dan sesuai EYD, tanpa mengarang fakta.
Selalu audit pola AI, tulis ulang, lalu uji Ritmis, Akurat, Sarat Makna, dan Alami.
Berikan skor lima dimensi. Kalau RASA gagal, perbaiki sebelum menyerahkan hasil.
```

## Prompt siap pakai

Tulis dari brief:

```text
Gunakan human-writing-editor edisi RASA. Tulis [jenis teks] untuk [pembaca] di [kanal].
Tujuan: [tujuan]. Nada: [nada]. Fakta yang boleh dipakai: [fakta]. Jangan menambah klaim.
```

Sunting teks yang sudah ada:

```text
Sunting teks ini dengan human-writing-editor edisi RASA. Pertahankan makna dan fakta.
Hapus pola AI, perbaiki EYD, lalu jalankan RASA. Tunjukkan versi final dan skornya.

Teks:
[tempel teks]
```

Audit tanpa menulis ulang:

```text
Audit teks ini dengan human-writing-editor edisi RASA. Jangan menulis ulang.
Sebut kutipan yang bermasalah, alasannya, dan prioritas perbaikannya.

Teks:
[tempel teks]
```

Bandingkan tiga versi:

```text
Buat tiga versi teks ini: satu netral, satu hangat, satu tegas. Skor ketiganya dengan
lima dimensi dan RASA. Pilih yang paling cocok untuk [pembaca] di [kanal].
```

Cocokkan suara:

```text
Pelajari contoh tulisan saya di bawah. Catat panjang kalimat, formalitas, tanda baca,
dan kata yang sering muncul. Lalu tulis ulang teks target dengan suara yang sama.

Contoh suara:
[tempel contoh]

Teks target:
[tempel teks]
```

Tulis teks antarmuka:

```text
Tulis microcopy untuk [layar atau fitur]. Pengguna: [siapa]. Aksi utama: [aksi].
Sertakan label tombol, pesan kosong, pesan error, dan pesan sukses.
Pakai bahasa polos, jangan menyalahkan pengguna, dan jalankan RASA.
```

## Struktur repo

```text
human-writing-editor/
├── README.md
├── SKILL.md
├── LICENSE
└── examples/
    ├── blog.md
    ├── email.md
    ├── score-only.md
    ├── script.md
    └── tweet.md
```

- `SKILL.md` berisi instruksi agen, termasuk mode Bahasa Indonesia dan gerbang RASA.
- `README.md` menjelaskan alur, aturan, contoh, dan cara memasang.
- `examples/` berisi contoh keluaran untuk beberapa kanal.
- `LICENSE` berisi lisensi MIT.

## Berkontribusi

Kontribusi terbuka untuk siapa saja. Kamu tidak perlu menulis ulang seluruh repo untuk membantu.

Cara berkontribusi:

1. Fork repo, lalu buat branch dengan nama yang jelas.
2. Ubah satu hal per pull request.
3. Sertakan contoh sebelum dan sesudah untuk perubahan aturan.
4. Jelaskan alasannya, bukan hanya apa yang diubah.
5. Pastikan tidak ada fakta baru yang dikarang.

Yang kami cari:

- contoh Bahasa Indonesia untuk kanal yang belum tercakup;
- kasus tepi EYD yang sering salah;
- kalibrasi skor RASA dengan contoh nyata;
- perbaikan kalimat yang masih kaku di README atau `SKILL.md`.

Sebelum mengirim pull request, periksa:

- [ ] Contoh memakai brief yang jelas.
- [ ] Fakta dan angka bisa dilacak.
- [ ] Tidak ada klaim tanpa sumber.
- [ ] Atribusi sumber tetap utuh.
- [ ] Teks baru lulus RASA.

## Peta jalan

Rencana ini bisa berubah. Tidak ada tanggal yang dijanjikan.

- v2.1: contoh Bahasa Indonesia untuk setiap kanal di `examples/`.
- v2.2: pemeriksa otomatis untuk daftar kata terlarang, panjang kalimat, dan perbedaan "di" dengan "di-".
- v2.3: panduan nada untuk industri yang sering menulis teks sensitif, seperti kesehatan dan keuangan.

## Lisensi dan atribusi

Repo ini memakai lisensi MIT. Lihat [LICENSE](LICENSE).

Sumber dan kontribusi:

- [human-writing-editor](https://github.com/feyber/human-writing-editor) oleh Feyber. Menjadi inti audit AI-ism, humanisasi, dan skor.
- [Gist Bahasa Indonesia plain dan RASA](https://gist.github.com/orepras/3e1ca8974fc51d11825f142fa6a66635) oleh [orepras](https://x.com/orepras). Menjadi sumber kerangka RASA, bahasa polos, EYD, inklusif, dan desain ramah trauma.
- Pola humanizer merujuk pada proyek [blader/humanizer](https://github.com/blader/humanizer) dan panduan [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).
- README edisi RASA disusun bersama DeepSeek, lalu ditinjau oleh manusia.

Kerangka RASA diadaptasi, bukan disalin mentah. Hak atas kerangka tetap milik penulis aslinya. Kalau kamu memakai ulang aturan dari repo ini, pertahankan atribusi yang sama.

## Kontributor

| Nama | Peran | Tautan |
| --- | --- | --- |
| Feyber | Pemilik repo, penulis Human Writing Editor, editor akhir. | [github.com/feyber](https://github.com/feyber) |
| [orepras](https://x.com/orepras) | Penulis skill Bahasa Indonesia plain dan kerangka RASA. | [Gist](https://gist.github.com/orepras/3e1ca8974fc51d11825f142fa6a66635) |
| DeepSeek | Agen AI. Menyusun draf README edisi RASA, memadukan aturan, dan menguji contoh. | [deepseek.com](https://www.deepseek.com) |
| Hermes Agent | Co-author `SKILL.md` versi 1.0.0. | tidak ada |

Urutan tidak menunjukkan besar kontribusi. Kontribusi agen AI ditinjau manusia sebelum digabungkan.

## Istilah

| Istilah | Arti |
| --- | --- |
| AI-ism | Pola bahasa yang sering muncul di keluaran model bahasa, seperti pembuka pemanasan dan kata hiasan. |
| Bahasa polos | Gaya menulis yang mudah dipahami pada bacaan pertama tanpa mengurangi substansi. |
| Brief | Ringkasan kebutuhan: pembaca, kanal, tujuan, fakta, dan batasan. |
| EYD | Ejaan yang Disempurnakan, standar ejaan Bahasa Indonesia. Edisi terbaru adalah Edisi V. |
| RASA | Gerbang mutu: Ritmis, Akurat, Sarat Makna, Alami. |
| Suara | Ciri khas tulisan yang membuatnya terdengar ditulis orang tertentu, bukan template. |
| Microcopy | Teks pendek di antarmuka: tombol, label, pesan error, dan petunjuk. |
| CTA | Ajakan bertindak, misalnya tombol atau tautan yang meminta pembaca melakukan sesuatu. |
| Lugas | Langsung ke inti, tanpa pemanasan dan tanpa kata yang tidak perlu. |

## Referensi

- [human-writing-editor](https://github.com/feyber/human-writing-editor)
- [Gist Bahasa Indonesia plain dan RASA](https://gist.github.com/orepras/3e1ca8974fc51d11825f142fa6a66635) oleh [orepras](https://x.com/orepras)
- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [blader/humanizer](https://github.com/blader/humanizer)
- [EYD Edisi V, Badan Pengembangan dan Pembinaan Bahasa](https://ejaan.kemdikbud.go.id/)

---

English summary: a portable agent skill for writing and editing Indonesian text. It combines AI-ism detection and a 50-point score from feyber/human-writing-editor with plain language, EYD, inclusive design, and the RASA gate (rhythm, accuracy, meaning density, natural voice) from the gist by [orepras](https://x.com/orepras). Contributions welcome.
