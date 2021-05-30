---
title: "Memuat laman web atau blog peribadi anda secara percuma"
date: 2021-04-24T12:06:25+06:00
description: Cara membuat laman web peribadi anda
menu:
  sidebar:
    name: Membuat laman web atau blog peribadi anda secara percuma
    identifier: tutorial laman web
    weight: 10
---

## Pengenalan

Dengan keadaan semasa Covid, mempunyai kehadiran dalam talian tidak pernah begitu penting. Kebanyakan orang akan bergantung kepada laman Facebook untuk mewujudkan kehadiran dalam talian, tanpa berfikir bahawa mereka membinanya dalam persekitaran tertutup. Dengan mempunyai nama domain dan laman web dalam domain yang menghubungkan ke rangkaian sosial lain adalah cara yang lebih baik apabila membina profil untuk nama, perniagaan, atau jenama anda. Dalam tutorial ini, saya akan ajar anda betapa senangnya membuat laman web atau blog yang mudah untuk CV peribadi atau jenama anda dengan percuma menggunakan GitHub sebagai penyedia hosting dan repositori kod. Tutorial ini adalah dibuat untuk pengguna Windows, tetapi langkah-langkah dalam tutorial ini adalah lebih kurang sama untuk pengguna Linux dan Mac OS. 
Untuk menyempurnakan tutorial ini, anda perlu ada:

* komputer dengan Windows and sambungan internet

```
- Mengapa penting untuk mempunyai laman web
- Kenapa sekarang lebih penting untuk mempunyai kehadiran dalam talian
- Betapa mudah dan murahnya untuk dilakukan oleh sesiapa sahaja
- Kami akan membina laman web statik di GitHub, secara percuma
```

## Laman web statik

Untuk menjalankan laman web kami secara percuma, laman web itu mestilah statik, kerana ia adalah laman web yang tidak berubah, semua pengguna yang melawati laman web itu akan nampak halaman yang sama, berbeza dengan laman web dinamik. Sebagai contoh untuk laman web dinamik, pengguna boleh log masuk dan data yang disesuaikan untuk mereka akan dipaparkan, laman web dinamik memerlukan pelayan backend untuk memproses dan memberikan data secara khusus kepada pengguna, sementara laman web statik tidak sama. Inilah sebab laman web statik sangat "murah" untuk dijalankan, bahawa perkhidmatan seperti GitHub membolehkan anda melakukannya secara percuma.

Sekiranya anda sudah mempunyai pengalaman pengkodan HTML dan CSS, anda boleh membuat laman web statik anda sendiri tanpa memerlukan alat penjana laman web statik. Kelebihan bagi memilih satu alat penjana laman web statik adalah ia dapat mengurangkan pengetahuan pengekodan yang anda perlukan, oleh itu anda hanya perlu memahami cara mengedit teks dan fail konfigurasi.

Untuk panduan ini, kami telah memilih Hugo.

### Hugo - Penjana laman web statik

