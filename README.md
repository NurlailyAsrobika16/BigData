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
<code>
<pre>
Kode program di bawah ini digunakan untuk membuat Broadcast Variable pada lingkungan pemrosesan Big Data menggunakan Apache Spark.
<b>broadcastVar = sc.broadcast(list(range(1, 100)))
broadcastVar.value</b>

Pada baris pertama kode program, sebuah Broadcast Variable dibuat dengan nama <code>broadcastVar</code> menggunakan fungsi <code>sc.broadcast()</code>. Variabel ini berisi nilai list dari angka-angka dari 1 sampai 99.

Pada baris kedua, dilakukan pemanggilan fungsi <code>value()</code> pada variabel <code>broadcastVar</code>. Fungsi ini mengembalikan nilai yang ada dalam Broadcast Variable <code>broadcastVar</code>. Karena Broadcast Variable berisi sebuah list dari angka-angka dari 1 sampai 99, maka output dari fungsi <code>value()</code> adalah list tersebut, yaitu:

[1, 2, 3, 4, ..., 98, 99]

Dalam Broadcast Variable, nilai hanya perlu dikirimkan satu kali dari driver program ke masing-masing node, sehingga menghemat bandwidth dan waktu pemrosesan data. Nilai dalam Broadcast Variable bersifat read-only dan tidak dapat diubah di node-node yang menerima nilai tersebut.
</pre>
</code>

## WordCount
<img src ="https://user-images.githubusercontent.com/72254185/230758997-c12b1efb-e167-4ec0-aa5d-95a979750a45.jpg" width="600px">
<img src ="https://user-images.githubusercontent.com/72254185/230759082-22bb8364-3af3-4da7-a19d-30eea7df2eab.jpg" width="600px">

<pre>
<code>
from operator import add
# mengimpor modul 'add' dari pustaka 'operator'

lines = sc.textFile("C:/Users/Asus X453/bigdata/spark3/bin/README.md")
# membaca file teks 'README.md' sebagai RDD (Resilient Distributed Dataset)

counts = lines.flatMap(lambda x: x.split(' ')) \
              .map(lambda x: (x, 1)) \
              .reduceByKey(add)
# melakukan pemetaan (mapping) setiap kata dalam RDD 'lines' dengan nilai awal 1, kemudian dilakukan reduksi dengan operasi penjumlahan pada setiap kata yang sama

output = counts.collect()
# mengumpulkan hasil reduksi ke dalam sebuah variabel 'output'

for (word, count) in output:
    # melakukan iterasi pada setiap pasangan kata dan jumlah kemunculannya dalam 'output'
    print("%s: %i" % (word, count))
    # mencetak kata dan jumlah kemunculannya dalam format string
</code>
</pre>

## UnderstandingRDD
<img src ="https://user-images.githubusercontent.com/72254185/230759144-c1e2effc-393e-4250-9258-185ddb6e1329.jpg" width="600px">
<img src ="https://user-images.githubusercontent.com/72254185/230759168-d679f207-9bbf-46bf-9662-7424cd49a068.jpg" width="600px">

## SystemCommandsReturnCode
<img src ="https://user-images.githubusercontent.com/72254185/230759249-3ab42c43-d307-476d-b8e1-e5ce2fd2809a.jpg" width="600px">

## SystemCommandsOutputCode
<img src ="https://user-images.githubusercontent.com/72254185/230759297-ecbd9c99-f7c0-44f7-a2e3-089b93c59a79.jpg" width="600px">
