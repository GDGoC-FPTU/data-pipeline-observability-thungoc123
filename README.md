[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574074&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability
**MHS:** 2A202600210
**Student Email:** nguyenthunngoc@gmail.com
**Name:** Nguyễn Thị Ngọc Thư

---

## Mo ta

Bài lab xây dựng một **ETL Pipeline (Extract, Transform, Load)** tự động để:
- **Extract** dữ liệu từ JSON
- **Validate** chất lượng dữ liệu (loại bỏ price <= 0, category rỗng)
- **Transform** dữ liệu (tính giá giảm 10%, chuyển category to Title Case, thêm timestamp)
- **Load** dữ liệu sạch ra CSV

Sau đó, kiểm tra tác động của **Data Quality** đến AI Agent bằng cách chạy agent trên:
1. **Clean Data** (processed_data.csv): Dữ liệu sạch từ ETL
2. **Garbage Data** (garbage_data.csv): Dữ liệu có lỗi (duplicate ID, wrong type, outliers, null values)

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
# Buoc 1: Tao garbage data (data co loi)
python generate_garbage.py

# Buoc 2: Chay agent tren Clean Data va Garbage Data
python agent_simulation.py

# Hoac chay tat ca cung luc:
python generate_garbage.py; python solution.py; python agent_simulation.py
```

**Output:** Agent tra loi sai khi dung Garbage Data (chon Nuclear Reactor $999999 thay vi Laptop $1200) voi Accuracy chi 2/10

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

**ETL Pipeline Results:**
- **Total Records Extracted:** 5 records (tu raw_data.json)
- **Valid Records:** 3 records (price > 0 AND category khong rong)
- **Dropped Records:** 2 records (Mystery Box: gia am -10; Phone: category rong)
- **Final Output:** 3 records luu vao processed_data.csv

**Key Insight:**
- **Clean Data:** Agent tra loi Laptop $1200 ✓ (Accuracy: 9/10)
- **Garbage Data:** Agent tra loi Nuclear Reactor $999999 ✗ (Accuracy: 2/10)
- **Ket luan:** Quality Data > Quality Prompt. Dung du lieu xau se dan den AI output xau, bao nhieu prompt tot di chung khong change duoc output.
