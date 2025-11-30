# Bank Customer Churn Prediction

## Mô tả ngắn gọn
Dự án này dự đoán khả năng khách hàng rời bỏ ngân hàng (churn) dựa trên dữ liệu giao dịch và thông tin cá nhân, sử dụng NumPy và các thuật toán học máy cơ bản.

## Mục lục
1. [Giới thiệu](#giới-thiệu)
2. [Dataset](#dataset)
3. [Method](#method)
4. [Installation & Setup](#installation--setup)
5. [Usage](#usage)
6. [Results](#results)
7. [Project Structure](#project-structure)
8. [Challenges & Solutions](#challenges--solutions)
9. [Future Improvements](#future-improvements)
10. [Contributors](#contributors)
11. [Thông tin tác giả](#thông-tin-tác-giả)
12. [Contact](#contact)
13. [License](#license)

## Giới thiệu
- **Mô tả bài toán:** Dự đoán khách hàng có rời bỏ ngân hàng hay không dựa trên dữ liệu lịch sử giao dịch và thông tin cá nhân.
- **Động lực & ứng dụng thực tế:** Giúp ngân hàng nhận diện sớm khách hàng có nguy cơ rời bỏ để có chiến lược giữ chân phù hợp, giảm thiểu tổn thất doanh thu.
- **Mục tiêu cụ thể:** Xây dựng pipeline xử lý dữ liệu, huấn luyện mô hình dự đoán churn, đánh giá hiệu quả và trực quan hóa kết quả.

## Dataset
- **Nguồn dữ liệu:** [BankChurners](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers) từ Kaggle.
- **Mô tả các features:**
  - `Customer_Age`, `Gender, Dependent_count`, `Education_Level`, `Marital_Status`, `Income_Category`, `Card_Category`, `Months_on_book`, `Total_Relationship_Count`, `Months_Inactive_12_mon`, `Contacts_Count_12_mon`, `Credit_Limit`, `Total_Revolving_Bal`, `Avg_Open_To_Buy`, `Total_Amt_Chng_Q4_Q1`, `Total_Trans_Amt`, `Total_Trans_Ct`, `Total_Ct_Chng_Q4_Q1`, `Avg_Utilization_Ratio`, `Attrition_Flag` (label).
- **Kích thước & đặc điểm:**
  - ~10,000 dòng, 23 cột. Dữ liệu đa dạng, có cả số và phân loại, có missing values.

## Method
- **Quy trình xử lý dữ liệu:**
  1. Khám phá dữ liệu (notebooks/01_data_exploration.ipynb)
  2. Tiền xử lý: loại bỏ missing values, mã hóa biến phân loại, chuẩn hóa dữ liệu (notebooks/02_preprocessing.ipynb)
  3. Lưu dữ liệu đã xử lý vào `data/processed/preprocessed_data.npz`
- **Thuật toán sử dụng:**
  - Logistic Regression (Numpy), Logistic Regression (Sklearn), KNN (Numpy)
- **Giải thích implement bằng NumPy:**
  - Các bước tiền xử lý, huấn luyện và dự đoán đều sử dụng NumPy để thao tác ma trận, vector hóa tính toán trọng số, hàm sigmoid, v.v.

## Installation & Setup
```bash
# Clone repo
$ git clone <repo_url>
$ cd BankChurn
# Cài đặt môi trường Python
$ python3 -m venv venv
$ source venv/bin/activate
# Cài đặt các package cần thiết
$ pip install -r requirements.txt
# Mở Jupyter Notebook
$ jupyter notebook
```

## Usage
- **Khám phá dữ liệu:**
  - Mở `notebooks/01_data_exploration.ipynb` để xem phân tích ban đầu.
- **Tiền xử lý:**
  - Chạy `notebooks/02_preprocessing.ipynb` để xử lý và lưu dữ liệu.
- **Huấn luyện & đánh giá mô hình:**
  - Chạy `notebooks/03_modeling.ipynb` để huấn luyện, đánh giá và trực quan hóa kết quả.
## Results
- **Kết quả đạt được:**
  - Độ chính xác (accuracy) trên tập test: ~0.89
  - Precision (churn): ~0.73
  - Recall (churn): ~0.51
  - F1-score: ~0.60
  - Confusion matrix (test):
    - True Negative (TN): 1636
    - False Positive (FP): 62
    - True Positive (TP): 166
    - False Negative (FN): 161
  - AUC (ROC Curve): ~0.90
- **Hình ảnh trực quan hóa:**
  - Biểu đồ phân phối churn, ROC curve, confusion matrix (xem chi tiết trong notebook `03_modeling.ipynb`).
- **So sánh & phân tích:**
  - Logistic Regression và KNN đều bị ảnh hưởng bởi mất cân bằng dữ liệu, precision cao nhưng recall thấp cho lớp churn.
  - Logistic Regression (numpy) và Sklearn cho kết quả tương đương, AUC cao nhưng recall còn hạn chế.
  - KNN không cải thiện nhiều do dữ liệu không có cụm rõ rệt cho lớp churn.
  - Nguyên nhân chủ yếu: tỷ lệ churn thấp (~16%), mô hình tuyến tính khó bắt quan hệ phức tạp.

## Project Structure
```
lab02/
├── data/
│   ├── raw/                           # Dữ liệu gốc (BankChurners.csv)
│   └── processed/                     # Dữ liệu đã xử lý (preprocessed_data.npz)
├── notebooks/                         # Jupyter Notebooks: khám phá, tiền xử lý, modeling
│   ├── 01_data_exploration.ipynb      # Phân tích, khám phá dữ liệu
│   ├── 02_preprocessing.ipynb         # Tiền xử lý dữ liệu
│   ├── 03_modeling.ipynb              # Huấn luyện, đánh giá mô hình
├── README.md                          # Tài liệu dự án
```

## Challenges & Solutions
- **Khó khăn:**
  - Trong bộ dữ liệu Bank Churn, tỷ lệ khách hàng rời đi chỉ chiếm khoảng 16%, trong khi 84% còn lại là khách hàng không rời đi. Điều này tạo ra sự mất cân bằng nghiêm trọng giữa hai lớp.
- **Giải pháp:**
  - Sử dụng thêm các chỉ số như Precision, Recall, F1-score để đánh giá mô hình thay vì chỉ dựa vào accuracy.
  - Trực quan hóa kết quả bằng confusion matrix và ROC–AUC để hiểu rõ mô hình đang bỏ sót bao nhiêu trường hợp rời đi.
  - Thử nghiệm hai mô hình khác nhau (Logistic Regression và KNN) để so sánh hiệu quả khi dữ liệu bị lệch lớp.

## Future Improvements
- Cân bằng lại dữ liệu bằng oversampling, undersampling hoặc điều chỉnh ngưỡng dự đoán để tăng khả năng phát hiện khách hàng rời đi.
- Thử nghiệm thêm các mô hình như Naive Bayes, SVM, Decision Tree hoặc các phương pháp ensemble để đánh giá hiệu suất đa chiều.
- Tối ưu hóa Logistic Regression bằng cách điều chỉnh learning rate, số epoch hoặc sử dụng mini-batch gradient descent.
- Sử dụng one-hot encoding cho các biến phân loại và thực hiện phân tích dữ liệu nâng cao để khai thác tốt hơn các đặc trưng.
- Đóng gói mô hình thành API, xây dựng dashboard trực quan hóa kết quả và tài liệu hóa pipeline để dễ dàng triển khai thực tế và mở rộng về sau.

## Contributors
- Huỳnh Yến Nhi

## Thông tin tác giả
- Họ tên: Huỳnh Yến Nhi
- MSSV: 23120151
- Trường: Đại học Khoa học Tự nhiên, ĐHQG HCM

## Contact
- Email: huynhyennhi2607@gmail.com
- Github: https://github.com/ynnhi2607

## License
MIT License