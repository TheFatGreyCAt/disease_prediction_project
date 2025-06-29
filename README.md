# Diabetes Prediction Project

## Thông tin thành viên đóng góp
- Họ tên: Nguyễn Hoàng Tùng
- Lớp: E2K73
- Mã sinh viên: 735105112

## Mục tiêu dự án
Dự án xây dựng hệ thống dự đoán nguy cơ mắc bệnh tiểu đường dựa trên dữ liệu y tế, sử dụng các thuật toán học máy hiện đại. Hệ thống hỗ trợ sàng lọc, cảnh báo sớm nguy cơ mắc bệnh, giúp bác sĩ và bệnh nhân chủ động phòng ngừa.

## Cấu trúc thư mục
```
├── data/
│   ├── raw/                # Dữ liệu gốc (diabetes.csv)
│   └── processed/          # Dữ liệu đã tiền xử lý, chia train/test
├── models/                 # Mô hình đã huấn luyện (.pkl)
├── notebooks/diabetes/     # Notebook phân tích, huấn luyện, đánh giá, triển khai
├── outputs/
│   ├── charts/             # Hình ảnh trực quan hóa, confusion matrix
│   └── reports/            # Báo cáo mô hình
├── venv                    # Môi trường ảo
├── requirements.txt        # Thư viện cần thiết
├── report.txt              # Báo cáo chi tiết
└── README.md               # Tài liệu này
```

## Quy trình thực hiện
1. **Tiền xử lý dữ liệu** (`notebooks/diabetes/01_preprocessing.ipynb`):
   - Làm sạch, xử lý giá trị bất thường, chuẩn hóa, chia train/test.
2. **Huấn luyện mô hình** (`02_model_training.ipynb`):
   - Thử nghiệm Logistic Regression, KNN, Random Forest, SVM.
   - Đánh giá bằng accuracy, f1-score, confusion matrix.
3. **Tuning mô hình** (`03_model_tuning_and_deployment.ipynb`):
   - Tối ưu siêu tham số KNN bằng GridSearchCV, RandomizedSearchCV.
   - Lưu mô hình tốt nhất.
4. **Đánh giá & Triển khai** (`04_model_prediction_and_deployment.ipynb`):
   - Đánh giá mô hình trên tập test.
   - Đóng gói hàm dự đoán cho dữ liệu mới (`src/diabetes/predict.py`).

## Sử dụng nhanh
### 1. Cài đặt thư viện và môi trường
```bash
pip install -r requirements.txt
```
[Tải và giải nén file venv.rar](https://drive.google.com/file/d/18NybXm5Ir42g9GPIs3Ortq7GvLXdP-Fc/view?usp=sharing)

### 2. Chạy các notebook theo thứ tự:
- 01_preprocessing.ipynb
- 02_model_training.ipynb
- 03_model_tuning_and_deployment.ipynb
- 04_model_prediction_and_deployment.ipynb

### 3. Dự đoán với mô hình đã huấn luyện
```python
from src.diabetes.predict import predict_diabetes
import pandas as pd
# input_data: DataFrame hoặc numpy array
result = predict_diabetes(input_data)
```

## Kết quả chính
- **KNN** là mô hình tốt nhất (accuracy ~81.2%, f1-score ~0.78).
- Đã đóng gói mô hình tại `models/best_model.pkl`.
- Báo cáo chi tiết: `outputs/reports/model_report.md`

## Thông tin liên hệ
- Liên hệ: [Nguyễn Hoàng Tùng] - [nhtung2705@gmail.com]
---
