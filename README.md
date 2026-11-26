# VJAA Quiz — Công cụ kiểm tra trắc nghiệm (VietJet Aviation Academy)

Web app tĩnh, chạy hoàn toàn trong trình duyệt (không cần server). Học viên mở link GitHub Pages để làm bài; giáo viên có thể thêm bộ đề mới ngay trên trình duyệt.

## 1. Có gì trong bản demo
- **Môn 1:** Aircraft Loading Procedure — 40 câu (đã nhúng sẵn kèm đáp án).
- **Môn 2:** An toàn sân đỗ (Môn mẫu) — 5 câu mẫu, chỉ để minh hoạ cơ chế nhiều môn. **Thay bằng đề thật** khi có.
- Chức năng: trộn câu/đáp án, chọn số câu, đặt giờ, điểm đạt, chấm điểm tự động, **xem lại đáp án đúng/sai**, làm lại.
- **Thêm bộ đề mới** (nút "➕ Bộ đề mới"): dán đề Moodle, tải file `.json`/`.txt`, hoặc export JSON.

## 2. Đưa lên GitHub Pages (5 phút)
1. Tạo repo mới trên GitHub (VD: `vjaa-quiz`).
2. Upload file `index.html` vào repo (và `README.md` nếu muốn).
3. Vào **Settings → Pages → Build and deployment**: chọn **Source: Deploy from a branch**, Branch = `main`, thư mục `/ (root)` → **Save**.
4. Đợi ~1 phút, link dạng `https://<tài-khoản>.github.io/vjaa-quiz/` sẽ hiện ra. Gửi link này cho học viên.

> Chỉ cần đúng 1 file `index.html` là chạy được — mọi thứ đã nhúng trong đó.

## 3. Thêm môn học mới
**Cách A — dán đề Moodle (nhanh nhất):** mở app → "➕ Bộ đề mới" → tab "Dán đề", đặt tên môn, dán nguyên văn đề (giữ các dòng `Select one:`, `a. b. c.` và `The correct answer is: …`) → "Phân tích" → "Lưu". Môn được lưu trong trình duyệt của máy đó.

**Cách B — nhúng cố định vào app (mọi học viên đều thấy):** thêm 1 phần tử vào mảng `BUILTIN_SUBJECTS` ở đầu thẻ `<script>` trong `index.html`, theo schema:

```json
{
  "name": "Tên môn",
  "note": "mô tả ngắn (tùy chọn)",
  "questions": [
    { "q": "Nội dung câu hỏi?", "options": ["Đáp án A", "Đáp án B", "Đáp án C"], "answer": 1 }
  ]
}
```
- `answer` = chỉ số đáp án đúng, **đếm từ 0** (0 = đáp án đầu tiên).
- Mẹo: trong app, import đề bằng Cách A rồi bấm **"Export JSON"** để lấy sẵn khối JSON đúng chuẩn, dán vào `BUILTIN_SUBJECTS`.

## 4. Định dạng đề Moodle được hỗ trợ
Mỗi câu gồm: dòng `Question N`, nội dung câu hỏi (có hoặc không có số thứ tự đầu dòng), dòng `Select one:`, các đáp án `a. … b. … c. …`, và dòng `The correct answer is: <nội dung đáp án đúng>`. Hệ thống tự khớp đáp án đúng theo nội dung, không phụ thuộc chữ cái a/b/c.

## 5. Lưu ý
- Môn thêm bằng Cách A chỉ lưu trên **máy/trình duyệt đó** (localStorage). Muốn mọi học viên thấy → dùng Cách B.
- App chạy offline sau khi tải trang. Không thu thập dữ liệu, không gửi đi đâu.
