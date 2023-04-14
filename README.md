# BigData

## Accumulator
<img src="https://user-images.githubusercontent.com/72254185/230758657-257a1d23-86ea-433c-ad99-5ff1cb938e6e.jpg" width="600px">
Kode program di atas menggunakan Spark's accumulator untuk menjumlahkan nilai-nilai dalam RDD (Resilient Distributed Datasets) dan mengeluarkan hasil penjumlahannya. Berikut adalah penjelasan baris per baris kode program tersebut:

<ol>
  <li>Membuat objek accumulator dengan nama myaccum dan nilai awal 0 menggunakan fungsi sc.accumulator(0):</li>
  <pre><code>myaccum = sc.accumulator(0)</code></pre>
  <li>Membuat RDD myrdd dengan nilai dari 1 hingga 99 menggunakan fungsi sc.parallelize(range(1,100)):</li>
  <pre><code>myrdd = sc.parallelize(range(1,100))</code></pre>
  <li>Mendefinisikan sebuah fungsi bernama add_to_accum yang mengambil dua argumen: value (nilai dari RDD) dan accum (accumulator). Fungsi ini menambahkan nilai dari value ke dalam accum menggunakan metode add dari accumulator:</li>
  <pre><code>def add_to_accum(value, accum):
    accum.add(value)</code></pre>
  <li>Menerapkan fungsi add_to_accum pada setiap nilai dari RDD myrdd menggunakan metode foreach. Argumen pertama adalah fungsi yang ingin diterapkan, yaitu lambda value: add_to_accum(value, myaccum) yang akan memanggil fungsi add_to_accum dengan nilai dari RDD dan accumulator myaccum:</li>
  <pre><code>myrdd.foreach(lambda value: add_to_accum(value, myaccum))</code></pre>
  <li>Mencetak hasil akhir penjumlahan yang disimpan dalam accumulator myaccum menggunakan metode value:</li>
  <pre><code>print(myaccum.value)</code></pre>
</ol>

## BroadCast
<img src ="https://user-images.githubusercontent.com/72254185/230758807-f9e43f5d-eca5-4f5d-9079-3c4e43bc3acc.jpg" width="600px">

<ul>
<li>Kode program di bawah ini digunakan untuk membuat Broadcast Variable pada lingkungan pemrosesan Big Data menggunakan Apache Spark.</li>
</ul>
<pre><code>broadcastVar = sc.broadcast(list(range(1, 100)))
broadcastVar.value</code></pre>
<ul>
<li>Pada baris pertama kode program, sebuah Broadcast Variable dibuat dengan nama <code>broadcastVar</code> menggunakan fungsi <code>sc.broadcast()</code>. Variabel ini berisi nilai list dari angka-angka dari 1 sampai 99.</li>
<li>Pada baris kedua, dilakukan pemanggilan fungsi <code>value()</code> pada variabel <code>broadcastVar</code>. Fungsi ini mengembalikan nilai yang ada dalam Broadcast Variable <code>broadcastVar</code>. Karena Broadcast Variable berisi sebuah list dari angka-angka dari 1 sampai 99, maka output dari fungsi <code>value()</code> adalah list tersebut, yaitu:</li>
</ul>
<pre><code>[1, 2, 3, 4, ..., 98, 99]</code></pre>
<p>Dalam Broadcast Variable, nilai hanya perlu dikirimkan satu kali dari driver program ke masing-masing node, sehingga menghemat bandwidth dan waktu pemrosesan data. Nilai dalam Broadcast Variable bersifat read-only dan tidak dapat diubah di node-node yang menerima nilai tersebut.</p>

## PairRDD
<img src ="https://user-images.githubusercontent.com/72254185/230758921-3642ba1c-4c9c-434e-bffd-827fbcc2ffb4.jpg" width="600px">

<ul>
  <li>Pertama-tama, sebuah list dengan nama <code>mylist</code> dibuat yang berisi tiga string: <code>"my"</code>, <code>"pair"</code>, dan <code>"rdd"</code>.</li>
  <li>Selanjutnya, list <code>mylist</code> dijadikan input untuk membuat sebuah RDD dengan menggunakan fungsi <code>sc.parallelize()</code>. RDD ini diberi nama <code>myRDD</code>.</li>
  <li>Setelah itu, dilakukan pemetaan (mapping) pada <code>myRDD</code> dengan menggunakan fungsi <code>map()</code>. Fungsi <code>map()</code> ini menerima sebuah fungsi lambda yang akan diterapkan pada setiap elemen RDD. Fungsi lambda ini akan mengembalikan tuple berisi elemen RDD tersebut dan panjang string dari elemen tersebut. Hasil pemetaan ini disimpan ke dalam sebuah RDD baru dengan nama <code>myPairRDD</code>.</li>
  <li>Pada baris selanjutnya, dilakukan pemanggilan fungsi <code>collect()</code> pada <code>myPairRDD</code>. Fungsi <code>collect()</code> ini akan mengembalikan seluruh elemen yang ada pada RDD <code>myPairRDD</code> dalam bentuk list. Oleh karena itu, output dari pemanggilan fungsi <code>collect()</code> pada <code>myPairRDD</code> adalah: <code>[('my', 2), ('pair', 4), ('rdd', 3)]</code>.</li>
  <li>Pada baris selanjutnya lagi, dilakukan pemanggilan fungsi <code>keys()</code> pada <code>myPairRDD</code>. Fungsi <code>keys()</code> ini akan mengembalikan kunci dari setiap tuple yang ada pada RDD <code>myPairRDD</code>. Oleh karena itu, output dari pemanggilan fungsi <code>keys()</code> pada <code>myPairRDD</code> adalah: <code>['my', 'pair', 'rdd']</code>.</li>
  <li>Pada baris terakhir, dilakukan pemanggilan fungsi <code>values()</code> pada <code>myPairRDD</code>. Fungsi <code>values()</code> ini akan mengembalikan nilai dari setiap tuple yang ada pada RDD <code>myPairRDD</code>. Oleh karena itu, output dari pemanggilan fungsi <code>values()</code> pada <code>myPairRDD</code> adalah: <code>[2, 4, 3]</code>.</li>