[Hugo](https://gohugo.io) adalah penjana laman web statik moden yang sangat popular dan ia ditulis dalam bahasa Go ([Golang](https://golang.org/)) yang kebetulan ia adalah Open Source dan bebas digunakan. Ia mempunyai komuniti yang besar dan pelbagai tema untuk dipilih. Kami akan menjelaskan secara terperinci apa yang dimaksudkan dengan "tema" di bahagian seterusnya.

### Menggunakan tema

Setelah anda memahami sedikit cara membuat dan menjalankan laman web statik yang mudah melalui Hugo, jika kami mahu membuat laman web sendiri di Hugo dari awal, ini akan memerlukan beberapa HTML, CSS, templat dan beberapa dalaman dari Hugo untuk membuat laman web 100% kami sendiri yang disesuaikan. Tetapi ada pilihan yang lebih mudah, seperti yang dinyatakan sebelum ini, Hugo memiliki komunitas yang besar dan mereka menawarkan banyak jenis laman web pra dibina, ini dipanggil tema.
Anda boleh navigasi tema di sini: <https://themes.gohugo.io/>

Cari satu tema yang anda suka untuk laman web anda, bergantung pada tujuannya anda boleh memilih dari, laman web peribadi, blog, atau yang lain.

Untuk panduan ini kami akan menggunakan tema [Ananke](https://themes.gohugo.io/gohugo-theme-ananke/).

### Menjalankan Hugo di Windows

Mari pasangkan Hugo dahulu dan membiasakan diri untuk membuat satu laman web asas dan pengubahsuaian tempatan daripada menggunakan Windows PowerShell.

Untuk panduan ini kami mengesyorkan Chocolatey, pengurus pakej Windows untuk memasang perisian prasyarat.
Ikut panduan ini untuk memasangkan Chocolatey jika anda belum melakukannya: <https://chocolatey.org/install>

Selepas Chocolatey dipasangkan, buka satu PowerShell terminal dan jalankan arahan berikut:

`choco install hugo -confirm`

Hugo seperti yang dinyatakan adalah penjana laman web statik, dan kami akan menggunakan ia untuk jalankan laman web secara tempatan di komputer kita.

`choco install github-desktop`

GitHub desktop akan memudahkan proses memuat naik kod sumber ke GitHub.

Syabas! Sekarang anda mempunyai Git dan Hugo dipasang pada mesin anda.

### Membuat laman web Hugo baru

Dalam PowerShell yang sama, arahkan ke direktori utama anda dengan arahan berikut `cd $HOME/Documents`

![powershell_home.png](/posts/personal-website-tutorial/powershell_home.png)

Seterusnya, kami akan beritahu Hugo untuk membina satu laman web baru, pilih nama untuknya seperti `personal-site`

`hugo new site <sitename>`

Setelah menjalankan arahan ini, Hugo akan membuat satu folder dengan nama yang sama dengan pelbagai fail di dalamnya, arahkan ke direktori itu dengan: `cd <sitename>` jika anda menyenaraikan fail di dalamnya dengan `ls`, ia sepatutnya kelihatan seperti:

![powershell_personal-site.png](/posts/personal-website-tutorial/powershell_personal-site.png)

Sekarang kami perlu memulakan projek baru ini sebagai satu Git repositori:

`git init`

Import tema yang anda pilih di bahagian sebelumnya:

`git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke`

Seterusnya, buka `config.toml` pada root folder dan nyatakan beberapa parameter untuk laman web Hugo ini, toml adalah fail teks, oleh itu anda boleh menggunakan Notepad, VSCode ataupun penyunting lain yang anda suka.

Kami akan ubah tajuk dan parameter baru yang dinamakan `theme` dengan nama tema yang dipilih. Fail anda akan nampak seperti ini:

```
baseURL = "http://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```

Simpan fail apabila anda selesai.

Seterusnya, jalankan laman web baru anda secara tempatan dengan tema yang dipilih:

`hugo server --watch`

Perintah di atas harus menghasilkan sesuatu yang serupa dengan ini:

```
hugo server --watch
Start building sites …

                   | EN
-------------------+-----
  Pages            |  7
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  1
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 13 ms
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Anda kini boleh melayari url berikut di penyemak imbas anda untuk melihat laman web baru anda💥:

http://localhost:1313

### Membuat perubahan dan menambah kandungan

Jika semua berjalan lancar, anda boleh lihat halaman yang sangat asas dengan tajuk laman web ini.

Di bahagian ini kami akan terus menerangkan bagaimana untuk menyesuaikan laman web ini lebih lanjut dan menambah lebih banyak halaman dan catatan.

Setiap tema Hugo mempunyai sekumpulan ciri-ciri asas dan mempunyai penyesuaian yang lebih khusus. Untuk membolehkan anda memilih sebarang tema, kami akan membimbing anda melalui ciri-ciri yang paling umum supaya anda dapat menerapkan pengetahuan ini, untuk digunakan dengan tema lain dan juga laman web yang anda akan membina pada masa depan.

Kami perlu membuat perbezaan antara 2 konsep terlebih dahulu, dalam Hugo ada **Pages** dan **Posts**, Page adalah bahagian statik di laman web anda yang tidak kerap berubah, seperti bahagian informasi tentang kita, sejarah organisasi anda, atau halaman hubungan. Seterusnya anda ada Post, yang merupakan artikel yang anda tulis dengan lebih kerap dan disusun mengikut tarikh penerbitan.

Mari kita bermula dengan halaman pertama, ia adalah halaman About Me. Buat folder baru di dalam `content`

direktori dinamakan `about-me` dan kemudian buat fail yang dinamakan `_index.md` di dalam.

Tambahkan kandungan berikut ke dalamnya:

```
---
title: "About Me"
date: 2021-03-27
draft: false
---

Write something about you here
```

Kami akan menambah satu post seterusnya, post ini boleh ditambah dengan membuat fail baru dalam `content/posts`.

Buat fail dinamakan `my-first-post.md` di dalam `content/posts` dengan kandungan berikut:

```
---
title: "My First Post"
date: 2021-03-27
draft: false
---

This is first post!
```

Jika anda kembali ke laman web anda di penyemak imbas, anda akan nampak post yang anda binakan tetapi bukan halaman about-us. Ini disebabkan oleh pengaktifkan menu pada tema, untuk membuat ini, mengeditkan `config.toml` sekali lagi dan tambah parameter berikut:

```
SectionPagesMenu = "main"
```

Simpan, dan ia akan memuatkan semula secara automatik dan menunjukkan About Me di sudut kanan atas laman web.

Setakat ini, laman web anda sepatutnya kelihatan seperti ini:![hugo_aboutMe.png](hugo_aboutMe.png?fileId=322829#mimetype=image%2Fpng&hasPreview=true)

Hugo sangat fleksibel dan mempunyai banyak pilihan yang boleh anda gunakan untuk menyesuaikan halaman anda, ingatkan bahawa untuk memformat teks anda boleh menggunakan semua ciri [Markdown](https://commonmark.org/), anda juga boleh tambah [feature images](https://github.com/theNewDynamic/gohugo-theme-ananke#change-the-hero-background) atau tanamkan gambar tambahan pada post dan halaman anda.

Jika anda mahu tambahkan satu gambar pada post atau halaman,letakkan gambar di dalam `static` folder dan gunakan sintaks berikut di dalam halaman atau post:

```
![Chocolate cake](/cake.jpg "A delicious chocolate cake")
```

Terus ulangi langkah ini, dengan menambahkan lebih banyak post, halaman dan kandungan yang anda mahukan untuk laman web anda.

Setelah anda berpuas hati dengan ini, teruskan ke bahagian seterusnya.

## Ke bulan 🚀

Sejauh ini kami melakukan pengubahsuaian dan melihatnya secara tempatan, mungkin anda fikir bahawa bagaimana laman web anda daripada dalam komputer, kepada tersedia secara terbuka di internet?

Terdapat beberapa langkah yang perlu anda ikuti untuk mengarkibkan ini dan kami akan memperincikannya di bahagian seterusnya

### Pengacaraan laman web di GitHub

Seperti yang kita nyatakan pada bahagian awal tutorial ini, kami akan menggunakan GitHub sebagai platform hosting untuk laman web kami, ciri utama GitHub adalah kod hosting tetapi mereka juga mempunyai perkhidmatan dipanggil GitHub pages yang membolehkan anda melakukan apa sahaja yang boleh anda bayangkan, hosting laman web statik anda, dan bahagian yang terbaik adalah 100% percuma, anda tidak perlu berurusan dengan penyedia hosting, pelayan maya, konfigurasi back-end, dan lain-lain.


Sekiranya anda ingin mengetahui lebih lanjut mengenai GitHub pages, boleh tengok video ini:
<<https://www.youtube.com/watch?v=2MsN8gpT6jY>>

### Membuat akaun GitHub


Untuk hos laman web anda di GitHub, anda memerlukan akaun, anda boleh membuatnya secara percuma di sini:
<https://github.com/join>

### Membuat 'repository'

Halaman GitHub dihubungkan kepada repositori GitHub, secara ringkas, kod yang anda masukkan ke dalam repositori tersedia sebagai halaman GitHub.

Pertama kita perlu membuat repositori, ini boleh dipanggil `personal-site`.

Sekarang kita ada repositori kod baru kami, kami perlu menghantar kod dari komputer kami ke GitHub, cara Git untuk memuat naik kod adalah menggunakan arahan "git push", tetapi sebelum itu kita perlu membuat beberapa langkah.

Pertama, kita perlu memberitahu kod kita di komputer bahawa itu adalah git repositori yang dihubungkan dengan GitHub, untuk melakukan ini kita jalankan:

`git remote add origin git@github.com:<your-username>/<your-repository-name>`

### 'Push' kod anda ke GitHub

Setelah mengetahui di mana "git server", kita perlu memberitahu kod mana yang ingin kita tolak, tindakan ini dipanggil "git commit", untuk kali ini, kami akan membuat komit besar dengan semua kod baru ini, tetapi biasanya anda melakukan potongan kecil yang menerangkan perkara-perkara yang telah diubah.

Buka GitHub Desktop dan pilih semua fail fail dan buat komit baru, tulis mesej komit dan klik ***commit*** *butang.*

Sebaik sahaja kita membuat semua kod yang dilakukan, kita hanya perlu menekan ke GitHub dengan mengklik butang penyegerakan:

Arahan ini memberitahu Git untuk mendorong semua kod yang dititikberatkan pada cawangan semasa ke cabang `main` in` origin` jika anda melihat perintah pertama yang kami tetapkan GitHub sebagai asal untuk repositori kod kami, oleh itu kod ini akan dimuat naik ke Repositori GitHub.


Hebat! anda baru sahaja membuat komit pertama anda!

Sekarang kod anda ada di GitHub, dan pada ketika ini anda boleh mengajak rakan untuk mula berkolaborasi dalam kod yang sama dan dia akan dapat memuat turun dan mendorong perubahan, ulasan atau komen mengenai pengubahsuaian tersebut dan memperbaiki laman web ini bersama-sama.

### Konfigurasikan GitHub Actions

Sejauh ini kami bergantung pada menjalankan Hugo secara tempatan untuk membina laman web tersebut secara tempatan dan kami menolak kod sumber ke GitHub, tetapi ini bukan laman terakhir, kami perlu memberitahu Hugo untuk membina atau mengemas fail akhir yang akan "served" kepada pengunjung laman web kami. Untuk ini kita akan menggunakan GitHub Actions.

GitHub Actions pada dasarnya adalah program kecil yang dapat melakukan sesuatu untuk kita. Jangan risau, kerana kita tidak perlu menulis program kita sendiri untuk ini. Sekali lagi, kita akan bergantung pada kekuatan Open Source dan kita akan menggunakan semula sesuatu yang telah dibuat oleh orang lain yang dikongsikan dengan semua orang.

Di bahagian ini kita akan mengkonfigurasi satu GitHub Action yang akan membina / mengemas laman web kita secara automatik setiap kali kita menggabungkan beberapa kod ke dalam cabang `main`.

Pertama, tambah 2 folder baru di akar projek anda dalam komputer: `.github` (bukan titik pada permulaan) dan di dalam folder yang lain nama `workflows` di dalam folder ini buat satu file bername \` gh-pages.yml \` dan tambahkan kandungan berikut:

```
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

Komit file baru ini dengan GitHub Desktop dan tolak kepada GitHub.

Sekira semuanya berjalan dengan lancar, anda seharusnya dapat menavigasi ke bahagian Actions dalam projek GitHub anda dan melihat jika berjaya (cari cek hijau).

![swappy-20210328_112840.png](swappy-20210328_112840.png?fileId=322982#mimetype=image%2Fpng&hasPreview=true)

Ini sekarang bermaksud bahawa setiap kali anda membuat perubahan ke laman web anda dan mendorong perubahan itu ke cawangan `main`, GitHub akan membuat versi terbaru laman web anda secara automatik dan menyimpannya ke cawangan yang dinama `gh-pages`.

### Konfigurasikan GitHub pages

Ok, sekarang kita mempunyai GitHub Action yang menolak laman web terakhir kita ke cawangan `gh-pages`, bagaimanakah kita boleh mengunjungi laman web kita di internet? Di sinilah halaman GitHub masuk.

Kita perlu memberitahu GitHub bahawa repositori kami ingin menggunakan halaman GitHub. Untuk melakukan ini, pergi ke tetapan repositori dan tatal ke bahagian bawah halaman ke tetapan GitHub Page. Di sini anda akan memilih cabang `gh-pages` dan \`/ (root)\`, klik butang Save.

![swappy-20210328_113512.png](swappy-20210328_113512.png?fileId=323000#mimetype=image%2Fpng&hasPreview=true)

Setelah mengklik butang Save, mesej di kotak hijau akan memberikan url untuk laman web baru anda.

Sempurna! sekarang laman web anda sudah siap, dan anda seharusnya dapat mengunjunginya dari mana sahaja di dunia menggunakan alamat seperti: 
**http://*username*.github.io/*repository***

Kini laman web anda dapat diterbitkan secara automatik setiap kali ada perubahan dengan senang! Bukankah ini luar biasa?

## Menambahkan domain tersuai

Pada dasarnya kami sudah selesai dengan panduan untuk menerbitkan laman web secara percuma di GitHub, tetapi ceri di atasnya adalah mempunyai nama domain tersuai yang menunjuk ke laman web baru kami. Ini akan memberi anda penampilan yang lebih profesional dan seiring dengan berjalannya waktu, domain anda sendiri akan membuat *authority* di internet, lihat ini jenis reputasi di Internet.

### Mendapatkan domain percuma atau berbayar

Terdapat beberapa laman web di mana anda boleh mendapatkan domain percuma selama 1 tahun, beberapa domain ini tidak mempunyai TLD seperti `*.tk` yang sangat biasa, anda boleh menggunakannya dan mendapatkan sesuatu seperti `you-username.tk`. Tetapi jika anda menggunakan laman web ini untuk sesuatu yang serius seperti laman web peribadi atau perniagaan, saya akan mengesyorkan sesuatu yang anda suka dan ingin mengekalkannya untuk tahun-tahun akan datang. 
(ingat masa anda mencipta gigglybear4u@hotmail.com e-mel tahun yang lalu? 🤣)

Kami mengesyorkan [Freenom](https://www.freenom.com/) untuk mendapatkan beberapa domain secara percuma selama 1 tahun, anda boleh memilih dari `.tk`, `.ml` `.ga`, `.cf` dan `.gp` memilih mana-mana jika anda mahu, anda boleh memilih salah satu yang bukan percuma, berharga lebih kurang $15 setahun.

### Freenom domain

![swappy-20210328_113914.png](swappy-20210328_113914.png?fileId=323013#mimetype=image%2Fpng&hasPreview=true)

Pastikan anda pilih percuma 1 tahun dan luangkan masa untuk mengkonfigurasi DNS untuk GitHub pages (`185.199.108.153`) :

![swappy-20210328_114015.png](swappy-20210328_114015.png?fileId=323012#mimetype=image%2Fpng&hasPreview=true)

### Konfigurasikan DNS

Setelah anda mempunyai nama domain berkilat baru anda, kami perlu memberitahunya apa yang harus dilakukan apabila sesiapa menaipkan ia di bar penyemak imbas. Untuk kes ini, kami akan membuat catatan `A` yang akan menunjuk ke alamat ip GitHub dan catatan` CNAME` untuk meneruskan permintaan ke `www.yourdomain.com` ke domain 'naked' `yourdomain.com`

Kami sudah membuat catatan DNS pada langkah sebelumnya, jadi tidak ada perkara lagi yang perlu dilakukan di laman Freenome, tetapi kami masih perlu memberitahu GitHub bahawa domain mana yang kami gunakan.

Pertama, kita perlu mengkonfigurasi laman web kita untuk menggunakan domain tersebut, kita perlu membuat 2 perkara.

Buat satu fail CNAME dengan nama domain di dalam `static` folder. Anda boleh menggunakan arahan baris tunggal ini untuk melakukannya sekali. Ingat bahawa arahan ini perlu dilaksanakan pada akar projek anda dengan menggunakan PowerShell.

```
echo "<your-domain-name>" > static/CNAME
```

Seterusnya, edit lagi `config.toml` dan kemas kini baris pertama di mana baseUrl ditetapkan, sekarang ia semestinya nama domain anda: \`baseUrl = "http://<your-domain-name>"

Komit perubahan ini dan tolak kepada GitHub.

Akhirnya kita hanya perlu pergi ke tetapan repositori di GitHub dan menetapkan nama domain kita:

![swappy-20210328_120412.png](swappy-20210328_120412.png?fileId=323036#mimetype=image%2Fpng&hasPreview=true)

Sekiranya dikehendaki (dan disyorkan) selepas 24 jam mengaktifkan pilihan ini, anda boleh mengaktifkan https untuk domain anda dengan memeriksa pilihan "Enforce HTTPS" dan mengemas kini lagi baseUrl di config.toml menjadi `https` bukannya `http`.

## Kesimpulan

Saya harap anda menikmati tutorial ini dan anda sekarang menjadi pemilik laman web peribadi yang bahagia di World Wide Web. Pada masa ini yang selalu berhubung dengan internet dari pelbagai perkara, mempunyai laman web yang mudah seperti ini macam tidak begitu penting untuk dilakukan, kerana sekarang semua orang menggunakan perkhidmatan awam seperti Facebook untuk menjadi tuan rumah halaman perniagaan mereka. Jangan biarkan ini menipu anda, ketika menggunakan halaman Facebook, anda meletakkan syarat untuk pengguna anda mempunyai akaun Facebook. Anda juga terhad kepada standard ciri dan reka bentuk Facebook, dan akhirnya dengan memiliki domain anda sendiri, anda adalah pemilik kandungan yang anda terbitkan.