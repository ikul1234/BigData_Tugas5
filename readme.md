## Bigdata 2020

# Tugas 4 Big DATA

- [Tugas 4 Big DATA](#tugas-4-big-data)
- [Tools](#tools)
- [Tugas](#tugas)
- [Running 2 Worker](#running-2-worker)
- [Hasil 2 Worker](#hasil-2-worker)
- [Running 5 Worker](#running-5-worker)
- [Hasil 5 Worker](#hasil-5-worker)
- [Kesimpulan](#kesimpulan)

# Tools
Tools yang diperlukan dalam tugas ini:
1. Docker Desktop
2. Apache Spark

# Tugas
Lakukan percobaan dengan mengganti parameter-parameter berikut:
* Jumlah worker: 2, 5
* Jumlah CPU: 2, 4
* Memory: 1G
* Partisi: 100, 1000 </br>

Untuk menambahkan worker, memodifikasi jumlah CPU dan memory, kalian bisa mengcopy file docker-compose.yml dan memodifikasi sesuai kebutuhan.</br>

Dokumentasikan percobaan kalian dengan baik dan buatlah kesimpulan dari hasil percobaan tersebut.

# Running 2 Worker
* Running Docker terlebih dahulu <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "docker")<br/>
* Masuk ke folder yang sudah ada file yml yang sudah diedit lalu jalankan ```docker-compose up -d``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "compose")<br/>
Berikut adalah isi yml file
```
version: "3"

networks:
  kafka-net:
    driver: bridge

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
volumes:
  hadoop_namenode:
  hadoop_datanode:
  hadoop_historyserver:
```
* Lalu buka ```http://localhost:8080/``` pada web browser untuk mengecek worker </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "2 workers")<br/>
* Lalu pada cmd jalankan ```docker ps``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "ps2worker")<br/>
* Lalu eksekusi container sesuai id ```docker exec -it <container_id> /bin/bash``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "exec")<br/>
* Cek hostname dengan command ```hostname -i``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "hostname")<br/>
* Jalankan syntax ```spark-submit --master spark://172.26.0.2:7077 examples/src/main/python/pi.py 100``` untuk 100 partisi (Untuk 1000 partisi ganti 100 menjadi 1000)</br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "sparksubmit")<br/>

# Hasil 2 Worker
Berikut adalah hasil 2 workers 100 partisi</br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "2worker100partisi")<br/>
Berikut adalah hasil 2 workers 1000 partisi</br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "2worker1000partisi")<br/>

# Running 5 Worker
* Running Docker terlebih dahulu <br/>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "docker")<br/>
* Masuk ke folder yang sudah ada file yml yang sudah diedit lalu jalankan ```docker-compose up -d``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "compose")<br/>
Berikut adalah isi yml file
```
version: "3"

networks:
  kafka-net:
    driver: bridge

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-3:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-4:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-5:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
volumes:
  hadoop_namenode:
  hadoop_datanode:
  hadoop_historyserver:
```
* Lalu buka ```http://localhost:8080/``` pada web browser untuk mengecek worker </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "5 workers")<br/>
* Lalu pada cmd jalankan ```docker ps``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "ps5worker")<br/>
* Lalu eksekusi container sesuai id ```docker exec -it <container_id> /bin/bash``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "exec")<br/>
* Cek hostname dengan command ```hostname -i``` </br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "hostname")<br/>
* Jalankan syntax ```spark-submit --master spark://172.26.0.2:7077 examples/src/main/python/pi.py 100``` untuk 100 partisi (Untuk 1000 partisi ganti 100 menjadi 1000)</br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "sparksubmit")<br/>

# Hasil 5 Worker
Berikut adalah hasil 5 workers 100 partisi</br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "5worker100partisi")<br/>
Berikut adalah hasil 5 workers 1000 partisi</br>
![alt text](https://github.com/farizmpr/Bigdata-2020/blob/master/tugas_4/picture/docker.jpg "5worker1000partisi")<br/>

# Kesimpulan
