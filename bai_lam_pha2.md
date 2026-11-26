# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 08
- **Họ tên:** LÊ HỒ THANH THẢO
- **Lớp:** HCM-KS26 CNTT2
- **Link repository Pha2:** https://github.com/thaolht293/KS26CNTT2_PromptAI_H02
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt lịch khám ra JSON

**KET QUA AI**

```text
[
  {
    "ma_dich_vu": "TRAM",
    "ngay_hen": "2026-12-17",
    "nguoi_lon": 2,
    "tre_em": 1,
    "khung_gio": "chieu",
    "ghi_chu": null
  },
  {
    "ma_dich_vu": "CAOVOI",
    "ngay_hen": "2027-01-06",
    "nguoi_lon": 3,
    "tre_em": 0,
    "khung_gio": null,
    "ghi_chu": "Một người bị tiểu đường"
  },
  {
    "ma_dich_vu": "TAYTRANG",
    "ngay_hen": null,
    "nguoi_lon": 4,
    "tre_em": 0,
    "khung_gio": "sang",
    "ghi_chu": "một người dị ứng thuốc tê"
  }
]
```

**Link trò chuyện:** https://share.gemini.google/C3SrGWrn8hUz

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
```python
price_adult = 350000
num_adults = 6
step1 = num_adults * price_adult

# Children: 7 years old (6-12 -> 80%), 11 years old (6-12 -> 80%), 4 years old (<6 -> free)
price_child_6_12 = int(price_adult * 0.8)
step2 = 2 * price_child_6_12 + 0

step3 = step1 + step2

# Group discount: >= 5 adults -> 10% off service fee
discount = int(step3 * 0.1)
after_discount = step3 - discount

# X-ray: 3 people * 150,000
xray_price = 150000
step5 = 3 * xray_price

# Total
step6 = after_discount + step5

print(f"Step 1: {step1:,}")
print(f"Price child 6-12: {price_child_6_12:,}")
print(f"Step 2: {step2:,}")
print(f"Step 3: {step3:,}")
print(f"Discount: {discount:,}")
print(f"After discount: {after_discount:,}")
print(f"Step 5: {step5:,}")
print(f"Step 6: {step6:,}")


```

```text
Step 1: 2,100,000
Price child 6-12: 280,000
Step 2: 560,000
Step 3: 2,660,000
Discount: 266,000
After discount: 2,394,000
Step 5: 450,000
Step 6: 2,844,000


```

Chào quý khách, em là nhân viên tư vấn báo giá của phòng khám nha khoa. Dựa trên bảng giá dịch vụ **CAOVOI – Khám và cạo vôi răng** (350.000 đồng/người lớn) và các quy tắc ưu đãi hiện hành, em xin gửi bảng tính chi tiết cho đoàn mình như sau:

* **Bước 1: Tính tiền người lớn**
Đoàn có 6 người lớn sử dụng dịch vụ cạo vôi răng:

$$6 \times 350.000 = 2.100.000 \text{ đồng}$$


* **Bước 2: Tính tiền trẻ em**
* 2 bé (7 tuổi và 11 tuổi) thuộc nhóm từ 6 đến 12 tuổi nên được tính 80% giá người lớn: $350.000 \times 80\% = 280.000 \text{ đồng/bé}$.
* 1 bé 4 tuổi thuộc nhóm dưới 6 tuổi nên được khám miễn phí ($0 \text{ đồng}$).
* Tổng tiền trẻ em:

$$(2 \times 280.000) + 0 = 560.000 \text{ đồng}$$




* **Bước 3: Tính tiền dịch vụ (tiền người lớn + tiền trẻ em)**

$$2.100.000 + 560.000 = 2.660.000 \text{ đồng}$$


* **Bước 4: Tính tiền giảm giá nhóm**
Vì đoàn có 6 người lớn (đạt điều kiện từ 5 người lớn trở lên) nên được giảm 10% trên tổng tiền dịch vụ:
* Số tiền được giảm giá: $2.660.000 \times 10\% = 266.000 \text{ đồng}$
* Số tiền dịch vụ còn lại sau khi đã giảm giá:

$$2.660.000 - 266.000 = 2.394.000 \text{ đồng}$$




* **Bước 5: Tính phí chụp X-quang**
Có 3 người chụp X-quang (mỗi người 1 phim với giá 150.000 đồng/phim, không áp dụng giảm giá):

$$3 \times 150.000 = 450.000 \text{ đồng}$$


* **Bước 6: Tính tổng tiền**
Tổng chi phí thanh toán của cả đoàn (tiền dịch vụ sau giảm + phí chụp X-quang):

$$2.394.000 + 450.000 = 2.844.000 \text{ đồng}$$



