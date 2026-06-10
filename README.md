# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** email@example.com
**Name:** Học viên

---

## Mo ta

Bài lab này hướng dẫn xây dựng một ETL Data Pipeline đơn giản và kiểm tra sự ảnh hưởng của Data Quality (Chất lượng dữ liệu) đến AI Agent. Em đã hoàn thành việc:
1. Viết code ETL (`solution.py`) để làm sạch, kiểm tra và chuyển đổi dữ liệu.
2. Thử nghiệm Agent với dữ liệu chuẩn và dữ liệu rác, sau đó hoàn thành file báo cáo `experiment_report.md`.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

Pipeline chạy thành công. Đã đọc dữ liệu từ raw_data.json, trong đó:
- Số record hợp lệ đã xử lý: 3
- Số record lỗi đã loại bỏ: 2 (do giá <= 0 hoặc category rỗng)
Agent chạy tốt với dữ liệu sạch (chọn Laptop) nhưng đưa ra kết quả vô lý với dữ liệu rác (chọn Nuclear Reactor do giá trị outlier).