</ul>

## WordCount
<img src ="https://user-images.githubusercontent.com/72254185/230758997-c12b1efb-e167-4ec0-aa5d-95a979750a45.jpg" width="600px">
<img src ="https://user-images.githubusercontent.com/72254185/230759082-22bb8364-3af3-4da7-a19d-30eea7df2eab.jpg" width="600px">
<ul>
    <li>Program ini membaca file "README.md" menggunakan fungsi <code>sc.textFile()</code> dan menyimpannya sebagai RDD bernama <code>lines</code>.</li>
    <li>RDD <code>lines</code> kemudian di-flatMap dengan fungsi lambda yang memisahkan setiap baris menjadi kata-kata dengan delimiter spasi.</li>
    <li>Kemudian, setiap kata di-mapping dengan fungsi lambda lain menjadi tuple berisi kata dan integer 1, yang akan digunakan untuk menghitung jumlah kemunculan kata tersebut di RDD.</li>
    <li>Selanjutnya, RDD di-reduceByKey dengan operator <code>add</code> untuk menghitung jumlah kemunculan setiap kata dalam RDD.</li>
    <li>Hasil perhitungan tersebut disimpan dalam variabel <code>output</code>.</li>
    <li>Hasil akhir kemudian dicetak dengan looping for pada setiap tuple <code>(word, count)</code> di dalam variabel <code>output</code>.</li>
</ul>


## UnderstandingRDD
<img src ="https://user-images.githubusercontent.com/72254185/230759144-c1e2effc-393e-4250-9258-185ddb6e1329.jpg" width="600px">
<img src ="https://user-images.githubusercontent.com/72254185/230759168-d679f207-9bbf-46bf-9662-7424cd49a068.jpg" width="600px">
<ul>
<li>Pada baris pertama, program ini memeriksa default parallelism pada lingkungan Apache Spark.</li>
<li>Kemudian, program membuat sebuah RDD dengan menggunakan fungsi <code>parallelize()</code> dan menentukan jumlah partisi yang dibutuhkan pada RDD.</li>
<li>Pada baris keempat, program menggunakan sebuah aksi <code>count()</code> untuk menghitung jumlah elemen dalam RDD.</li>
<li>Pada baris kelima, program menggunakan <code>mapPartitionsWithIndex()</code> untuk menampilkan data di setiap partisi RDD.</li>
<li>Pada baris keenam hingga delapan, program menambahkan partisi pada RDD menggunakan fungsi <code>repartition()</code>, dan mengurangi jumlah partisi pada RDD menggunakan fungsi <code>coalesce()</code>.</li>
<li>Pada baris kesembilan, program menggunakan fungsi <code>toDebugString()</code> untuk menampilkan Lineage Graph dari RDD.</li>
</ul>

## SystemCommandsReturnCode
<img src ="https://user-images.githubusercontent.com/72254185/230759249-3ab42c43-d307-476d-b8e1-e5ce2fd2809a.jpg" width="600px">
<ul>
<li>Program di atas merupakan program Scala yang menjalankan perintah shell pada sistem operasi Unix/Linux.</li>
<li>Pada baris pertama, digunakan <code>import sys.process._</code> untuk mengimpor package <code>sys.process</code> yang menyediakan fungsi-fungsi untuk menjalankan perintah shell pada sistem operasi.</li>
<li>Pada baris kedua, dilakukan eksekusi perintah shell <code>"ls /tmp" !</code> menggunakan operator <code>!</code> pada String <code>"ls /tmp"</code>, yang artinya menjalankan perintah <code>ls /tmp</code> pada shell. Perintah ini akan menampilkan list file dan direktori yang ada pada direktori <code>/tmp</code>.</li>
<li>Hasil eksekusi perintah shell akan disimpan pada variabel <code>res</code> dengan tipe data <code>Int</code>. Nilai yang disimpan adalah status code dari eksekusi perintah. Jika perintah berhasil dieksekusi, maka status code yang dihasilkan adalah 0, sedangkan jika gagal dieksekusi, maka status code yang dihasilkan adalah nilai selain 0.</li>
<li>Pada baris terakhir, dilakukan pencetakan hasil eksekusi perintah shell dengan memanggil variabel <code>res</code> pada String <code>"result = "+res</code>.</li>
</ul>

## SystemCommandsOutputCode
<img src ="https://user-images.githubusercontent.com/72254185/230759297-ecbd9c99-f7c0-44f7-a2e3-089b93c59a79.jpg" width="600px">
<ul>
<li>Program ini menggunakan bahasa Scala untuk menjalankan command line hadoop fs -ls pada sistem operasi. </li>
<li>Pada baris pertama, kita mengimport library <code>sys.process._</code> untuk menjalankan command line.</li>
<li>Baris kedua adalah perintah untuk menjalankan command <code>hadoop fs -ls</code>. Operator <code>!!</code> digunakan untuk mengeksekusi perintah tersebut dan mengembalikan output dalam bentuk string.</li>
<li>Pada baris ketiga, output dari command tersebut dicetak dalam bentuk string.</li>
</ul>
