# BÀI 3: GIẢI MÃ HIỆN TƯỢNG CHÊNH LỆCH TOKENIZATION TIẾNG VIỆT

## PHẦN 1. PHÂN TÍCH CƠ CHẾ BPE

### 1. BPE hoạt động như thế nào?

BPE (Byte-Pair Encoding) là thuật toán tách văn bản thành các đơn vị nhỏ gọi là Token.

- Văn bản được mã hóa thành các đơn vị byte.
- Thuật toán BPE ghép những chuỗi byte xuất hiện thường xuyên thành các Token.
- Những từ hoặc ký tự ít phổ biến có thể bị chia thành nhiều Token nhỏ hơn.

Đối với tiếng Việt, các ký tự có dấu như ă, â, ê, ô, ơ, ư và các dấu thanh có thể khiến cách mã hóa phức tạp hơn. Nếu chuỗi ký tự ít xuất hiện trong dữ liệu huấn luyện của Tokenizer, chúng có thể bị chia thành nhiều Token.

### 2. Phân tích bảng số liệu

| Tiêu chí | Tiếng Anh | Tiếng Việt |
|---|---:|---:|
| Số từ | 100 | 100 |
| Số Token | 118 | 285 |
| Token/từ | 1,18 | 2,85 |

Tỷ lệ chênh lệch:

285 / 118 ≈ 2,42 lần.

Như vậy, Mẫu B sử dụng số Token gấp khoảng 2,4 lần Mẫu A.

**Nguyên nhân:**

- Tokenizer thường nhận diện nhiều cụm từ tiếng Anh phổ biến thành Token hoàn chỉnh.
- Một số chuỗi ký tự tiếng Việt có dấu có thể ít phổ biến hơn trong dữ liệu huấn luyện.
- Vì vậy, văn bản tiếng Việt có thể bị chia thành nhiều đơn vị nhỏ hơn.

**Kết luận:** Tokenizer không nhất thiết bị lỗi đếm trùng. Sự chênh lệch chủ yếu đến từ cách mã hóa và phân tách văn bản thành Token.

## PHẦN 2. TỐI ƯU PROMPT TIẾNG VIỆT

Hoàng có thể áp dụng 2 kỹ thuật sau:

### Kỹ thuật 1: Loại bỏ từ ngữ dư thừa

- Viết yêu cầu ngắn gọn, đi thẳng vào mục tiêu.
- Loại bỏ câu chào hỏi, lời dẫn và các cụm từ lặp lại.
- Giữ nguyên thông tin quan trọng và điều kiện của yêu cầu.

Ví dụ:

Prompt dài:
"Bạn hãy giúp tôi viết một bài giới thiệu sản phẩm rau củ hữu cơ của siêu thị MartX. Tôi muốn bài viết có nội dung hấp dẫn, dễ hiểu và phù hợp với khách hàng."

Prompt tối ưu:
"Viết bài giới thiệu rau củ hữu cơ MartX, hấp dẫn, dễ hiểu, hướng đến khách hàng."

### Kỹ thuật 2: Dùng cấu trúc và từ khóa ngắn gọn

- Chia yêu cầu thành các ý rõ ràng.
- Sử dụng từ khóa thay cho những câu diễn giải dài.
- Chỉ giữ những tiêu chí cần thiết để AI thực hiện đúng nhiệm vụ.

Ví dụ:

Prompt dài:
"Bạn hãy viết nội dung quảng cáo cho sản phẩm rau củ hữu cơ của MartX. Nội dung cần nêu được nguồn gốc sản phẩm, độ tươi ngon và lợi ích đối với sức khỏe. Giọng văn cần thân thiện và thuyết phục."

Prompt tối ưu:

"Nhiệm vụ: Viết quảng cáo rau củ hữu cơ MartX.
Yêu cầu: Nêu nguồn gốc, độ tươi, lợi ích sức khỏe. Giọng văn thân thiện, thuyết phục."
