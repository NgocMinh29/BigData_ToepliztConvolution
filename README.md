
# Chạy mã ECG phân tán với PySpark trên Ubuntu (VirtualBox)

## Mục tiêu
Chạy pipeline xử lý tín hiệu ECG, với phần pooling thực hiện phân tán bằng Spark, trên môi trường **Ubuntu ảo hóa (VirtualBox)** với Jupyter Notebook.

---

## Yêu cầu hệ thống

- Hệ điều hành host: Windows / macOS
- VirtualBox + Ubuntu 20.04/22.04 (trên máy ảo)
- RAM máy ảo: ít nhất **4GB**
- Python 3.8+, pip

---

## Bước 1: Cài Ubuntu trên VirtualBox

1. Tải ISO từ [ubuntu.com](https://ubuntu.com/download)
2. Tạo VM mới trên VirtualBox:
   - Loại: Linux
   - Phiên bản: Ubuntu (64-bit)
   - RAM: 4096MB
   - Ổ cứng: 30GB trở lên
3. Gắn file ISO, cài Ubuntu

---

## Bước 2: Cài Spark & môi trường

### 2.1. Cài Java JDK
```bash
sudo apt update
sudo apt install default-jdk -y
```

### 2.2. Tải và giải nén Spark
```bash
cd ~/Desktop
wget https://archive.apache.org/dist/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz
tar -xvzf spark-3.5.1-bin-hadoop3.tgz
mv spark-3.5.1-bin-hadoop3 spark
```


### 2.3. Cài thư viện Python cần thiết
```bash
sudo apt install python3-pip -y
pip3 install pyspark jupyter numpy pandas matplotlib scikit-learn pywt
```

---

## Bước 3: Khởi động Spark hoặc Jupyter

### Tùy chọn 1: Khởi động shell PySpark
```bash
cd ~/spark-3.5.1-bin-hadoop3
./bin/pyspark 
```

### Tùy chọn 2: Khởi động Jupyter Notebook
```bash
jupyter notebook
```

---

## Bước 4: Chạy notebook ECG

1. Tạo notebook mới trong Jupyter
2. Dán toàn bộ mã Python xử lý ECG vào
3. Chạy lần lượt từng cell

---

## Gợi ý khởi tạo Spark trong mã

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("DistributedECG") \
    .master("local[*]") \
    .config("spark.driver.memory", "4g") \
    .getOrCreate()
```


---


