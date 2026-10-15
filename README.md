# Submission MPK — Kotlin Fundamentals Assessment

**Kumpulan latihan Kotlin/JVM untuk fundamental pemrograman, control flow, generics, collections, coroutines, dan pemecahan masalah sederhana.**

Repository ini merupakan proyek latihan/submission Dicoding yang terdiri atas **5 exam utama** dan **5 optional exam**. Setiap soal memiliki implementasi Kotlin, program contoh, dan instruksi tersendiri. Gradle menyediakan task untuk menjalankan pengujian otomatis.

> **Jenis proyek:** aplikasi/latihan **Kotlin JVM**, bukan aplikasi Android. Tidak ada antarmuka mobile, backend API, atau database pada repository ini. Dokumentasi menjelaskan implementasi yang diperiksa; build dan hasil pengujian belum diverifikasi dengan menjalankan Gradle.

## Daftar latihan

### Lima exam utama

| Latihan | Materi | Implementasi |
| --- | --- | --- |
| [Exam 1 — Fundamental](src/main/kotlin/com/dicoding/exam/exam1/README.MD) | Operator, kondisi, perulangan | `isEvenNumber()`, `moreThanFive()`, dan `result(number) = number * (number + 10)` |
| [Exam 2 — Control Flow](src/main/kotlin/com/dicoding/exam/exam2/README.MD) | Nullable values, Elvis operator, string template | `calculate(a, b, c)` dengan default `c = 50` serta format teks hasil |
| [Exam 3 — Generics](src/main/kotlin/com/dicoding/exam/exam3/README.MD) | Generic function dan type checks | `checkType()` mengenali `Int`, `String`, `Boolean`, `Double`, `List`, dan `Map` |
| [Exam 4 — Collections](src/main/kotlin/com/dicoding/exam/exam4/README.MD) | `Map` dan key-value pairs | `vehicle()` mengembalikan atribut kendaraan sebagai map |
| [Exam 5 — Coroutines](src/main/kotlin/com/dicoding/exam/exam5/README.MD) | `suspend`, `delay`, `async`/`await` | Penjumlahan dan perkalian asinkron dengan delay 3 dan 2 detik |

### Lima optional exam

| Latihan | Materi | Implementasi |
| --- | --- | --- |
| [Optional 1 — Sum of Big Three](src/main/kotlin/com/dicoding/exam/optionalexam1/README.MD) | Collections dan fungsi | Menjumlahkan tiga bilangan terbesar dari `vararg` |
| [Optional 2 — Min and Max](src/main/kotlin/com/dicoding/exam/optionalexam2/README.MD) | Transformasi digit | Menjumlahkan digit terkecil dan terbesar dalam bilangan |
| [Optional 3 — Manipulate String](src/main/kotlin/com/dicoding/exam/optionalexam3/README.MD) | Regular expression dan string | Mengalikan angka dalam string atau menggabungkan angka bila string tidak memiliki digit |
| [Optional 4 — Middle Characters](src/main/kotlin/com/dicoding/exam/optionalexam4/README.MD) | Indeks dan substring | Mengambil satu atau dua karakter tengah |
| [Optional 5 — Concat String](src/main/kotlin/com/dicoding/exam/optionalexam5/README.MD) | Function reference | Menggabungkan dua string melalui `String::plus` |

Setiap folder mempunyai file `README.MD` sendiri yang memuat soal, ketentuan, dan contoh hasil. Lihat file tersebut untuk instruksi asli masing-masing latihan.

## Teknologi dan tooling

| Area | Versi / library yang digunakan |
| --- | --- |
| Bahasa | Kotlin **1.9.0** |
| Platform | Kotlin/JVM (bukan Android) |
| Build | Gradle Wrapper **8.3**, Kotlin DSL |
| Coroutines | `kotlinx-coroutines-core:1.6.2` |
| Testing | Spek 2 (`2.0.18`), JUnit 5 |
| Lint | Plugin Kotlinter `3.16.0` |
| Test report | Task kustom `testReportExam` dan laporan hasil JSON |

