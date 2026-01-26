# Industrial-Smart-Quality-Control-System

## 💡 Industrial & Real-world Projects

# 🏭 Industrial Smart Quality Control System

## 📌 Tổng quan dự án (Project Overview)
Hệ thống kiểm soát chất lượng thông minh (Smart QC) ứng dụng trí tuệ nhân tạo để tự động hóa quy trình kiểm tra ngoại quan trên **băng chuyền sản xuất thực tế**. Hệ thống được tối ưu hóa để chạy trực tiếp trên các thiết bị Edge Computing, giúp phát hiện tức thời các sai sót về nhãn mác và đóng gói.

---

## 🎯 Mục tiêu & Các lỗi mục tiêu (Target Defects)
Hệ thống thực hiện kiểm tra 100% sản phẩm đi qua băng chuyền, nhận diện chính xác các lỗi:

* **Ngược nhãn (Inverted Label):** Nhãn bị xoay ngược hướng so với thiết kế.
* **Sai kích thước (Wrong Label Size):** Nhãn không đúng quy cách kỹ thuật.
* **Vị trí nhãn sai (Wrong Position):** Nhãn dán lệch khỏi vùng chỉ định trên sản phẩm.
* **Lệch nhãn/tem (Skew/Alignment Error):** Nhãn bị dán chéo, không thẳng hàng hoặc bị nhăn.



---

## 🛠 Công nghệ & Phần cứng (Tech Stack & Hardware)

### 🤖 Deep Learning Models
Hệ thống kết hợp đa mô hình để đạt độ tin cậy cao nhất:
* **Object Detection:** `YOLOv11s` & `YOLOv8n` (Xác định nhanh vùng chứa nhãn).
* **Deep Feature Analysis:** `ResNet`, `CNN` & `Vision Transformer (ViT)` (Phân loại chi tiết lỗi và hướng nhãn).

### ⚡ Edge AI Platforms (Deployment)
Hệ thống được thiết kế linh hoạt để triển khai trên các dòng máy tính nhúng của NVIDIA:
* **NVIDIA Jetson Orin:** Dùng cho các dây chuyền tốc độ cực cao, chạy các model phức tạp như ViT với độ trễ thấp.
* **NVIDIA Jetson Nano:** Giải pháp tối ưu chi phí cho các tác vụ kiểm tra cơ bản sử dụng YOLOv8n.
* **Workstation:** `NVIDIA RTX 5060` dùng cho việc huấn luyện mô hình và xử lý trung tâm.

### 🔌 Industrial Integration
* **Camera:** Kết nối trực tiếp với `Keyence`, `Basler`, `Cognex` qua giao thức GigE hoặc USB 3.0.
* **Băng chuyền (Conveyor Belt):** Tích hợp cảm biến trigger và bộ điều khiển để thu thập dữ liệu và loại bỏ sản phẩm lỗi đồng bộ theo thời gian thực.

---

## 📊 Thu thập dữ liệu & Chỉ số hiệu năng (Data & Metrics)

### 📥 Thu thập dữ liệu thực tế (Real-world Data Collection)
* **Dữ liệu tại hiện trường:** Hình ảnh được thu thập trực tiếp từ băng chuyền sản xuất để mô phỏng chính xác điều kiện ánh sáng, bụi bẩn và tốc độ thực tế.
* **Data Augmentation:** Sử dụng kỹ thuật tăng cường dữ liệu để xử lý vấn đề mất cân bằng lớp (Class Imbalance) do sản phẩm lỗi thường chiếm tỉ lệ rất nhỏ trong thực tế.

### 📈 Chỉ số hiệu năng mục tiêu
Hệ thống ưu tiên chỉ số **Precision** để đảm bảo giảm thiểu tối đa việc chẩn đoán nhầm sản phẩm tốt thành lỗi (tránh lãng phí tài nguyên).

| Chỉ số | Giá trị mục tiêu | Ghi chú |
| :--- | :--- | :--- |
| **Precision (Độ chính xác xác nhận)** | **0.85 - 0.93** | Đảm bảo sản phẩm bị loại bỏ thực sự là hàng lỗi |
| **Tốc độ xử lý (Latency)** | **< 30-50ms** | Tối ưu hóa bằng TensorRT trên Jetson Orin/Nano |
| **Môi trường chạy** | **Băng chuyền thực tế** | Hoạt động ổn định 24/7 trong điều kiện công nghiệp |

---

## ⚠️ Thách thức kỹ thuật
* **Unstable Lighting:** Ánh sáng nhà xưởng thay đổi gây ảnh hưởng đến độ chuẩn xác của hình ảnh.
* **Edge Optimization:** Tối ưu hóa các model Deep Learning nặng (ViT, ResNet) để chạy mượt mà trên tài nguyên giới hạn của Jetson Nano.
* **Real-time Sync:** Đồng bộ hóa giữa camera, AI và tay gạt (Actuator) trên băng chuyền tốc độ cao.

## Demo: https://drive.google.com/drive/folders/1eB9T30dr32sdrMfVHRAxU4xskb_FIG_o?usp=drive_link