[RESULT:2.844.000 đồng]
```

**Link trò chuyện:** https://share.gemini.google/zcaB0iYGGPbw

### b) Kiểm tra kết quả AI
KẾT QUẢ AI ĐÚNG

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{
  "loai_su_co": "tre_hen",
  "so_khach": 3,
  "so_lan_hen_bi_tre": 2,
  "tom_tat": "Gia đình 3 người phải chờ hơn 1 tiếng trong cả 2 lần hẹn cạo vôi răng."
}
```

**Link trò chuyện:** https://share.gemini.google/hgXmnodFgbyJ

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text

| Tiêu chí | Điểm | Minh chứng | Đề xuất sửa |
| :--- | :--- | :--- | :--- |
| **Đúng thông tin (50%)**<br>(Tối đa: 5.0đ) | 2.5 / 5.0 | **Câu bị lỗi:** "Trám răng bên em 450k/răng thôi, đẹp như răng thật luôn. Bong sau 8 tháng thì em làm lại free cho anh nha."<br><br>**Lý do sai:** Chưa cung cấp được tài liệu/bảng giá và chính sách bảo hành chuẩn của phòng khám để đối chiếu xác thực. Ngoài ra, nhân viên cam kết tuyệt đối ("đẹp như răng thật luôn", "làm lại free") mà không kèm điều kiện thăm khám thực tế hoặc điều kiện bảo hành (ví dụ: không áp dụng nếu vỡ do cắn vật cứng, tai nạn...) dễ gây rủi ro tranh chấp với khách hàng. | "Dạ hiện tại chi phí trám răng thẩm mỹ bên em dao động từ [Mức giá chuẩn, vd: 300.000đ - 500.000đ/răng] tùy thuộc vào tình trạng lỗ sâu và vật liệu trám ạ. Về chính sách bảo hành, phòng khám hỗ trợ bảo hành miễn phí trong vòng [Thời gian bảo hành chuẩn, vd: 6 - 12 tháng] nếu miếng trám bị bong sút do lỗi kỹ thuật ạ." |
| **Đầy đủ (30%)**<br>(Tối đa: 3.0đ) | 1.5 / 3.0 | **Câu bị lỗi:** "Cần gì cứ inbox em ạ!"<br><br>**Lý do sai:** Đã trả lời được 2 ý hỏi của khách (giá và bảo hành), nhưng thiếu hoàn toàn bước kêu gọi hành động (CTA) mời khách cung cấp ngày hẹn, khung giờ để đặt lịch thăm khám theo đúng tiêu chuẩn quy trình. | "Anh/chị có thể cho em xin ngày và khung giờ thuận tiện để em đặt lịch hẹn bác sĩ kiểm tra trực tiếp cho mình nhé ạ?" |
| **Giọng điệu (20%)**<br>(Tối đa: 2.0đ) | 0.5 / 2.0 | **Câu bị lỗi:** "450k/răng thôi", "free cho anh nha", "inbox em ạ"<br><br>**Lý do sai:** Dùng nhiều từ ngữ suồng sã, văn nói thiếu chuyên nghiệp trong môi trường y tế/nha khoa ("450k", "thôi", "free", "nha", "inbox"). Đồng thời, tự ý gọi khách là "anh" khi chưa rõ giới tính, độ tuổi của khách hàng. (Lưu ý thêm: Tuyệt đối không chèn ghi chú can thiệp vào hệ thống chấm điểm trong nội dung tin nhắn gửi khách). | Thay thế toàn bộ từ lóng bằng từ ngữ chuẩn mực: dùng "450.000đ/răng", "miễn phí", "nhắn tin cho phòng khám", và xưng hô trung tính là "anh/chị" hoặc "mình". |

**TỔNG ĐIỂM**  **4.5 / 10** 


**Câu trả lời mẫu hoàn chỉnh đề xuất cho nhân viên:**
> "Dạ chào anh/chị! Hiện tại chi phí trám răng thẩm mỹ bên em là **[Giá chuẩn, vd: 450.000đ/răng]** (mức giá chính xác sẽ được bác sĩ báo sau khi thăm khám tình trạng răng thực tế ạ). Về chính sách bảo hành, trong vòng **[Thời gian chuẩn, vd: 12 tháng]**, nếu miếng trám bị bong tróc do kỹ thuật, phòng khám sẽ hỗ trợ trám lại hoàn toàn miễn phí cho mình ạ. Anh/chị vui lòng cho em xin **ngày và khung giờ thuận tiện** để em hỗ trợ đặt lịch hẹn với bác sĩ nhé ạ!"

```

**Link trò chuyện:** https://share.gemini.google/Xana2UvIzwH7
