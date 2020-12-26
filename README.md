Disusun Oleh :  
        1. Husef Sholikhul Ibad (185410110)
        2. Annisa Salsabila (185410070)
        
   
   Apache Spark adalah teknologi komputasi clustering yang sangat cepat dan dirancang untuk kebutuhan yang memerlukan penanganan data secara cepat seperti big data dan machine learning.

    Fitur andalan Apache spark adalah kumpulan memori yang dapat meningkatkan kecepatan pemrosesan aplikasi. Spark dirancang untuk menutupi berbagai beban kerja, seperti proses aplikasi, algoritma berulang-ulang, query interaktif, dan transmisi. Selain mendukung semua beban kerja pada setiap sistem, fitur apache spark ini juga dapat mengurangi beban maintenance management.

    Apache Spark akan mengontrol semua metode data dari berbagai repository, seperti dari Hadoop Distributed classification system (HDFS), NoSQL Database dan penyimpanan data relatif, seperti Apache Hive.

    Spark akan mengelola memori pendukung untuk membantu proses yang sedang berjalan, contohnya saat sedang menganalisis data.spark akan membagi semua proses ke dalam memori pendukung sehingga dapat memaksimalkan kinerja sistem.

    Spark sendiri terdiri dari Spark Core dan beberapa Library pendukung. inti dari Spark engine adalah distributed execution engine, dan API Java, Scala maupun Python yang kemudian Library tambahan akan berjalan diatas Spark Core untuk melakukan berbagai proses seperti Streaming, SQL, machine learning.

    Kelemahan Hadoop

      ●	Kecepatan pemrosesan rendah: di Hadoop, algoritma MapReduce, yang merupakan algoritma paralel dan terdistribusi, memproses kumpulan data yang sangat besar.

      ●	Pemrosesan batch: Hadoop mengimplementasikan pemrosesan batch, yang mengumpulkan data dan kemudian memprosesnya secara massal. Meskipun pemrosesan batch efisien untuk memproses volume data yang besar, ia tidak memproses data transmisi. Akibatnya, kinerjanya menjadi lebih lambat.

      ●	Tidak memiliki Pipeline: Hadoop tidak mendukung pipeline (yaitu, urutan tahapan di mana ID keluaran dari tahap sebelumnya adalah input dari tahap berikutnya).

      ●	Sulit untuk digunakan: Pengembang MapReduce perlu menulis kode mereka sendiri untuk setiap operasi, yang membuat pekerjaan menjadi sangat sulit. Selain itu, MapReduce tidak memiliki mode interaktif.

      ●	Latency: Di Hadoop, struktur MapReduce lebih lambat karena mendukung berbagai format, struktur, dan data yang besar.

      ●	Longline kode: karena Hadoop ditulis dalam Java, kode ini luas. Dan itu membutuhkan waktu lebih lama untuk menjalankan program.
 

Membangun Infrastruktur Apache Spark

Sebelum memasang perangkat lunak baru, ada baiknya untuk menyegarkan basis data paket perangkat lunak lokal Anda untuk memastikan Anda mengakses versi terbaru.

    1. Pastikan kalian memiliki vm, buka terminal lalu masukkan kode ssh berikut : 
         ssh root@47.254.242.17
         
    2. Sebelum menginstall apache spark, kita membutuhkan sebuah Packages / mengistall dependensi yang diperlukan seperti JDK .
          root@iZ8psi2f05o3u61bvpd:~# sudo apt install default-jdk
          
    3. Cek java Version, sekaligus mengecek apakah JDK sudah terinstall seperti yang kita inginkan.
          root@iZ8psi2f05o3u61bvpd:~# java --version
          
    4. Unduh Spark dari situs web dengan menggunakan perintah wget/curl dan tautan langsung untuk mengunduh arsip :
          root@iZ8psi2f05o3u61bvpd:~# curl -O https://downloads.apache.org/spark/spark-2.4.7/spark-2.4.7-bin-hadoop2.7.tgz
    
    5. Selanjutnya Extract file spark yang kita download tadi dengan perintah tar. Disini dilakukan proses kompresi file apache yang sudah didownload sebelumnya dengan menggunakan perintah dibawah ini :
          root@iZ8psi2f05o3u61bvpd:~# tar xvzf spark-2.4.7-bin-hadoop2.7.tgz 
   
    6. setelah file ter extract semua, pindahkan spark-2.4.7-bin-hadoop2.7 ke directory /opt/spark, menggunakan perintah mv.
          root@iZ8psi2f05o3u61bvpd:~# sudo mv spark-2.4.7-bin-hadoop2.7 /opt/spark
    
    7. Kemudian masuklah ke directory /opt/spark dengan menggunakan perintah cd.
          root@iZ8psi2f05o3u61bvpd:~# cd /opt/spark/ 
   
    8. setelah masuk ke directory /opt/spark, run master.sh menggunakan perintah berikut :
          root@iZ8psi2f05o3u61bvpd:/opt/spark# sudo sbin/start-master.sh

          Setelah dikonfigurasi, selanjutnya adalah start server-master spark. Perintah sebelumnya menambahkan direktori yang diperlukan ke variabel PATH sistem, jadi perintah ini dapat dijalankan dari direktori manapun ;
     
    9. Gunakan perintah cat untuk mengetahui url spark untuk digunakan menjalankan perintah slave nantinya.
           root@root@iZ8psi2f05o3u61bvpd:/opt/spark# cat /opt/spark/logs/spark-root-org.apache.spark.deploy.master.Master-1 iZ8psi2f05o3u61bvpd.out

    10. Selanjutnya kita jalankan Spark Slave Server menggunakan perintah :
            root@root@iZ8psi2f05o3u61bvpd:/opt/spark# sudo
            sbin/start-slave.sh
            spark://root@iZ8psi2f05o3u61bvpd:7077

            (Perintah diatas sesuai dengan hasil langkah ke 9)
         --> Perintah ini digunakan untuk mengetahui proses yang sedang berjalan dan lokasi spark yang dapat diakses melalui web.
    
    11. Buat lah file input.txt menggunakan perintah pico seperti berikut :   
             root@iZ8psi2f05o3u61bvpd:/opt/spark# pico input.txt
             
             (Text  akan diinputkan :)
             
             Lalu isilah dengan konten dibawah ini(text), kemudian save dengan tekan CTRL X , lalu tekan Y, kemudian tekan Enter.
    
     12. Lalu bukalah Spark Shell menggunakan perintah :
              root@iZ8psi2f05o3u61bvpd:/opt/spark# bin/spark-shell

     13. Diatas merupakan tampilan dari Spark, disini kita bisa menginputkan text didalamnya.

     14. Tuliskan perintah berikut pada Spark Shell :
              scala> val inputfile = sc.textFile("input.txt")
              scala> val counts = inputfile.flatMap(line => line.split("")).map(word => (word,1)).reduceByKey(_+_);
              scala> counts.cache()
              scala> counts.saveAsTextFile("output")
              
     15. Setelah itu, keluar dari spark-shell dengan menekan CTRL + C.
     
     16. Kemudian untuk melihat hasilnya Kita harus masuk ke directory output terlebih dahulu gunakan perintah cd seperti berikut :
              scala> root@iZ8psi2f05o3u61bvpd:/opt/spark# cd output/
              
              Lalu gunakan perintah cat untuk melihat hasilnya :
              root@iZ8psi2f05o3u61bvpd:/opt/spark/output# cat part-00000
              
     17. Shut Down Apache Spark Untuk mematikan proses dari Apache dapat menggunakan perintah seperti berikut : 
              stop-slave.sh stop-master.sh
              exit ()





