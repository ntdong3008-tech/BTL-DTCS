# Bản Thiết Kế Dự Án: Hệ Thống Điều Khiển BỘ BIẾN ĐỔI PFC KIỂU BOOST (ĐỀ 35)

## 1. Mục Tiêu Dự Án
- **Bài toán:** Biến đổi điện áp xoay chiều (AC) từ lưới điện thành điện áp một chiều (DC) ổn định, đồng thời đảm bảo dòng điện hút từ lưới có hình sin và cùng pha với điện áp (Hệ số công suất $cos(\phi) \approx 1$).
- **Thông số kỹ thuật:**
  - Lưới điện ($U_{in}$): 220VAC $\pm$ 10%, Tần số: 50Hz $\pm$ 1%.
  - Điện áp đầu ra ($U_{out}$): 400VDC.
  - Công suất định mức ($P$): 1kW.
- **Yêu cầu kỹ thuật cốt lõi:** Sử dụng **Bộ bù loại 2 (Type 2 Compensator)** cho các mạch vòng điều khiển dòng điện và điện áp.

---

## 2. Ý Tưởng & Chiến Thuật Giải Quyết Bài Toán

### 2.1. Cấu trúc phần cứng (Mạch lực)
Mạch sẽ gồm 2 phần chính:
1. **Cầu chỉnh lưu Diode:** Chuyển điện áp AC 220V/50Hz thành điện áp DC nhấp nhô (dạng 2 nửa chu kỳ).
2. **Mạch Boost (Tăng áp):** Nhận điện áp DC nhấp nhô, băm xung (PWM) thông qua MOSFET để tăng áp lên mức 400VDC phẳng.
   - **Tính toán cuộn cảm (L):** Sẽ được tính dựa trên độ đập mạch dòng điện cho phép (thường chọn $\approx 15\% - 20\%$ dòng đỉnh). Cuộn cảm này giúp "bơm" dòng liên tục.
   - **Tính toán tụ điện (C):** Sẽ được tính dựa trên độ đập mạch điện áp đầu ra (thường cho phép dao động $\approx 1\% - 2\%$). Do mạch PFC có nhấp nhô công suất ở tần số 100Hz (gấp đôi tần số lưới), tụ $C$ phải đủ lớn để gánh phần này.

### 2.2. Chiến lược Điều khiển (Trái tim của hệ thống)
Áp dụng cấu trúc **Điều khiển dòng điện trung bình (Average Current Mode Control)** với 2 vòng lặp lồng nhau:

*   **Vòng ngoài (Mạch vòng Điện áp):** 
    *   **Nhiệm vụ:** Giữ áp ra luôn ở mức 400V.
    *   **Tốc độ:** Phải phản hồi RẤT CHẬM (Tần số cắt chỉ khoảng $10Hz - 20Hz$). Nếu để nó phản hồi nhanh, nó sẽ cố gắng dập tắt dải sóng 100Hz, làm méo mó dòng điện đầu vào.
    *   **Bộ điều khiển:** Dùng **Bộ bù loại 2**. Đầu ra của vòng này sẽ quy định biên độ dòng điện mà mạch cần rút từ lưới điện.

*   **Vòng trong (Mạch vòng Dòng điện):**
    *   **Nhiệm vụ:** Ép dòng điện chạy qua cuộn cảm $L$ phải có hình dáng giống y hệt hình dáng điện áp lưới (hình sin).
    *   **Tốc độ:** Phải phản hồi RẤT NHANH (Tần số cắt bằng khoảng 1/10 tần số băm xung PWM) để bám sát sự thay đổi của hình sin.
    *   **Bộ điều khiển:** Dùng **Bộ bù loại 2**.

### 2.3. Tại sao lại là "Bộ bù loại 2" (Type 2 Compensator)?
Bộ bù loại 2 về bản chất là một bộ điều khiển PI được "độ" thêm một điểm cực tần số cao (High-frequency pole). 
- **Khâu Tích phân (Origin pole):** Triệt tiêu sai lệch tĩnh (đảm bảo áp ra đúng 400V, không bị tụt).
- **Điểm không (Zero):** Tăng góc pha, giúp hệ thống không bị dao động (ổn định).
- **Điểm cực (High-frequency pole):** Lọc sạch nhiễu do quá trình đóng cắt của MOSFET sinh ra, giúp hệ thống không bị "phát điên" vì nhiễu.

---

## 3. Kế Hoạch Triển Khai Mô Phỏng (Dùng Matlab/Simulink)

Không làm tất cả cùng lúc để tránh việc mạch báo lỗi không biết sửa ở đâu. Sẽ làm theo 3 bước cuốn chiếu:

- **Bước 1: Chạy hở (Open-loop).** Lắp nguyên phần mạch lực (Nguồn AC + Chỉnh lưu + Boost). Đặt một chu kỳ xung (Duty Cycle) cố định để xem điện áp có tăng lên được không, mạch có nối sai dây không.
- **Bước 2: Đóng vòng dòng điện.** Cấp cho mạch một tín hiệu hình sin mẫu. Chỉ dùng vòng lặp dòng điện (Type 2) xem dòng có bám theo hình sin được không.
- **Bước 3: Đóng vòng điện áp (Hoàn thiện).** Lắp vòng điện áp vào. Bật chạy mô phỏng.

