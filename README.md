## 💡 Industrial & Real-world Projects

# 🏭 Industrial Smart Quality Control System

## 📌 Tổng quan dự án (Project Overview)
Hệ thống kiểm soát chất lượng thông minh (Smart QC) ứng dụng trí tuệ nhân tạo để tự động hóa quy trình kiểm tra ngoại quan trên **băng chuyền sản xuất thực tế**. Hệ thống được thiết kế để hoạt động 24/7, thu thập dữ liệu thực tế và đưa ra quyết định loại bỏ sản phẩm lỗi ngay trên các thiết bị Edge Computing.

---

# 🏭 Industrial Smart Quality Control System

## 📌 Tổng quan dự án (Project Overview)
Hệ thống kiểm soát chất lượng thông minh (Smart QC) ứng dụng trí tuệ nhân tạo để tự động hóa quy trình kiểm tra ngoại quan trên **băng chuyền sản xuất thực tế**. Hệ thống được thiết kế để hoạt động 24/7, thu thập dữ liệu thực tế và đưa ra quyết định loại bỏ sản phẩm lỗi ngay trên các thiết bị Edge Computing.

---

## 🎯 Mục tiêu & Các lỗi mục tiêu (Target Defects)
Hệ thống thực hiện kiểm soát 100% sản phẩm, tập trung vào các lỗi nhãn mác và khuyết tật bao bì phổ biến:

* **Ngược nhãn (Inverted Label):** Nhãn bị xoay sai hướng (180°) do lỗi cấp phôi.
* **Sai kích thước (Wrong Label Size):** Nhầm lẫn giữa các loại nhãn của các mã hàng (SKU) khác nhau.
* **Vị trí nhãn sai (Wrong Position):** Nhãn dán không đúng tọa độ quy định.
* **Lệch nhãn/tem (Skew/Alignment Error):** Nhãn bị dán nghiêng, lệch trục hoặc nhăn bề mặt.
* **Sai ren cổ chai (Bottle Neck Thread Defect):** Phát hiện các lỗi biến dạng ren, ren bị mẻ, thiếu ren hoặc sai bước ren, đảm bảo nắp chai có thể đóng kín tuyệt đối.



---

## ⚙️ Tối ưu hóa & Triển khai (Optimization & Deployment)

Để đáp ứng yêu cầu xử lý thời gian thực trên băng chuyền tốc độ cao với tài nguyên giới hạn, hệ thống áp dụng các kỹ thuật nén và tăng tốc mô hình:

### 🚀 Model Optimization Pipeline
* **ONNX Conversion:** Chuyển đổi các mô hình từ framework gốc (PyTorch/TensorFlow) sang định dạng trung gian **ONNX** để tối ưu hóa đồ thị tính toán.
* **TensorRT Acceleration:** Sử dụng thư viện **NVIDIA TensorRT** để tối ưu hóa mô hình cho nhân Tensor trên GPU.
* **Engine File Generation:** Biên dịch mô hình thành file **.engine** (Serialization) giúp giảm tối đa kích thước và tăng tốc độ suy luận (Inference) lên gấp 3-5 lần.
* **Quantization:** Áp dụng kỹ thuật FP16 hoặc INT8 quantization để giảm dung lượng mô hình mà vẫn giữ được độ chính xác cần thiết cho thiết bị nhúng.

### ⚡ Edge AI Platforms
* **NVIDIA Jetson Orin:** Chạy các mô hình Ensemble (YOLO + ViT) cho dây chuyền phức tạp.
* **NVIDIA Jetson Nano:** Triển khai các bản mô hình đã rút gọn (Engine file) cho các tác vụ phân loại cơ bản.
* **Workstation:** `NVIDIA RTX 5060` dùng để huấn luyện và quản lý dữ liệu tập trung.

---

## 🛠 Tech Stack & Kiến trúc mô hình
* **Core Models:** `YOLOv11s`, `YOLOv8n`, `ResNet`, `CNN`, `Vision Transformer (ViT)`.
* **Image Processing:** `OpenCV` (Thu thập và tiền xử lý ảnh từ Camera Keyence, Basler, Cognex).
* **Storage:** `PostgreSQL` lưu trữ Log lỗi và Metadata.
* **Inference Engine:** `ONNX Runtime` & `TensorRT`.

---

## 📊 Dữ liệu & Chỉ số hiệu năng (Data & Metrics)

### 📥 Thu thập dữ liệu thực tế (Real-world Data Collection)
* **Dữ liệu hiện trường:** Trực tiếp thu thập từ camera công nghiệp trên băng chuyền để lấy mẫu các điều kiện thực tế (ánh sáng thay đổi, rung động cơ học, độ mờ của chai nựa).
* **Augmentation:** Xử lý vấn đề Class Imbalance (lỗi ren và nhãn thường hiếm hơn sản phẩm đạt) bằng cách mô phỏng các lỗi thực tế.

