<a id="top"></a>

<!-- Banner -->
<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: none;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>

<h1 align="center"><b>NHẬN DẠNG<br>(PATTERN RECOGNITION)</b></h>

[![Status](https://img.shields.io/badge/status-done-blue?style=flat-square)](https://github.com/DoThiThuTrang/CS338.N21.KHCL)
[![GitHub contributors](https://img.shields.io/github/contributors/DoThiThuTrang/CS338.N21.KHCL?style=flat-square)](https://github.com/DoThiThuTrang/CS338.N21.KHCL/graphs/contributors)
[![Status](https://img.shields.io/badge/language-python-blue?style=flat-square)](https://github.com/DoThiThuTrang/CS338.N21.KHCL)

## [BẢNG MỤC LỤC](#top)
* [Giới thiệu môn học](#giới-thiệu-môn-học)
* [Thông tin các thành viên](#thông-tin-về-các-thành-viên-nhóm)
* [Thông tin đồ án](#thông-tin-đồ-án)
* [Các bước cần thiết](#các-bước-cần-thiết)
* [Deployment](#deployment)

## [GIỚI THIỆU MÔN HỌC](#top)
* **Tên môn học:** Nhận dạng - Pattern Recognition
* **Mã môn học:** CS338
* **Mã lớp:** CS338.N21.KHCL
* **Năm học:** HK2 (2022 - 2023)
* **Giảng viên:** ThS. Đỗ Văn Tiến

## [THÔNG TIN VỀ CÁC THÀNH VIÊN NHÓM](#top)

| STT    | MSSV          | Họ và Tên                |Vai trò    | Github                                          | Email                   |
| :----: |:-------------:| :-----------------------:|:---------:|:-----------------------------------------------:|:-------------------------:
| 1      | 20520278      | Phạm Hoàng Phúc          | Thành viên | [pahopu](https://github.com/pahopu)            | 20520278@gm.uit.edu.vn   |
| 2      | 20520816      | Đỗ Thị Thu Trang         | Trưởng nhóm| [DoThiThuTrang](https://github.com/DoThiThuTrang)| 20520816@gm.uit.edu.vn   |
| 3      | 20521663      | Nguyễn Đặng Bảo Ngọc     | Thành viên | [ngocndb03](https://github.com/ngocndb03)      | 20521663@gm.uit.edu.vn   |

## [THÔNG TIN ĐỒ ÁN](#top)
* **Đề tài đồ án:** Nhận dạng sản phẩm tạp hóa trong siêu thị - Supermarket Product Detection
* **Ngôn ngữ lập trình:** Python

## [CÁC BƯỚC CẦN THIẾT](#top)
Chúng tôi đã thực hiện qua 4 giai đoạn để giải quyết bài toán trên. Các giai đoạn đó sẽ lần lượt về data, train, validation và predict.

![image](https://github.com/DoThiThuTrang/CS338.N21.KHCL/assets/79435891/4daef96e-8769-48e9-af35-4d5c3cce541a)

### 1. Dữ liệu
#### a. Thông tin bộ dữ liệu
* **Bộ dữ liệu lựa chọn:** Freiburg Groceries Dataset (2014)
* **Nguồn dataset:** http://aisdatasets.informatik.uni-freiburg.de/freiburg_groceries_dataset/
* **Số lượng:** 4800 bức ảnh của các đối tượng là hàng hóa được bày bán trong siêu thị. Những bức ảnh này được chụp ở nhiều góc độ khác nhau của từng hàng hóa, do đó, sẽ có sự khác nhau cả về độ sáng, kích thước cũng như góc độ của hàng hóa đó.   
* **Số nhóm phân loại:** 25 nhóm sản phẩm phổ biến khác nhau.
  
![image](Images/dataset.png)

#### b. Xử lý dữ liệu
Dữ liệu ban đầu không groundtruth đi kèm, do đó chúng tôi đã tiến hành đóng khung (bounding box) và gắn nhãn cho dữ liệu.
* **Đóng khung (bounding box):**
Makesense là công cụ chúng tôi dùng để đóng khung dữ liệu của mình. **Makesene** cho phép người dùng được tạo khung theo đúng kích thước của vật phẩm trong hình, đi kèm là gắn nhãn dữ liệu. Thông tin được xuất ra sẽ theo định dạng của YOLO.
* **Gắn nhãn cho dữ liệu:** Các hình ảnh đã được đóng khung của mỗi sản phẩm sẽ được tổ chức thành các folder riêng biệt, chúng tôi sử dụng python để gắn nhãn cho các bounding bõ này.
  
### 2. Train
Chúng tôi đã tham khảo các nguồn của YOLOv5 như **ultralytics** như một nền tảng để có thể phát triển mô hình của mình phù hợp với bộ dữ liệu mà chúng tôi đã chọn. Chúng tôi sẽ tập trung vào 4 thông số chính: 
| STT    | Thông số         | Giá trị          |Giải thích                                                                                                          |
| :----: |:----------------:| :---------------:|:------------------------------------------------------------------------------------------------------------------:|
| 1      | weight           | YOLOv5s.pt       | Mô hình YOLO5s có 63 lớp tích chập, và kích thước trọng số (weights size) là 14.9 MB.                              |
| 2      | epochs           | 200              | Cho phép mô hình học được nhiều thông tin hơn và không gây tình trạng overfitting, phù hợp với cấu hình hệ thống.  |
| 3      | batch-size       | 64               | Tăng tốc độ tính toán, cũng như cung cấp đủ mẫu để mô hình có thể tính toán và cập nhật tham số.                   |
| 4      | imgsize          | 416              | Phù hợp với backbone của cấu hình YOLOv5s, kích thước phù hợp với bộ dữ liệu của nhóm để không bị co, mờ quá nhiều.|

### 3. Validation
![image](https://github.com/DoThiThuTrang/CS338.N21.KHCL/assets/79435891/41e8a114-5296-4b56-b3a1-f6f1da8a5bb5)

  Kết quả cho thấy các hàm loss cho chiều hướng đi xuống, điều này cho thấy mô hình học rất tốt trên bộ dữ liệu chúng tôi cung cấp. Bên cạnh đó kết quả recall và precission cũng khá cao khi đạt đến 0.996 cho recall và 0.992 cho precision. 
  
  Với các giá trị mAP chúng tôi tính toán với thresold = 0.5, ngưỡng này giúp mô hình quyết định xem một đối tượng có được coi là phát hiện hay không. Khi xác suất dự đoán vượt quá ngưỡng 0.5, đối tượng được coi là được phát hiện, và ngược lại, nếu xác suất 
dự đoán thấp hơn 0.5, đối tượng không được coi là phát hiện. Do đó, với xu hướng đi lên của biểu đồ, đồng nghĩa với việc mô hình có khả năng tìm thấy và phân loại đúng nhiều đối tượng.

  Bên cạnh đó, chúng tôi còn sử dụng độ đo mAP_0.5:0.95, biểu đồ cũng cho thấy kết quả của độ đo này có xu hướng đi lên. Do đó, mô hình của chúng tôi đã có khả năng nhận diện đối tượng với độ chính xác cao trên một phạm vi ngưỡng rộng, bao gồm các đối tượng với xác suất dự đoán gần 0.5 và các đối tượng có xác suất dự đoán gần 0.95. 

### 4. Predict
![image](https://github.com/DoThiThuTrang/CS338.N21.KHCL/assets/79435891/b0ffbf4a-5047-4576-bd25-6340846f6580)


## [DEPLOYMENT](#top)

### 1. Giới thiệu
* **Công cụ hỗ trợ:** Streamlit
* **Link demo:** [link](https://drive.google.com/file/d/1A8Z_NneHT906PZraNkhBzUzwNszRX0fH/view)

### 2. Các bước cần thiết

#### a. Clone project
Clone project repository bằng câu lệnh dưới đây.

```bash
git clone https://github.com/DoThiThuTrang/CS338.N21.KHCL.git
```

#### b. Cài đặt thư viện
Bạn cần tiến hành cài đặt các thư viện cần thiết cho project với câu lệnh dưới đây.

```bash
cd Deployment
pip install -r requirements.txt
```

#### c. Chạy code
Sau khi cài đặt thư viện, dùng câu lệnh dưới đây để chạy code.
```bash
streamlit run app.py
```