Konfigurasi tersebut tercantum dalam [`build.gradle.kts`](build.gradle.kts), [`gradle/wrapper/gradle-wrapper.properties`](gradle/wrapper/gradle-wrapper.properties), dan direktori [`buildSrc/`](buildSrc/).

## Cara menjalankan

### Persyaratan

- **JDK 17** atau versi yang kompatibel dengan Gradle 8.3 dan plugin Kotlin yang digunakan.
- Akses internet pada proses setup pertama untuk mengunduh Gradle dan dependency.
- Terminal. IntelliJ IDEA dapat digunakan untuk menjalankan fungsi `main()` contoh secara individual.

Tidak perlu menginstal Gradle secara global jika menggunakan **Gradle Wrapper** yang tersedia di repository.

### 1. Clone

```bash
git clone https://github.com/alfrzhb/submission-mpk.git
cd submission-mpk
```

### 2. Jalankan pengujian

**macOS / Linux:**

```bash
./gradlew test
```

**Windows (PowerShell):**

```powershell
.\gradlew.bat test
```

Proyek mengonfigurasi `test` dengan JUnit Platform dan memiliki dua rangkaian tes:

- [`ExamTestMain.kt`](src/test/kotlin/ExamTestMain.kt) — menguji lima exam utama.
- [`ExamTestOptional.kt`](src/test/kotlin/ExamTestOptional.kt) — menguji lima exam opsional.

Untuk menjalankan salah satunya saja:

**macOS / Linux:**

```bash
./gradlew test --tests ExamTestMain
./gradlew test --tests ExamTestOptional
```

**Windows:**

```powershell
.\gradlew.bat test --tests ExamTestMain
.\gradlew.bat test --tests ExamTestOptional
```

> **Catatan:** task tambahan `runMainCriteriaTest`, `runOptionalCriteriaTest`, dan `runAllTest` juga didefinisikan, tetapi implementasinya memanggil executable `gradle` secara langsung. Jika Gradle global tidak terpasang pada `PATH`, task tersebut berpotensi gagal. Menggunakan `./gradlew test` atau `.\gradlew.bat test` lebih aman.

### 3. Jalankan pemeriksaan gaya kode

**macOS / Linux:**

```bash
./gradlew lint
```

**Windows:**

```powershell
.\gradlew.bat lint
```

Task `lint` menggunakan Kotlinter dan dikonfigurasi menulis laporan ke direktori `build/lint-result/`.

### 4. Jalankan contoh latihan

Buka proyek di IntelliJ IDEA, lalu jalankan fungsi `main()` pada folder latihan yang ingin diperiksa, misalnya:

- `src/main/kotlin/com/dicoding/exam/exam1/Exam1Main.kt`
- `src/main/kotlin/com/dicoding/exam/exam5/Exam5Main.kt`
- `src/main/kotlin/com/dicoding/exam/optionalexam1/OptionalExam1Main.kt`

Masing-masing latihan mempunyai contoh `Main.kt`; sejumlah fungsi `main()` bersifat `private` pada level file. **Jangan mengasumsikan `./gradlew run` dapat memilih exam otomatis:** plugin `application` tersedia, tetapi tidak ditemukan penetapan `application.mainClass` sebagai entry point tunggal pada konfigurasi build.

## Contoh implementasi

### Conditional logic

```kotlin
fun isEvenNumber(number: Int) = number % 2 == 0
fun moreThanFive(number: Int) = number > 5
fun result(number: Int) = number * (number + 10)
```

### Null safety

```kotlin
fun calculate(valueA: Int, valueB: Int, valueC: Int?): Int {
    return valueA + (valueB - (valueC ?: 50))
}
```

Jika `valueC` adalah `null`, kode menggunakan default `50` melalui Elvis operator (`?:`).

### Coroutines

