# Tugas2-aplikasi-cuaca-ionic-vue
# Aplikasi Prakiraan Cuaca Jakarta (WeatherApp)

## Deskripsi Proyek

WeatherApp merupakan aplikasi prakiraan cuaca sederhana yang dikembangkan menggunakan **Ionic Framework, Vue.js 3, dan TypeScript**. Aplikasi ini mengambil data temperatur per jam dari Open-Meteo API untuk wilayah Jakarta, kemudian menampilkannya dalam bentuk kartu agar mudah dibaca.

Proyek ini dibuat sebagai bagian dari tugas praktik perkuliahan untuk menerapkan penggunaan API, pengolahan data JSON, dan penampilan data secara dinamis pada aplikasi berbasis web.

## Sumber Data API

Aplikasi menggunakan Open-Meteo API dengan endpoint berikut:

`https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m`

Data yang digunakan meliputi:
- `time`: waktu pengukuran temperatur.
- `temperature_2m`: temperatur udara pada ketinggian 2 meter, dalam derajat Celsius.

## Teknologi yang Digunakan

- Ionic Framework untuk komponen antarmuka.
- Vue.js 3 untuk membangun tampilan reaktif.
- TypeScript untuk penulisan kode.
- Axios untuk mengambil data dari API.
- Open-Meteo API sebagai sumber data temperatur.

## Alur Kerja Aplikasi

1. Aplikasi mengirimkan permintaan data ke Open-Meteo API menggunakan Axios.
2. Respons API diterima dalam format JSON.
3. Data waktu dan temperatur diambil dari bagian `hourly`.
4. Data dipetakan ke dalam array reaktif Vue dan dibatasi menjadi 10 data pertama agar tampilan tetap ringkas.
5. Data ditampilkan menggunakan komponen Ionic dan perulangan `v-for`.
6. Waktu ditampilkan dalam format yang lebih mudah dibaca oleh pengguna di Indonesia.
7. Aplikasi menggunakan simbol cuaca berdasarkan rentang temperatur sebagai elemen visual pendukung.

**Catatan:** Simbol cuaca pada aplikasi ditentukan berdasarkan temperatur, bukan berdasarkan kondisi cuaca aktual dari API. Oleh karena itu, simbol tersebut hanya berfungsi sebagai ilustrasi.

## Struktur Proyek

Bagian utama proyek meliputi:

- `src/`: kode sumber aplikasi.
- `src/views/CuacaPage.vue`: halaman utama yang mengolah dan menampilkan data cuaca.
- `src/router/`: pengaturan navigasi halaman.
- `src/components/`: komponen antarmuka yang digunakan jika tersedia.
- `public/`: berkas statis.
- `package.json`: informasi proyek dan daftar dependensi.
- `package-lock.json`: catatan versi dependensi yang terpasang.

Struktur tersebut merupakan gambaran umum. Susunan folder dapat berbeda sesuai konfigurasi proyek.

## Cara Menjalankan Proyek

Pastikan Node.js dan npm sudah terpasang di komputer.

1. Unduh repository melalui tombol **Code → Download ZIP**, kemudian ekstrak berkasnya. Alternatifnya, gunakan perintah `git clone` jika Git sudah tersedia.
2. Buka terminal pada folder utama proyek yang berisi `package.json`.
3. Instal dependensi dengan perintah:

   ```bash
   npm install
   ```

4. Jalankan aplikasi menggunakan:

   ```bash
   npm run dev
   ```

5. Buka alamat lokal yang ditampilkan oleh terminal pada browser.

Jika perintah `npm run dev` tidak tersedia, periksa bagian `scripts` dalam `package.json` dan gunakan perintah yang memang disediakan oleh proyek.

## Tujuan Pembelajaran

Melalui proyek ini, mahasiswa berlatih mengambil data dari API eksternal, membaca struktur respons JSON, mengolah array, menggunakan data reaktif Vue, serta menampilkan informasi secara dinamis dengan komponen Ionic.

## Sumber

- Open-Meteo. [Weather Forecast API](https://open-meteo.com/en/docs).
- Ionic Framework. [Dokumentasi Resmi Ionic Vue](https://ionicframework.com/docs/vue).
- Vue.js. [Dokumentasi Resmi Vue.js](https://vuejs.org/guide/introduction.html).
