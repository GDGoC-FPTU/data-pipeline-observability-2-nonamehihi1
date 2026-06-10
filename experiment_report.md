# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** (Dien ten cua ban)
**Date:** (Dien ngay thuc hien)

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Agent đã chọn đúng sản phẩm đồ điện tử giá cao nhất hợp lý. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 0 | Agent đã chọn sai sản phẩm do dữ liệu outlier không hợp lệ. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai khi sử dụng Garbage Data chủ yếu do dữ liệu rác chứa các giá trị ngoại lai (outliers) quá lớn, ví dụ như sản phẩm "Nuclear Reactor" với giá 999999. Vì logic của Agent dựa trên việc tìm sản phẩm có giá cao nhất (`idxmax()`) trong một danh mục, nó sẽ ưu tiên chọn các outlier này bất kể sản phẩm đó có thực sự hợp lý hay không.

Ngoài ra, dữ liệu rác còn chứa các vấn đề khác như trùng lặp ID, sai kiểu dữ liệu (vd: giá tiền là chữ), hoặc giá trị bị Null. Mặc dù trong trường hợp này, ngoại lai về giá là nguyên nhân trực tiếp làm hỏng logic của Agent, các vấn đề chất lượng dữ liệu khác cũng có thể gây ra lỗi (crash) nếu Agent không được xử lý ngoại lệ cẩn thận (ví dụ cố gắng tính toán trên chuỗi "ten dollars"). Do đó, nếu không có bước Validate & Transform ở Data Pipeline, AI Agent sẽ trực tiếp "ăn" dữ liệu rác và đưa ra kết quả sai lệch hoặc thậm chí bị sập.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý.

Cho dù prompt của Agent có hoàn hảo đến đâu, nếu dữ liệu đầu vào (Knowledge Base) chứa rác, Agent vẫn sẽ đưa ra những câu trả lời sai lệch (Garbage In, Garbage Out). Data Pipeline chất lượng cao sẽ đảm bảo dữ liệu đưa vào Agent là chính xác, từ đó giúp Agent hoạt động tin cậy hơn.