```kotlin
suspend fun sum(valueA: Int, valueB: Int): Int {
    delay(3000)
    return valueA + valueB
}

suspend fun multiple(valueA: Int, valueB: Int): Int {
    delay(2000)
    return valueA * valueB
}
```

Pada contoh `Exam5Main.kt`, kedua operasi dipanggil menggunakan `async` dan diambil dengan `await` dalam `runBlocking`. Delay terjadi pada coroutine; implementasinya bukan pemanggilan HTTP maupun background service Android.

### Collections

```kotlin
fun sumOfBigThree(vararg numbers: Int): Int =
    numbers.sortedDescending().take(3).sum()
```

Fungsi tersebut mengambil tiga nilai terbesar, termasuk jika ada nilai yang sama.

## Struktur repository

```text
submission-mpk/
├── README.md
├── build.gradle.kts                    # Kotlin/JVM, dependencies, test/lint tasks
├── settings.gradle.kts
├── gradlew
├── gradlew.bat
├── gradle/wrapper/                     # Gradle 8.3 wrapper
├── buildSrc/                            # Custom test-report task
└── src/
    ├── main/kotlin/com/dicoding/exam/
    │   ├── exam1/                      # Fundamental
    │   ├── exam2/                      # Control Flow
    │   ├── exam3/                      # Generics
    │   ├── exam4/                      # Collections
    │   ├── exam5/                      # Coroutines
    │   ├── optionalexam1/              # Three largest values
    │   ├── optionalexam2/              # Min/max digits
    │   ├── optionalexam3/              # String and numeric processing
    │   ├── optionalexam4/              # Middle characters
    │   └── optionalexam5/              # String concatenation
    └── test/kotlin/
        ├── ExamTestMain.kt
        ├── ExamTestOptional.kt
        └── ExtentionsTest.kt            # Shared test helpers
```

Setiap direktori exam memuat file implementasi, file contoh `Main.kt`, dan `README.MD` yang menjelaskan persyaratan tugas.

## Pengujian dan batasan

- Source sudah berisi implementasi untuk **10 latihan**, tetapi **status kelulusan test belum diperiksa melalui eksekusi Gradle** dalam audit dokumentasi ini.
- Test suite menggunakan **Spek 2** dan helper assertion pada `ExtentionsTest.kt`. Task `testReportExam` memproses laporan JUnit XML dan menulis ringkasan JSON jika data tes tersedia.
- Beberapa solusi mengasumsikan input mengikuti batasan soal. Sebagai contoh, fungsi transformasi digit tidak memvalidasi angka negatif, sementara fungsi manipulasi string melakukan konversi `toInt()` yang berisiko error untuk deretan digit yang melebihi batas integer.
- Fungsi pengambil karakter tengah tidak dirancang untuk string kosong; ketentuan soal hanya mengizinkan panjang minimum satu karakter.
- Tidak ada deployment, konfigurasi backend, maupun antarmuka pengguna. Tujuan repository ini adalah menunjukkan praktik Kotlin fundamental dan penyelesaian assessment.

## Ketentuan submission

Petunjuk masing-masing exam mengingatkan agar tidak:

1. Mengubah fungsi `main()` yang disediakan untuk pemeriksaan.
2. Mengubah atau menghapus nama fungsi/variabel yang menjadi kontrak soal, kecuali bagian yang memang diminta.
3. Menambah fungsi yang tidak berkaitan dengan tugas.
4. Mengubah struktur package atau memindahkan file assessment.

Ketentuan tersebut adalah konteks asli latihan. Perubahan README ini **tidak memodifikasi source, konfigurasi Gradle, maupun file pengujian**.

---

**Repository:** [alfrzhb/submission-mpk](https://github.com/alfrzhb/submission-mpk) · **Default branch:** `main`

Dokumentasi disusun berdasarkan source Kotlin, file instruksi, konfigurasi Gradle, dan test yang tersedia.