### Các Kịch Bản Test (Bắt Buộc):
1. **Test thay đổi tải:** Chạy ổn định ở tải 1kW. Sau đó tại thời điểm $t=1s$, đóng ngắt công tắc giảm tải xuống còn 0.5kW. Đánh giá xem điện áp 400V có bị vọt lố nhiều không, và mất bao lâu để phục hồi.
2. **Test thay đổi lưới:** Cho áp lưới tụt từ 220V xuống 198V (-10%). Xem mạch có tự động hút thêm dòng điện để bù công suất và giữ nguyên áp 400V không.

---

## 4. Cấu Trúc Slide Báo Cáo Dự Kiến
1. **Giới thiệu:** Tên đề tài, tên thành viên, tóm tắt nhiệm vụ (PFC Boost 1kW, 400V).
2. **Mô hình hóa hệ thống:**
   - Sơ đồ nguyên lý mạch lực.
   - Các công thức tính $L, C$.
   - Hàm truyền đạt của mạch Boost.
3. **Thiết kế Bộ điều khiển:**
   - Cấu trúc 2 vòng lặp (vẽ sơ đồ khối).
   - Hàm truyền của Bộ bù loại 2. Trình bày cách tính ra các con số (R, C trong mạch bù).
4. **Kết quả Mô phỏng (Matlab/Simulink):**
   - Hình ảnh mạch Simulink tổng thể.
   - Đồ thị khi chạy bình thường (Khoe dòng điện đồng pha với điện áp lưới - chứng minh PFC thành công).
   - Đồ thị kịch bản 1: Thay đổi tải.
   - Đồ thị kịch bản 2: Thay đổi điện áp lưới.
5. **So sánh Thiết kế Số / Tương tự:** 
   - Đưa hệ thống về dạng Z-domain (Rời rạc hóa bộ điều khiển). So sánh kết quả mô phỏng.
6. **Kết luận & Phụ lục.**

## 5. Phân Chia Nhân Sự & Khối Lượng Công Việc
Do bản chất môn học khá nặng, nhóm 2 thành viên sẽ chia nhiệm vụ theo dạng "Kẹp chả" (Một người thiên về thực hành phần mềm, một người thiên về toán và trình bày). Tuy nhiên, cả hai phải thường xuyên trao đổi chéo để hiểu sản phẩm của nhau.

### 🧑‍💻 Thành viên A: Chuyên trách Mô phỏng & Phần mềm (Simulation Lead)
**Trách nhiệm chính:** "Biến các con số trên giấy thành hệ thống chạy được".
- **Giai đoạn 1 & 2:** Làm quen với Matlab/Simulink (hoặc Plecs). Tự tay kéo thả và nối dây phần mạch lực hở (Cầu chỉnh lưu, Cuộn cảm, MOSFET, Diode, Tụ điện).
- **Giai đoạn 3:** Xây dựng sơ đồ khối cấu trúc điều khiển. Tạo các Block đại diện cho **Bộ bù loại 2** dựa trên thông số Thành viên B đưa cho.
- **Giai đoạn 4 (Quan trọng nhất):** Tiến hành chạy mô phỏng. Khi đồ thị bị nhiễu hoặc sai, tự tay tinh chỉnh (fine-tune) các thông số bộ điều khiển để đồ thị đạt chuẩn. Chạy 2 kịch bản Test (đổi tải, đổi áp lưới) và xuất/chụp các đồ thị (waveform) đẹp nhất để gửi cho Thành viên B.
- **Quản lý source code:** Đảm bảo các file `.slx` luôn được lưu và đẩy (Push) lên GitHub đầy đủ.

### 📝 Thành viên B: Chuyên trách Toán & Báo cáo (Theory & Documentation Lead)
**Trách nhiệm chính:** "Tính toán thông số chuẩn xác và đóng gói sản phẩm hoàn hảo".
- **Giai đoạn 1 & 2:** Nghiên cứu kỹ file `Control_PFC.pdf`. Trích xuất các công thức cần thiết. Thay số của Đề 35 (1kW, 400VDC, 220VAC) vào để chốt lại giá trị chính xác của $L$ và $C$. Chuyển số này cho Thành viên A nhập vào phần mềm.
- **Giai đoạn 3:** Xử lý bài toán khó nhất: Tìm hàm truyền và tính toán các giá trị điện trở ($R$), tụ điện ($C$) bên trong cấu trúc của **Bộ bù loại 2** cho cả vòng dòng điện và điện áp.
- **Giai đoạn 4 & 5:** Dàn dựng file Slide báo cáo trên nền Template chuẩn của ĐHBK Hà Nội. Nhận ảnh đồ thị từ Thành viên A để chèn vào. Soạn thảo các biến đổi toán học vào phần Phụ lục.

### 🤝 Nhiệm vụ Chung (Phối hợp)
- Cùng nhau họp xem xét lại sơ đồ khối điều khiển xem có bị ngược dấu hoặc sai logic không (lỗi rất hay gặp khiến mô phỏng "nổ").
- Cùng phân tích, nhận xét ý nghĩa của các đồ thị sau khi chạy kịch bản mô phỏng.
- Tập duyệt thuyết trình và đặt câu hỏi phản biện chéo cho nhau để chuẩn bị bảo vệ.
