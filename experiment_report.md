# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-XXXX
**Name:** (Dien ten cua ban)
**Date:** (Dien ngay thuc hien)

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 9/10 | Correct response - identified best electronics product with accurate price |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 2/10 | Incorrect response - picked outlier/corrupted data instead of valid product |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Dữ liệu garbage chứa nhiều vấn đề chất lượng:
- **Missing ID (20%)**: Hàng cuối không có ID, không đầy đủ
- **Distinct values không chính xác (60%)**: So với processed_data có 100% distinct values, garbage data bị lặp lại
- **Wrong data types**: Cột price có giá trị non-numeric như "ten dollars" thay vì số
- **Extreme outliers**: Nuclear Reactor có giá $999999 vốn là sai lệch, không hợp lý
- **Null values**: Hàng cuối missing value ở ID và category
- **Logic error**: AI lấy best choice dựa trên max price, nhưng do dữ liệu bị sai category assignment và chứa outlier → dữ liệu đầu vào không clean, kéo theo output sai lệch

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý - **Quality Data là yếu tố quan trọng hơn**

AI chỉ là một bộ não, output luôn dựa vào input là gì. Độ chính xác của kết quả phụ thuộc hoàn toàn vào chất lượng dữ liệu đầu vào. Dù prompt như thế nào tốt đi chăng nữa, nếu dữ liệu bị lỗi (duplicate, outlier, null, wrong type), AI vẫn sẽ cho ra kết quả sai. Vậy nên, đảm bảo data quality là bước quan trọng nhất trong ETL pipeline.