### 📈 Chỉ số hiệu năng mục tiêu
Hệ thống ưu tiên chỉ số **Precision** (Độ chính xác xác nhận) để tránh việc dừng máy hoặc loại bỏ nhầm sản phẩm đạt chuẩn.

| Chỉ số | Giá trị mục tiêu | Ghi chú |
| :--- | :--- | :--- |
| **Precision** | **0.85 - 0.93** | Đảm bảo tính tin cậy của quyết định loại bỏ |
| **Tốc độ xử lý** | **< 30ms / sản phẩm** | Đã tối ưu qua TensorRT Engine |
| **Môi trường** | **Băng chuyền thực tế** | Hoạt động ổn định 24/7 dưới rung động công nghiệp |

---

## ⚠️ Thách thức kỹ thuật
* **Hardware Constraints:** Tối ưu hóa mô hình nặng (ViT/ResNet) để chạy mượt mà trên tài nguyên giới hạn của Jetson Nano.
* **Small Defect Detection:** Lỗi ren cổ chai thường rất nhỏ, đòi hỏi độ phân giải camera cao và mô hình AI nhạy cảm với các chi tiết tinh vi.
* **Real-time Sync:** Đồng bộ hóa tín hiệu từ AI đến hệ thống cơ khí loại bỏ sản phẩm trên băng chuyền.


---

## ⚙️ Tối ưu hóa & Triển khai (Optimization & Deployment)

Để đáp ứng yêu cầu xử lý thời gian thực trên băng chuyền tốc độ cao với tài nguyên giới hạn, hệ thống áp dụng các kỹ thuật nén và tăng tốc mô hình:

### 🚀 Model Optimization Pipeline
* **ONNX Conversion:** Chuyển đổi các mô hình từ framework gốc (PyTorch/TensorFlow) sang định dạng trung gian **ONNX** để tối ưu hóa đồ thị tính toán.
* **TensorRT Acceleration:** Sử dụng thư viện **NVIDIA TensorRT** để tối ưu hóa mô hình cho nhân Tensor trên GPU.
* **Engine File Generation:** Biên dịch mô hình thành file **.engine** (Serialization) giúp giảm tối đa kích thước và tăng tốc độ suy luận (Inference) lên gấp 3-5 lần so với thông thường.
* **Quantization:** Áp dụng kỹ thuật FP16 hoặc INT8 quantization để giảm dung lượng mô hình mà vẫn giữ được độ chính xác cần thiết.

### ⚡ Edge AI Platforms
* **NVIDIA Jetson Orin:** Chạy các mô hình Ensemble (YOLO + ViT) cho dây chuyền phức tạp.
* **NVIDIA Jetson Nano:** Triển khai các bản mô hình đã rút gọn (Engine file) cho các tác vụ phân loại cơ bản.
* **Workstation:** `NVIDIA RTX 5060` dùng để huấn luyện và quản lý dữ liệu tập trung.

---

## 🛠 Tech Stack & Kiến trúc mô hình
* **Core Models:** `YOLOv11s`, `YOLOv8n`, `ResNet`, `CNN`, `Vision Transformer (ViT)`.
* **Image Processing:** `OpenCV` (Thu thập và tiền xử lý ảnh từ Camera Keyence, Basler, Cognex).
* **Storage:** `PostgreSQL` lưu trữ Log lỗi và Metadata.
* **Inference:** `ONNX Runtime` & `TensorRT`.

---

## 📊 Dữ liệu & Chỉ số hiệu năng (Data & Metrics)

### 📥 Thu thập dữ liệu thực tế (Real-world Data Collection)
* **Dữ liệu hiện trường:** Trực tiếp thu thập từ camera công nghiệp trên băng chuyền để lấy mẫu các điều kiện thực tế (ánh sáng thay đổi, rung động cơ học).
* **Augmentation:** Xử lý vấn đề Class Imbalance bằng cách mô phỏng các lỗi hiếm gặp từ dữ liệu thực tế thu được.

### 📈 Chỉ số hiệu năng mục tiêu
Hệ thống ưu tiên chỉ số **Precision** (Độ chính xác xác nhận) để tránh việc dừng máy hoặc loại bỏ nhầm sản phẩm đạt chuẩn.

| Chỉ số | Giá trị mục tiêu | Ghi chú |
| :--- | :--- | :--- |
| **Precision** | **0.85 - 0.93** | Đảm bảo tính tin cậy của quyết định loại bỏ |
| **Tốc độ xử lý** | **< 30ms / sản phẩm** | Đã tối ưu qua TensorRT Engine |
| **Môi trường** | **Băng chuyền thực tế** | Chịu được các tác động môi trường nhà xưởng |

---

### Demo: [https://drive.google.com/drive/folders/1eB9T30dr32sdrMfVHRAxU4xskb_FIG_o?usp=drive_link](https://drive.google.com/drive/folders/1SxIDtwbnsQlO3FvqJkyTdKspGBzYx1n4?usp=drive_link)
