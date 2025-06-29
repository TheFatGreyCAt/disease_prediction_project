# BÁO CÁO MÔ HÌNH DỰ ĐOÁN BỆNH TIỂU ĐƯỜNG

## 1. Giới thiệu dự án
Dự án xây dựng hệ thống dự đoán nguy cơ mắc bệnh tiểu đường dựa trên dữ liệu y tế của bệnh nhân, sử dụng các thuật toán học máy hiện đại. Mục tiêu là hỗ trợ sàng lọc, cảnh báo sớm nguy cơ mắc bệnh, giúp bác sĩ và bệnh nhân chủ động phòng ngừa.

## 2. Mô tả dữ liệu
- **Nguồn dữ liệu:** `data/raw/diabetes.csv`.
- **Đặc trưng:** 8 thuộc tính lâm sàng:
    - Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI, DiabetesPedigreeFunction, Age.
    - Nhãn Outcome (0: không bệnh, 1: có bệnh).
- **Tiền xử lý:**
    - Loại bỏ giá trị bất thường (0 ở các cột không hợp lý) bằng cách thay thế bằng trung vị.
    - Kiểm tra và xử lý missing values.
    - Chuẩn hóa dữ liệu bằng StandardScaler.
    - Chia train/test theo tỉ lệ 80/20, đảm bảo phân phối nhãn cân bằng.
    - Lưu dữ liệu đã xử lý tại `data/processed/`.

## 3. Khám phá và trực quan hóa dữ liệu
- Phân tích phân phối các đặc trưng, kiểm tra outlier, missing value.
- Trực quan hóa:
    - Histogram, boxplot cho các đặc trưng (`outputs/charts/nb1_histogram_all_features.png`, `nb1_boxplot_all_features.png`).
    - Ma trận tương quan (`outputs/charts/nb1_correlation_matrix.png`).
    - Phân phối nhãn Outcome (`outputs/charts/nb1_countplot_outcome.png`).

## 4. Quy trình xây dựng mô hình

### 4.1. Huấn luyện và đánh giá mô hình
- **Các mô hình thử nghiệm:**
    - Logistic Regression
    - K-Nearest Neighbors (KNN)
    - Random Forest
    - Support Vector Machine (SVM)
- **Đánh giá bằng các chỉ số:**
    - Accuracy, Precision, Recall, F1-score, Confusion Matrix.
- **Kết quả tổng quan:**

| Mô hình              | Accuracy | F1-score | Nhận xét chính |
|----------------------|----------|----------|----------------|
| Logistic Regression  | ~80.5%   | ~0.80    | Ổn định, recall lớp 1 thấp |
| KNN                  | ~81.2%   | ~0.78    | Cân bằng tốt nhất, được chọn |
| Random Forest        | ~78.3%   | ~0.72    | Chưa đủ mạnh, recall thấp |
| SVM                  | ~79.2%   | ~0.76    | Chưa cân bằng, recall lớp 1 thấp |

- **Biểu đồ confusion matrix:** `outputs/charts/nb2_confusion_matrix_*.png`

#### Đánh giá chi tiết từng mô hình:
- **Logistic Regression:**
    - Accuracy ~80.5%, F1-score ~0.80
    - Recall lớp 1 thấp, dễ bỏ sót bệnh nhân.
    - Precision lớp 0 cao, mô hình thiên về nhận diện người không bị bệnh.
- **KNN:**
    - Accuracy ~81.2%, F1-score ~0.78
    - Cân bằng tốt nhất giữa hai lớp, tuy recall lớp 1 vẫn chưa cao.
    - Được chọn làm mô hình cuối cùng.
- **Random Forest:**
    - Accuracy ~78.3%, F1-score ~0.72
    - Hiệu suất thấp hơn, recall lớp 1 kém.
- **SVM:**
    - Accuracy ~79.2%, F1-score ~0.76
    - Chưa cân bằng, recall lớp 1 thấp.

### 4.2. Tuning và lựa chọn mô hình
- **Tuning KNN:** Sử dụng GridSearchCV và RandomizedSearchCV để tối ưu các siêu tham số (n_neighbors, weights, metric).
- **Kết quả:** KNN mặc định cho kết quả tốt hơn bản tuning.
- **Lưu mô hình tốt nhất:** `models/best_model.pkl` (KNN với n_neighbors=19).

## 5. Triển khai và dự đoán thực tế

- **Đánh giá mô hình trên tập test:** Được thực hiện trong notebook `04_model_prediction_and_deployment.ipynb`.
- **Hàm dự đoán cho dữ liệu mới:** Đã đóng gói thành module `src/diabetes/predict.py` với hàm `predict_diabetes`.
- **Quy trình sử dụng lại mô hình:**
    - Tải mô hình đã huấn luyện bằng `joblib`.
    - Dự đoán trên dữ liệu mới (có thể là DataFrame hoặc array).
    - Có thể tích hợp vào ứng dụng thực tế hoặc API.

## 6. Kết luận & Đề xuất
- **KNN** là mô hình phù hợp nhất cho bài toán này, cho kết quả cân bằng giữa các chỉ số đánh giá.
- Tuy nhiên, recall lớp 1 còn thấp, cần cân nhắc các kỹ thuật cân bằng dữ liệu (SMOTE, oversampling) hoặc thử nghiệm các mô hình phức tạp hơn (ensemble, boosting).
- Đề xuất kiểm thử thêm trên dữ liệu thực tế, triển khai API dự đoán, và tiếp tục cải tiến mô hình.

## 7. Tài liệu tham khảo & Phụ lục
- **Mã nguồn:** `notebooks/diabetes/`, `src/diabetes/`
- **Hình ảnh, biểu đồ:** `outputs/charts/`
- **Mô hình:** `models/best_model.pkl`
- **Tham khảo:**
    - https://www.kaggle.com/code/melikedilekci/diabetes-dataset-for-beginners
    - https://www.kaggle.com/code/chanchal24/diabetes-dataset-eda-prediction-with-7-models
    - https://www.kaggle.com/code/tumpanjawat/diabetes-eda-random-forest-hp
    - https://machinelearningcoban.com/
    - ChatGPT

---