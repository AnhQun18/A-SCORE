# Credit Scorecard (A-Score) Development - Home Credit Default Risk

## 1. Overview
Dự án tập trung xây dựng mô hình thẻ điểm tín dụng (Application Scorecard) nhằm giải quyết bài toán "Bất đối xứng thông tin" cho nhóm khách hàng dưới chuẩn (The Unbanked) tại Home Credit. Mô hình giúp tự động hóa quyết định phê duyệt tín dụng, tối ưu hóa lợi nhuận và quản trị rủi ro theo tiêu chuẩn Basel II.

## 2. Methodology & Pipeline
Mô hình sử dụng thuật toán **Logistic Regression** với quy trình xử lý dữ liệu chặt chẽ (**Leakage-Free**):
*   **Data Sources:** Tích hợp 3 nhóm dữ liệu: Đơn vay hiện tại (Application), Lịch sử CIC (Bureau), và Lịch sử nội bộ (Previous Application).
*   **Feature Engineering:** Thực hiện tổng hợp dữ liệu (aggregation), xử lý outlier bằng IQR Capping, và chuẩn hóa bằng **WOE Encoding**.
*   **Feature Selection:** Quy trình 3 tầng lọc nghiêm ngặt:
    1. Lọc theo Information Value (IV > 0.03).
    2. Loại bỏ đa cộng tuyến (Correlation < 0.6).
    3. Kiểm định thống kê (Chi-square p < 0.05).
*   **Result:** Lựa chọn được 21 biến đặc trưng có sức dự báo cao nhất.

## 3. Key Metrics & Results
Mô hình đạt kết quả kiểm chứng (Validation Set) ổn định và đạt chuẩn vận hành:
*   **AUROC:** 0.7495
*   **Gini Coefficient:** 0.4990
*   **KS Statistic:** 0.3755
*   **PSI (Population Stability Index):** 0.0011 (Cực kỳ ổn định, không data leakage).

## 4. Business Impact
*   **Minh bạch:** Chuyển đổi hệ số Logistic sang thang điểm 300-850 (tương tự FICO), giúp giải thích lý do từ chối/phê duyệt cho khách hàng.
*   **Tối ưu vận hành:** Thiết lập hệ thống điểm cắt (Cut-off) tự động:
    *   **>= 650:** Chấp thuận tự động (< 3% bad rate).
    *   **580 – 649:** Thẩm định thủ công.
    *   **< 580:** Từ chối tự động.

## 5. Technologies & Tools
*   **Language:** Python (Pandas, NumPy, Scikit-learn).
*   **Methodology:** Logistic Regression, Weight of Evidence (WOE) Encoding.
*   **Environment:** Colab (tối ưu hóa memory xử lý dữ liệu lớn).

---
*Dự án được thực hiện trong khuôn khổ học phần Quản trị Rủi ro Định lượng 2 tại Trường Đại học Kinh tế Quốc dân (NEU).*
