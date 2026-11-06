# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

- **MSSV: 2A202603623**
- **Họ và tên: VoSyThaiSon**
- **SEED** (in ở ô đầu notebook):

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | Có |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | Có |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | Có |

## 2. Kết quả chính

<img width="1201" height="572" alt="image" src="https://github.com/user-attachments/assets/eb158af2-c750-4794-8110-ea70944ab905" />

## 3. Dự đoán và thực tế

Dự đoán LLM lớn tốt hơn model nhỏ: thực tế gpt-6-luna (model nhỏ) có kết quả là 20b F1 0.952 > 120b F1 0.930. Lệch vì model lớn không luôn tốt hơn trên bài phân loại đơn giản, và 40 tin quá ít để kết luận.

Dự đoán F1 của LLM trên test thường: thực tế kết quả cho thấy LLM giữ được chất lượng trên case khó (0.933), còn BoW và 3b tụt mạnh.

Dự đoán accuracy trên 50 case khó: BoW (0.54) thấp hơn mức đoán tất cả là spam (0.58), lệch so với ước lượng ban đầu khoảng 0.6–0.75.

## 4. Phân tích 50 case khó

Model tụt nhiều nhất là BoW (0.889 → 0.378 F1) và 3b (0.947 → 0.583).

Case 1: “Hi Mum, I dropped my phone...” (spam, thao túng). Không có từ khoá quảng cáo; BoW đoán ham vì chỉ thấy từ đời thường.

Case 2: “C0ngr4tulat10ns! Y0u h4ve w0n...” (spam, né từ khoá). Leetspeak tạo token ngoài vocab; BoW không có trọng số.

## 5. Thử thách cá nhân

3 giá trị đều gần bằng nhau chênh lệch ít nên không thể kết luận k = 5 tốt nhất, k = 1 chỉ dựa vào một hàng xóm nên train sẽ yếu, phương sai cao còn k = 25 sẽ quyết định lớp đa số của vùng lân cận ví dụ như spam nhiều hơn ham thì kéo về spam.

## 6. Phương án cho sản phẩm thật

Phương án cân bằng nhất là 3b, nếu chấp nhận F1 0.964; BoW nếu cần tốc độ tối đa và chấp nhận F1 thấp hơn. Chi phí LLM ước tính: 1 tỷ token input x  0.10/1M= 100/ngày, cộng 10 triệu token output x  0.50/1M= 5/ngày, khoảng $105/ngày.

## 7. AI log và điều đã học

<img width="1721" height="197" alt="image" src="https://github.com/user-attachments/assets/2084bcac-dde1-47b2-bcd3-785f3541554d" />
