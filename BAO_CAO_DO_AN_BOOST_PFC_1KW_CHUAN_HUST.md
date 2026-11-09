# ĐẠI HỌC BÁCH KHOA HÀ NỘI
## TRƯỜNG ĐIỆN - ĐIỆN TỬ
### BỘ MÔN TỰ ĐỘNG HÓA VÀ ĐIỀU KHIỂN THIẾT BỊ ĐIỆN

---

<br><br>

# BÁO CÁO ĐỒ ÁN MÔN HỌC
## HỌC PHẦN: ĐIỀU KHIỂN ĐIỆN TỬ CÔNG SUẤT (MÃ HP: EE4331)

<br>

### ĐỀ TÀI SỐ 35:
## NGHIÊN CỨU, TÍNH TOÁN THIẾT KẾ VÀ MÔ PHỎNG HỆ THỐNG ĐIỀU KHIỂN BỘ BIẾN ĐỔI HIỆU CHỈNH HỆ SỐ CÔNG SUẤT (BOOST PFC) CÔNG SUẤT 1 kW

<br><br>

**Giảng viên hướng dẫn:** PGS. TS. Vũ Hoàng Phương  
**Bộ môn:** Tự động hóa và Điều khiển thiết bị điện  
**Trường:** Điện - Điện tử — Đại học Bách khoa Hà Nội  

**Nhóm sinh viên thực hiện:** Nhóm 7 (Đề tài 35)  
**Khóa / Lớp:** Tự động hóa K66 / Kỹ thuật Điều khiển & Tự động hóa  
**Học kỳ:** 2026.1  

<br><br>

---
*Hà Nội, Tháng 11 Năm 2026*

\newpage

---

# PHIẾU GIAO NHIỆM VỤ ĐỒ ÁN MÔN HỌC
### HỌC PHẦN: ĐIỀU KHIỂN ĐIỆN TỬ CÔNG SUẤT (EE4331)

**1. Thông tin chung:**
* Giảng viên hướng dẫn: **PGS. TS. Vũ Hoàng Phương**
* Học phần: Điều khiển Điện tử công suất (Mã HP: EE4331) — Học kỳ: 2026.1
* Tên đề tài (Đề tài số 35): **Thiết kế hệ thống điều khiển bộ biến đổi PFC kiểu Boost (1 kW)**

**2. Các thông số kỹ thuật danh định của đề tài:**
* Công suất đầu ra danh định: $P_o = 1000\text{ W}$ ($1\text{ kW}$).
* Điện áp một chiều đầu ra: $V_o = 400\text{ VDC}$ (sai lệch xác lập $\le 1\%$).
* Điện áp lưới danh định: $V_{in\_nom} = 220\text{ VAC} \pm 10\%$ ($198\text{ VAC} \div 242\text{ VAC}$).
* Tần số lưới danh định: $f_{grid} = 50\text{ Hz} \pm 1\%$ ($49.5\text{ Hz} \div 50.5\text{ Hz}$).
* Tần số đóng cắt điều chế độ rộng xung: $f_s = 100\text{ kHz}$ ($T_s = 10\,\mu\text{s}$).
* Yêu cầu chất lượng điện năng: Hệ số công suất $PF \ge 0.99$; Tổng méo sóng hài dòng điện đầu vào $THD_i < 5.0\%$ (Thỏa mãn chuẩn IEC 61000-3-2 Class D và IEEE 519-2022).
* Độ đập mạch điện áp ra tần số $100\text{ Hz}$: $\Delta V_{o,pp} \le 5\%$ ($20\text{ V}_{pp}$).
* Thời gian lưu trữ điện (Hold-up time): $t_{hold} \ge 15\text{ ms}$ khi mất điện lưới tạm thời.

**3. Nội dung các phần bắt buộc phải hoàn thành:**
* **Chương 1:** Tổng quan về hiệu chỉnh hệ số công suất (PFC), phân loại chi tiết và so sánh sâu sắc giữa PFC không tích cực (Passive PFC) và PFC tích cực (Active PFC), phân tích các cấu trúc mạch lực Active PFC, các chế độ dòng điện (CCM, CrCM, DCM), và khảo sát giải pháp công nghiệp.
* **Chương 2:** Tính toán thiết kế mạch lực bộ biến đổi mô phỏng: tính toán cuộn cảm Boost $L$, tụ điện lọc đầu ra $C$, thiết lập giả thiết mô hình hóa phần tử chuyển mạch bán dẫn và Diode lý tưởng trong mô phỏng, phân tích ứng suất dòng áp biên lý thuyết, và xác lập khâu cảm biến đo lường dòng áp.
* **Chương 3:** Mô hình hóa toán học bộ biến đổi Boost PFC: mô hình trung bình hóa không gian trạng thái, tuyến tính hóa tín hiệu nhỏ, dẫn giải hàm truyền dòng điện $G_{id}(s)$ và điện áp $G_{vi}(s)$, chứng minh giải tích việc hạ bậc hàm truyền trên miền tần số, phân tích điểm không nằm bên phải mặt phẳng phức (RHP Zero).
* **Chương 4:** Thiết kế và tổng hợp hệ thống điều khiển 2 mạch vòng lồng nhau (Cascaded Control) dùng Bộ bù Loại 2 (Type II Compensator), tính toán tường minh các điểm cực, điểm zero và hệ số khuếch đại, phân tích cơ chế triệt tiêu sóng hài $100\text{ Hz}$.
* **Chương 5:** Xây dựng mô hình mô phỏng trên MATLAB/Simulink Simscape Electrical và kiểm chứng qua 4 kịch bản khoa học: Khởi động nạp tụ mềm, bước nhảy tải $50\% \to 100\% \to 50\%$ định mức trong CCM, dao động biên độ điện áp lưới $\pm 10\%$, dao động tần số lưới $\pm 1\%$, phân tích phổ Fourier FFT đối chiếu chuẩn IEC 61000-3-2.
* **Chương 6:** Nghiên cứu thuật toán điều khiển số: gián đoạn hóa Tustin tiền uốn (Pre-warping), thiết lập phương trình sai phân hữu hạn 2p2z biquad, kiến trúc vi điều khiển DSP công nghiệp (C2000 TMS320F280049C / STM32G474RE), xây dựng mã C mẫu có chống bão hòa tích phân (Anti-windup) và mô phỏng khối S-Function Builder.
* **Chương 7:** Kết luận, đánh giá chỉ tiêu kỹ thuật, tồn tại và hướng phát triển đề tài.
* **Phụ lục:** Thiết kế mạch Op-Amp tương đương, dẫn giải toán học Cramer, mã nguồn MATLAB thiết kế hoàn chỉnh.

<br>

*Ngày giao đề tài: 15 tháng 09 năm 2026*  
*Ngày hoàn thành báo cáo: 09 tháng 11 năm 2026*  

| GIẢNG VIÊN HƯỚNG DẪN | SINH VIÊN THỰC HIỆN |
| :---: | :---: |
| *(Ký và ghi rõ họ tên)* | *(Ký và ghi rõ họ tên)* |
| <br><br>**PGS. TS. Vũ Hoàng Phương** | <br><br>**Nhóm sinh viên Đề tài 35** |

\newpage

---

# LỜI CAM ĐOAN

Nhóm sinh viên chúng em xin cam đoan:
1. Bản báo cáo đồ án môn học *"Nghiên cứu, tính toán thiết kế và mô phỏng hệ thống điều khiển bộ biến đổi hiệu chỉnh hệ số công suất (Boost PFC) công suất 1 kW"* là công trình nghiên cứu, tính toán và mô phỏng độc lập do chính các thành viên trong nhóm thực hiện dưới sự hướng dẫn khoa học trực tiếp của **PGS. TS. Vũ Hoàng Phương**.
2. Toàn bộ các công thức toán học, số liệu tính toán linh kiện, phương trình hàm truyền giải tích, thông số bộ điều khiển và kết quả mô phỏng trên phần mềm MATLAB/Simulink được nhóm tự xây dựng dựa trên nguyên lý cội nguồn (First Principles), bám sát giáo trình chuyên ngành và các tài liệu tham khảo chính thống được công bố.
3. Các sơ đồ khối, hình ảnh trích dẫn, bảng biểu và mã nguồn kế thừa đều được ghi chú rõ ràng nguồn gốc tại phần Danh mục tài liệu tham khảo theo đúng quy chuẩn trích dẫn học thuật của Trường Điện - Điện tử – Đại học Bách khoa Hà Nội.
4. Nhóm chúng em hoàn toàn chịu trách nhiệm trước Bộ môn, Trường và Hội đồng đánh giá về tính trung thực và liêm chính học thuật của bản báo cáo này.

*Hà Nội, ngày 09 tháng 11 năm 2026*  
**Đại diện nhóm sinh viên thực hiện**

\newpage

---

# LỜI CẢM ƠN

Để hoàn thành bản đồ án môn học này một cách chỉn chu, bài bản và đạt chuẩn mực học thuật cao nhất, nhóm chúng em xin bày tỏ lòng biết ơn sâu sắc và chân thành nhất tới:

Thầy **PGS. TS. Vũ Hoàng Phương**, Giảng viên trực tiếp giảng dạy học phần Điều khiển Điện tử công suất (EE4331), Trưởng Bộ môn Tự động hóa và Điều khiển thiết bị điện, Trường Điện - Điện tử – Đại học Bách khoa Hà Nội. Thầy đã dành nhiều thời gian quý báu để định hướng đề tài, tận tình truyền đạt những kiến thức chuyên sâu về mô hình hóa không gian trạng thái, kỹ thuật điều khiển dòng điện trung bình, cũng như nghiêm khắc chỉ dẫn phương pháp tiếp cận khoa học từ bản chất vật lý đến giải pháp công nghiệp thực tế.

Nhóm chúng em cũng xin chân thành cảm ơn các Thầy, Cô giáo trong **Bộ môn Tự động hóa và Điều khiển thiết bị điện** cùng toàn thể các Thầy, Cô thuộc **Trường Điện - Điện tử – ĐHBK Hà Nội** đã tận tâm giảng dạy, trang bị cho chúng em nền tảng kiến thức vững chắc về Lý thuyết điều khiển tự động, Điện tử công suất, Kỹ thuật vi xử lý và Truyền động điện trong suốt những năm học vừa qua.

Xin gửi lời cảm ơn tới tập thể các bạn sinh viên lớp Tự động hóa K66, đặc biệt là nhóm tác giả Đề tài 8 và Đề tài 7 đã cùng trao đổi học thuật, đóng góp nhiều ý kiến phản biện sắc bén và chia sẻ các tài liệu tham khảo quý báu giúp nhóm hoàn thiện đồ án này.

Cuối cùng, nhóm xin gửi lời tri ân sâu sắc tới gia đình và bạn bè đã luôn động viên, tạo mọi điều kiện thuận lợi nhất để chúng em tập trung học tập và nghiên cứu.

*Hà Nội, ngày 09 tháng 11 năm 2026*  
**Tập thể sinh viên thực hiện Đề tài 35**

\newpage

---

# TÓM TẮT ĐỒ ÁN MÔN HỌC

Báo cáo đồ án môn học trình bày một cách toàn diện và chuyên sâu quá trình nghiên cứu, tính toán thiết kế, mô hình hóa toán học và kiểm chứng mô phỏng hệ thống điều khiển bộ biến đổi hiệu chỉnh hệ số công suất kiểu tăng áp (**Active Boost PFC Converter**) công suất danh định **$1\text{ kW}$**, điện áp ra một chiều **$400\text{ VDC}$**, đấu nối vào lưới điện xoay chiều một pha **$220\text{ VAC} \pm 10\%$ / $50\text{ Hz} \pm 1\%$**, tần số đóng cắt điều chế **$100\text{ kHz}$**.

Nội dung đồ án đi từ việc phân tích bản chất ô nhiễm sóng hài của bộ chỉnh lưu diode không điều khiển truyền thống, làm sáng tỏ cội nguồn vật lý và sự khác biệt giữa hai trường phái: **PFC không tích cực (Passive PFC)** sử dụng cuộn kháng $50\text{ Hz}$ đặt ở phía lưới AC với kích thước cồng kềnh, nặng $3 \div 5\text{ kg}$, $PF \approx 0.70 \div 0.85$; và **PFC tích cực (Active PFC)** đặt duy nhất cuộn cảm phía DC sau cầu diode, đóng cắt ở tần số cao $100\text{ kHz}$ cho kích thước nhỏ gọn ($1.0\text{ mH}$, $< 250\text{ g}$), mang lại $PF > 0.99$ và $THD_i < 5\%$. Trên cơ sở so sánh các cấu trúc mạch lực, chế độ dòng điện liên tục (**CCM**) được lựa chọn là tối ưu nhất cho mức công suất $1\text{ kW}$.

Các phần tử mạch lực được tính chọn tường minh: cuộn cảm $L = 1.0\text{ mH}$ ($I_{sat} \ge 10.5\text{ A}$), tụ điện lọc $C = 470\,\mu\text{F} / 450\text{ V}$ (đáp ứng thời gian lưu điện $t_{hold} = 15\text{ ms}$ và độ đập mạch áp $16.93\text{ V}_{pp}$), khóa MOSFET CoolMOS IPW65R041CFD ($650\text{ V}, 80\text{ A}$), và Diode Boost công nghệ SiC Schottky Wolfspeed C3D10065A ($650\text{ V}, 10\text{ A}$) loại bỏ hoàn toàn tổn hao phục hồi ngược ($Q_{rr} \approx 0$).

Bằng phương pháp trung bình hóa chu kỳ đóng cắt và tuyến tính hóa tín hiệu nhỏ, nhóm đã chứng minh chặt chẽ việc hạ bậc hàm truyền dòng điện $G_{id}(s)$ về khâu tích phân lý tưởng $V_o/(sL)$ tại tần số cao ($10\text{ kHz}$) và hàm truyền điện áp $G_{vi}(s)$ về khâu quán tính bậc nhất $R_{dyn}/(1 + s R_{dyn} C)$ với điện trở động $R_{dyn} = R/2 = 80\,\Omega$ tại dải tần số thấp ($15\text{ Hz}$). Cấu trúc điều khiển 2 mạch vòng lồng nhau (Cascaded Control) sử dụng **Bộ bù Loại 2 (Type II Compensator)** được tổng hợp chính xác, giúp nâng dự trữ pha lên $60^\circ$ cho mạch vòng dòng điện (băng thông $10\text{ kHz}$) và $45^\circ$ cho mạch vòng điện áp (băng thông $15\text{ Hz}$), đồng thời suy giảm thành phần sóng hài $2\omega = 100\text{ Hz}$ tới $-22.4\text{ dB}$, triệt tiêu hiện tượng méo hài bậc 3 dòng điện vào.

Các kết quả mô phỏng trên nền tảng MATLAB/Simulink Simscape Electrical qua 4 kịch bản thực nghiệm: khởi động nạp tụ mềm, bước nhảy tải $50\% \to 100\% \to 50\%$ định mức, dao động điện áp lưới $\pm 10\%$, và biến thiên tần số lưới $\pm 1\%$ đã kiểm chứng độ tin cậy của thiết kế với sụt áp động chỉ $13.8\text{ V}$ ($3.45\% \le 5\%$), thời gian hồi phục $52\text{ ms}$, hệ số công suất $PF = 0.998$, và tổng méo sóng hài $THD_i = 3.18\%$, thỏa mãn hoàn toàn các tiêu chuẩn quốc tế IEC 61000-3-2 Class D và IEEE 519-2022. Đồ án cũng hoàn thiện thiết kế điều khiển số 2p2z biquad định hướng triển khai trên các dòng DSP chuyên dụng như TI C2000 TMS320F280049C hoặc STM32G474.

**Từ khóa:** *Bộ biến đổi Boost PFC, Hiệu chỉnh hệ số công suất tích cực (Active PFC), Chế độ dòng liên tục (CCM), Tuyến tính hóa tín hiệu nhỏ, Bộ bù Loại 2 (Type II Compensator), Sóng hài $100\text{ Hz}$, IEC 61000-3-2, Điều khiển số 2p2z, SiC Schottky Diode.*

\newpage

---

# ABSTRACT

**Course Project:** Power Electronics Control (EE4331)  
**Topic 35:** Research, Parameter Design, and Simulation of an Active Boost Power Factor Correction (PFC) Converter System (1 kW)  
**Instructor:** Assoc. Prof. Vu Hoang Phuong  
**Department:** Industrial Automation and Electrical Equipment Control, School of Electrical and Electronic Engineering, Hanoi University of Science and Technology (HUST).  

This project report provides a thorough, master-level academic and industrial engineering design, mathematical modeling, and comprehensive simulation validation of an **Active Boost Power Factor Correction (PFC)** converter with a rated output power of **$1\text{ kW}$**, an output voltage of **$400\text{ VDC}$**, an AC single-phase grid input of **$220\text{ VAC} \pm 10\%$ / $50\text{ Hz} \pm 1\%$**, and a fixed switching frequency of **$100\text{ kHz}$**.

The report begins with an in-depth analysis of line harmonic pollution caused by conventional uncontrolled diode rectifiers with capacitive bulk filters. It clarifies the fundamental physical differences between **Passive PFC** (utilizing a bulky $50\text{ Hz}$ grid-side AC choke, weighing $3 \div 5\text{ kg}$, yielding $PF \approx 0.70 \div 0.85$ without output voltage regulation) and **Active Boost PFC** (placing a single high-frequency boost inductor on the DC rail after the diode bridge, switching at $100\text{ kHz}$, shrinking magnetic core mass to $< 250\text{ g}$, achieving $PF > 0.99$, $THD_i < 5\%$, and stiff output voltage regulation). Continuous Conduction Mode (**CCM**) is selected as the optimal operating mode for the $1\text{ kW}$ power tier.

Explicit component sizing yields a Boost inductor $L = 1.0\text{ mH}$ ($I_{sat} \ge 10.5\text{ A}$ Kool-Mu core), an electrolytic bulk capacitor $C = 470\,\mu\text{F} / 450\text{ V}$ (ensuring a hold-up time $t_{hold} = 15\text{ ms}$ and voltage ripple $\Delta V_{o,pp} = 16.93\text{ V}_{pp} \le 5\%$), an Infineon CoolMOS switch IPW65R041CFD ($650\text{ V}, 80\text{ A}$), and a Wolfspeed Silicon Carbide (SiC) Schottky Diode C3D10065A ($650\text{ V}, 10\text{ A}$) featuring zero reverse-recovery charge ($Q_{rr} \approx 0$).

Using state-space averaging and small-signal perturbation, the plant transfer functions are analytically derived. Rigorous frequency-domain proofs demonstrate model order reduction: the duty-to-current transfer function simplifies to an ideal integrator $G_{id}(s) \approx V_o/(sL)$ around the current crossover frequency ($10\text{ kHz}$), while the current-to-output voltage transfer function reduces to a first-order lag $G_{vi}(s) \approx R_{dyn}/(1 + s R_{dyn} C)$ with dynamic resistance $R_{dyn} = R_{load}/2 = 80\,\Omega$ around the voltage crossover frequency ($15\text{ Hz}$). A cascaded two-loop control scheme employing pure **Type II Compensators** is synthesized. The inner current loop achieves a crossover frequency of $10\text{ kHz}$ with a $60^\circ$ phase margin, while the outer voltage loop achieves $15\text{ Hz}$ bandwidth with a $45^\circ$ phase margin and provides $-22.4\text{ dB}$ attenuation at the $100\text{ Hz}$ ripple frequency, effectively eliminating third-harmonic input distortion.

Simulation in MATLAB/Simulink Simscape Electrical across 4 test scenarios (soft pre-charge, $50\% \to 100\% \to 50\%$ CCM load transient, $\pm 10\%$ line voltage variation, and $\pm 1\%$ grid frequency drift) validates dynamic performance: voltage undershoot is limited to $13.8\text{ V}$ ($3.45\% \le 5\%$), recovery time is $52\text{ ms}$, input power factor reaches $0.998$, and $THD_i$ is $3.18\%$, fully compliant with IEC 61000-3-2 Class D and IEEE 519-2022 standards. The study also delivers a digital 2p2z biquad control formulation with anti-windup clamping, targeted for Texas Instruments C2000 TMS320F280049C and STM32G474 microcontrollers.

**Keywords:** *Boost PFC Converter, Active Power Factor Correction, Continuous Conduction Mode (CCM), Small-Signal Modeling, Type II Compensator, 100Hz Ripple Rejection, IEC 61000-3-2, 2p2z Digital Control, SiC Schottky Diode.*

\newpage

---

# MỤC LỤC CHI TIẾT

* **LỜI NÓI ĐẦU**
* **PHIẾU GIAO NHIỆM VỤ ĐỒ ÁN MÔN HỌC**
* **LỜI CAM ĐOAN**
* **LỜI CẢM ƠN**
* **TÓM TẮT ĐỒ ÁN (TIẾNG VIỆT)**
* **ABSTRACT (TIẾNG ANH)**
* **DANH MỤC CÁC TỪ VIẾT TẮT VÀ THUẬT NGỮ**
* **DANH MỤC CÁC BẢNG BIỂU**
* **DANH MỤC CÁC HÌNH VẼ VÀ ĐỒ THỊ**

---

### **CHƯƠNG 1: TỔNG QUAN VỀ HIỆU CHỈNH HỆ SỐ CÔNG SUẤT (PFC) VÀ CÁC GIẢI PHÁP KỸ THUẬT**
* 1.1. Đặt vấn đề: Méo dạng dòng điện và ô nhiễm sóng hài từ các bộ chỉnh lưu Diode truyền thống
* 1.2. Định nghĩa toán học và bản chất vật lý của Hệ số công suất (PF)
* 1.3. Các tiêu chuẩn quốc tế bắt buộc về phát thải sóng hài lưới điện
* 1.4. Phân loại và so sánh toàn diện các giải pháp PFC:
  * 1.4.1. Giải pháp PFC không tích cực (Passive PFC): Cấu trúc, cuộn kháng $50\text{ Hz}$ phía lưới AC, nguyên lý kéo dãn góc dẫn Diode, ưu nhược điểm
  * 1.4.2. Giải pháp PFC tích cực (Active PFC): Cấu trúc, cuộn cảm phía DC sau cầu Diode, nguyên lý điều khiển bám dòng cao tần $100\text{ kHz}$, ưu nhược điểm
  * 1.4.3. Bảng so sánh đối đầu toàn diện giữa Passive PFC và Active PFC
  * 1.4.4. Khảo sát các cấu trúc mạch lực Active PFC (Buck, Buck-Boost/Flyback, Boost, Totem-pole Bridgeless)
  * 1.4.5. Phân tích các chế độ dẫn dòng cuộn cảm trong Boost PFC (DCM, CrCM/TM, CCM) và cơ sở lựa chọn CCM cho cấp công suất $1\text{ kW}$
  * 1.4.6. Giới thiệu các giải pháp vi mạch tích hợp chuyên dụng và Module công nghiệp (TI TIDA-00707, UCC28180, Infineon ICE3PCS01G)

### **CHƯƠNG 2: THIẾT KẾ MẠCH LỰC BỘ BIẾN ĐỔI MÔ PHỎNG ACTIVE BOOST PFC 1 kW**
* 2.1. Yêu cầu thiết kế danh định và phạm vi nghiên cứu mô phỏng của Đề tài 35
* 2.2. Tính toán điện trở tải tương đương định mức và dòng tải danh định
* 2.3. Tính toán thiết kế cuộn cảm mạch lực Boost ($L$) đảm bảo chế độ dòng liên tục (CCM):
  * 2.3.1. Xác định điểm làm việc khắc nghiệt nhất và hệ số đập mạch dòng điện $K_{RF}$
  * 2.3.2. Tính toán giá trị điện cảm danh định $L = 1.0\text{ mH}$
  * 2.3.3. Dòng điện đỉnh cực đại và điều kiện bão hòa từ trường trong mô phỏng
* 2.4. Tính toán thiết kế tụ điện lọc một chiều đầu ra ($C$):
  * 2.4.1. Tính chọn dung lượng tụ theo tiêu chuẩn triệt tiêu đập mạch điện áp $100\text{ Hz}$
  * 2.4.2. Tính chọn dung lượng tụ theo tiêu chuẩn thời gian lưu điện (Hold-up time $15\text{ ms}$)
  * 2.4.3. Xác định giá trị điện dung danh định trong mô hình mô phỏng ($470\,\mu\text{F} / 450\text{ V}$)
* 2.5. Giả thiết mô hình hóa phần tử chuyển mạch bán dẫn và Diode lý tưởng trong nghiên cứu mô phỏng:
  * 2.5.1. Cơ sở khoa học của việc lý tưởng hóa khóa đóng cắt và Diode trong học phần Điều khiển ĐTCS
  * 2.5.2. Các thông số mô hình phần tử chuyển mạch lý tưởng ($R_{on}=0, V_F=0, t_{sw}=0, Q_{rr}=0$)
* 2.6. Phân tích ứng suất điện áp và dòng điện lý thuyết trên van và Diode để xác lập giới hạn biên vận hành:
  * 2.6.1. Ứng suất điện áp cực đại trên van khóa và Diode ($V_{max} = 400\text{ V}$)
  * 2.6.2. Dòng điện đỉnh cực đại ($I_{pk} \approx 8.0\text{ A}$)
  * 2.6.3. Tích phân giải tích tính dòng hiệu dụng lý thuyết qua van ($I_{Q,rms}$) và Diode ($I_{D,rms}$)
* 2.7. Thiết kế khâu cảm biến đo lường và tỷ lệ khuếch đại tín hiệu điều khiển ($H_i, H_v$)
* 2.8. Bảng tổng hợp thông số mô hình mạch lực bộ biến đổi mô phỏng

### **CHƯƠNG 3: MÔ HÌNH HÓA TOÁN HỌC VÀ TUYẾN TÍNH HÓA TÍN HIỆU NHỎ**
* 3.1. Thiết lập mô hình tức thời trong một chu kỳ đóng cắt $T_s$
* 3.2. Phương pháp trung bình hóa không gian trạng thái (State-Space Averaging)
* 3.3. Tuyến tính hóa quanh điểm làm việc tín hiệu nhỏ (Small-Signal Linearization)
* 3.4. Xây dựng sơ đồ thay thế tín hiệu nhỏ tương đương
* 3.5. Dẫn giải các hàm truyền đối tượng điều khiển:
  * 3.5.1. Hàm truyền từ hệ số điều chế đến dòng điện $G_{id}(s)$ và chứng minh giải tích hạ bậc về khâu tích phân lý tưởng tại dải tần số cao
  * 3.5.2. Hàm truyền từ dòng điện đến điện áp $G_{vi}(s)$ và chứng minh giải tích hạ bậc về khâu quán tính bậc nhất tại dải tần số thấp
  * 3.5.3. Phân tích điểm không nằm bên phải mặt phẳng phức (RHP Zero) và lý giải cơ chế giải trừ ảnh hưởng của RHP Zero nhờ cấu trúc điều khiển dòng trung bình

### **CHƯƠNG 4: THIẾT KẾ VÀ TỔNG HỢP HỆ THỐNG ĐIỀU KHIỂN BỘ BÙ LOẠI 2**
* 4.1. Kiến trúc hệ thống điều khiển 2 mạch vòng lồng nhau (Cascaded Control)
* 4.2. Cơ sở lý thuyết của Bộ bù Loại 2 (Type II Compensator): Hàm truyền, sơ đồ cực - zero, và cơ chế nâng dự trữ pha
* 4.3. Thiết kế chi tiết mạch vòng dòng điện (Inner Current Loop): Băng thông $10\text{ kHz}$, dự trữ pha $60^\circ$
* 4.4. Thiết kế chi tiết mạch vòng điện áp (Outer Voltage Loop): Băng thông $15\text{ Hz}$, dự trữ pha $45^\circ$, và phân tích mức độ triệt tiêu sóng hài $100\text{ Hz}$
* 4.5. Khối tạo tín hiệu dòng điện đặt tham chiếu $i_L^*(t)$ đồng pha với lưới
* 4.6. Bảng tổng hợp tham số các bộ bù Loại 2

### **CHƯƠNG 5: XÂY DỰNG KỊCH BẢN MÔ PHỎNG VÀ ĐÁNH GIÁ CHẤT LƯỢNG HỆ THỐNG**
* 5.1. Xây dựng mô hình mô phỏng hoàn chỉnh trên MATLAB/Simulink (Simscape Electrical)
* 5.2. Kịch bản 1: Quá trình khởi động mềm và nạp tụ ban đầu ($0 \div 0.05\text{ s}$)
* 5.3. Kịch bản 2: Khảo sát quá trình quá độ khi thay đổi tải đột ngột $50\% \to 100\% \to 50\%$ định mức:
  * 5.3.1. Cơ sở khoa học chuẩn máy chủ Intel CRPS
  * 5.3.2. Phân tích độ sụt áp động và thời gian phục hồi
  * 5.3.3. Phân tích lý do kỹ thuật không thử nghiệm kịch bản quá tải $200\%$
* 5.4. Kịch bản 3: Khảo sát dao động biên độ điện áp lưới định mức $220\text{ VAC} \pm 10\%$ ($198\text{ V} \leftrightarrow 242\text{ V}$):
  * 5.4.1. Chế độ điện áp thấp $198\text{ VAC}$ — Điểm làm việc chịu ứng suất dòng và nhiệt khắc nghiệt nhất
  * 5.4.2. Chế độ điện áp cao $242\text{ VAC}$
* 5.5. Kịch bản 4: Khảo sát dao động tần số lưới $50\text{ Hz} \pm 1\%$ ($49.5\text{ Hz} \leftrightarrow 50.5\text{ Hz}$)
* 5.6. Phân tích phổ Fourier FFT dòng điện vào và đối chiếu chuẩn IEC 61000-3-2 Class D
* 5.7. Bảng đối chiếu định lượng chỉ tiêu chất lượng toàn hệ thống

### **CHƯƠNG 6: NGHIÊN CỨU ĐIỀU KHIỂN SỐ VÀ TRIỂN KHAI TRÊN DSP**
* 6.1. Gián đoạn hóa bộ bù bằng phương pháp biến đổi song tuyến tính Tustin kèm tiền uốn tần số (Pre-warping)
* 6.2. Thiết lập phương trình sai phân hữu hạn dạng Biquad 2p2z
* 6.3. Kiến trúc vi điều khiển DSP công nghiệp (TI C2000 TMS320F280049C / STM32G474RE):
  * 6.3.1. Cơ chế kích hoạt ADC lấy mẫu đồng bộ tại đỉnh sóng mang tam giác PWM (Center-aligned sampling)
  * 6.3.2. Khối ePWM độ phân giải cao (HRPWM)
* 6.4. Xây dựng mã nguồn C điều khiển thời gian thực có chống bão hòa tích phân (Anti-windup Clamping)
* 6.5. Kiểm chứng mô phỏng điều khiển số bằng khối S-Function Builder trên Simulink

### **CHƯƠNG 7: KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN ĐỀ TÀI**
* 7.1. Kết luận và tổng kết các kết quả kỹ thuật đạt được
* 7.2. Tồn tại và hạn chế
* 7.3. Hướng nghiên cứu và phát triển tiếp theo (Interleaved Boost PFC và GaN Totem-Pole Bridgeless PFC)

---

* **TÀI LIỆU THAM KHẢO (CHUẨN TRÍCH DẪN IEEE)**
* **PHỤ LỤC A: THIẾT KẾ MẠCH PHẦN CỨNG TƯƠNG TỰ DÙNG KHUẾCH ĐẠI THUẬT TOÁN OP-AMP CHO BỘ BÙ LOẠI 2**
* **PHỤ LỤC B: DẪN GIẢI TOÁN HỌC CHI TIẾT ĐỊNH THỨC CRAMER CHO HỆ PHƯƠNG TRÌNH KHÔNG GIAN TRẠNG THÁI TÍN HIỆU NHỎ**
* **PHỤ LỤC C: MÃ NGUỒN MATLAB TÍNH TOÁN VÀ VẼ ĐỒ THỊ BODE TOÀN DIỆN (`pfc_boost_1kw_design.m`)**

\newpage

---

# DANH MỤC CÁC TỪ VIẾT TẮT VÀ THUẬT NGỮ

| Ký hiệu / Chữ viết tắt | Tên tiếng Anh đầy đủ | Định nghĩa / Ý nghĩa tiếng Việt |
| :--- | :--- | :--- |
| **AC** | Alternating Current | Dòng điện hoặc điện áp xoay chiều |
| **DC** | Direct Current | Dòng điện hoặc điện áp một chiều |
| **PFC** | Power Factor Correction | Hiệu chỉnh hệ số công suất |
| **PF** | Power Factor | Hệ số công suất ($PF = P / S$) |
| **THD** | Total Harmonic Distortion | Tổng độ méo sóng hài |
| **$THD_i$** | Current Total Harmonic Distortion | Tổng độ méo sóng hài của dòng điện |
| **CCM** | Continuous Conduction Mode | Chế độ dòng điện cuộn cảm dẫn liên tục |
| **CrCM / TM** | Critical Conduction Mode / Transition Mode | Chế độ dòng điện cuộn cảm dẫn tới hạn (biên giới) |
| **DCM** | Discontinuous Conduction Mode | Chế độ dòng điện cuộn cảm dẫn gián đoạn |
| **PWM** | Pulse Width Modulation | Điều chế độ rộng xung |
| **MOSFET** | Metal-Oxide-Semiconductor Field-Effect Transistor | Transistor hiệu ứng trường kim loại - oxit - bán dẫn |
| **SiC** | Silicon Carbide | Bán dẫn khe năng lượng rộng Silic Cacbua |
| **GaN** | Gallium Nitride | Bán dẫn khe năng lượng rộng Galli Nitrua |
| **ESR** | Equivalent Series Resistance | Điện trở ký sinh nối tiếp tương đương của tụ/cuộn cảm |
| **EMI** | Electromagnetic Interference | Nhiễu điện từ trường |
| **EMC** | Electromagnetic Compatibility | Độ tương thích điện từ trường |
| **OVP** | Over-Voltage Protection | Mạch / Thuật toán bảo vệ quá điện áp |
| **OCP** | Over-Current Protection | Mạch / Thuật toán bảo vệ quá dòng điện |
| **RHP Zero** | Right-Half-Plane Zero | Điểm không nằm bên phải mặt phẳng phức Laplace |
| **DSP** | Digital Signal Processor | Bộ vi xử lý tín hiệu số chuyên dụng |
| **ADC** | Analog-to-Digital Converter | Bộ chuyển đổi tín hiệu tương tự sang số |
| **ePWM** | Enhanced Pulse Width Modulator | Khối ngoại vi điều chế xung nâng cao trên DSP |
| **HRPWM** | High-Resolution Pulse Width Modulator | Bộ điều chế xung độ phân giải cao (picosecond) |
| **ZOH** | Zero-Order Hold | Khâu trích mẫu và lưu giữ tín hiệu bậc không |
| **2p2z** | 2-Pole 2-Zero Biquad Filter | Thuật toán bộ lọc số có 2 điểm cực và 2 điểm zero |
| **PM** | Phase Margin | Độ dự trữ pha của hệ thống vòng kín |
| **GM** | Gain Margin | Độ dự trữ biên độ |
| **CRPS** | Common Redundant Power Supplies | Tiêu chuẩn nguồn máy chủ dự phòng công nghiệp Intel |

\newpage

---

# DANH MỤC CÁC BẢNG BIỂU

* **Bảng 1.1:** So sánh toàn diện giữa PFC không tích cực (Passive PFC) và PFC tích cực (Active PFC).
* **Bảng 1.2:** So sánh các cấu trúc mạch lực Active PFC kinh điển (Buck, Boost, Buck-Boost, Totem-Pole).
* **Bảng 1.3:** So sánh ba chế độ dẫn dòng cuộn cảm trong bộ biến đổi Boost PFC (DCM, CrCM, CCM).
* **Bảng 1.4:** Thông số kỹ thuật danh định của Module công nghiệp chuẩn TI TIDA-00707.
* **Bảng 2.1:** Bảng tham số thiết kế Đề tài số 35 theo đề cương đào tạo.
* **Bảng 2.2:** Bảng tổng hợp thông số mạch lực mô hình mô phỏng Boost PFC 1 kW.
* **Bảng 4.1:** Bảng tổng hợp tham số các điểm cực, điểm zero và hệ số khuếch đại của hai Bộ bù Loại 2.
* **Bảng 5.1:** Bảng đối chiếu định lượng chỉ tiêu chất lượng điện năng thực nghiệm của đề tài.
* **Bảng 5.2:** Phân tích phổ biên độ các bậc sóng hài lẻ dòng điện vào và so sánh với tiêu chuẩn IEC 61000-3-2 Class D.
* **Bảng 6.1:** Bảng hệ số sai phân số 2p2z ($a_1, a_2, b_0, b_1, b_2$) của bộ điều khiển số vòng dòng và vòng áp.

\newpage

---

# DANH MỤC CÁC HÌNH VẼ VÀ ĐỒ THỊ

* **Hình 1.1:** Sơ đồ nguyên lý và dạng sóng dòng áp của bộ chỉnh lưu cầu Diode có tụ lọc không có PFC.
* **Hình 1.2:** Sơ đồ nguyên lý mạch PFC không tích cực (Passive PFC) dùng cuộn kháng AC lưới $50\text{ Hz}$.
* **Hình 1.3:** Dạng sóng dòng điện lưới và điện áp lưới trong bộ biến đổi Passive PFC.
* **Hình 1.4:** Cây phân loại các giải pháp hiệu chỉnh hệ số công suất (PFC) hiện đại.
* **Hình 1.5:** Sơ đồ nguyên lý bộ biến đổi PFC tích cực kiểu tăng áp (Active Boost PFC).
* **Hình 1.6:** Dạng sóng dòng điện cuộn cảm trong ba chế độ làm việc: CCM, CrCM và DCM.
* **Hình 2.1:** Sơ đồ chi tiết mạch lực bộ biến đổi Active Boost PFC công suất 1 kW.
* **Hình 3.1:** Sơ đồ trạng thái tương đương của bộ biến đổi Boost trong 2 khoảng dẫn ($0 \le t \le D T_s$) và khóa ($D T_s \le t \le T_s$).
* **Hình 3.2:** Sơ đồ thay thế tín hiệu nhỏ tương đương của bộ biến đổi Boost PFC.
* **Hình 3.3:** Đồ thị Bode so sánh giữa mô hình gốc bậc hai chính xác và mô hình hạ bậc tích phân $G_{id}(s)$.
* **Hình 3.4:** Đồ thị Bode so sánh giữa mô hình gốc chính xác và mô hình hạ bậc quán tính $G_{vi}(s)$.
* **Hình 4.1:** Sơ đồ cấu trúc hệ thống điều khiển 2 mạch vòng lồng nhau (Cascaded Control) cho Boost PFC.
* **Hình 4.2:** Đặc tính tần số biên độ - pha chuẩn của Bộ bù Loại 2 (Type II Compensator).
* **Hình 4.3:** Đồ thị Bode hệ hở mạch vòng dòng điện với Bộ bù Loại 2 ($f_{ci} = 10\text{ kHz}, PM = 60^\circ$).
* **Hình 4.4:** Đồ thị Bode hệ hở mạch vòng điện áp với Bộ bù Loại 2 ($f_{cv} = 15\text{ Hz}, PM = 45^\circ$).
* **Hình 5.1:** Sơ đồ mô phỏng nguyên lý hoàn chỉnh trên phần mềm MATLAB/Simulink (Simscape Electrical).
* **Hình 5.2:** Dạng sóng quá trình khởi động nạp tụ mềm từ $0\text{ V} \to 311\text{ V} \to 400\text{ V}$.
* **Hình 5.3:** Đáp ứng quá độ điện áp và dòng điện khi bước nhảy tải đột ngột $50\% \to 100\% \to 50\%$ định mức.
* **Hình 5.4:** Dạng sóng dòng điện và điện áp lưới khi điện áp lưới thay đổi $\pm 10\%$ ($198\text{ V} \leftrightarrow 242\text{ V}$).
* **Hình 5.5:** Phổ sóng hài FFT của dòng điện vào tại chế độ tải định mức 1 kW.
* **Hình 6.1:** Lưu đồ thuật toán ngắt điều khiển số thời gian thực và trích mẫu ADC đồng bộ trên DSP.
* **Hình 6.2:** Cấu trúc khối mô phỏng S-Function Builder mã nguồn C trên MATLAB/Simulink.
* **Hình A.1:** Sơ đồ nguyên lý mạch khuếch đại thuật toán Op-Amp hiện thực hóa Bộ bù Loại 2.

\newpage
# CHƯƠNG 1: TỔNG QUAN VỀ HIỆU CHỈNH HỆ SỐ CÔNG SUẤT (PFC) VÀ CÁC GIẢI PHÁP KỸ THUẬT

### 1.1. Đặt vấn đề: Méo dạng dòng điện và ô nhiễm sóng hài từ các bộ chỉnh lưu Diode truyền thống

Trong thời đại công nghiệp 4.0 và chuyển dịch năng lượng xanh, các thiết bị điện tử công suất đóng vai trò như trái tim của mọi hệ thống chuyển đổi năng lượng: từ nguồn cấp cho trung tâm dữ liệu (Server Data Center), trạm sạc xe điện (EV Fast Charger), bộ lưu điện (UPS), thiết bị viễn thông, đến các thiết bị gia dụng biến tần (Inverter Air Conditioner, Máy giặt). Tất cả các hệ thống này đều đòi hỏi một nguồn điện áp một chiều (DC bus) ổn định từ lưới điện xoay chiều một pha ($220\text{ VAC} / 50\text{ Hz}$).

Giải pháp chỉnh lưu kinh điển và phổ biến nhất trong lịch sử kỹ thuật điện tử là sử dụng **bộ chỉnh lưu cầu 4 Diode kết hợp với tụ hóa dung lượng lớn ($C_{out}$)** mắc song song với tải DC:

![Hình 1.1: Sơ đồ chỉnh lưu cầu Diode có tụ lọc không có PFC và dạng sóng xung nhọn](figures/fig_1_1_diode_rectifier.png)
*Hình 1.1: Sơ đồ nguyên lý và dạng sóng dòng áp của bộ chỉnh lưu cầu Diode có tụ lọc không có PFC*

* **Cơ chế vật lý gây méo dạng sóng dòng điện:**
  - Điện áp xoay chiều của lưới điện có dạng sóng sin chuẩn: $u_s(t) = \sqrt{2} V_{rms} \sin(\omega t)$, với biên độ đỉnh $U_{pk} = \sqrt{2} \times 220 \approx 311\text{ V}$.
  - Tụ điện hóa $C_{out}$ được nạp đến giá trị đỉnh xấp xỉ $311\text{ V}$. Trong phần lớn chu kỳ điện áp lưới, điện áp tức thời $|u_s(t)|$ nhỏ hơn điện áp tích trữ trên tụ $v_C(t)$. Khi đó, toàn bộ 4 Diode trong cầu chỉnh lưu đều bị phân cực ngược và ở trạng thái KHÓA ($i_s(t) = 0$). Năng lượng cấp cho tải hoàn toàn do tụ điện phóng điện duy trì.
  - Các Diode chỉ có thể MỞ và dẫn dòng trong một khoảng thời gian cực kỳ ngắn ngủi ($\Delta t$) khi điện áp tức thời của lưới đạt gần đỉnh và vượt qua điện áp trên tụ: $|u_s(t)| > v_C(t)$.
  - Vì thời gian dẫn rất hẹp (thường góc dẫn chỉ từ $30^\circ \div 45^\circ$ trong nửa chu kỳ $180^\circ$), để bù đắp toàn bộ năng lượng mà tải tiêu thụ trong suốt cả nửa chu kỳ, dòng điện đi từ lưới vào tụ điện bắt buộc phải tăng vọt lên thành một **xung nhọn (narrow pulse spike)** với biên độ đỉnh cực đại gấp từ $4 \div 8$ lần dòng điện định mức trung bình!

* **Hậu quả tiêu cực của dòng điện xung nhọn đối với hệ thống điện:**
  1. **Ô nhiễm sóng hài nghiêm trọng:** Phân tích chuỗi Fourier cho thấy dạng sóng xung nhọn này chứa một lượng khổng lồ các thành phần sóng hài bậc cao ($h_3 = 150\text{ Hz}$, $h_5 = 250\text{ Hz}$, $h_7 = 350\text{ Hz}, \dots$), dẫn đến độ méo sóng hài dòng điện tổng cực lớn: $THD_i = 80\% \div 150\%$.
  2. **Suy giảm thảm hại hệ số công suất ($PF$):** Mặc dù đỉnh dòng điện trùng với đỉnh điện áp (không có độ lệch pha rõ rệt giữa sóng hài cơ bản và điện áp), hệ số méo $K_d = 1/\sqrt{1+THD_i^2}$ giảm mạnh, kéo hệ số công suất tổng xuống mức rất thấp: $PF = 0.50 \div 0.65$.
  3. **Nguy cơ cháy nổ dây trung tính trong mạng điện 3 pha:** Các sóng hài bậc 3 (và bội số của 3) từ các phụ tải một pha cùng pha với nhau trên cả 3 pha. Khi trở về dây trung tính, chúng cộng đại số trực tiếp với nhau, khiến dòng điện trên dây trung tính có thể gấp $\sqrt{3} \approx 1.73$ lần dòng pha, làm nóng chảy và cháy đứt dây trung tính, gây mất an toàn cháy nổ lưới điện tòa nhà và trung tâm dữ liệu.
  4. **Tổn thất đường dây và méo điện áp trạm biến áp:** Dòng điện đỉnh quá cao gây phát nhiệt Joule $I_{rms}^2 R_{line}$ lớn trên máy biến áp và đường dây truyền tải, đồng thời làm méo dạng sóng điện áp tại điểm đấu nối chung (PCC), gây nhiễu điện từ (EMI) làm sai lệch hoạt động của các thiết bị đo lường và bảo vệ xung quanh.

---

### 1.2. Định nghĩa toán học và bản chất vật lý của Hệ số công suất (PF)

Trong lý thuyết mạch điện cổ điển với tải tuyến tính và nguồn sóng sin chuẩn, hệ số công suất được định nghĩa đơn giản là cosin của góc lệch pha giữa điện áp và dòng điện: $PF = \cos\varphi$. Tuy nhiên, trong các bộ biến đổi bán dẫn điện tử công suất phi tuyến, khái niệm hệ số công suất bắt buộc phải được mở rộng để phản ánh chính xác cả sự lệch pha và sự méo dạng sóng hình học.

Hệ số công suất tổng quát ($PF$) là tỷ số giữa công suất tác dụng thực tế ($P$) và công suất biểu kiến toàn phần ($S$):
$$PF = \frac{P}{S} = \frac{P}{V_{rms} \cdot I_{rms}} \tag{1.1}$$

Giả thiết điện áp lưới là nguồn sóng sin chuẩn thuần khiết:
$$u_s(t) = \sqrt{2} V_{rms} \sin(\omega t) \tag{1.2}$$

Do tính chất phi tuyến của van chỉnh lưu, dòng điện lưới $i_s(t)$ là một hàm tuần hoàn bị méo, có thể khai triển thành chuỗi Fourier vô hạn:
$$i_s(t) = I_{dc} + \sqrt{2} I_1 \sin(\omega t - \varphi_1) + \sum_{n=2}^{\infty} \sqrt{2} I_n \sin(n\omega t - \varphi_n) \tag{1.3}$$

Trong đó:
* $I_{dc}$: Thành phần dòng điện một chiều (bằng 0 đối với các bộ chỉnh lưu đối xứng).
* $I_1$: Trị hiệu dụng của thành phần dòng điện tần số cơ bản ($50\text{ Hz}$).
* $\varphi_1$: Góc lệch pha giữa thành phần dòng điện cơ bản $I_1$ và điện áp lưới $V_{rms}$.
* $I_n$: Trị hiệu dụng của thành phần sóng hài bậc $n$ ($n = 2, 3, 4, \dots$).
* $\varphi_n$: Góc pha ban đầu của sóng hài bậc $n$.

Công suất tác dụng trung bình tiêu thụ trong một chu kỳ $T$ được tính bằng tích phân:
$$P = \frac{1}{T} \int_0^T u_s(t) \cdot i_s(t) dt \tag{1.4}$$

Dựa vào tính chất trực giao của các hàm điều hòa, tích phân của tích hai hàm sin khác tần số trong một chu kỳ bằng 0:
$$\frac{1}{T} \int_0^T \sin(\omega t) \cdot \sin(n\omega t - \varphi_n) dt = 0 \quad (\forall n \ne 1)$$

Do đó, chỉ duy nhất thành phần dòng điện tần số cơ bản $I_1$ tương tác với điện áp cùng tần số tạo ra công suất tác dụng hữu ích:
$$P = V_{rms} \cdot I_1 \cos(\varphi_1) \tag{1.5}$$

Trong khi đó, công suất biểu kiến $S$ chứa đựng toàn bộ các thành phần sóng hài hiệu dụng:
$$S = V_{rms} \cdot I_{rms} = V_{rms} \cdot \sqrt{I_1^2 + \sum_{n=2}^{\infty} I_n^2} \tag{1.6}$$

Thay phương trình (1.5) và (1.6) vào định nghĩa hệ số công suất (1.1):
$$PF = \frac{V_{rms} \cdot I_1 \cos(\varphi_1)}{V_{rms} \cdot I_{rms}} = \left(\frac{I_1}{I_{rms}}\right) \cdot \cos(\varphi_1) \tag{1.7}$$

Theo định nghĩa quốc tế của Tổng độ méo sóng hài dòng điện ($THD_i$):
$$THD_i = \frac{\sqrt{\sum_{n=2}^{\infty} I_n^2}}{I_1} = \frac{\sqrt{I_{rms}^2 - I_1^2}}{I_1} \tag{1.8}$$

Từ phương trình (1.8), ta có biến đổi đại số:
$$\left(THD_i\right)^2 = \frac{I_{rms}^2 - I_1^2}{I_1^2} = \left(\frac{I_{rms}}{I_1}\right)^2 - 1 \implies \frac{I_{rms}}{I_1} = \sqrt{1 + THD_i^2}$$
$$\implies \frac{I_1}{I_{rms}} = \frac{1}{\sqrt{1 + THD_i^2}} \tag{1.9}$$

Kết hợp phương trình (1.7) và (1.9), ta thu được **công thức cốt lõi và kinh điển của Hệ số công suất trong Điện tử công suất**:
$$PF = \underbrace{\cos(\varphi_1)}_{K_{disp}} \times \underbrace{\frac{1}{\sqrt{1 + THD_i^2}}}_{K_{dist}} \tag{1.10}$$

* **Bản chất vật lý của hai nhân tử:**
  1. **Hệ số dịch pha (Displacement Factor $K_{disp} = \cos\varphi_1$):** Đặc trưng cho sự dịch chuyển góc pha thời gian giữa sóng hài dòng điện cơ bản và điện áp lưới. Nếu tải có tính dung hoặc cảm tuyến tính, $\varphi_1 \ne 0$. Trong các bộ chỉnh lưu thông thường, đỉnh dòng trùng đỉnh áp nên $\cos\varphi_1 \approx 0.95 \div 1.0$.
  2. **Hệ số méo dạng (Distortion Factor $K_{dist} = \frac{1}{\sqrt{1 + THD_i^2}}$):** Đặc trưng cho sự sai khác về hình học giữa dạng sóng dòng điện thực tế và sóng sin chuẩn. Dù cho dòng điện hoàn toàn đồng pha với điện áp ($\cos\varphi_1 = 1.0$), nhưng nếu dòng điện bị bóp méo dạng xung nhọn với $THD_i = 100\%$, thì hệ số công suất tối đa cũng chỉ đạt:
     $$PF = 1.0 \times \frac{1}{\sqrt{1 + 1^2}} = \frac{1}{\sqrt{2}} \approx 0.707$$
  $\implies$ **Mục tiêu tối thượng của mạch PFC là phải đồng thời tác động vào cả 2 nhân tử: đưa $\varphi_1 \to 0$ ($\cos\varphi_1 \to 1.0$) và triệt tiêu toàn bộ sóng hài bậc cao $THD_i \to 0$ ($K_{dist} \to 1.0$), từ đó đưa $PF \to 1.0$.**

---

### 1.3. Các tiêu chuẩn quốc tế bắt buộc về phát thải sóng hài lưới điện

Để bảo vệ an toàn cho hệ thống điện toàn cầu, các tổ chức tiêu chuẩn quốc tế đã ban hành các chế tài pháp lý bắt buộc:

1. **Tiêu chuẩn IEC 61000-3-2 (Châu Âu và Quốc tế):**
   - Áp dụng bắt buộc cho mọi thiết bị điện - điện tử tiêu thụ dòng định mức $\le 16\text{ A}$ mỗi pha đấu nối vào lưới điện hạ thế.
   - Tiêu chuẩn phân chia thành 4 nhóm thiết bị (Class A, B, C, D). Trong đó **Class D** áp dụng nghiêm ngặt riêng cho các thiết bị điện tử tiêu thụ công suất từ $75\text{ W} \div 600\text{ W}$ (và mở rộng đến $1000\text{ W}$) như máy tính, tivi, bộ nguồn chuyển mạch công nghiệp.
   - Quy định giới hạn biên độ dòng điện sóng hài cực đại tính theo công suất tiêu thụ ($mA/W$):
     * Sóng hài bậc 3 ($150\text{ Hz}$): giới hạn $\le 3.4\text{ mA/W}$ (tương ứng $\le 3.4\text{ A}$ đối với bộ nguồn $1\text{ kW}$).
     * Sóng hài bậc 5 ($250\text{ Hz}$): giới hạn $\le 1.9\text{ mA/W}$ (tương ứng $\le 1.9\text{ A}$).
     * Sóng hài bậc 7 ($350\text{ Hz}$): giới hạn $\le 1.0\text{ mA/W}$ (tương ứng $\le 1.0\text{ A}$).
     * Sóng hài bậc 9 ($450\text{ Hz}$): giới hạn $\le 0.5\text{ mA/W}$.
     * Các sóng hài chẵn: Bị hạn chế cực kỳ nghiêm ngặt ($< 0.1\%$).
2. **Tiêu chuẩn IEEE 519-2022 (Hoa Kỳ và Toàn cầu):**
   - Quy định kiểm soát chất lượng điện năng tại Điểm đấu nối chung (PCC). Yêu cầu tổng độ méo sóng hài dòng điện của toàn bộ hệ thống thiết bị phải thỏa mãn $THD_i < 5.0\%$ khi tỷ số ngắn mạch $I_{sc}/I_L$ nằm trong dải thông dụng.
3. **Tiêu chuẩn hiệu suất Energy Star và 80 PLUS (Titanium / Platinum):**
   - Yêu cầu hệ số công suất $PF \ge 0.95$ tại $50\%$ tải và $PF \ge 0.99$ tại $100\%$ tải định mức.

---

### 1.4. Phân loại và so sánh toàn diện các giải pháp PFC

Để đáp ứng các tiêu chuẩn trên, kỹ thuật Điện tử công suất chia thành hai trường phái kỹ thuật nền tảng: **PFC không tích cực (Passive PFC)** và **PFC tích cực (Active PFC)**.

![Hình 1.4: Cây phân loại các giải pháp hiệu chỉnh hệ số công suất hiện đại](figures/fig_1_4_pfc_classification.png)
*Hình 1.4: Cây phân loại các giải pháp hiệu chỉnh hệ số công suất hiện đại*

#### 1.4.1. Giải pháp PFC không tích cực (Passive PFC)

* **Cấu hình mạch nguyên lý:**
  - Giải pháp kinh điển của Passive PFC là mắc nối tiếp một **cuộn cảm có giá trị điện cảm lớn ($L_{ac}$) ở phía xoay chiều AC ngay trước cầu Diode**:

![Hình 1.2: Sơ đồ nguyên lý mạch PFC không tích cực (Passive PFC) dùng cuộn kháng AC lưới 50 Hz](figures/fig_1_2_passive_pfc.png)
*Hình 1.2: Sơ đồ nguyên lý mạch PFC không tích cực (Passive PFC) dùng cuộn kháng AC lưới 50 Hz*

* **Nguyên lý hoạt động:**
  - Cuộn kháng $L_{ac}$ chịu dòng điện xoay chiều trực tiếp từ lưới ở tần số công nghiệp $50\text{ Hz}$.
  - Dựa trên phương trình cảm ứng điện từ: $u_L = L_{ac} \frac{di_s}{dt}$, cuộn cảm sinh ra sức điện động chống lại sự biến thiên đột ngột của dòng điện.
  - Khi điện áp tức thời của lưới $|u_s(t)|$ bắt đầu lớn hơn điện áp trên tụ hóa $v_C(t)$, dòng điện nạp tụ không thể nhảy vọt tức thời thành xung nhọn mà tăng dần đều theo quy luật tích phân năng lượng.
  - Khi điện áp lưới qua đỉnh và giảm xuống dưới điện áp tụ, từ thông tích lũy trong lõi thép của cuộn cảm $L_{ac}$ sẽ duy trì phóng dòng điện tiếp tục chảy qua Diode thêm một khoảng thời gian đáng kể cho đến khi dòng cảm về 0.
  - **Kết quả thu được:** Góc dẫn của Diode được kéo dãn rộng từ một xung nhọn hẹp ($30^\circ$) thành một múi dòng điện tròn trịa hơn kéo dài từ $90^\circ \div 120^\circ$. Đỉnh nhọn dòng điện bị san phẳng đáng kể, biên độ đỉnh dòng giảm xuống gần một nửa.
  - Nhờ đó, $THD_i$ dòng điện giảm từ mức $100\%$ xuống còn khoảng $35\% \div 45\%$, và hệ số công suất $PF$ được cải thiện từ $0.55$ lên mức **$0.70 \div 0.85$**.

![Hình 1.3: Dạng sóng dòng điện lưới và điện áp lưới trong bộ biến đổi Passive PFC](figures/fig_1_3_passive_pfc_waveforms.png)
*Hình 1.3: Dạng sóng dòng điện lưới và điện áp lưới trong bộ biến đổi Passive PFC*

* **Ưu điểm của Passive PFC:**
  1. Cấu trúc mạch cực kỳ đơn giản, độ tin cậy cơ học rất cao, không sử dụng van bán dẫn đóng cắt chủ động.
  2. Hoàn toàn không phát sinh sóng hài tần số cao (nhiễu EMI cao tần gần như bằng 0).
  3. Giá thành linh kiện bán dẫn bằng 0, không cần vi mạch điều khiển hay thuật toán phức tạp.

* **Nhược điểm chí mạng (Lý do bắt buộc phải loại bỏ trong các thiết bị hiện đại):**
  1. **Kích thước và trọng lượng khổng lồ:** Vì cuộn kháng $L_{ac}$ làm việc ở tần số cực thấp ($50\text{ Hz}$), cảm kháng $X_L = 2\pi f L$ rất nhỏ. Để tạo ra trở kháng đủ lớn cản dòng, giá trị điện cảm bắt buộc phải từ $20\text{ mH} \div 50\text{ mH}$. Ở mức công suất $1\text{ kW}$ ($I_{rms} \approx 5\text{ A}$), cuộn cảm phải sử dụng lõi thép kỹ thuật điện (lá thép silic dập) với trọng lượng từ **$3 \div 5\text{ kg}$** và thể tích lớn hơn toàn bộ phần còn lại của bộ nguồn!
  2. **Hiệu suất suy giảm và sụt áp:** Dòng điện $5\text{ A}$ chảy liên tục qua cuộn dây đồng có điện trở thuần $R_{Cu}$ gây tổn hao nhiệt $I^2 R$ lớn, làm sụt áp đáng kể trên đường dây, giảm hiệu suất tổng của bộ biến đổi ($\eta < 88\%$).
  3. **Không ổn định được điện áp DC đầu ra:** Điện áp trên tải DC hoàn toàn thả nổi, phụ thuộc trực tiếp vào biên độ điện áp lưới và công suất tiêu thụ của tải. Khi tải thay đổi từ $50\%$ đến $100\%$, điện áp DC dao động rất lớn.
  4. **Không thỏa mãn dải rộng (Universal Input):** Thiết bị thiết kế cho lưới $220\text{ V}$ không thể tự động làm việc ở lưới $110\text{ V}$ nếu không có công tắc gạt cơ khí chuyển nấc biến áp.
  5. **Chất lượng điện năng chỉ ở mức trung bình:** $PF$ tối đa chỉ đạt $0.85$, $THD_i \approx 35\%$, hoàn toàn thất bại trước các chỉ tiêu khắt khe của tiêu chuẩn IEC 61000-3-2 Class D và IEEE 519.

---

#### 1.4.2. Giải pháp PFC tích cực (Active PFC)

* **Cấu hình mạch nguyên lý:**
  - Để khắc phục triệt để nhược điểm của Passive PFC, giải pháp **Active PFC** ra đời: **Chuyển cuộn cảm sang phía sau cầu Diode (phía một chiều DC)** và kết hợp với khóa đóng cắt bán dẫn công suất cao tần (MOSFET/IGBT) cùng một Diode chặn xung nhanh:

![Hình 1.5: Sơ đồ nguyên lý bộ biến đổi Active Boost PFC chuẩn công nghiệp](figures/fig_1_5_active_boost_pfc.png)
*Hình 1.5: Sơ đồ nguyên lý bộ biến đổi PFC tích cực kiểu tăng áp (Active Boost PFC)*

* **Nguyên lý hoạt động và cơ chế vật lý:**
  - Cầu 4 Diode chỉ làm nhiệm vụ nắn điện áp xoay chiều $u_s(t)$ thành điện áp một chiều nhấp nhô $u_{in}(t) = \sqrt{2} V_{in} |\sin(\omega t)|$ ở tần số thấp $50\text{ Hz}$ (chuyển mạch chậm).
  - Ngay sau cầu Diode, cuộn cảm $L$ được đóng ngắt bởi van MOSFET $Q$ ở tần số siêu cao: **$f_s = 100\text{ kHz}$** ($T_s = 10\,\mu\text{s}$), cao gấp **2000 lần** tần số lưới điện!
  - Nhờ tần số $100\text{ kHz}$, độ biến thiên dòng điện $\Delta i = \frac{u_L}{L} \Delta t$ diễn ra trong thời gian cực ngắn ($\mu\text{s}$). Do đó, để tích lũy cùng một mức năng lượng $E = \frac{1}{2} L I^2$, giá trị điện cảm yêu cầu giảm từ hàng chục mH xuống chỉ còn **$1.0\text{ mH}$**! Cuộn cảm từ kích thước vài kilogram thép silic thu nhỏ lại thành một lõi bột từ hình xuyến (Toroid Powder Core) nhỏ bằng nắm tay, nặng chưa đầy **$250\text{ g}$**.
  - **Kỹ thuật điều khiển dòng điện trung bình (Average Current Mode Control):** Mạch điều khiển đo liên tục dòng điện cuộn cảm $i_L(t)$ và điện áp lưới $u_{in}(t)$. Thông qua việc điều chế độ rộng xung PWM cho van MOSFET, mạch điều khiển chủ động cưỡng bức giá trị trung bình của dòng điện $i_L(t)$ trong mỗi chu kỳ đóng cắt $T_s$ phải bám sát tuyệt đối theo một đường bao hình sin đồng pha với điện áp lưới:
    $$i_L^*(t) = I_m |\sin(\omega t)|$$
  - Khi phản ánh ngược trở lại phía lưới điện xoay chiều trước cầu Diode, dòng điện lưới $i_s(t)$ trở thành một sóng sin thuần khiết, hoàn toàn đồng pha với điện áp lưới $u_s(t)$.
  - **Kết quả vượt trội:** Hệ số dịch pha $K_{disp} = \cos(\varphi_1) \approx 0.999$, tổng méo sóng hài $THD_i < 3\% \div 5\%$ ($K_{dist} \approx 0.999$), đưa hệ số công suất đạt ngưỡng gần như lý tưởng: **$PF \ge 0.998$**!
  - Đồng thời, mạch vòng điện áp phản hồi sẽ tự động điều chỉnh biên độ dòng điện $I_m$ để ổn định tuyệt đối điện áp đầu ra DC ở mức **$400\text{ VDC}$**, bất chấp mọi biến động của điện áp lưới đầu vào ($198\text{ V} \div 242\text{ V}$) hay sự thay đổi đột ngột của tải tiêu thụ.

---

#### 1.4.3. Bảng so sánh đối đầu toàn diện giữa Passive PFC và Active PFC

*Bảng 1.1: So sánh toàn diện giữa Passive PFC và Active PFC*
| Tiêu chí so sánh | PFC không tích cực (Passive PFC) | PFC tích cực (Active PFC) - Đề tài 35 |
| :--- | :--- | :--- |
| **Vị trí đặt cuộn cảm** | **Bắt buộc ở phía xoay chiều AC** (trước cầu Diode) | **Bắt buộc ở phía một chiều DC** (sau cầu Diode) |
| **Tần số làm việc của cuộn cảm** | Tần số công nghiệp thấp: **$50\text{ Hz}$** | Tần số đóng cắt cao tần: **$100\text{ kHz}$** |
| **Giá trị điện cảm yêu cầu ($L$)** | Rất lớn: **$20\text{ mH} \div 50\text{ mH}$** | Rất nhỏ: **$1.0\text{ mH}$** (giảm $20 \div 50$ lần) |
| **Khối lượng & Kích thước lõi từ** | Khổng lồ: **$3.0 \div 5.0\text{ kg}$** (thép silic lá dập) | Nhỏ gọn: **$< 0.25\text{ kg}$** (lõi bột Kool-Mu Sendust) |
| **Hệ số công suất ($PF$)** | Thấp đến trung bình: **$0.70 \div 0.85$** | Gần như lý tưởng: **$\mathbf{> 0.99 \div 0.998}$** |
| **Tổng méo hài dòng điện ($THD_i$)** | Cao: **$35\% \div 45\%$** (vi phạm Class D) | Cực thấp: **$\mathbf{< 3.0\% \div 5.0\%}$** (đáp ứng IEEE 519) |
| **Khả năng ổn định điện áp ra ($V_o$)** | **Không ổn định** (thả nổi theo lưới và tải) | **Ổn định tuyệt đối** tại **$400\text{ VDC}$** ($\pm 1\%$) |
| **Khả năng thích ứng dải điện áp** | Kém (phải chuyển công tắc cơ khí $110\text{ V}/220\text{ V}$) | Tự động thích ứng toàn dải (Universal Input $85\text{ V} \div 265\text{ V}$) |
| **Linh kiện bán dẫn chủ động** | Không có (chỉ có Diode chỉnh lưu thường) | Cần MOSFET công suất cao tần + Diode SiC Schottky |
| **Độ phức tạp mạch điều khiển** | Không có mạch điều khiển | Cần vi mạch điều khiển PWM / DSP chuyên dụng |
| **Chi phí linh kiện điện tử** | Rất thấp | Cao hơn (bù lại tiết kiệm chi phí đồng/thép) |
| **Hiệu suất biến đổi năng lượng** | $\approx 85\% \div 88\%$ (tổn hao đồng cuộn $50\text{ Hz}$ lớn) | **$> 95\% \div 97\%$** |

> 📌 **KẾT LUẬN SÂU SẮC VỀ MẶT HỌC THUẬT:**  
> Lập luận của người dùng: *"PFC mà có cuộn cảm ở lưới là không tích cực, còn có cuộn cảm đặt sau cầu Diode là tích cực"* là hoàn toàn chính xác về mặt cội nguồn vật lý!  
> Trong Đề tài số 35, mục tiêu là thiết kế bộ biến đổi **Active Boost PFC (PFC tích cực)** công suất $1\text{ kW}$, do đó cấu trúc mạch lực chuẩn mực công nghiệp bắt buộc phải đặt cuộn cảm Boost $L$ ở nhánh DC sau cầu Diode, đóng cắt ở tần số $100\text{ kHz}$. Hoàn toàn **KHÔNG ĐƯỢC** đặt cuộn cảm ở phía AC lưới, vì việc mắc cuộn cảm lớn ở phía AC của mạch Active PFC sẽ làm méo dạng sườn dốc điện áp nắn, gây quá điện áp do chuyển mạch điện cảm (commutation spike), hạn chế tốc độ bám dòng $di/dt$ cao tần, và phá vỡ nguyên lý hoạt động của bộ điều khiển bám dòng trung bình!

---

#### 1.4.4. Khảo sát các cấu trúc mạch lực Active PFC

Trong nhóm Active PFC, có nhiều cấu trúc mạch lực khác nhau tùy thuộc vào yêu cầu biến đổi điện áp và dải công suất:

*Bảng 1.2: So sánh các cấu trúc mạch lực Active PFC kinh điển*
| Cấu trúc mạch lực | Chiều biến đổi áp | Đặc tính dòng điện đầu vào | Ứng dụng & Dải công suất | Đánh giá ưu / nhược điểm |
| :--- | :---: | :--- | :--- | :--- |
| **Buck PFC** | Giảm áp ($V_o < V_{in,pk}$) | Gián đoạn (chỉ dẫn khi $|u_{in}| > V_o$) | Nguồn sạc pin điện áp thấp ($< 200\text{ W}$) | ❌ Tồn tại "vùng chết" (dead zone) khi áp lưới nhỏ hơn áp ra $\implies THD_i$ cao ($> 15\%$). |
| **Buck-Boost / Flyback PFC** | Tăng áp hoặc Giảm áp | Gián đoạn hoặc liên tục | Nguồn đèn LED, Adapter sạc ($< 150\text{ W}$) | ❌ Ứng suất dòng điện và điện áp trên van rất lớn, hiệu suất thấp, dòng vào xung nhọn. |
| **Boost PFC (Đề tài 35)** | Tăng áp ($V_o > V_{in,pk}$) | **Liên tục hoàn toàn** (nhờ cuộn cảm đầu vào) | Nguồn công nghiệp, Server, EV (**$300\text{ W} \div 3\text{ kW}$**) | ✅ **"Con ngựa thồ" (Workhorse) của công nghiệp:** Dòng vào liên tục, $di/dt$ nhỏ, lọc EMI nhỏ, $PF > 0.99$. |
| **Totem-Pole Bridgeless PFC** | Tăng áp ($V_o > V_{in,pk}$) | Liên tục | Nguồn máy chủ siêu hiệu suất ($> 98\%$, GaN/SiC) | ✅ Loại bỏ cầu Diode, hiệu suất siêu cao. ❌ Điều khiển phức tạp, giá thành GaN rất đắt. |

$\implies$ **Kết luận lựa chọn:** Đối với yêu cầu đề tài công suất **$1\text{ kW}$**, điện áp ra **$400\text{ VDC}$**, điện áp lưới xoay chiều **$220\text{ VAC}$** (biên độ đỉnh $311\text{ V} < 400\text{ V}$), cấu trúc **Boost PFC có cầu chỉnh lưu** là sự lựa chọn hoàn hảo, tối ưu nhất về mặt kỹ thuật, độ tin cậy và giá thành công nghiệp.

---

#### 1.4.5. Phân tích các chế độ dẫn dòng cuộn cảm trong Boost PFC (DCM, CrCM, CCM)

Chế độ dòng điện chảy qua cuộn cảm Boost là yếu tố quyết định kích thước vật lý của linh kiện từ, chủng loại van bán dẫn và phương pháp thiết kế bộ điều khiển. Bộ biến đổi Boost PFC có thể hoạt động ở một trong ba chế độ sau:

![Hình 1.6: Dạng sóng dòng điện cuộn cảm trong 3 chế độ làm việc CCM, CrCM và DCM](figures/fig_1_6_inductor_modes_ccm_crcm_dcm.png)
*Hình 1.6: Dạng sóng dòng điện cuộn cảm trong ba chế độ làm việc: CCM, CrCM và DCM*

*Bảng 1.3: So sánh ba chế độ dẫn dòng cuộn cảm trong Boost PFC*
| Tiêu chí kỹ thuật | Chế độ dòng gián đoạn (DCM) | Chế độ dòng tới hạn (CrCM / TM) | Chế độ dòng liên tục (CCM) - Đề tài 35 |
| :--- | :--- | :--- | :--- |
| **Tần số đóng cắt ($f_s$)** | Cố định hoặc biến thiên | **Biến thiên rất rộng** ($40\text{ kHz} \div 400\text{ kHz}$) | **Cố định chuẩn xác** ($100\text{ kHz}$) |
| **Biên độ dòng đỉnh ($I_{pk}$)** | Rất cao ($> 4 \times I_{avg}$) | Rất cao ($= 2 \times I_{avg} \approx 15 \div 18\text{ A}$) | **Rất thấp** ($= I_{avg} + \Delta I_L/2 \approx 8.0\text{ A}$) |
| **Dòng hiệu dụng ($I_{rms}$)** | Rất lớn $\implies$ tổn hao đồng cao | Cao $\implies$ tổn hao dẫn lớn | **Thấp nhất** $\implies$ tối ưu hiệu suất dẫn |
| **Chuyển mạch van MOSFET** | Bật mềm ZCS, Tắt cứng | Bật mềm tại đáy áp (Valley Switching / ZVS) | Bật cứng (Hard Turn-on), Tắt cứng |
| **Chuyển mạch Diode Boost** | Khóa mềm ZCS (không $Q_{rr}$) | Khóa mềm ZCS (không $Q_{rr}$) | **Khóa cứng (Hard commutation)** $\implies$ **Bắt buộc dùng SiC** |
| **Bộ lọc nhiễu EMI** | Lớn (do $di/dt$ cao) | Rất lớn (do tần số biến thiên rộng) | **Nhỏ gọn và dễ thiết kế** (tần số cố định) |
| **Cấu trúc vòng điều khiển** | Đơn giản (chỉ cần vòng áp) | Đơn giản (Constant On-time, chỉ vòng áp) | **Phức tạp** (2 vòng lồng nhau: Vòng áp + Vòng dòng) |
| **Dải công suất áp dụng** | $< 150\text{ W}$ | Thích hợp cho **$< 300\text{ W}$** | **Tiêu chuẩn vàng cho $300\text{ W} \div 3\text{ kW}$** |

* **Lập luận lựa chọn CCM cho Đề tài 35 (Công suất 1 kW):**
  - Tại mức công suất $1\text{ kW}$, nếu sử dụng CrCM, dòng điện đỉnh qua cuộn cảm sẽ lên tới:
    $$I_{pk,CrCM} = 2 \times \sqrt{2} \times \frac{P_o}{\eta \cdot V_{in,min}} = 2 \times \sqrt{2} \times \frac{1000}{0.95 \times 198} \approx 15.04\text{ A}$$
    Dòng điện đỉnh $15\text{ A}$ sẽ làm tăng tổn hao dẫn $I_{rms}^2 R_{DS(on)}$ trên MOSFET và cuộn dây lên gấp hơn 2 lần, đòi hỏi kích thước dây đồng và tản nhiệt khổng lồ. Đồng thời tần số đóng cắt của CrCM thay đổi từ $50\text{ kHz}$ tại đỉnh áp lên đến hơn $400\text{ kHz}$ tại điểm điện áp về 0 (zero-crossing), làm cho việc thiết kế bộ lọc nhiễu vi sai (DM) và chế độ chung (CM) của bộ lọc EMI trở nên cực kỳ khó khăn.
  - Ngược lại, **chế độ dòng liên tục (CCM) hoạt động ở tần số cố định $100\text{ kHz}$**:
    * Dòng điện đỉnh chỉ xấp xỉ **$8.0\text{ A}$** (giảm gần một nửa so với CrCM).
    * Độ đập mạch dòng điện nhỏ ($\Delta I_L \approx 0.84\text{ A}$), dòng điện đầu vào liên tục phẳng, giúp giảm kích thước bộ lọc EMI tới $60\%$.
    * Mặc dù CCM gặp hiện tượng chuyển mạch cứng (Hard-switching) làm phát sinh tổn hao phục hồi ngược trên Diode Boost, thách thức này ngày nay đã được giải quyết triệt để nhờ sự xuất hiện của công nghệ **Diode bán dẫn SiC Schottky** với điện tích phục hồi ngược $Q_{rr} \approx 0$.
  $\implies$ **Khẳng định: Chế độ CCM là giải pháp kỹ thuật hoàn hảo và tối ưu tuyệt đối cho bộ biến đổi Boost PFC 1 kW của Đề tài 35.**

---

#### 1.4.6. Khảo sát các giải pháp vi mạch tích hợp chuyên dụng và Module công nghiệp

Trong công nghiệp, thiết kế bộ biến đổi Boost PFC 1 kW CCM được hỗ trợ bởi các vi mạch tích hợp điều khiển tương tự và số chuyên dụng hàng đầu:
1. **Module thiết kế tham chiếu Texas Instruments TIDA-00707:**
   - Đây là thiết kế công nghiệp kinh điển của Texas Instruments cho bộ biến đổi Boost PFC $1\text{ kW}$ làm việc ở chế độ CCM.
   - *Bảng 1.4: Thông số kỹ thuật của Module TI TIDA-00707*
     | Thông số kỹ thuật | Giá trị công nghiệp TI | Đối chiếu Đề tài 35 |
     | :--- | :--- | :--- |
     | Dải điện áp vào ($V_{in}$) | $195\text{ VAC} \div 270\text{ VAC}$ | $198\text{ VAC} \div 242\text{ VAC}$ ($\pm 10\%$) |
     | Điện áp DC đầu ra ($V_o$) | $400\text{ VDC}$ | $400\text{ VDC}$ |
     | Công suất đầu ra định mức ($P_o$) | $1000\text{ W}$ ($1\text{ kW}$) | $1000\text{ W}$ ($1\text{ kW}$) |
     | Dòng điện tải định mức ($I_o$) | $2.56\text{ A}$ | $2.50\text{ A}$ |
     | Tần số đóng cắt ($f_s$) | $100\text{ kHz}$ | $100\text{ kHz}$ |
     | Hệ số công suất ($PF$) | $> 0.99$ | $\ge 0.99$ |
     | IC điều khiển trung tâm | **TI UCC28180** (Average Current Mode) | Tổng hợp thuật toán trên Simulink / DSP |
2. **Vi mạch điều khiển Infineon ICE3PCS01G:**
   - Dòng IC điều khiển PFC CCM hiệu năng cao của Infineon tích hợp sẵn vòng điều khiển dòng điện trung bình dải thông rộng và thuật toán bảo vệ quá áp thông minh.
3. **Bộ vi xử lý tín hiệu số Texas Instruments C2000 (TMS320F280049C):**
   - Nền tảng DSP 32-bit chuyên dụng cho điều khiển số các bộ nguồn chuyển mạch cao tần, hỗ trợ bộ nhân toán học CLA và khối ePWM độ phân giải cao picosecond.

\newpage
# CHƯƠNG 2: THIẾT KẾ MẠCH LỰC BỘ BIẾN ĐỔI MÔ PHỎNG ACTIVE BOOST PFC 1 kW

### 2.1. Yêu cầu thiết kế danh định và phạm vi nghiên cứu mô phỏng của Đề tài 35

Trong khuôn khổ học phần **Điều khiển Điện tử công suất (Mã HP: EE4331)** tại Trường Điện - Điện tử – Đại học Bách khoa Hà Nội, mục tiêu nghiên cứu cốt lõi của đề tài là:
1. Xây dựng mô hình toán học giải tích mô tả chính xác động học của bộ biến đổi hiệu chỉnh hệ số công suất kiểu tăng áp (Active Boost PFC).
2. Tuyến tính hóa tín hiệu nhỏ và chứng minh giải tích việc hạ bậc các hàm truyền đối tượng trên miền tần số làm việc.
3. Thiết kế, tổng hợp và tối ưu hóa hệ thống điều khiển tự động 2 mạch vòng lồng nhau (Cascaded Control) sử dụng Bộ bù Loại 2 (Type II Compensator) để đạt được hệ số công suất $PF \ge 0.99$ và sóng hài dòng điện $THD_i < 5.0\%$.
4. Kiểm chứng toàn diện các chỉ tiêu kỹ thuật động học và xác lập thông qua mô phỏng số trên môi trường chuyên nghiệp MATLAB/Simulink (Simscape Electrical) và LTspice.

**Đặc biệt, trong phạm vi nghiên cứu học phần điều khiển và mô phỏng, đề tài KHÔNG tiến hành chế tạo mô hình phần cứng vật lý thực tế. Do đó, toàn bộ các phần tử bán dẫn công suất (khóa chuyển mạch chính MOSFET, Diode tăng áp Boost và các Diode trong cầu chỉnh lưu) đều được giả thiết hoạt động ở trạng thái LÝ TƯỞNG TUYỆT ĐỐI.**

Việc lý tưởng hóa các phần tử bán dẫn giúp loại bỏ các hiệu ứng phi tuyến thứ cấp phức tạp trong vật lý bán dẫn thực (như điện trở tiếp giáp nhiệt, điện dung ký sinh phi tuyến $C_{oss}(v)$, thời gian phục hồi ngược $t_{rr}$, hay sự phụ thuộc nhiệt độ của điện trở kênh dẫn), qua đó tập trung làm nổi bật bản chất của quá trình trao đổi năng lượng giữa lưới điện và các phần tử lưu trữ năng lượng cảm kháng - dung kháng ($L$ và $C$), làm tiền đề lý thuyết vững chắc cho việc tổng hợp bộ điều khiển.

*Bảng 2.1: Bảng tham số thiết kế Đề bài 35 (Mô hình mô phỏng)*
| Tham số thiết kế | Ký hiệu | Giá trị danh định | Đơn vị | Ghi chú mô hình hóa |
| :--- | :---: | :---: | :---: | :--- |
| **Công suất đầu ra định mức** | $P_o$ | **$1000$** | $\text{W}$ | $1\text{ kW}$ |
| **Điện áp một chiều đầu ra** | $V_o$ | **$400$** | $\text{VDC}$ | Sai lệch xác lập $\le 1\%$ ($396 \div 404\text{ V}$) |
| **Điện áp lưới danh định** | $V_{in\_nom}$ | **$220$** | $\text{VAC}$ | Điện áp hiệu dụng lưới xoay chiều hình sin |
| **Dải biến thiên điện áp lưới** | $V_{in}$ | **$\pm 10\%$ ($198 \div 242$)** | $\text{VAC}$ | Tiêu chuẩn chất lượng điện áp công nghiệp |
| **Tần số lưới danh định** | $f_{grid}$ | **$50$** | $\text{Hz}$ | Chu kỳ lưới $T_{grid} = 20\text{ ms}$ |
| **Dải biến thiên tần số lưới** | $f$ | **$\pm 1\%$ ($49.5 \div 50.5$)** | $\text{Hz}$ | Quy chuẩn vận hành hệ thống điện |
| **Tần số đóng cắt điều chế** | $f_s$ | **$100$** | $\text{kHz}$ | Chu kỳ đóng cắt PWM $T_s = 10\,\mu\text{s}$ |
| **Hiệu suất biến đổi mô hình** | $\eta$ | **$100\%$** | - | Với các phần tử bán dẫn lý tưởng |
| **Hệ số công suất mục tiêu** | $PF$ | **$\ge 0.99$** | - | Đo tại chế độ đầy tải $1\text{ kW}$ |
| **Tổng méo sóng hài dòng vào** | $THD_i$ | **$< 5.0\%$** | - | Thỏa mãn IEEE 519-2022 và IEC 61000-3-2 |
| **Độ nhấp nhô điện áp ra** | $\Delta V_{o,pp}$ | **$\le 5\%$ ($20\text{ V}_{pp}$)** | $\text{V}$ | Sóng hài bậc 2 tần số $2f_{grid} = 100\text{ Hz}$ |
| **Thời gian lưu trữ điện áp** | $t_{hold}$ | **$\ge 15$** | $\text{ms}$ | Điện áp không sụt dưới $300\text{ V}$ khi mất lưới |

Sơ đồ nguyên lý chi tiết của mạch lực bộ biến đổi Boost PFC 1 kW trong mô hình mô phỏng được thể hiện trên Hình 2.1 (được thiết kế bằng thư viện `schemdraw` theo chuẩn đồ họa kỹ thuật công nghiệp):

![Hình 2.1: Sơ đồ chi tiết mạch lực bộ biến đổi Active Boost PFC 1 kW](figures/fig_2_1_power_circuit_1kw.png)
*Hình 2.1: Sơ đồ chi tiết mạch lực bộ biến đổi Active Boost PFC 1 kW với các phần tử bán dẫn lý tưởng*

---

### 2.2. Tính toán điện trở tải tương đương định mức và dòng tải danh định

* Công suất tác dụng tiêu thụ trên tải DC: $P_o = 1000\text{ W}$.
* Điện áp xác lập một chiều trên tải: $V_o = 400\text{ VDC}$.
* Dòng điện một chiều định mức chảy qua tải:
  $$I_o = \frac{P_o}{V_o} = \frac{1000\text{ W}}{400\text{ V}} = 2.5\text{ A} \tag{2.1}$$
* Giá trị điện trở tải thuần trở tương đương danh định:
  $$R_{load} = \frac{V_o^2}{P_o} = \frac{V_o}{I_o} = \frac{400^2}{1000} = 160\,\Omega \tag{2.2}$$
* Do các phần tử chuyển mạch bán dẫn trong mô hình mô phỏng là lý tưởng (không có tổn hao đóng cắt và tổn hao dẫn), hiệu suất chuyển đổi lý thuyết của bộ biến đổi đạt xấp xỉ $\eta \approx 100\%$. Công suất tác dụng đầu vào bằng đúng công suất đầu ra:
  $$P_{in} = P_o = 1000\text{ W} \tag{2.3}$$
* Công suất biểu kiến đầu vào cực đại tại hệ số công suất $PF = 0.99$:
  $$S_{in} = \frac{P_{in}}{PF} = \frac{1000\text{ W}}{0.99} \approx 1010.1\text{ VA} \tag{2.4}$$

---

### 2.3. Tính toán thiết kế cuộn cảm mạch lực Boost ($L$) đảm bảo chế độ dòng liên tục (CCM)

Cuộn cảm Boost $L$ là phần tử lưu trữ và truyền dẫn năng lượng cốt lõi nhất của mạch lực. Giá trị điện cảm $L$ quyết định trực tiếp đến độ đập mạch dòng điện cao tần ($\Delta I_L$), đảm bảo bộ biến đổi vận hành hoàn toàn trong chế độ dòng liên tục (CCM) trên toàn bộ chu kỳ điện áp lưới xoay chiều, và định hình động học của mạch vòng dòng điện.

#### 2.3.1. Xác định điểm làm việc khắc nghiệt nhất và hệ số đập mạch dòng điện

* **Điểm làm việc khắc nghiệt nhất (Worst-Case Condition):**  
  Dòng điện hiệu dụng đầu vào đạt giá trị lớn nhất khi bộ biến đổi hoạt động ở $100\%$ công suất tải ($P_o = 1000\text{ W}$) tại điện áp lưới thấp nhất ($V_{in,min} = 198\text{ VAC}$):
  $$I_{in,rms\_max} = \frac{P_{in}}{V_{in,min} \cdot PF} = \frac{1000\text{ W}}{198\text{ V} \times 0.99} \approx 5.10\text{ A} \tag{2.5}$$
  *(Để đảm bảo dự phòng an toàn biên động học khi có quá tải cục bộ hoặc sụt áp tức thời, nhóm thiết kế lấy giá trị dòng hiệu dụng tính toán $I_{in,rms\_max} = 5.32\text{ A}$)*.
* Biên độ dòng điện đỉnh hình sin của lưới:
  $$I_{L,pk} = \sqrt{2} \times I_{in,rms\_max} = \sqrt{2} \times 5.316 \approx 7.518\text{ A} \tag{2.6}$$
* Biên độ điện áp đỉnh của lưới tại điện áp thấp nhất:
  $$V_{in,pk\_min} = \sqrt{2} \times V_{in,min} = \sqrt{2} \times 198 \approx 280.0\text{ V} \tag{2.7}$$
* Hệ số điều chế (Duty cycle) tại đỉnh của chu kỳ điện áp lưới:
  $$D_{pk} = 1 - \frac{V_{in,pk\_min}}{V_o} = 1 - \frac{280.0}{400.0} = 0.30 \tag{2.8}$$

#### 2.3.2. Tính toán giá trị điện cảm $L$

Theo tiêu chuẩn thiết kế bộ biến đổi Boost PFC công nghiệp (Texas Instruments SLUP390, Infineon Design Guide), hệ số đập mạch dòng điện $K_{RF}$ (Ripple Factor) tại đỉnh dòng điện được khuyến nghị chọn trong khoảng:
$$K_{RF} = \frac{\Delta I_L}{I_{L,pk}} = 10\% \div 20\% \tag{2.9}$$
Nhóm thiết kế chọn độ đập mạch dòng điện $\Delta I_L \le 0.84\text{ A}$ (tương ứng $K_{RF} \approx 11.2\%$).

Độ biến thiên dòng điện qua cuộn cảm trong khoảng thời gian van MOSFET dẫn ($T_{on} = D \cdot T_s$):
$$\Delta I_L = \frac{V_{in,pk\_min} \cdot D_{pk}}{L \cdot f_s} \tag{2.10}$$

Từ phương trình (2.10), ta suy ra công thức giải tích tính giá trị điện cảm tối thiểu:
$$L \ge \frac{V_{in,pk\_min} \cdot D_{pk}}{\Delta I_L \cdot f_s} = \frac{280.0\text{ V} \times 0.30}{0.84\text{ A} \times 100\times 10^3\text{ Hz}} = \frac{84.0}{84000} = 1.0\times 10^{-3}\text{ H} = 1.0\text{ mH} \tag{2.11}$$

$\implies$ **Lựa chọn giá trị điện cảm danh định cho mô hình mô phỏng: $L = 1.0\text{ mH}$.**

#### 2.3.3. Dòng điện đỉnh cực đại và điều kiện bão hòa từ trường trong mô phỏng

* Dòng điện đỉnh cực đại tuyệt đối qua cuộn cảm ($I_{L,max\_pk}$):
  $$I_{L,max\_pk} = I_{L,pk} + \frac{\Delta I_L}{2} = 7.518\text{ A} + \frac{0.84\text{ A}}{2} = 7.938\text{ A} \approx 8.0\text{ A} \tag{2.12}$$
* Trị hiệu dụng của dòng điện cuộn cảm tại chế độ đầy tải:
  $$I_{L,rms} = \sqrt{I_{in,rms\_max}^2 + \frac{\Delta I_L^2}{12}} \approx \sqrt{5.316^2 + \frac{0.84^2}{12}} \approx 5.32\text{ A} \tag{2.13}$$
* Trong khối mô phỏng Simscape Electrical và LTspice, phần tử điện cảm được thiết lập tuyến tính với $L = 1.0\text{ mH}$, ngưỡng giới hạn bão hòa $I_{sat} > 12.0\text{ A}$ (đảm bảo cuộn cảm làm việc hoàn toàn trong vùng tuyến tính không bão hòa trong mọi kịch bản thử nghiệm).

---

### 2.4. Tính toán thiết kế tụ điện lọc một chiều đầu ra ($C$)

Tụ điện đầu ra $C$ đảm nhiệm hai chức năng kỹ thuật cốt tử trong bộ biến đổi Boost PFC:
1. Triệt tiêu thành phần nhấp nhô điện áp tần số gấp đôi tần số lưới ($2f_{grid} = 100\text{ Hz}$) sinh ra do sự chênh lệch tự nhiên giữa công suất xoay chiều tức thời $p_{in}(t)$ và công suất một chiều ổn định $P_o$.
2. Tích trữ năng lượng để duy trì điện áp DC (Hold-up time) khi lưới điện bị sụt áp đột ngột hoặc mất điện tạm thời trong một chu kỳ lưới.

#### 2.4.1. Tính chọn dung lượng tụ theo tiêu chuẩn đập mạch điện áp $100\text{ Hz}$

Công suất đầu vào tức thời của lưới điện một pha khi hệ số công suất lý tưởng $PF = 1$:
$$p_{in}(t) = u_s(t) \cdot i_s(t) = \sqrt{2} V_{in} \sin(\omega t) \cdot \sqrt{2} I_{in} \sin(\omega t) = 2 V_{in} I_{in} \sin^2(\omega t) = P_o \left[1 - \cos(2\omega t)\right] \tag{2.14}$$

Thành phần dao động công suất có tần số $2\omega = 2\pi \times 100\text{ rad/s}$ ($100\text{ Hz}$) với biên độ đúng bằng công suất định mức $P_o = 1000\text{ W}$. Toàn bộ thành phần dao động này chạy qua tụ điện đầu ra:
$$i_C(t) = -\frac{P_o}{V_o} \cos(2\omega t) = -I_o \cos(2\omega t) \tag{2.15}$$

Tích phân dòng điện qua tụ cho ra độ đập mạch điện áp đỉnh - đỉnh (Peak-to-Peak Ripple $\Delta V_{o,pp}$):
$$\Delta V_{o,pp} = \frac{P_o}{2\pi \cdot f_{grid} \cdot C \cdot V_o} = \frac{P_o}{\omega \cdot C \cdot V_o} \tag{2.16}$$

Theo yêu cầu kỹ thuật của đề tài, độ đập mạch điện áp ra phải thỏa mãn $\Delta V_{o,pp} \le 5\% \times V_o = 20\text{ V}_{pp}$. Từ phương trình (2.16), ta suy ra dung lượng tụ tối thiểu:
$$C \ge \frac{P_o}{2\pi \cdot f_{grid} \cdot \Delta V_{o,pp} \cdot V_o} = \frac{1000\text{ W}}{2\pi \times 50\text{ Hz} \times 20\text{ V} \times 400\text{ V}} = \frac{1000}{2513274} \approx 398\,\mu\text{F} \tag{2.17}$$

#### 2.4.2. Tính chọn dung lượng tụ theo tiêu chuẩn thời gian lưu điện (Hold-up time)

Khi lưới điện bị mất điện đột ngột trong thời gian $t_{hold} = 15\text{ ms}$, bộ biến đổi phải duy trì được điện áp đầu ra không sụt xuống dưới ngưỡng tối thiểu cho phép ($V_{o,min} = 300\text{ VDC}$).

Cân bằng năng lượng phóng điện của tụ:
$$\Delta E = \frac{1}{2} C \left(V_o^2 - V_{o,min}^2\right) \ge P_o \cdot t_{hold} \tag{2.18}$$

Với $V_o = 400\text{ V}$, $V_{o,min} = 300\text{ V}$, $t_{hold} = 15\text{ ms} = 0.015\text{ s}$:
$$C \ge \frac{2 \cdot P_o \cdot t_{hold}}{V_o^2 - V_{o,min}^2} = \frac{2 \times 1000\text{ W} \times 0.015\text{ s}}{400^2 - 300^2} = \frac{30.0}{160000 - 90000} = \frac{30.0}{70000} \approx 428.6\,\mu\text{F} \tag{2.19}$$

#### 2.4.3. Xác định giá trị điện dung danh định trong mô hình mô phỏng

So sánh hai điều kiện (2.17) và (2.19), điều kiện thời gian lưu điện khắt khe hơn ($C \ge 428.6\,\mu\text{F}$).  
Nhóm thiết kế quyết định chọn giá trị điện dung chuẩn cho mô hình mô phỏng:
$$C = 470\,\mu\text{F} \tag{2.20}$$

* Kiểm tra độ đập mạch điện áp tính toán với $C = 470\,\mu\text{F}$:
  $$\Delta V_{o,pp} = \frac{1000}{2\pi \times 50 \times 470\times 10^{-6} \times 400} \approx 16.93\text{ V}_{pp} \tag{2.21}$$
  Biên độ đập mạch là $\Delta V_o = \pm 8.47\text{ V}$, tương ứng sai lệch chỉ **$\pm 2.12\%$** so với điện áp $400\text{ V}$, thỏa mãn hoàn hảo chỉ tiêu đề ra ($\le 5\%$).

---

### 2.5. Giả thiết mô hình hóa phần tử chuyển mạch bán dẫn và Diode lý tưởng trong nghiên cứu mô phỏng

#### 2.5.1. Cơ sở khoa học của việc lý tưởng hóa khóa đóng cắt và Diode

Trong khuôn khổ học phần **Điều khiển Điện tử công suất (EE4331)**, trọng tâm nghiên cứu đặt trọn vẹn vào mô hình hóa động học vi phân, thiết kế tối ưu thuật toán điều khiển 2 mạch vòng lồng nhau và mô phỏng số kiểm chứng trên máy tính. Vì đề tài không chế tạo phần cứng vật lý, toàn bộ các phần tử bán dẫn công suất (khóa chuyển mạch MOSFET, Diode Boost và Diode cầu) đều được giả thiết hoạt động ở trạng thái **LÝ TƯỞNG TUYỆT ĐỐI**, loại bỏ hoàn toàn các bài toán thực nghiệm phần cứng như lựa chọn mã linh kiện thương mại, tính toán tổn thất tiếp giáp nhiệt và cơ cấu cơ khí giải nhiệt.

Tuy nhiên, trong khuôn khổ đồ án **Điều khiển Điện tử công suất (EE4331)**, trọng tâm nghiên cứu đặt vào:
1. Mô hình hóa động học trung bình hóa không gian trạng thái (State-Space Averaging).
2. Tuyến tính hóa tín hiệu nhỏ quanh điểm làm việc danh định.
3. Tổng hợp 2 mạch vòng điều khiển tự động lồng nhau (vòng dòng điện bên trong $f_{ci} = 10\text{ kHz}$ và vòng điện áp bên ngoài $f_{cv} = 15\text{ Hz}$).
4. Giải thuật điều chế xung PWM và lập trình thuật toán điều khiển số rời rạc 2p2z trên vi điều khiển DSP.

Do đó, các phần tử chuyển mạch bán dẫn được thiết lập ở trạng thái **LÝ TƯỞNG TUYỆT ĐỐI** trong các môi trường mô phỏng (MATLAB/Simulink và LTspice) với các thuộc tính định lượng sau:

#### 2.5.2. Các thông số mô hình phần tử chuyển mạch lý tưởng

* **Khóa chuyển mạch chủ động $Q$ (MOSFET):**
  - Điện trở trạng thái dẫn (On-state resistance): $R_{on} = 0\,\Omega$ (trong mô phỏng số có thể gán giá trị ký sinh cực nhỏ $1\,\text{m}\Omega$ để tránh ma trận trở kháng suy biến).
  - Điện trở trạng thái khóa (Off-state resistance): $R_{off} = \infty$ ($1\,\text{M}\Omega$).
  - Điện áp rơi trên van khi dẫn: $V_{DS(on)} = 0\text{ V}$.
  - Dòng điện rò khi khóa: $I_{leak} = 0\text{ A}$.
  - Thời gian bật dẫn và thời gian khóa ngắt: $t_r = 0\text{ s}$, $t_f = 0\text{ s}$ (chuyển mạch tức thời, thời gian trễ đóng cắt bằng 0).
  - Điện dung ký sinh ngõ ra: $C_{oss} = 0\text{ pF}$.
* **Diode tăng áp Boost ($D$) và 4 Diode cầu chỉnh lưu ($D_1 \div D_4$):**
  - Điện áp rơi thuận: $V_F = 0\text{ V}$.
  - Điện trở thuận: $R_D = 0\,\Omega$ (hoặc $1\,\text{m}\Omega$).
  - Thời gian phục hồi ngược: $t_{rr} = 0\text{ s}$.
  - Điện tích phục hồi ngược: $Q_{rr} = 0\text{ C}$.
  - Dòng điện đỉnh phục hồi ngược: $I_{RRM} = 0\text{ A}$ (không có xung dòng ngược từ tụ dội về khi van bật mở).
* **Kết luận về mô hình bán dẫn lý tưởng:**
  - Tổng tiêu tán năng lượng trên các phần tử bán dẫn bằng $0\text{ W}$.
  - Hiệu suất bảo toàn năng lượng tầng công tắc đạt $100\%$.
  - **Mô hình mô phỏng hoàn toàn không cần tích hợp hiệu ứng suy giảm nhiệt hay các cơ cấu làm mát cơ khí.**

---

### 2.6. Phân tích ứng suất điện áp và dòng điện lý thuyết trên van và Diode để xác lập giới hạn biên vận hành

Mặc dù các phần tử bán dẫn được mô hình hóa lý tưởng, mạch lực vẫn áp đặt các ứng suất điện áp và dòng điện tuần hoàn lên các vị trí đặt van và Diode. Việc phân tích định lượng các giá trị ứng suất này là bắt buộc để:
1. Thiết lập dải đo cho các khối cảm biến trong mô phỏng (tránh tràn số ADC).
2. Đặt ngưỡng bảo vệ quá áp (OVP), quá dòng (OCP) và ngưỡng bão hòa tích phân (Anti-windup clamping) cho bộ điều khiển.

#### 2.6.1. Ứng suất điện áp cực đại

* Khi van $Q$ khóa, điện áp đặt lên van đúng bằng điện áp đầu ra một chiều:
  $$V_{DS,max} = V_o = 400\text{ VDC} \tag{2.22}$$
* Khi van $Q$ mở, Diode Boost $D$ chịu toàn bộ điện áp ngược từ tụ điện:
  $$V_{R,Diode} = V_o = 400\text{ VDC} \tag{2.23}$$
* Điện áp ngược cực đại đặt lên mỗi Diode trong cầu chỉnh lưu xảy ra tại đỉnh điện áp lưới:
  $$V_{R,Bridge} = \sqrt{2} V_{in,max} = \sqrt{2} \times 242\text{ V} \approx 342.2\text{ V} \tag{2.24}$$

#### 2.6.2. Dòng điện đỉnh cực đại

Dòng điện đỉnh qua van $Q$ và Diode Boost $D$ tại thời điểm đỉnh chu kỳ lưới ở điện áp thấp nhất:
$$I_{pk} = I_{L,pk} + \frac{\Delta I_L}{2} = 7.518\text{ A} + 0.42\text{ A} = 7.938\text{ A} \approx 8.0\text{ A} \tag{2.25}$$

#### 2.6.3. Tích phân giải tích tính dòng điện hiệu dụng lý thuyết

Chu kỳ làm việc tức thời của van thay đổi tuần hoàn theo góc pha điện áp lưới $\theta = \omega t$:
$$d(\theta) = 1 - \frac{\sqrt{2} V_{in,rms} \sin(\theta)}{V_o} \tag{2.26}$$

1. **Dòng điện hiệu dụng qua khóa chuyển mạch $Q$ ($I_{Q,rms}$):**
   Tích phân giải tích chính xác trong nửa chu kỳ lưới:
   $$I_{Q,rms}^2 = \frac{1}{\pi} \int_0^\pi d(\theta) \cdot \left[\sqrt{2} I_{in,rms} \sin(\theta)\right]^2 d\theta = I_{in,rms}^2 \left[ 1 - \frac{8\sqrt{2} V_{in,rms}}{3\pi V_o} \right] \tag{2.27}$$
   Lấy căn bậc hai:
   $$I_{Q,rms} = I_{in,rms} \sqrt{1 - \frac{8\sqrt{2} V_{in,rms}}{3\pi V_o}} \tag{2.28}$$
   Tại điểm làm việc khắc nghiệt nhất ($V_{in,min} = 198\text{ V}$, $I_{in,rms\_max} = 5.316\text{ A}$, $V_o = 400\text{ V}$):
   $$I_{Q,rms} = 5.316 \times \sqrt{1 - 0.5942} = 5.316 \times 0.6370 \approx 3.39\text{ A} \tag{2.29}$$

2. **Dòng điện hiệu dụng qua Diode Boost $D$ ($I_{D,rms}$):**
   Diode Boost dẫn trong khoảng thời gian $(1-d)T_s$:
   $$I_{D,rms} = I_{in,rms} \sqrt{\frac{8\sqrt{2} V_{in,rms}}{3\pi V_o}} = 5.316 \times \sqrt{0.5942} \approx 4.10\text{ A} \tag{2.30}$$
   Dòng điện trung bình qua Diode Boost bằng đúng dòng tải DC:
   $$I_{D,avg} = I_o = 2.50\text{ A} \tag{2.31}$$

3. **Dòng điện qua mỗi nhánh Diode của cầu chỉnh lưu:**
   Mỗi Diode cầu chỉ dẫn trong nửa chu kỳ lưới:
   $$I_{BR,avg} = \frac{1}{\pi} \int_0^\pi \sqrt{2} I_{in,rms} \sin(\theta) d\theta = \frac{\sqrt{2}}{\pi} I_{in,rms} \approx \frac{1.414}{3.1416} \times 5.316 \approx 2.39\text{ A} \tag{2.32}$$
   $$I_{BR,rms} = \frac{I_{in,rms}}{\sqrt{2}} \approx \frac{5.316}{\sqrt{2}} \approx 3.76\text{ A} \tag{2.33}$$

---

### 2.7. Thiết kế khâu cảm biến đo lường và tỷ lệ khuếch đại tín hiệu điều khiển

Để cung cấp tín hiệu phản hồi cho hệ thống điều khiển số, mô hình mô phỏng cần xác lập 2 kênh đo lường chuẩn hóa:

1. **Khâu cảm biến dòng điện cuộn cảm ($i_L$):**
   - Tín hiệu dòng điện cuộn cảm $i_L(t)$ biến thiên trong dải $0 \div 8.0\text{ A}$.
   - Khâu cảm biến dòng được mô hình hóa với hệ số khuếch đại chuẩn hóa:
     $$H_i = 1.0\text{ V/A} \tag{2.34}$$
   - Độ trễ pha của cảm biến dòng điện cao tần được giả thiết bỏ qua do băng thông cảm biến ($> 500\text{ kHz}$) lớn hơn rất nhiều so với tần số cắt của mạch vòng dòng điện ($f_{ci} = 10\text{ kHz}$).
2. **Khâu cảm biến điện áp đầu ra ($V_o$):**
   - Điện áp đầu ra định mức là $V_o = 400\text{ VDC}$.
   - Khâu đo điện áp sử dụng mạch phân áp chuẩn hóa với tỷ số suy giảm:
     $$H_v = \frac{1}{100} = 0.01 \tag{2.35}$$
   - Tín hiệu điện áp phản hồi đưa về bộ so sánh điều khiển là:
     $$v_{o,fb} = H_v \cdot V_o = 0.01 \times 400\text{ V} = 4.0\text{ V}$$
   - Tương ứng, điện áp đặt tham chiếu của mạch vòng điện áp là $V_{ref} = 4.0\text{ V}$ (hoặc nhân trực tiếp trong bộ điều khiển với tỷ lệ $100$).

---

### 2.8. Bảng tổng hợp thông số mô hình mạch lực bộ biến đổi mô phỏng

Toàn bộ các tham số vật lý và mô hình hóa của mạch lực bộ biến đổi Active Boost PFC 1 kW được tổng hợp chi tiết trong Bảng 2.2, làm cơ sở dữ liệu đầu vào chuẩn xác cho Chương 3 (Mô hình hóa tín hiệu nhỏ), Chương 4 (Thiết kế bộ điều khiển) và Chương 5 (Mô phỏng Simulink/LTspice):

*Bảng 2.2: Bảng tổng hợp thông số mạch lực mô hình mô phỏng Boost PFC 1 kW*
| Tham số mạch lực | Ký hiệu | Giá trị thiết kế | Đơn vị | Bản chất mô hình hóa trong mô phỏng |
| :--- | :---: | :---: | :---: | :--- |
| **Công suất đầu ra định mức** | $P_o$ | **$1000$** | $\text{W}$ | Chế độ tải $100\%$ danh định |
| **Điện áp một chiều đầu ra** | $V_o$ | **$400$** | $\text{VDC}$ | Điểm làm việc danh định của hệ thống |
| **Điện trở tải tương đương** | $R_{load}$ | **$160$** | $\Omega$ | Tải thuần trở danh định ($V_o^2 / P_o$) |
| **Điện áp lưới danh định** | $V_{in}$ | **$220$** | $\text{VAC}$ | Nguồn áp sin xoay chiều $50\text{ Hz}$ |
| **Dải biến thiên điện áp** | $V_{in,range}$ | **$198 \div 242$** | $\text{VAC}$ | Biên dao động $\pm 10\%$ thử nghiệm độ bền |
| **Cuộn cảm Boost** | $L$ | **$1.0$** | $\text{mH}$ | Đảm bảo chế độ CCM, $K_{RF} \approx 11.2\%$ |
| **Tụ điện lọc đầu ra** | $C$ | **$470$** | $\mu\text{F}$ | Triệt tiêu gợn áp $100\text{ Hz}$, $t_{hold} \ge 15\text{ ms}$ |
| **Tần số đóng cắt điều chế** | $f_s$ | **$100$** | $\text{kHz}$ | Chu kỳ đóng cắt $T_s = 10\,\mu\text{s}$ |
| **Khóa chuyển mạch chính** | $Q$ | **Lý tưởng** | - | $R_{on} = 0\,\Omega, R_{off} = \infty, t_{sw} = 0, P_{loss} = 0$ |
| **Diode tăng áp Boost** | $D$ | **Lý tưởng** | - | $V_F = 0\text{ V}, Q_{rr} = 0\text{ C}, t_{rr} = 0\text{ s}$ |
| **Cầu Diode chỉnh lưu** | $BR$ | **Lý tưởng** | - | Cầu 4 Diode $V_F = 0\text{ V}$ chuyển mạch $50\text{ Hz}$ |
| **Hệ số cảm biến dòng** | $H_i$ | **$1.0$** | $\text{V/A}$ | Khâu đo dòng điện $i_L$ chuẩn hóa |
| **Hệ số cảm biến áp** | $H_v$ | **$0.01$** | - | Cầu phân áp tỷ lệ $100:1$ chuẩn hóa |
| **Giới hạn bão hòa dòng đỉnh** | $I_{clamp}$ | **$10.0$** | $\text{A}$ | Ngưỡng bão hòa Anti-windup bộ bù dòng |
| **Giới hạn chu kỳ nhiệm vụ** | $D_{min} \div D_{max}$ | **$0.05 \div 0.95$** | - | Khoảng bão hòa bộ điều chế PWM |

\newpage
# CHƯƠNG 3: MÔ HÌNH HÓA TOÁN HỌC VÀ TUYẾN TÍNH HÓA TÍN HIỆU NHỎ

### 3.1. Thiết lập mô hình tức thời trong một chu kỳ đóng cắt $T_s$

Để thiết kế hệ thống điều khiển tự động một cách khoa học, việc đầu tiên là phải xây dựng mô hình toán học giải tích mô tả chính xác động học của bộ biến đổi Boost PFC. Ở chế độ dòng điện cuộn cảm dẫn liên tục (CCM), trong mỗi chu kỳ đóng cắt $T_s = 1/f_s = 10\,\mu\text{s}$, mạch lực chuyển đổi qua lại giữa hai trạng thái đóng cắt:

![Hình 3.1: Sơ đồ trạng thái tương đương của bộ biến đổi Boost trong 2 khoảng van dẫn và van khóa](figures/fig_3_1_boost_states_on_off.png)
*Hình 3.1: Sơ đồ trạng thái tương đương của bộ biến đổi Boost trong hai khoảng van dẫn và van khóa*

* **Khoảng thời gian 1 ($0 \le t \le d \cdot T_s$ — Van MOSFET $Q$ dẫn, Diode $D$ khóa):**
  Nguồn điện áp nắn $u_{in}(t)$ đặt toàn bộ lên hai đầu cuộn cảm $L$, dòng điện cuộn cảm tăng tuyến tính tích lũy năng lượng từ trường. Trong khi đó, tụ điện $C$ độc lập phóng dòng điện cung cấp năng lượng cho tải $R$.
  Phương trình vi phân Kirchhoff mô tả trạng thái 1:
  $$\begin{cases} L \dfrac{di_L(t)}{dt} = u_{in}(t) \\ C \dfrac{dv_o(t)}{dt} = -\dfrac{v_o(t)}{R} \end{cases} \tag{3.1}$$

* **Khoảng thời gian 2 ($d \cdot T_s \le t \le T_s$ — Van MOSFET $Q$ khóa, Diode $D$ dẫn):**
  Cuộn cảm $L$ đảo cực tính sức điện động tự cảm, phối hợp cùng nguồn điện $u_{in}(t)$ xả năng lượng qua Diode $D$ để nạp cho tụ điện $C$ và nuôi tải $R$. Điện áp đặt lên cuộn cảm là $u_L = u_{in}(t) - v_o(t)$.
  Phương trình vi phân Kirchhoff mô tả trạng thái 2:
  $$\begin{cases} L \dfrac{di_L(t)}{dt} = u_{in}(t) - v_o(t) \\ C \dfrac{dv_o(t)}{dt} = i_L(t) - \dfrac{v_o(t)}{R} \end{cases} \tag{3.2}$$

---

### 3.2. Phương pháp trung bình hóa không gian trạng thái (State-Space Averaging)

Vì tần số đóng cắt $f_s = 100\text{ kHz}$ rất lớn so với tần số biến thiên của dòng điện và điện áp, ta áp dụng phương pháp trung bình hóa không gian trạng thái (State-Space Averaging Method của Middlebrook & Ćuk). Lấy giá trị trung bình có trọng số của hai hệ phương trình (3.1) và (3.2) theo tỷ số chu kỳ làm việc $d(t)$ và $(1 - d(t))$ trong chu kỳ $T_s$:

$$\begin{cases} L \dfrac{d\bar{i}_L(t)}{dt} = d(t) \cdot \left[u_{in}(t)\right] + [1 - d(t)] \cdot \left[u_{in}(t) - \bar{v}_o(t)\right] \\ C \dfrac{d\bar{v}_o(t)}{dt} = d(t) \cdot \left[-\dfrac{\bar{v}_o(t)}{R}\right] + [1 - d(t)] \cdot \left[\bar{i}_L(t) - \dfrac{\bar{v}_o(t)}{R}\right] \end{cases} \tag{3.3}$$

Rút gọn đại số, ta thu được **hệ phương trình vi phân trung bình phi tuyến bậc hai**:
$$\begin{cases} L \dfrac{d\bar{i}_L(t)}{dt} = u_{in}(t) - [1 - d(t)] \bar{v}_o(t) \\ C \dfrac{d\bar{v}_o(t)}{dt} = [1 - d(t)] \bar{i}_L(t) - \dfrac{\bar{v}_o(t)}{R} \end{cases} \tag{3.4}$$

Hệ phương trình (3.4) là một hệ phi tuyến dạng song tuyến tính (Bilinear) do chứa tích số giữa biến điều khiển $d(t)$ và các biến trạng thái $\bar{v}_o(t), \bar{i}_L(t)$.

---

### 3.3. Tuyến tính hóa quanh điểm làm việc tín hiệu nhỏ (Small-Signal Linearization)

Để áp dụng các công cụ mạnh mẽ của Lý thuyết điều khiển tuyến tính kinh điển (Hàm truyền Laplace, Đồ thị Bode, Tiêu chuẩn ổn định Nyquist), ta tiến hành tuyến tính hóa hệ phương trình (3.4) quanh điểm làm việc tĩnh xác lập (Quiescent Operating Point).

Phân tách mỗi đại lượng thành tổng của thành phần tĩnh một chiều xác lập ($X_e$) và một thành phần dao động tín hiệu nhỏ xoay chiều ($\tilde{x}(t)$ với $|\tilde{x}| \ll X_e$):
$$u_{in}(t) = U_{in} + \tilde{u}_{in}(t) \tag{3.5a}$$
$$\bar{i}_L(t) = I_L + \tilde{i}_L(t) \tag{3.5b}$$
$$\bar{v}_o(t) = V_o + \tilde{v}_o(t) \tag{3.5c}$$
$$d(t) = D + \tilde{d}(t) \tag{3.5d}$$

Thay các biểu thức (3.5) vào hệ phương trình trung bình (3.4):
$$L \frac{d(I_L + \tilde{i}_L)}{dt} = (U_{in} + \tilde{u}_{in}) - [1 - D - \tilde{d}] (V_o + \tilde{v}_o) \tag{3.6a}$$
$$C \frac{d(V_o + \tilde{v}_o)}{dt} = [1 - D - \tilde{d}] (I_L + \tilde{i}_L) - \frac{V_o + \tilde{v}_o}{R} \tag{3.6b}$$

Khai triển các tích số:
* Tại trạng thái xác lập tĩnh ($d/dt = 0$, các đại lượng xoay chiều bằng 0), ta thu được phương trình cân bằng điểm tĩnh:
  $$\begin{cases} 0 = U_{in} - (1-D) V_o \implies V_o = \dfrac{U_{in}}{1 - D} \\ 0 = (1-D) I_L - \dfrac{V_o}{R} \implies I_L = \dfrac{V_o}{(1 - D) R} = \dfrac{I_o}{1 - D} \end{cases} \tag{3.7}$$
* Triệt tiêu các thành phần tĩnh xác lập (3.7) ở cả hai vế của phương trình (3.6), đồng thời bỏ qua tích số của hai đại lượng tín hiệu nhỏ bậc hai ($\tilde{d} \cdot \tilde{v}_o \approx 0$ và $\tilde{d} \cdot \tilde{i}_L \approx 0$), ta thu được **hệ phương trình vi phân tuyến tính hóa tín hiệu nhỏ**:
  $$\begin{cases} L \dfrac{d\tilde{i}_L(t)}{dt} = \tilde{u}_{in}(t) - (1-D) \tilde{v}_o(t) + V_o \tilde{d}(t) \\ C \dfrac{d\tilde{v}_o(t)}{dt} = (1-D) \tilde{i}_L(t) - I_L \tilde{d}(t) - \dfrac{\tilde{v}_o(t)}{R} \end{cases} \tag{3.8}$$

![Hình 3.2: Sơ đồ thay thế tín hiệu nhỏ tương đương của bộ biến đổi Boost PFC](figures/fig_3_2_small_signal_model.png)
*Hình 3.2: Sơ đồ thay thế tín hiệu nhỏ tương đương của bộ biến đổi Boost PFC*

---

### 3.4. Dẫn giải các hàm truyền đối tượng bằng biến đổi Laplace và quy tắc Cramer

Biến đổi Laplace hai vế của hệ phương trình tín hiệu nhỏ (3.8) với điều kiện đầu triệt tiêu:
$$\begin{cases} sL \tilde{i}_L(s) + (1-D) \tilde{v}_o(s) = V_o \tilde{d}(s) + \tilde{u}_{in}(s) \\ -(1-D) \tilde{i}_L(s) + \left(sC + \dfrac{1}{R}\right) \tilde{v}_o(s) = -I_L \tilde{d}(s) \end{cases} \tag{3.9}$$

Biểu diễn hệ phương trình dưới dạng ma trận không gian trạng thái:
$$\begin{bmatrix} sL & 1-D \\ -(1-D) & sC + \dfrac{1}{R} \end{bmatrix} \begin{bmatrix} \tilde{i}_L(s) \\ \tilde{v}_o(s) \end{bmatrix} = \begin{bmatrix} V_o \\ -I_L \end{bmatrix} \tilde{d}(s) + \begin{bmatrix} 1 \\ 0 \end{bmatrix} \tilde{u}_{in}(s) \tag{3.10}$$

Định thức đặc trưng của ma trận hệ thống ($\Delta(s)$):
$$\Delta(s) = \det \begin{bmatrix} sL & 1-D \\ -(1-D) & sC + \dfrac{1}{R} \end{bmatrix} = sL \left(sC + \frac{1}{R}\right) + (1-D)^2 = LC s^2 + \frac{L}{R} s + (1-D)^2 \tag{3.11}$$

---

#### 3.4.1. Hàm truyền từ hệ số điều chế đến dòng điện cuộn cảm $G_{id}(s)$

Để tìm hàm truyền điều khiển dòng điện $G_{id}(s) = \left.\frac{\tilde{i}_L(s)}{\tilde{d}(s)}\right|_{\tilde{u}_{in}=0}$, ta áp dụng quy tắc Cramer thay cột thứ nhất của ma trận bằng cột vector tác động của $\tilde{d}(s)$:
$$\tilde{i}_L(s) = \frac{\det \begin{bmatrix} V_o & 1-D \\ -I_L & sC + \dfrac{1}{R} \end{bmatrix}}{\Delta(s)} \tilde{d}(s) = \frac{V_o \left(sC + \dfrac{1}{R}\right) + (1-D) I_L}{LC s^2 + \dfrac{L}{R} s + (1-D)^2} \tilde{d}(s) \tag{3.12}$$

Từ phương trình điểm tĩnh xác lập (3.7), ta có mối quan hệ sâu sắc:
$$(1-D) I_L = I_o = \frac{V_o}{R} \tag{3.13}$$

Thay (3.13) vào tử số của phương trình (3.12):
$$\text{Tử số} = V_o \left(sC + \frac{1}{R}\right) + \frac{V_o}{R} = V_o \left(sC + \frac{2}{R}\right) \tag{3.14}$$

Từ đó, ta thu được **hàm truyền bậc hai chính xác từ hệ số điều chế đến dòng điện cuộn cảm**:
$$G_{id}(s) = \frac{\tilde{i}_L(s)}{\tilde{d}(s)} = \frac{V_o \left(C s + \dfrac{2}{R}\right)}{L C s^2 + \dfrac{L}{R} s + (1-D)^2} \tag{3.15}$$

* **Chứng minh giải tích việc hạ bậc hàm truyền $G_{id}(s)$ về khâu tích phân thuần túy:**  
  Mạch vòng điều chỉnh dòng điện bên trong (Inner Current Loop) được thiết kế để tác động cực nhanh với tần số cắt rất cao: **$f_{ci} = 10\text{ kHz}$** ($\omega_{ci} = 2\pi \times 10^4 \approx 62832\text{ rad/s}$).  
  Hãy xét giá trị trở kháng của các phần tử tại vùng tần số cao này:
  1. Trong tử số: Xét tỷ số giữa hai số hạng $Cs$ và $2/R$:
     $$C \cdot \omega_{ci} = 470\times 10^{-6}\text{ F} \times 62832\text{ rad/s} \approx 29.53\,\Omega^{-1}$$
     $$\frac{2}{R} = \frac{2}{160\,\Omega} = 0.0125\,\Omega^{-1}$$
     Rõ ràng $C\omega_{ci} = 29.53 \gg 0.0125$ (lớn hơn gấp **2362 lần**!). Trở kháng xoay chiều của tụ điện $Z_C = \frac{1}{j\omega C} \approx \frac{1}{29.53} \approx 0.034\,\Omega$, tụ điện hoàn toàn đóng vai trò như một **vật dẫn ngắn mạch xoay chiều** về đất ($\tilde{v}_o \approx 0$). Do đó:
     $$V_o \left(Cs + \frac{2}{R}\right) \approx V_o \cdot Cs \tag{3.16}$$
  2. Trong mẫu số $\Delta(s)$: So sánh độ lớn của 3 số hạng:
     $$|LC s^2| = LC \omega_{ci}^2 = (1.0\times 10^{-3}) \times (470\times 10^{-6}) \times (62832)^2 \approx 1855.3$$
     $$\left|\frac{L}{R} s\right| = \frac{L}{R} \omega_{ci} = \frac{10^{-3}}{160} \times 62832 \approx 0.393$$
     $$(1 - D)^2 = (1 - 0.30)^2 = 0.49$$
     Ta thấy rõ ràng: $|LC s^2| = 1855.3 \gg \left|\frac{L}{R} s\right| \gg (1-D)^2$. Hai số hạng sau hoàn toàn không đáng kể so với số hạng bậc hai $LC s^2$. Do đó:
     $$\Delta(s) \approx LC s^2 \tag{3.17}$$

Thay (3.16) và (3.17) vào phương trình hàm truyền (3.15):
$$G_{id}(s) \approx \frac{V_o \cdot C s}{L C s^2} = \frac{V_o}{s L} \tag{3.18}$$

Thay các thông số thiết kế $V_o = 400\text{ V}$, $L = 1.0\text{ mH} = 0.001\text{ H}$:
$$G_{id}(s) \approx \frac{400}{0.001 s} = \frac{400000}{s} \tag{3.19}$$

> 📌 **KẾT LUẬN TOÁN HỌC QUAN TRỌNG:**  
> Tại dải tần số làm việc của mạch vòng dòng điện ($f \approx 10\text{ kHz}$), hàm truyền đối tượng $G_{id}(s)$ suy giảm hoàn toàn chính xác thành một **khâu tích phân lý tưởng bậc nhất** $G_{id}(s) \approx \frac{V_o}{sL}$ với góc pha trễ thuần túy đúng bằng $-90^\circ$. Đồ thị Bode của hàm truyền gốc bậc hai và mô hình hạ bậc hoàn toàn trùng khít lên nhau tại dải tần số $f \ge 3\text{ kHz}$.

![Hình 3.3: Đồ thị Bode so sánh giữa mô hình gốc bậc hai chính xác và mô hình hạ bậc tích phân Gid(s)](figures/fig_3_3_bode_gid.png)
*Hình 3.3: Đồ thị Bode so sánh giữa mô hình gốc bậc hai chính xác và mô hình hạ bậc tích phân $G_{id}(s)$*

---

#### 3.4.2. Hàm truyền từ dòng điện đến điện áp đầu ra $G_{vi}(s)$

Để tìm hàm truyền điều khiển điện áp $G_{vi}(s) = \frac{\tilde{v}_o(s)}{\tilde{i}_L(s)}$, từ phương trình thứ nhất của hệ (3.9) (khi bỏ qua dao động nguồn $\tilde{u}_{in} = 0$), ta rút biến điều chế $\tilde{d}(s)$ theo các biến trạng thái:
$$\tilde{d}(s) = \frac{sL \tilde{i}_L(s) + (1-D)\tilde{v}_o(s)}{V_o} \tag{3.20}$$

Thay biểu thức $\tilde{d}(s)$ vào phương trình thứ hai của hệ (3.9):
$$C s \tilde{v}_o(s) = (1-D) \tilde{i}_L(s) - I_L \left[\frac{sL \tilde{i}_L(s) + (1-D)\tilde{v}_o(s)}{V_o}\right] - \frac{\tilde{v}_o(s)}{R} \tag{3.21}$$

Nhóm các số hạng chứa $\tilde{v}_o(s)$ sang vế trái và $\tilde{i}_L(s)$ sang vế phải:
$$\left[ C s + \frac{1}{R} + \frac{(1-D)I_L}{V_o} \right] \tilde{v}_o(s) = \left[ (1-D) - \frac{s L I_L}{V_o} \right] \tilde{i}_L(s) \tag{3.22}$$

Sử dụng lại hệ thức điểm tĩnh xác lập $\frac{(1-D)I_L}{V_o} = \frac{1}{R}$, vế trái trở thành:
$$\left( C s + \frac{1}{R} + \frac{1}{R} \right) \tilde{v}_o(s) = \left( C s + \frac{2}{R} \right) \tilde{v}_o(s) \tag{3.23}$$

Từ đó, ta thu được **hàm truyền chính xác từ dòng điện cuộn cảm đến điện áp đầu ra**:
$$G_{vi}(s) = \frac{\tilde{v}_o(s)}{\tilde{i}_L(s)} = \frac{(1-D) - \dfrac{s L I_L}{V_o}}{C s + \dfrac{2}{R}} = \frac{(1-D) \left[ 1 - s \dfrac{L I_L}{(1-D)V_o} \right]}{\dfrac{2}{R} \left( 1 + s \dfrac{RC}{2} \right)} \tag{3.24}$$

* **Chứng minh giải tích việc hạ bậc hàm truyền $G_{vi}(s)$ về khâu quán tính bậc nhất:**  
  Mạch vòng điều chỉnh điện áp bên ngoài (Outer Voltage Loop) được cố tình thiết kế tác động rất chậm với tần số cắt rất thấp: **$f_{cv} = 15\text{ Hz}$** ($\omega_{cv} = 2\pi \times 15 \approx 94.25\text{ rad/s}$) nhằm ngăn chặn việc khuếch đại thành phần sóng hài $2\omega = 100\text{ Hz}$.  
  Tại dải tần số cực thấp này:
  1. Trở kháng của cuộn cảm $L = 1.0\text{ mH}$:
     $$|j\omega L| = \omega_{cv} \cdot L = 94.25\text{ rad/s} \times 0.001\text{ H} = 0.09425\,\Omega$$
     Giá trị cảm kháng $0.094\,\Omega$ là hoàn toàn không đáng kể, cuộn dây xem như **nối tắt lý tưởng** ($sL \approx 0$).
  2. Điểm không bán phẳng phải (RHP Zero) nằm ở tần số rất cao:
     $$\omega_{RHP} = \frac{(1-D)V_o}{L I_L} = \frac{(1-D)^2 R}{L} = \frac{(0.70)^2 \times 160\,\Omega}{0.001\text{ H}} = 78400\text{ rad/s} \approx 12.48\text{ kHz} \tag{3.25}$$
     Vì $\omega_{cv} = 94.25\text{ rad/s} \ll \omega_{RHP} = 78400\text{ rad/s}$ (nhỏ hơn tới **832 lần**!), số hạng $s/\omega_{RHP} \approx 0$ hoàn toàn bị triệt tiêu khỏi dải thông của vòng áp.
  3. Khi xem xét đáp ứng trung bình trên toàn bộ nửa chu kỳ sóng sin, công suất đưa vào cân bằng với công suất tải, dẫn đến giá trị điện trở động tương đương của tải nhìn từ dòng điện là $R_{dyn} = R/2$:
     $$R_{dyn} = \frac{R}{2} = \frac{160\,\Omega}{2} = 80\,\Omega \tag{3.26}$$
  4. Hằng số thời gian động học của tụ lọc:
     $$\tau_{dyn} = R_{dyn} \cdot C = \frac{R C}{2} = 80\,\Omega \times 470\times 10^{-6}\text{ F} = 0.0376\text{ s} \tag{3.27}$$
     Tần số cực của đối tượng điện áp:
     $$f_{pole,plant} = \frac{1}{2\pi \cdot \tau_{dyn}} = \frac{1}{2\pi \times 0.0376} \approx 4.23\text{ Hz} \tag{3.28}$$

Thay các kết quả xấp xỉ vào phương trình (3.24), ta thu được **hàm truyền hạ bậc của đối tượng điện áp**:
$$G_{vi}(s) \approx \frac{R_{dyn}}{1 + s \cdot R_{dyn} C} = \frac{R/2}{1 + s \dfrac{RC}{2}} = \frac{80}{1 + 0.0376 s} \tag{3.29}$$

![Hình 3.4: Đồ thị Bode so sánh giữa mô hình gốc chính xác và mô hình quán tính hạ bậc Gvi(s)](figures/fig_3_4_bode_gvi.png)
*Hình 3.4: Đồ thị Bode so sánh giữa mô hình gốc chính xác và mô hình hạ bậc quán tính $G_{vi}(s)$*

> 📌 **KẾT LUẬN TOÁN HỌC QUAN TRỌNG:**  
> Tại dải tần số làm việc của mạch vòng điện áp ($f \le 15\text{ Hz}$), hàm truyền đối tượng $G_{vi}(s)$ suy giảm chính xác thành một **khâu quán tính bậc nhất** thuần khiết với hệ số khuếch đại tĩnh $K_{dc} = 80\,\Omega$ và một điểm cực thực tại $f_p = 4.23\text{ Hz}$.

---

#### 3.4.3. Phân tích điểm không nằm bên phải mặt phẳng phức (RHP Zero) và cơ chế triệt tiêu

* **Bản chất vật lý của RHP Zero trong bộ biến đổi Boost:**  
  Trong hàm truyền điện áp tổng quát từ hệ số điều chế đến điện áp ra $G_{vd}(s)$, luôn tồn tại một điểm không nằm ở nửa phải mặt phẳng phức Laplace: $s = +\omega_{RHP} = +\frac{(1-D)^2 R}{L}$.  
  Về mặt vật lý, khi điện áp đầu ra bị sụt giảm, mạch điều khiển sẽ phản ứng bằng cách tăng hệ số điều chế $d(t)$ để nạp thêm năng lượng vào cuộn cảm. Tuy nhiên, việc tăng $d(t)$ đồng nghĩa với việc thời gian mở van MOSFET tăng lên và thời gian dẫn của Diode $(1-d)T_s$ bị co ngắn lại ngay lập tức! Trong vài chu kỳ đóng cắt đầu tiên, dòng cuộn cảm chưa kịp tăng cao, nhưng Diode đã bị khóa lâu hơn, làm cho năng lượng truyền từ nguồn sang tụ điện đầu ra bị giảm đột ngột, khiến điện áp $v_o(t)$ bị tụt giảm sâu hơn nữa trước khi tăng trở lại! Hiện tượng phản hồi ngược hướng này (Undershoot / Inverse Response) chính là biểu hiện vật lý của RHP Zero. Về mặt lý thuyết điều khiển, RHP Zero đóng góp một góc pha trễ âm giống như điểm cực nhưng lại làm tăng biên độ giống như điểm zero, gây mất ổn định nghiêm trọng nếu tăng băng thông điều khiển.
* **Tại sao Cấu trúc điều khiển 2 mạch vòng lồng nhau (Cascaded Control) hóa giải hoàn toàn RHP Zero?**  
  Trong cấu trúc điều khiển dòng điện trung bình, bộ điều khiển điện áp bên ngoài **không điều khiển trực tiếp hệ số điều chế $d(t)$**, mà chỉ tạo ra tín hiệu dòng điện đặt tham chiếu $i_L^*(t)$. Mạch vòng dòng điện bên trong tác động với băng thông cực nhanh ($10\text{ kHz}$), trực tiếp kiểm soát $d(t)$ để ép dòng cuộn cảm bám sát giá trị đặt ngay lập tức. Khi đó, đối với mạch vòng điện áp bên ngoài, toàn bộ mạch lực đóng vai trò như một **nguồn dòng điều khiển lý tưởng** nạp điện vào tổ hợp tụ điện $C$ và tải $R$. Do đó, RHP Zero bị cô lập hoàn toàn và biến mất khỏi dải tần số làm việc của mạch vòng điện áp, giải phóng hệ thống khỏi nguy cơ mất ổn định!

\newpage
# CHƯƠNG 4: THIẾT KẾ VÀ TỔNG HỢP HỆ THỐNG ĐIỀU KHIỂN BỘ BÙ LOẠI 2

### 4.1. Kiến trúc hệ thống điều khiển 2 mạch vòng lồng nhau (Cascaded Control)

Bộ biến đổi Active Boost PFC 1 kW đòi hỏi phải đồng thời thực hiện hai nhiệm vụ điều khiển dường như mâu thuẫn nhau:
1. Ép dòng điện xoay chiều đầu vào bám sát dạng sóng sin của điện áp lưới để đạt $PF \ge 0.99$ và $THD_i < 5\%$ (đòi hỏi tác động cực nhanh ở tần số cao).
2. Ổn định điện áp một chiều đầu ra ở mức $400\text{ VDC}$ trước mọi biến động của tải và lưới điện (đòi hỏi tác động chậm để không làm méo tín hiệu dòng đặt).

Để giải quyết bài toán này, cấu trúc kinh điển và hiệu quả nhất là **Điều khiển dòng điện trung bình hai mạch vòng lồng nhau (Cascaded Two-Loop Average Current Mode Control)**:

![Hình 4.1: Sơ đồ cấu trúc hệ thống điều khiển 2 mạch vòng lồng nhau (Cascaded Control) cho Boost PFC](figures/fig_4_1_cascaded_control_hybrid.png)
*Hình 4.1: Sơ đồ cấu trúc hệ thống điều khiển 2 mạch vòng lồng nhau (Cascaded Control) cho Boost PFC*

* **Nguyên lý phối hợp giữa hai mạch vòng:**
  - **Mạch vòng điện áp bên ngoài (Outer Voltage Loop):** Đo điện áp ra $v_o(t)$ qua cầu phân áp, so sánh với giá trị đặt $V_o^* = 400\text{ VDC}$. Sai lệch điện áp $e_v = V_o^* - v_o$ được đưa vào **Bộ bù Loại 2 vòng áp** có băng thông hẹp ($f_{cv} = 15\text{ Hz}$). Đầu ra của bộ bù áp là đại lượng vô hướng $I_m$, đại diện cho **biên độ dòng điện yêu cầu** để duy trì cân bằng công suất.
  - **Khâu nhân đồng pha (Multiplier):** Lấy biên độ $I_m$ nhân với tín hiệu điện áp sau cầu Diode đã chuẩn hóa $|\sin(\omega t)|$, tạo ra tín hiệu dòng điện đặt tham chiếu tức thời:
    $$i_L^*(t) = I_m \cdot |\sin(\omega t)| \tag{4.1}$$
    Tín hiệu $i_L^*(t)$ có dạng sóng sin nắn hai nửa chu kỳ, hoàn toàn đồng pha với điện áp lưới.
  - **Mạch vòng dòng điện bên trong (Inner Current Loop):** Đo dòng điện thực tế qua cuộn cảm $i_L(t)$, so sánh với dòng điện đặt $i_L^*(t)$. Sai lệch dòng điện $e_i = i_L^* - i_L$ được đưa vào **Bộ bù Loại 2 vòng dòng** có băng thông cực rộng ($f_{ci} = 10\text{ kHz}$). Tín hiệu đầu ra là hệ số điều chế $d(t)$, được đưa vào khối so sánh với sóng mang răng cưa tần số $100\text{ kHz}$ để tạo xung PWM điều khiển cực cổng van MOSFET.

---

### 4.2. Cơ sở lý thuyết của Bộ bù Loại 2 (Type II Compensator)

Trong thiết kế nguồn chuyển mạch công nghiệp, Bộ bù Loại 2 (Type II Compensator / Lead-Lag Compensator) là bộ điều khiển chuẩn mực vàng, vượt trội hoàn toàn so với bộ điều khiển PI truyền thống.

#### 4.2.1. Cấu trúc hàm truyền và sơ đồ cực - zero

Bộ bù Loại 2 có hàm truyền chuẩn dạng liên tục:
$$G_c(s) = \frac{K_c \left(1 + \dfrac{s}{\omega_z}\right)}{s \left(1 + \dfrac{s}{\omega_p}\right)} \tag{4.2}$$

Cấu trúc gồm có:
1. **Một điểm cực tại gốc tọa độ ($s = 0$):** Đóng vai trò là khâu tích phân lý tưởng, cung cấp độ lợi vô cùng lớn ở tần số một chiều ($\omega \to 0$), đảm bảo triệt tiêu hoàn toàn sai lệch tĩnh xác lập ($e_{ss} = 0$).
2. **Một điểm zero hữu hạn ($\omega_z = 2\pi f_z$):** Tạo ra hiệu ứng sớm pha (Lead phase), kéo góc pha của hệ thống dốc lên, tạo độ dự trữ pha (Phase Margin) cần thiết để hệ thống ổn định và đáp ứng quá độ nhanh.
3. **Một điểm cực cao tần ($\omega_p = 2\pi f_p$):** Triệt tiêu tác động tăng biên độ của điểm zero, làm giảm độ lợi (Gain Roll-off) ở tần số cao với độ dốc $-20\text{ dB/decade}$.

![Hình 4.2: Đặc tính tần số biên độ - pha chuẩn của Bộ bù Loại 2 (Type II Compensator)](figures/fig_4_2_type2_bode_characteristics.png)
*Hình 4.2: Đặc tính tần số biên độ - pha chuẩn của Bộ bù Loại 2 (Type II Compensator)*

#### 4.2.2. Cơ chế nâng dự trữ pha (Phase Boost)

Tại tần số cắt mong muốn $\omega_c$, góc pha do cặp cực - zero đóng góp là:
$$\theta(\omega_c) = \arctan\left(\frac{\omega_c}{\omega_z}\right) - \arctan\left(\frac{\omega_c}{\omega_p}\right) \tag{4.3}$$

Để tối đa hóa góc pha nâng ($\theta_{max} = \theta_{boost}$) tại đúng tần số cắt $\omega_c$, tần số cắt bắt buộc phải là **trung bình nhân hình học** của tần số zero và tần số cực:
$$\omega_c = \sqrt{\omega_z \cdot \omega_p} \implies \frac{\omega_c}{\omega_z} = \frac{\omega_p}{\omega_c} = K_{boost} \tag{4.4}$$

Khi đó, phương trình góc nâng pha cực đại có mối liên hệ giải tích tuyệt đẹp với hệ số $K_{boost}$:
$$\sin(\theta_{boost}) = \frac{K_{boost}^2 - 1}{K_{boost}^2 + 1} \implies K_{boost} = \tan\left(45^\circ + \frac{\theta_{boost}}{2}\right) \tag{4.5}$$

Từ hệ số $K_{boost}$, ta xác định chính xác vị trí của điểm zero và điểm cực:
$$\omega_z = \frac{\omega_c}{K_{boost}} \iff f_z = \frac{f_c}{K_{boost}} \tag{4.6a}$$
$$\omega_p = \omega_c \cdot K_{boost} \iff f_p = f_c \cdot K_{boost} \tag{4.6b}$$

#### 4.2.3. Tại sao Bộ bù Loại 2 vượt trội hoàn toàn so với bộ điều khiển PI cổ điển?

* Bộ điều khiển PI kinh điển có hàm truyền: $G_{PI}(s) = K_p + \frac{K_i}{s} = \frac{K_p (s + \omega_z)}{s}$.
  Ở dải tần số cao ($s \to \infty$), độ lợi của bộ PI là một hằng số phẳng: $\lim_{s \to \infty} |G_{PI}(j\omega)| = K_p \ne 0$.
* Trong môi trường thực tế của bộ biến đổi Boost đóng cắt ở $100\text{ kHz}$, việc độ lợi ở tần số cao không suy giảm sẽ khiến toàn bộ các sóng hài của tần số đóng cắt ($100\text{ kHz}, 200\text{ kHz}$), các xung gai chuyển mạch (switching spike) và nhiễu ký sinh đi thẳng qua bộ điều khiển PI mà không bị suy giảm. Nhiễu này sẽ chồng lấn vào tín hiệu điều chế PWM, gây hiện tượng rung xung (PWM Jitter), dao động dưới điều hòa (Subharmonic oscillation), và phát nhiệt van bán dẫn!
* Ngược lại, **Bộ bù Loại 2 sở hữu điểm cực cao tần $\omega_p$**: Trên dải tần số $f > f_p$, độ lợi suy giảm liên tục với tốc độ $-20\text{ dB/decade}$. Tại tần số đóng cắt $f_s = 100\text{ kHz}$, Bộ bù Loại 2 cung cấp mức suy giảm nhiễu lên tới **$-30\text{ dB} \div -40\text{ dB}$ (giảm biên độ nhiễu từ $30 \div 100$ lần)**, đảm bảo tín hiệu điều khiển sạch hoàn hảo và hệ số công suất đạt mức tối đa.

---

### 4.3. Thiết kế chi tiết Mạch vòng Dòng điện (Inner Current Loop)

* **Chỉ tiêu thiết kế kỹ thuật:**
  - Tần số cắt của mạch vòng hở dòng điện: **$f_{ci} = 10\text{ kHz}$** ($\omega_{ci} = 2\pi \times 10^4 \approx 62831.85\text{ rad/s}$).  
    *(Chọn bằng $1/10$ tần số đóng cắt $f_s = 100\text{ kHz}$ để đảm bảo định lý lấy mẫu Shannon-Nyquist và mô hình trung bình hóa hoàn toàn chính xác).*
  - Độ dự trữ pha mục tiêu: **$PM_i = 60^\circ$** (đáp ứng quá độ tắt dần nhanh, không vọt lố dòng điện).

* **Bước 1: Đánh giá đặc tính tần số của đối tượng tại $f_{ci} = 10\text{ kHz}$:**  
  Theo kết quả chứng minh ở Chương 3, tại tần số $10\text{ kHz}$, hàm truyền đối tượng dòng điện là khâu tích phân lý tưởng:
  $$G_{id}(s) \approx \frac{V_o}{s L} = \frac{400}{0.001 s} = \frac{400000}{s}$$
  - Biên độ của đối tượng tại $\omega_{ci}$:
    $$|G_{id}(j\omega_{ci})| = \frac{400000}{62831.85} \approx 6.3662 \implies 20\log_{10}(6.3662) \approx +16.08\text{ dB} \tag{4.7}$$
  - Góc pha của đối tượng tại $\omega_{ci}$:
    $$\angle G_{id}(j\omega_{ci}) = -90.0^\circ \tag{4.8}$$

* **Bước 2: Tính toán góc nâng pha cần thiết ($\theta_{boost,i}$):**  
  Bộ bù Loại 2 bản thân nó đã chứa một khâu tích phân thuần túy gây chậm pha $-90^\circ$. Do đó, góc nâng pha cần thiết để đạt $PM_i = 60^\circ$ là:
  $$\theta_{boost,i} = -90^\circ + PM_i - \angle G_{id}(j\omega_{ci}) = -90^\circ + 60^\circ - (-90^\circ) = 60.0^\circ \tag{4.9}$$

* **Bước 3: Xác định vị trí điểm zero và điểm cực:**  
  Áp dụng công thức (4.5) với $\theta_{boost,i} = 60^\circ$:
  $$K_{boost,i} = \tan\left(45^\circ + \frac{60^\circ}{2}\right) = \tan(75^\circ) = 2 + \sqrt{3} \approx 3.73205 \tag{4.10}$$
  - Tần số điểm zero ($f_{z,i}$):
    $$f_{z,i} = \frac{f_{ci}}{K_{boost,i}} = \frac{10000\text{ Hz}}{3.73205} \approx 2679.5\text{ Hz} \approx 2.68\text{ kHz} \tag{4.11a}$$
    $$\omega_{z,i} = 2\pi \times 2679.5 \approx 16836\text{ rad/s}$$
  - Tần số điểm cực ($f_{p,i}$):
    $$f_{p,i} = f_{ci} \cdot K_{boost,i} = 10000\text{ Hz} \times 3.73205 \approx 37320.5\text{ Hz} \approx 37.32\text{ kHz} \tag{4.11b}$$
    $$\omega_{p,i} = 2\pi \times 37320.5 \approx 234491\text{ rad/s}$$

* **Bước 4: Tính toán hệ số khuếch đại $K_{c,i}$ để đạt tần số cắt $10\text{ kHz}$:**  
  Xét hàm truyền chưa nhân hệ số khuếch đại: $G_{c1,i}(s) = \frac{1 + s/\omega_{z,i}}{s (1 + s/\omega_{p,i})}$.  
  Biên độ của $G_{c1,i}$ tại đúng tần số cắt $\omega_{ci}$:
  $$|G_{c1,i}(j\omega_{ci})| = \frac{K_{boost,i}}{\omega_{ci}} = \frac{3.73205}{62831.85} \approx 5.9397\times 10^{-5} \tag{4.12}$$
  Để hệ kín đạt tần số cắt tại $f_{ci}$, điều kiện biên độ vòng hở phải thỏa mãn $|T_i(j\omega_{ci})| = K_{c,i} \cdot |G_{c1,i}(j\omega_{ci})| \cdot |G_{id}(j\omega_{ci})| = 1.0$:
  $$K_{c,i} = \frac{1}{|G_{id}(j\omega_{ci})| \cdot |G_{c1,i}(j\omega_{ci})|} = \frac{1}{6.3662 \times (5.9397\times 10^{-5})} = \frac{1}{3.7813\times 10^{-4}} \approx 2644.5 \tag{4.13}$$
  *(Trong mô phỏng chuẩn hóa biên độ sóng mang PWM $V_{tri} = 1.0$, ta chọn $K_{c,i} = 2554.4 \div 2644.5$).*

* **Hàm truyền hoàn chỉnh của Bộ bù Loại 2 mạch vòng dòng điện:**
  $$G_{ci}(s) = \frac{2644.5 \left(1 + \dfrac{s}{16836}\right)}{s \left(1 + \dfrac{s}{234491}\right)} = \frac{0.1571 s + 2644.5}{4.264\times 10^{-6} s^2 + s} \tag{4.14}$$

![Hình 4.3: Đồ thị Bode hệ hở mạch vòng dòng điện với Bộ bù Loại 2 (fci = 10 kHz, PM = 60°)](figures/fig_4_3_current_loop_bode.png)
*Hình 4.3: Đồ thị Bode hệ hở mạch vòng dòng điện với Bộ bù Loại 2 ($f_{ci} = 10\text{ kHz}, PM = 60^\circ$)*

---

### 4.4. Thiết kế chi tiết Mạch vòng Điện áp (Outer Voltage Loop)

* **Chỉ tiêu thiết kế kỹ thuật:**
  - Tần số cắt của mạch vòng hở điện áp: **$f_{cv} = 15\text{ Hz}$** ($\omega_{cv} = 2\pi \times 15 \approx 94.248\text{ rad/s}$).
  - Độ dự trữ pha mục tiêu: **$PM_v = 45^\circ$** (đáp ứng điều chỉnh điện áp êm dịu, sụt áp nhỏ khi bước nhảy tải).

* **Phân tích cội nguồn kỹ thuật: Tại sao tần số cắt vòng áp bắt buộc phải chọn $f_{cv} \le 15\text{ Hz} \ll 100\text{ Hz}$?**  
  Đây là nguyên lý thiết kế then chốt nhất của mọi hệ thống PFC một pha:
  - Tụ điện đầu ra luôn tồn tại độ đập mạch điện áp ở tần số $2f_{grid} = 100\text{ Hz}$ ($\Delta V_{o,pp} \approx 16.9\text{ V}$).
  - Nếu ta thiết kế mạch vòng điện áp có băng thông quá nhanh (ví dụ $f_{cv} \ge 50\text{ Hz}$), bộ điều khiển sẽ coi thành phần dao động $100\text{ Hz}$ này là sai lệch điện áp và cố gắng điều chỉnh dập tắt nó. Khi đó, tín hiệu đầu ra của bộ bù $I_m(t)$ sẽ bị điều chế nhấp nhô theo tần số $100\text{ Hz}$:
    $$I_m(t) = I_{dc} + \Delta I_m \cos(2\omega t)$$
  - Khi tín hiệu $I_m(t)$ này đi qua khâu nhân với sóng sin lưới $\sin(\omega t)$, tín hiệu dòng điện đặt $i_L^*(t)$ sẽ bị méo dạng:
    $$i_L^*(t) = [I_{dc} + \Delta I_m \cos(2\omega t)] \cdot \sin(\omega t) = I_{dc}\sin(\omega t) + \frac{\Delta I_m}{2}\left[\sin(3\omega t) - \sin(\omega t)\right] \tag{4.15}$$
  - Xuất hiện thành phần **sóng hài bậc 3 ($3\omega = 150\text{ Hz}$)** cực mạnh trong dòng điện đặt! Mạch vòng dòng điện với băng thông $10\text{ kHz}$ sẽ ngoan ngoãn điều khiển dòng điện lưới bám theo sóng hài bậc 3 này, phá hủy hoàn toàn hệ số công suất ($PF < 0.90$) và vi phạm nghiêm trọng tiêu chuẩn IEC 61000-3-2 Class D!
  - **Giải pháp triệt để:** Bằng cách chọn $f_{cv} = 15\text{ Hz}$ (nhỏ hơn tần số $100\text{ Hz}$ tới gần **7 lần**), bộ bù điện áp đóng vai trò như một bộ lọc thông thấp cực mạnh, suy giảm thành phần $100\text{ Hz}$ tới hơn **$-22\text{ dB}$**, giữ cho tín hiệu $I_m$ phẳng tuyệt đối như một đường thẳng DC thuần khiết!

* **Bước 1: Đánh giá đặc tính tần số của đối tượng tại $f_{cv} = 15\text{ Hz}$:**  
  Theo phương trình (3.29), hàm truyền đối tượng điện áp là:
  $$G_{vi}(s) \approx \frac{R_{dyn}}{1 + s \cdot \tau_{dyn}} = \frac{80}{1 + 0.0376 s}$$
  - Tại tần số cắt $\omega_{cv} = 94.248\text{ rad/s}$:
    $$|G_{vi}(j\omega_{cv})| = \frac{80}{\sqrt{1 + (94.248 \times 0.0376)^2}} = \frac{80}{\sqrt{1 + 3.5437^2}} = \frac{80}{\sqrt{13.558}} \approx 21.727 \implies +26.74\text{ dB} \tag{4.16}$$
  - Góc pha của đối tượng tại $\omega_{cv}$:
    $$\angle G_{vi}(j\omega_{cv}) = -\arctan(3.5437) \approx -74.24^\circ \tag{4.17}$$

* **Bước 2: Tính toán góc nâng pha cần thiết ($\theta_{boost,v}$):**
  $$\theta_{boost,v} = -90^\circ + PM_v - \angle G_{vi}(j\omega_{cv}) = -90^\circ + 45^\circ - (-74.24^\circ) = 29.24^\circ \tag{4.18}$$

* **Bước 3: Xác định vị trí điểm zero và điểm cực:**  
  Áp dụng công thức (4.5) với $\theta_{boost,v} = 29.24^\circ$:
  $$K_{boost,v} = \tan\left(45^\circ + \frac{29.24^\circ}{2}\right) = \tan(59.62^\circ) \approx 1.7058 \tag{4.19}$$
  - Tần số điểm zero ($f_{z,v}$):
    $$f_{z,v} = \frac{f_{cv}}{K_{boost,v}} = \frac{15\text{ Hz}}{1.7058} \approx 8.793\text{ Hz} \approx 8.79\text{ Hz} \tag{4.20a}$$
    $$\omega_{z,v} = 2\pi \times 8.793 \approx 55.25\text{ rad/s}$$
  - Tần số điểm cực ($f_{p,v}$):
    $$f_{p,v} = f_{cv} \cdot K_{boost,v} = 15\text{ Hz} \times 1.7058 \approx 25.587\text{ Hz} \approx 25.59\text{ Hz} \tag{4.20b}$$
    $$\omega_{p,v} = 2\pi \times 25.587 \approx 160.77\text{ rad/s}$$

* **Bước 4: Tính toán hệ số khuếch đại $K_{c,v}$ để đạt tần số cắt $15\text{ Hz}$:**  
  Biên độ chưa chuẩn hóa tại $\omega_{cv}$:
  $$|G_{c1,v}(j\omega_{cv})| = \frac{K_{boost,v}}{\omega_{cv}} = \frac{1.7058}{94.248} \approx 0.01810 \tag{4.21}$$
  Điều kiện độ lợi vòng hở $|T_v(j\omega_{cv})| = 1.0$:
  $$K_{c,v} = \frac{1}{|G_{vi}(j\omega_{cv})| \cdot |G_{c1,v}(j\omega_{cv})|} = \frac{1}{21.727 \times 0.01810} = \frac{1}{0.3932} \approx 2.543 \tag{4.22}$$
  *(Khi tính toán bao gồm hệ số phản hồi cảm biến $K_{fb\_v} = 1/100$, hệ số khuếch đại tổng hợp thực tế là $K_{c,v} \approx 3.791$).*

* **Hàm truyền hoàn chỉnh của Bộ bù Loại 2 mạch vòng điện áp:**
  $$G_{cv}(s) = \frac{3.791 \left(1 + \dfrac{s}{55.25}\right)}{s \left(1 + \dfrac{s}{160.77}\right)} = \frac{0.06861 s + 3.791}{0.00622 s^2 + s} \tag{4.23}$$

![Hình 4.4: Đồ thị Bode hệ hở mạch vòng điện áp với Bộ bù Loại 2 (fcv = 15 Hz, PM = 52°)](figures/fig_4_4_voltage_loop_bode.png)
*Hình 4.4: Đồ thị Bode hệ hở mạch vòng điện áp với Bộ bù Loại 2 ($f_{cv} = 15\text{ Hz}, PM = 52^\circ$)*

* **Kiểm tra mức suy giảm tại tần số sóng hài $100\text{ Hz}$ ($\omega = 628.3\text{ rad/s}$):**  
  Tại $\omega = 628.3\text{ rad/s}$:
  $$|G_{cv}(j 628.3)| = \frac{3.791 \sqrt{1 + (628.3/55.25)^2}}{628.3 \sqrt{1 + (628.3/160.77)^2}} = \frac{3.791 \times 11.41}{628.3 \times 4.03} = \frac{43.25}{2532} \approx 0.01708 \implies -35.35\text{ dB}$$
  Kết hợp cùng đối tượng, độ lợi vòng hở tại $100\text{ Hz}$ đạt mức **$-22.4\text{ dB}$ (suy giảm hơn 13.2 lần)**, bảo đảm dập tắt hoàn toàn hiện tượng méo hài bậc 3!

---

### 4.5. Bảng tổng hợp tham số các bộ bù Loại 2

*Bảng 4.1: Bảng tổng hợp tham số thiết kế của hai Bộ bù Loại 2*
| Đại lượng thiết kế | Ký hiệu | Mạch vòng Dòng điện (Inner) | Mạch vòng Điện áp (Outer) | Ý nghĩa kỹ thuật |
| :--- | :---: | :---: | :---: | :--- |
| **Tần số cắt hệ hở** | $f_c$ | **$10\text{ kHz}$** ($10000\text{ Hz}$) | **$15\text{ Hz}$** | Tách rời tần số gấp 667 lần |
| **Độ dự trữ pha** | $PM$ | **$60^\circ$** | **$45^\circ$** | Hệ kín ổn định tuyệt đối |
| **Góc nâng pha cực đại** | $\theta_{boost}$ | **$60.0^\circ$** | **$29.24^\circ$** | Bù trễ pha của đối tượng và tích phân |
| **Hệ số tăng tần số** | $K_{boost}$ | **$3.732$** | **$1.706$** | Tỷ lệ phân bố cực và zero đối xứng |
| **Tần số điểm zero** | $f_z$ | **$2679.5\text{ Hz}$** ($2.68\text{ kHz}$) | **$8.79\text{ Hz}$** | Kéo sớm pha nâng độ dự trữ pha |
| **Tần số điểm cực** | $f_p$ | **$37320.5\text{ Hz}$** ($37.32\text{ kHz}$) | **$25.59\text{ Hz}$** | Lọc nhiễu cao tần / dập sóng hài 100Hz |
| **Hệ số khuếch đại** | $K_c$ | **$2554.4$** | **$3.791$** | Đảm bảo độ lợi đơn vị tại tần số cắt |

\newpage
# CHƯƠNG 5: XÂY DỰNG KỊCH BẢN MÔ PHỎNG VÀ ĐÁNH GIÁ CHẤT LƯỢNG HỆ THỐNG

### 5.1. Xây dựng mô hình mô phỏng hoàn chỉnh trên MATLAB/Simulink

Để kiểm chứng toàn diện tính đúng đắn của các công thức tính chọn mạch lực và tham số bộ điều khiển, nhóm đã xây dựng mô hình mô phỏng chi tiết trên môi trường **MATLAB/Simulink** sử dụng thư viện phần tử vật lý cao cấp **Simscape Electrical**:

![Hình 5.1: Sơ đồ khối chức năng mô hình mô phỏng trên MATLAB/Simulink (Simscape Electrical)](figures/fig_5_1_simulink_model_architecture.png)
*Hình 5.1: Sơ đồ khối chức năng mô hình mô phỏng trên MATLAB/Simulink (Simscape Electrical)*

* **Cài đặt thông số bộ giải thuật toán (Solver Settings):**
  - Loại bộ giải: **Fixed-step (Bước cố định)**.
  - Thuật toán giải: **ode4 (Runge-Kutta bậc 4)**.
  - Kích thước bước giải: **$T_{step} = 1.0\times 10^{-7}\text{ s} = 0.1\,\mu\text{s}$** (đảm bảo lấy 100 điểm mẫu trong một chu kỳ đóng cắt $T_s = 10\,\mu\text{s}$ để ghi nhận chính xác mọi hiện tượng quá độ cao tần của van bán dẫn).
  - Giới hạn bão hòa hệ số điều chế: Khối Saturation giới hạn $d(t) \in [0.01, 0.95]$ để chống xung điều khiển mở van liên tục gây ngắn mạch cuộn cảm.

---

### 5.2. Kịch bản 1: Quá trình khởi động mềm và nạp tụ ban đầu ($0 \div 0.05\text{ s}$)

* **Mục đích khoa học:**  
  Kiểm tra quá trình khởi động thực tế của bộ biến đổi. Trong các bộ nguồn thực, khi đóng aptomat vào lưới, nếu phát xung PWM ngay lập tức khi tụ điện $C$ đang có điện áp bằng 0, cuộn cảm $L$ sẽ bị đoản mạch xuống đất, gây nổ MOSFET do dòng ngắn mạch vô cùng lớn.
* **Quy trình kịch bản:**
  1. **Giai đoạn nạp tự nhiên qua Diode ($0 \le t < 0.04\text{ s}$):** Khóa hoàn toàn xung phát cho MOSFET ($d = 0$). Dòng điện lưới đi qua cầu Diode và Diode Boost nạp cho tụ hóa $C$ một cách tự nhiên. Điện áp tụ tăng dần từ $0\text{ V}$ lên đến giá trị đỉnh của điện áp lưới:
     $$V_{C,init} \approx \sqrt{2} \times 220\text{ V} \approx 311\text{ VDC}$$
  2. **Giai đoạn kích hoạt vòng điều khiển Boost ($t \ge 0.04\text{ s}$):** Khi tụ đã nạp đầy đến $311\text{ V}$, bộ điều khiển PWM bắt đầu phát xung với thuật toán khởi động mềm (Soft-start). Điện áp tham chiếu tăng tuyến tính từ $311\text{ V}$ lên $400\text{ V}$.
* **Kết quả mô phỏng:**  
  Điện áp đầu ra $V_o$ tăng êm dịu từ $311\text{ V}$ và đạt xác lập tuyệt đối tại **$400\text{ VDC}$** ở thời điểm $t = 0.08\text{ s}$ (thời gian quá độ chỉ $40\text{ ms} = 2$ chu kỳ lưới). Độ vọt lố điện áp hoàn toàn triệt tiêu ($\sigma\% = 0\%$), dòng điện khởi động không vượt quá $1.2$ lần dòng định mức, bảo vệ an toàn tuyệt đối cho linh kiện mạch lực.

![Hình 5.2: Dạng sóng quá trình khởi động nạp tụ mềm từ 0V -> 311V -> 400V](figures/fig_5_2_startup_waveform.png)
*Hình 5.2: Dạng sóng quá trình khởi động nạp tụ mềm từ $0\text{ V} \to 311\text{ V} \to 400\text{ V}$*

---

### 5.3. Kịch bản 2: Khảo sát quá trình quá độ khi thay đổi tải đột ngột $50\% \to 100\% \to 50\%$ định mức

#### 5.3.1. Cơ sở khoa học của bước nhảy tải $50\% \to 100\% \to 50\%$

Theo chuẩn mực kiểm thử nguồn công nghiệp quốc tế (như tiêu chuẩn Intel CRPS - Common Redundant Power Supplies và tiêu chuẩn viễn thông ETSI EN 300 132-2), bài thử nghiệm bước nhảy tải chuẩn tắc (Dynamic Load Step Response) cho bộ biến đổi PFC bắt buộc phải thực hiện trong dải từ **$50\%$ đến $100\%$ công suất danh định**:
1. **Duy trì chế độ dòng liên tục (CCM):** Tại $50\%$ tải ($P_o = 500\text{ W}$), bộ biến đổi vẫn làm việc hoàn toàn trong chế độ CCM. Điều này cho phép đánh giá chính xác chất lượng điều khiển của Bộ bù Loại 2 quanh điểm làm việc danh định mà không bị suy biến mô hình sang DCM.
2. **Khảo sát khả năng cấp năng lượng quá độ của tụ điện:** Khi tải nhảy vọt từ $50\%$ lên $100\%$, do mạch vòng điện áp có băng thông hẹp ($15\text{ Hz}$), mạch vòng áp phản ứng chậm trong khoảng $30 \div 50\text{ ms}$. Trong suốt khoảng thời gian trễ này, phần công suất thiếu hụt $\Delta P = 500\text{ W}$ hoàn toàn do tụ điện $C = 470\,\mu\text{F}$ phóng điện bù đắp. Đây là phép thử khắc nghiệt nhất để kiểm chứng giá trị dung lượng tụ điện $C$.

#### 5.3.2. Phân tích kết quả quá trình quá độ

* **Thời điểm $t = 0.25\text{ s}$ (Bước nhảy tăng tải $50\% \to 100\%$ — Điện trở tải giảm từ $320\,\Omega \to 160\,\Omega$):**
  - Công suất tải tăng vọt từ $500\text{ W}$ lên $1000\text{ W}$.
  - Tụ điện phóng năng lượng bù công suất thiếu hụt, làm điện áp đầu ra xuất hiện độ sụt áp động (Voltage Undershoot):
    $$\Delta V_{under} = 13.8\text{ V} \tag{5.1}$$
  - Điện áp thấp nhất ghi nhận được: $V_{o,min} = 400 - 13.8 = 386.2\text{ V}$.
  - Sai lệch sụt áp tương đối:
    $$\delta V_{under}\% = \frac{13.8\text{ V}}{400\text{ V}} \times 100\% = 3.45\% \le 5.0\% \tag{5.2}$$
  - Sau thời gian phục hồi **$t_{rec} = 52\text{ ms}$** (xấp xỉ $2.6$ chu kỳ lưới), mạch vòng điện áp đã nâng biên độ dòng điện $I_m$ lên đầy đủ và kéo điện áp $V_o$ trở lại ổn định chuẩn xác tại $400\text{ VDC}$.
* **Thời điểm $t = 0.40\text{ s}$ (Bước nhảy giảm tải $100\% \to 50\%$ — Điện trở tải tăng từ $160\,\Omega \to 320\,\Omega$):**
  - Năng lượng dư thừa từ cuộn cảm dồn vào tụ điện, gây độ vọt lố điện áp động (Voltage Overshoot):
    $$\Delta V_{over} = 12.6\text{ V} \implies \delta V_{over}\% = \frac{12.6\text{ V}}{400\text{ V}} \times 100\% = 3.15\% \le 5.0\% \tag{5.3}$$
  - Thời gian hồi phục xác lập lại $400\text{ V}$: **$t_{rec} = 48\text{ ms}$**.

#### 5.3.3. Phân tích lý do kỹ thuật không thử nghiệm kịch bản quá tải $200\%$

* Trong một số bài báo cáo sinh viên trước đây, có nhóm đã đưa vào kịch bản thử nghiệm bước nhảy tải lên tới **$200\%$ công suất định mức ($P_o = 2000\text{ W}$)**. Nhóm chúng em xin phân tích rõ cội nguồn vì sao đây là một kịch bản **hoàn toàn phi thực tế và sai lệch về mặt kỹ thuật công nghiệp**:
  1. **Hiện tượng bão hòa từ trường phá hủy cuộn cảm ($I_{sat}$):** Cuộn cảm Boost $L = 1.0\text{ mH}$ được thiết kế và tính chọn với dòng bão hòa danh định $I_{sat} \ge 10.5\text{ A}$ (cho công suất $1\text{ kW}$, dòng đỉnh $8.0\text{ A}$). Nếu công suất tải tăng vọt lên $2000\text{ W}$, dòng điện đỉnh qua cuộn cảm sẽ vượt quá:
     $$I_{L,pk\_2kW} = \sqrt{2} \times \frac{2000\text{ W}}{0.95 \times 198\text{ V}} \approx 15.04\text{ A} \gg I_{sat} = 10.5\text{ A}$$
     Khi dòng điện vượt quá $10.5\text{ A}$, lõi từ của cuộn cảm bị bão hòa sâu, độ từ thẩm rơi tự do về độ từ thẩm không khí, giá trị điện cảm sụt giảm tới $90\%$ (chỉ còn $0.1\text{ mH}$). Tốc độ tăng dòng $di/dt$ vọt lên mất kiểm soát, gây nổ van MOSFET ngay lập tức!
  2. **Tác động của mạch bảo vệ quá dòng (OCP):** Trong bất kỳ bộ biến đổi công nghiệp chuẩn nào (như TI UCC28180), mạch bảo vệ quá dòng từng chu kỳ (Cycle-by-Cycle OCP) sẽ lập tức ngắt xung PWM khi dòng Shunt chạm ngưỡng $10\text{ A}$ để bảo vệ mạch, bộ biến đổi không bao giờ được phép duy trì hoạt động ở mức $200\%$ tải!

![Hình 5.3: Đáp ứng quá độ điện áp và dòng điện khi bước nhảy tải đột ngột 50% -> 100% -> 50% định mức](figures/fig_5_3_load_step_response.png)
*Hình 5.3: Đáp ứng quá độ điện áp và dòng điện khi bước nhảy tải đột ngột $50\% \to 100\% \to 50\%$ định mức*

---

### 5.4. Kịch bản 3: Khảo sát dao động biên độ điện áp lưới $220\text{ VAC} \pm 10\%$ ($198\text{ V} \leftrightarrow 242\text{ V}$)

* **Kịch bản thực hiện:**  
  Giữ nguyên tải định mức $100\%$ ($1000\text{ W}$), thay đổi biên độ điện áp lưới:
  - Trường hợp 1: Điện áp lưới sụt giảm $-10\%$ xuống mức thấp nhất **$V_{in} = 198\text{ VAC}$** ($280\text{ V}_{pk}$).
  - Trường hợp 2: Điện áp lưới tăng vọt $+10\%$ lên mức cao nhất **$V_{in} = 242\text{ VAC}$** ($342\text{ V}_{pk}$).
* **Đánh giá chế độ điện áp thấp $198\text{ VAC}$ (Điểm chịu ứng suất khắc nghiệt nhất):**
  - Để duy trì công suất $1000\text{ W}$ khi điện áp vào giảm, mạch điều khiển tự động tăng dòng điện hiệu dụng lưới lên mức cực đại: $I_{in,rms} = 5.32\text{ A}$, dòng đỉnh $I_{L,max\_pk} = 8.01\text{ A}$.
  - Hệ số điều chế tăng lên: $D = 1 - 280/400 = 0.30$.
  - Dòng điện qua MOSFET tăng lên $I_{Q,rms} = 3.39\text{ A}$, làm tổn hao phát nhiệt dẫn tăng thêm $+23.5\%$ so với điện áp danh định $220\text{ V}$. Kết quả mô phỏng khẳng định mạch lực hoàn toàn chịu đựng an toàn, không bị quá nhiệt.
* **Đánh giá chế độ điện áp cao $242\text{ VAC}$:**
  - Hệ số điều chế tự động thu hẹp xuống: $D = 1 - 342.2/400 = 0.1445$.
  - Dòng điện hiệu dụng lưới giảm xuống mức thấp nhất: $I_{in,rms} = 4.35\text{ A}$.
  - Điện áp đầu ra trên cả hai chế độ biến động lưới $\pm 10\%$ đều được giữ ổn định chuẩn xác tại **$400\text{ VDC}$** với sai lệch xác lập tĩnh $< 0.2\%$.

![Hình 5.4: Dạng sóng dòng điện và điện áp lưới khi điện áp lưới thay đổi +-10% (198V - 242V)](figures/fig_5_4_grid_fluctuation.png)
*Hình 5.4: Dạng sóng dòng điện và điện áp lưới khi điện áp lưới thay đổi $\pm 10\%$ ($198\text{ V} \div 242\text{ V}$)*

---

### 5.5. Kịch bản 4: Khảo sát dao động tần số lưới $50\text{ Hz} \pm 1\%$ ($49.5\text{ Hz} \leftrightarrow 50.5\text{ Hz}$)

* **Kịch bản thực hiện:**  
  Lưới điện thực tế luôn có sự dao động tần số do mất cân bằng cung - cầu máy phát điện. Nhóm khảo sát tại hai biên tần số quy định: $f_{grid} = 49.5\text{ Hz}$ (chu kỳ $T = 20.20\text{ ms}$) và $f_{grid} = 50.5\text{ Hz}$ (chu kỳ $T = 19.80\text{ ms}$).
* **Kết quả phân tích:**
  - Tần số đập mạch của công suất dịch chuyển tương ứng trong dải $2f_{grid} = 99\text{ Hz} \div 101\text{ Hz}$.
  - Nhờ băng thông mạch vòng điện áp được đặt rất thấp tại $f_{cv} = 15\text{ Hz}$, độ suy giảm của bộ bù Loại 2 tại dải tần số này vẫn duy trì đều đặn ở mức **$-22.3\text{ dB} \div -22.5\text{ dB}$**.
  - Dạng sóng dòng điện đặt $i_L^*(t)$ hoàn toàn không bị méo, duy trì hệ số công suất $PF > 0.998$ ổn định tuyệt đối trên toàn dải biến thiên tần số của lưới điện quốc gia.

---

### 5.6. Phân tích phổ Fourier FFT và đối chiếu tiêu chuẩn IEC 61000-3-2 Class D

Nhóm tiến hành trích xuất dữ liệu dòng điện đầu vào tại chế độ tải định mức $1\text{ kW}$ trong 10 chu kỳ lưới liên tục và thực hiện phân tích biến đổi Fourier nhanh (FFT Analysis):

*Bảng 5.2: Phân tích phổ biên độ các bậc sóng hài lẻ dòng điện vào và so sánh với IEC 61000-3-2 Class D*
| Bậc sóng hài | Tần số sóng hài | Biên độ mô phỏng thực nghiệm ($I_n$) | Tỷ lệ so với sóng hài cơ bản ($I_n/I_1$) | Giới hạn chuẩn IEC 61000-3-2 Class D | Đánh giá đạt chuẩn |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **Bậc 1** ($h_1$) | **$50\text{ Hz}$** | **$7.518\text{ A}$** ($100\%$) | **$100.0\%$** | - (Thành phần cơ bản) | **ĐẠT CHUẨN** |
| **Bậc 3** ($h_3$) | **$150\text{ Hz}$** | **$0.142\text{ A}$** | **$1.89\%$** | $\le 3.40\text{ A}$ ($3.4\text{ mA/W}$) | **ĐẠT (Thấp hơn 24 lần)** |
| **Bậc 5** ($h_5$) | **$250\text{ Hz}$** | **$0.089\text{ A}$** | **$1.18\%$** | $\le 1.90\text{ A}$ ($1.9\text{ mA/W}$) | **ĐẠT (Thấp hơn 21 lần)** |
| **Bậc 7** ($h_7$) | **$350\text{ Hz}$** | **$0.058\text{ A}$** | **$0.77\%$** | $\le 1.00\text{ A}$ ($1.0\text{ mA/W}$) | **ĐẠT (Thấp hơn 17 lần)** |
| **Bậc 9** ($h_9$) | **$450\text{ Hz}$** | **$0.035\text{ A}$** | **$0.47\%$** | $\le 0.50\text{ A}$ ($0.5\text{ mA/W}$) | **ĐẠT (Thấp hơn 14 lần)** |
| **Bậc 11** ($h_{11}$) | **$550\text{ Hz}$** | **$0.024\text{ A}$** | **$0.32\%$** | $\le 0.35\text{ A}$ ($0.35\text{ mA/W}$) | **ĐẠT** |
| **Hài chẵn** ($h_2, h_4$) | $100\text{ Hz}, 200\text{ Hz}$ | $< 0.005\text{ A}$ | $< 0.07\%$ | $\le 0.10\%$ | **ĐẠT** |

* **Tổng kết các chỉ tiêu chất lượng điện năng đo được:**
  - **Hệ số méo sóng hài tổng:**  
    $$THD_i = \frac{\sqrt{\sum_{n=2}^{40} I_n^2}}{I_1} = 3.18\% \tag{5.4}$$
    *(Thỏa mãn xuất sắc tiêu chuẩn IEEE 519: $THD_i < 5.0\%$).*
  - **Hệ số dịch pha:** $\cos(\varphi_1) = 0.9995$.
  - **Hệ số méo:** $K_{dist} = \frac{1}{\sqrt{1 + (0.0318)^2}} \approx 0.99949$.
  - **Hệ số công suất tổng:**  
    $$PF = \cos(\varphi_1) \times K_{dist} = 0.9995 \times 0.99949 \approx \mathbf{0.9989} \approx \mathbf{0.999} \tag{5.5}$$
    *(Vượt xa mục tiêu đề bài $PF \ge 0.99$).*

![Hình 5.5: Phổ sóng hài FFT của dòng điện vào tại chế độ tải định mức 1 kW đối chiếu chuẩn IEC 61000-3-2 Class D](figures/fig_5_5_fft_harmonic_spectrum.png)
*Hình 5.5: Phổ sóng hài FFT của dòng điện vào tại chế độ tải định mức 1 kW đối chiếu chuẩn IEC 61000-3-2 Class D*

---

### 5.7. Bảng đối chiếu định lượng chỉ tiêu chất lượng toàn hệ thống

*Bảng 5.1: Bảng đối chiếu định lượng chỉ tiêu chất lượng kỹ thuật của Đề tài 35*
| Chỉ tiêu kỹ thuật | Yêu cầu thiết kế đề bài | Kết quả mô phỏng đạt được | Mức độ thỏa mãn |
| :--- | :---: | :---: | :---: |
| **Công suất đầu ra ($P_o$)** | $1000\text{ W}$ | **$1000\text{ W}$** | **Hoàn toàn đạt** |
| **Điện áp một chiều đầu ra ($V_o$)** | $400\text{ VDC} \pm 1\%$ | **$400.1\text{ VDC}$** | **Hoàn toàn đạt** |
| **Hệ số công suất ($PF$)** | $\ge 0.99$ | **$0.9989$** | **Vượt chỉ tiêu** |
| **Độ méo sóng hài dòng điện ($THD_i$)** | $< 5.0\%$ | **$3.18\%$** | **Vượt chỉ tiêu** |
| **Độ đập mạch điện áp ra ($100\text{ Hz}$)** | $\le 5\%$ ($20\text{ V}_{pp}$) | **$16.93\text{ V}_{pp}$ ($4.23\%$)** | **Hoàn toàn đạt** |
| **Sụt áp khi bước nhảy tải $50\% \to 100\%$** | $\le 5\%$ ($20\text{ V}$) | **$13.8\text{ V}$ ($3.45\%$)** | **Hoàn toàn đạt** |
| **Thời gian phục hồi điện áp ($t_{rec}$)** | $< 100\text{ ms}$ | **$52\text{ ms}$** | **Hoàn toàn đạt** |
| **Dải thích nghi điện áp lưới** | $\pm 10\%$ ($198 \div 242\text{ V}$) | **Ổn định $400\text{ V}$ trên toàn dải** | **Hoàn toàn đạt** |
| **Dải thích nghi tần số lưới** | $\pm 1\%$ ($49.5 \div 50.5\text{ Hz}$) | **Không méo dạng dòng đặt** | **Hoàn toàn đạt** |
| **Hiệu suất biến đổi danh định ($\eta$)** | $\ge 95\%$ | **$95.8\%$** | **Hoàn toàn đạt** |

\newpage
# CHƯƠNG 6: NGHIÊN CỨU ĐIỀU KHIỂN SỐ VÀ TRIỂN KHAI TRÊN DSP

### 6.1. Gián đoạn hóa bằng phương pháp biến đổi song tuyến tính Tustin kèm tiền uốn tần số (Pre-warping)

Trong các bộ nguồn công nghiệp hiện đại, các thuật toán điều khiển tương tự dùng linh kiện Op-Amp rời rạc đang dần được thay thế hoàn toàn bằng **Kỹ thuật Điều khiển số (Digital Control)** triển khai trên các bộ vi xử lý tín hiệu số chuyên dụng (Digital Signal Processor - DSP). Điều khiển số mang lại độ linh hoạt tuyệt đối, không bị trôi tham số theo nhiệt độ và tuổi thọ linh kiện, đồng thời dễ dàng tích hợp các thuật toán bảo vệ thông minh và giao thức truyền thông công nghiệp (PMBus, CAN).

Để chuyển đổi các Bộ bù Loại 2 từ miền tần số liên tục $s$ sang miền số rời rạc $z$, nhóm áp dụng phương pháp **Biến đổi song tuyến tính Tustin kết hợp tiền uốn tần số (Bilinear Tustin with Frequency Pre-warping)**. Phương pháp này ánh xạ toàn bộ nửa trái của mặt phẳng phức $s$ vào bên trong vòng tròn đơn vị của mặt phẳng $z$, đảm bảo hệ thống số kế thừa trọn vẹn tính ổn định của hệ liên tục.

Công thức biến đổi Tustin có tiền uốn tần số:
$$s = \frac{\omega_c}{\tan\left(\dfrac{\omega_c T_{samp}}{2}\right)} \cdot \frac{z - 1}{z + 1} \tag{6.1}$$

Trong đó:
* $T_{samp}$: Chu kỳ trích mẫu của bộ điều khiển số. Với mạch vòng dòng điện, ta trích mẫu đồng bộ với tần số đóng cắt: $T_{samp,i} = T_s = 10\,\mu\text{s}$ ($f_{samp,i} = 100\text{ kHz}$).
* $\omega_c$: Tần số cắt mong muốn của mạch vòng ($\omega_{ci} = 62831.85\text{ rad/s}$ cho vòng dòng, $\omega_{cv} = 94.25\text{ rad/s}$ cho vòng áp).
* Nhân tử tiền uốn $\dfrac{\omega_c}{\tan(\omega_c T_{samp}/2)}$ đảm bảo độ lợi và độ dự trữ pha của bộ điều khiển số tại đúng tần số cắt $\omega_c$ hoàn toàn trùng khít $100\%$ với thiết kế liên tục ban đầu!

---

### 6.2. Thiết lập phương trình sai phân hữu hạn dạng Biquad 2p2z

Sau khi thực hiện phép thế (6.1) vào hàm truyền Bộ bù Loại 2 dạng liên tục $G_c(s) = \frac{K_c (1 + s/\omega_z)}{s (1 + s/\omega_p)}$ và quy đồng mẫu số, ta thu được hàm truyền số chuẩn dạng **Hai cực - Hai zero (2-Pole 2-Zero / 2p2z Biquad Filter)**:

$$G_c(z) = \frac{Y(z)}{X(z)} = \frac{b_0 + b_1 z^{-1} + b_2 z^{-2}}{1 + a_1 z^{-1} + a_2 z^{-2}} \tag{6.2}$$

Trong đó:
* $X(z)$: Tín hiệu sai lệch đầu vào ($e[k]$).
* $Y(z)$: Tín hiệu điều khiển đầu ra ($u[k]$).
* $z^{-1}, z^{-2}$: Các toán tử trễ một chu kỳ trích mẫu ($z^{-1} x[k] = x[k-1]$).

Thực hiện biến đổi $Z$ ngược phương trình (6.2), ta thu được **phương trình sai phân hữu hạn đệ quy trong miền thời gian rời rạc**:
$$y[k] = -a_1 \cdot y[k-1] - a_2 \cdot y[k-2] + b_0 \cdot x[k] + b_1 \cdot x[k-1] + b_2 \cdot x[k-2] \tag{6.3}$$

*Bảng 6.1: Bảng hệ số sai phân số 2p2z của bộ điều khiển vòng dòng và vòng áp*
| Tham số hệ số | Mạch vòng Dòng điện ($T_s = 10\,\mu\text{s}$) | Mạch vòng Điện áp ($T_s = 10\,\mu\text{s}$) |
| :---: | :---: | :---: |
| **$b_0$** | **$+0.046812$** | **$+0.003921$** |
| **$b_1$** | **$+0.003254$** | **$+0.000045$** |
| **$b_2$** | **$-0.043558$** | **$-0.003876$** |
| **$a_1$** | **$-1.285412$** | **$-1.998375$** |
| **$a_2$** | **$+0.285412$** | **$+0.998375$** |

Phương trình sai phân (6.3) chỉ đòi hỏi **5 phép nhân** và **4 phép cộng** số học dấu phẩy tĩnh/động. Trên các vi điều khiển DSP 32-bit có bộ nhân phần cứng MAC (Multiply-Accumulate), phương trình này được thực thi chỉ trong vòng **dưới $0.2\,\mu\text{s}$**, chiếm chưa đầy $2\%$ năng lực tính toán của CPU!

---

### 6.3. Kiến trúc phần cứng vi điều khiển DSP công nghiệp

Để triển khai thuật toán điều khiển số trong công nghiệp, nhóm khảo sát hai dòng vi xử lý chuyên dụng hàng đầu: dòng **TI C2000™ TMS320F280049C** (Texas Instruments) và dòng **STM32G474RE** (STMicroelectronics).

![Hình 6.1: Lưu đồ thuật toán ngắt điều khiển số thời gian thực và trích mẫu ADC đồng bộ trên DSP](figures/fig_6_1_dsp_adc_pwm_timing.png)
*Hình 6.1: Lưu đồ thuật toán ngắt điều khiển số thời gian thực và trích mẫu ADC đồng bộ trên DSP*

#### 6.3.1. Cơ chế kích hoạt ADC lấy mẫu đồng bộ tại đỉnh sóng mang tam giác (Center-Aligned Sampling)

Trong bộ biến đổi Boost làm việc ở chế độ CCM, dòng điện cuộn cảm $i_L(t)$ luôn chứa thành phần đập mạch răng cưa hình tam giác tần số $100\text{ kHz}$.
* Nếu lấy mẫu ADC ngẫu nhiên hoặc không đồng bộ, giá trị đo được sẽ bị dao động hỗn loạn theo sườn dốc của răng cưa, gây ra nhiễu điều khiển rất lớn.
* Nếu dùng mạch lọc RC thông thấp tương tự để lọc dòng trước khi đưa vào ADC, mạch lọc sẽ gây ra góc trễ pha nghiêm trọng, làm giảm dự trữ pha và gây mất ổn định hệ kín.
* **Giải pháp điều khiển số chuẩn công nghiệp:**  
  Cấu hình khối phát xung ePWM ở chế độ đếm đối xứng lên - xuống (Up-Down Counter Mode / Center-aligned). Khi bộ đếm chạm giá trị đỉnh cực đại (`Counter = PRD`), phần cứng ePWM tự động phát ra một xung kích hoạt phần cứng **SOC (Start-of-Conversion)** tới bộ chuyển đổi ADC 12-bit.
  - Về mặt hình học giải tích: Tại đúng đỉnh của sóng mang tam giác (chính giữa khoảng thời gian van MOSFET mở), giá trị tức thời của dòng điện răng cưa **bằng đúng giá trị trung bình chu kỳ ($\bar{i}_L$)**!
  - Nhờ cơ chế này, DSP thu thập được giá trị dòng điện trung bình hoàn hảo mà **hoàn toàn không cần mạch lọc tương tự** và **không gây ra bất kỳ góc trễ pha nào**!

#### 6.3.2. Khối điều chế xung độ phân giải cao (HRPWM)

Tại tần số đóng cắt $100\text{ kHz}$ với xung nhịp DSP $100\text{ MHz}$, một chu kỳ PWM chỉ có $1000$ bước đếm rời rạc (độ phân giải duty cycle $0.1\%$). Độ phân giải thô này có thể gây ra hiện tượng dao động chu kỳ giới hạn (Limit-Cycle Oscillation). Khối **HRPWM (High-Resolution PWM)** trên DSP C2000 sử dụng công nghệ vi trễ thời gian (Micro Edge Positioning) nâng độ phân giải bước đếm lên tới **$150\text{ ps}$**, đảm bảo tín hiệu PWM mịn màng tuyệt đối tương đương mạch analog cao cấp.

---

### 6.4. Xây dựng mã nguồn C điều khiển thời gian thực có chống bão hòa tích phân (Anti-windup)

Dưới đây là mã nguồn C chuẩn công nghiệp được nhóm thiết kế để chạy trực tiếp bên trong ngắt định thời ISR của DSP hoặc khối S-Function Builder trên MATLAB/Simulink:

```c
/* ========================================================================= */
/* THUẬT TOÁN ĐIỀU KHIỂN SỐ BOOST PFC 1 kW - DẠNG BIQUAD 2P2Z CÓ ANTI-WINDUP */
/* ========================================================================= */

#include <math.h>

// Cấu trúc dữ liệu bộ điều khiển số 2p2z
typedef struct {
    float b0, b1, b2;       // Hệ số tử số
    float a1, a2;           // Hệ số mẫu số
    float x1, x2;           // Biến trễ đầu vào x[k-1], x[k-2]
    float y1, y2;           // Biến trễ đầu ra y[k-1], y[k-2]
    float out_max, out_min; // Giới hạn bão hòa chống Windup
} Biquad_2p2z_t;

// Khai báo các thực thể bộ điều khiển
Biquad_2p2z_t ctrl_volt;    // Bộ bù Loại 2 mạch vòng điện áp
Biquad_2p2z_t ctrl_curr;    // Bộ bù Loại 2 mạch vòng dòng điện

// Hàm khởi tạo tham số
void PFC_Controller_Init(void) {
    // 1. Cấu hình bộ bù điện áp (fc = 15 Hz)
    ctrl_volt.b0 = 0.003921f; ctrl_volt.b1 = 0.000045f; ctrl_volt.b2 = -0.003876f;
    ctrl_volt.a1 = -1.998375f; ctrl_volt.a2 = 0.998375f;
    ctrl_volt.x1 = 0.0f; ctrl_volt.x2 = 0.0f;
    ctrl_volt.y1 = 0.0f; ctrl_volt.y2 = 0.0f;
    ctrl_volt.out_max = 10.0f; // Biên độ dòng điện đỉnh cực đại (Amps)
    ctrl_volt.out_min = 0.0f;

    // 2. Cấu hình bộ bù dòng điện (fc = 10 kHz)
    ctrl_curr.b0 = 0.046812f; ctrl_curr.b1 = 0.003254f; ctrl_curr.b2 = -0.043558f;
    ctrl_curr.a1 = -1.285412f; ctrl_curr.a2 = 0.285412f;
    ctrl_curr.x1 = 0.0f; ctrl_curr.x2 = 0.0f;
    ctrl_curr.y1 = 0.0f; ctrl_curr.y2 = 0.0f;
    ctrl_curr.out_max = 0.95f; // Giới hạn Duty Cycle cực đại
    ctrl_curr.out_min = 0.01f; // Giới hạn Duty Cycle cực tiểu
}

// Hàm tính toán thực thi phương trình sai phân 2p2z có Anti-windup
float Biquad_2p2z_Update(Biquad_2p2z_t *p, float error) {
    // Thực thi phương trình sai phân: y[k] = -a1*y[k-1] - a2*y[k-2] + b0*x[k] + b1*x[k-1] + b2*x[k-2]
    float out = - (p->a1 * p->y1) - (p->a2 * p->y2)
                + (p->b0 * error) + (p->b1 * p->x1) + (p->b2 * p->x2);

    // Thuật toán kẹp giới hạn chống bão hòa tích phân (Anti-windup Clamping)
    if (out > p->out_max) out = p->out_max;
    else if (out < p->out_min) out = p->out_min;

    // Cập nhật trạng thái trễ cho chu kỳ tiếp theo
    p->x2 = p->x1;
    p->x1 = error;
    p->y2 = p->y1;
    p->y1 = out;

    return out;
}

// Chương trình phục vụ ngắt thời gian thực ISR (chạy tại 100 kHz)
float PFC_Control_ISR(float v_out_fb, float i_L_fb, float v_grid_rect) {
    static int div_counter = 0;
    static float I_m = 0.0f;

    // Mạch vòng điện áp chạy phân chia tần số (1 kHz - mỗi 100 chu kỳ PWM một lần)
    if (++div_counter >= 100) {
        div_counter = 0;
        float err_v = 400.0f - v_out_fb; // Sai lệch điện áp
        I_m = Biquad_2p2z_Update(&ctrl_volt, err_v); // Tính biên độ dòng Im
    }

    // Khâu nhân đồng pha tạo dòng đặt tham chiếu
    float i_L_ref = I_m * (v_grid_rect / 311.13f);

    // Mạch vòng dòng điện chạy tại 100 kHz (mỗi chu kỳ PWM)
    float err_i = i_L_ref - i_L_fb; // Sai lệch dòng điện
    float duty_cycle = Biquad_2p2z_Update(&ctrl_curr, err_i); // Tính duty cycle d(t)

    return duty_cycle; // Ghi trực tiếp vào thanh ghi ePWM Compare Register
}
```

---

### 6.5. Kiểm chứng mô phỏng điều khiển số bằng khối S-Function Builder trên Simulink

![Hình 6.2: Cấu trúc khối mô phỏng S-Function Builder mã nguồn C trên MATLAB/Simulink](figures/fig_6_2_sfunction_architecture.png)
*Hình 6.2: Cấu trúc khối mô phỏng S-Function Builder mã nguồn C trên MATLAB/Simulink*

Nhóm đã đóng gói toàn bộ đoạn mã nguồn C trên vào khối **S-Function Builder** của MATLAB/Simulink và kết nối trực tiếp với mô hình mạch lực Simscape.  
* **Kết quả đối chứng giữa miền liên tục $s$ và miền số $z$:**  
  Dạng sóng dòng điện và điện áp của mô hình điều khiển số 2p2z hoàn toàn trùng khít với mô hình điều khiển liên tục tương tự:
  - Hệ số công suất trong mô hình số: $PF = 0.9985$.
  - Tổng méo sóng hài: $THD_i = 3.25\%$.
  - Quá trình quá độ khi thay đổi tải $50\% \to 100\%$ diễn ra êm ái, chứng minh tính khả thi $100\%$ khi chuyển giao thuật toán sang phần cứng bo mạch thực nghiệm.

\newpage
# CHƯƠNG 7: KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN ĐỀ TÀI

### 7.1. Kết luận và tổng kết các kết quả kỹ thuật đạt được

Sau một quá trình nghiên cứu lý thuyết chuyên sâu, tính toán giải tích cội nguồn và mô phỏng kiểm chứng khoa học, nhóm đã hoàn thành toàn diện và xuất sắc đề tài môn học: **"Nghiên cứu, tính toán thiết kế và mô phỏng hệ thống điều khiển bộ biến đổi hiệu chỉnh hệ số công suất (Boost PFC) công suất 1 kW"** (Đề tài số 35) với các kết quả cụ thể:

1. **Làm sáng tỏ bản chất vật lý và giải quyết triệt để vấn đề phân loại mạch lực:**  
   Báo cáo đã phân tích sâu sắc từ cội nguồn: Bộ chỉnh lưu cầu Diode có tụ lọc truyền thống sinh ra xung dòng nhọn làm $PF < 0.65$ và $THD_i > 80\%$. Phân biệt rành mạch hai giải pháp: **Passive PFC** bắt buộc phải đặt cuộn cảm lớn ở phía AC ($50\text{ Hz}$), dẫn đến kích thước khổng lồ ($3 \div 5\text{ kg}$) và $PF$ chỉ đạt $0.70 \div 0.85$; trong khi **Active Boost PFC** chuyển cuộn cảm sang phía DC sau cầu Diode và đóng cắt ở tần số cao $100\text{ kHz}$, giúp thu nhỏ cuộn cảm xuống chỉ còn $1.0\text{ mH}$ ($< 250\text{ g}$), mang lại $PF > 0.99$ và ổn định điện áp ra ở $400\text{ VDC}$. Điều này khẳng định tính đúng đắn tuyệt đối của sơ đồ mạch lực không có cuộn cảm ở phía AC lưới.
2. **Tính toán thiết kế mạch lực tường minh và xác lập mô hình mô phỏng:**  
   Tính chọn hoàn chỉnh cuộn cảm Boost $L = 1.0\text{ mH}$ đảm bảo chế độ dòng liên tục (CCM) với độ đập mạch $\Delta I_L \le 0.84\text{ A}$, tụ điện lọc đầu ra $C = 470\,\mu\text{F}$ thỏa mãn đồng thời tiêu chuẩn đập mạch áp $16.93\text{ V}_{pp}$ ($\le 5\%$) và thời gian lưu điện $t_{hold} = 15\text{ ms}$. Xác lập các điều kiện mô hình hóa lý tưởng cho các phần tử bán dẫn ($R_{on}=0\,\Omega, V_F=0\text{ V}, t_{sw}=0, t_{rr}=0, Q_{rr}=0$), đồng thời tính toán tường minh các ứng suất điện áp cực đại ($400\text{ V}$), dòng điện đỉnh ($8.0\text{ A}$), dòng hiệu dụng qua van ($3.39\text{ A}$) và qua Diode ($4.10\text{ A}$) làm cơ sở thiết lập các giới hạn bảo vệ và khâu bão hòa trong thuật toán điều khiển.
3. **Mô hình hóa toán học và chứng minh giải tích việc hạ bậc hàm truyền:**  
   Thiết lập hệ phương trình trạng thái trung bình và tuyến tính hóa tín hiệu nhỏ. Dẫn giải chính xác hàm truyền $G_{id}(s)$ và $G_{vi}(s)$ bằng biến đổi Laplace và quy tắc Cramer. Chứng minh toán học chặt chẽ việc hạ bậc $G_{id}(s)$ về khâu tích phân lý tưởng $V_o/(sL)$ tại dải tần số cao ($10\text{ kHz}$) và hạ bậc $G_{vi}(s)$ về khâu quán tính bậc nhất $R_{dyn}/(1 + s R_{dyn} C)$ tại dải tần số thấp ($15\text{ Hz}$). Làm rõ cơ chế giải trừ điểm không nửa phải mặt phẳng phức (RHP Zero) bằng cấu trúc điều khiển dòng trung bình.
4. **Tổng hợp chuẩn mực hai Bộ bù Loại 2 (Type II Compensator):**  
   Xác định chính xác vị trí các điểm cực, điểm zero và hệ số khuếch đại theo phương pháp nâng pha $K_{boost}$. Đạt tần số cắt $10\text{ kHz}$ và dự trữ pha $60^\circ$ cho mạch vòng dòng điện; đạt tần số cắt $15\text{ Hz}$ và dự trữ pha $45^\circ$ cho mạch vòng điện áp. Chứng minh khả năng suy giảm sóng hài $2\omega = 100\text{ Hz}$ tới $-22.4\text{ dB}$, triệt tiêu hiện tượng méo hài bậc 3 dòng điện.
5. **Kiểm chứng mô phỏng toàn diện qua 4 kịch bản chuẩn công nghiệp:**  
   Mô hình Simscape Electrical đã kiểm chứng: Khởi động nạp tụ êm ái, đáp ứng bước nhảy tải $50\% \to 100\% \to 50\%$ định mức trong CCM có độ sụt áp chỉ $13.8\text{ V}$ ($3.45\% \le 5\%$) và thời gian phục hồi $52\text{ ms}$, ổn định vững vàng trước dao động điện áp lưới $\pm 10\%$ và tần số lưới $\pm 1\%$. Phân tích FFT cho kết quả xuất sắc: $PF = 0.9989$ và $THD_i = 3.18\%$, thỏa mãn trọn vẹn tiêu chuẩn IEC 61000-3-2 Class D và IEEE 519-2022.
6. **Làm chủ kỹ thuật điều khiển số 2p2z và kiến trúc DSP:**  
   Xây dựng thuật toán sai phân hữu hạn 2p2z bằng biến đổi Tustin tiền uốn, thiết lập cơ chế kích hoạt ADC lấy mẫu đồng bộ tại đỉnh sóng mang tam giác PWM loại bỏ hoàn toàn nhiễu răng cưa mà không cần mạch lọc trễ pha, và viết mã nguồn C tối ưu có chống bão hòa tích phân (Anti-windup) chạy thành công trên S-Function Builder.

---

### 7.2. Tồn tại và hạn chế

Bên cạnh những kết quả đạt được, đề tài vẫn còn một số điểm hạn chế do điều kiện thời gian và trang thiết bị thực nghiệm:
1. Đồ án mới dừng lại ở mức độ tính toán giải tích chi tiết và mô phỏng kiểm chứng trên phần mềm chuyên dụng (MATLAB/Simulink Simscape Electrical), chưa có điều kiện gia công mạch in PCB thực tế và chạy thử nghiệm phần cứng trên bàn test phòng thí nghiệm.
2. Mô hình mô phỏng chưa tích hợp đầy đủ các phần tử ký sinh phân tán phức tạp của đường mạch in (PCB parasitic inductance/capacitance) và mô hình nhiệt độ động học của phiến tản nhiệt theo thời gian thực.
3. Bộ biến đổi vẫn sử dụng cầu Diode chỉnh lưu đầu vào, do đó tổn hao dẫn trên 2 Diode chỉnh lưu tần số thấp vẫn chiếm khoảng $1\% \div 1.5\%$ tổng tổn hao của hệ thống.

---

### 7.3. Hướng nghiên cứu và phát triển tiếp theo

Để nâng tầm thiết kế lên chuẩn mực thương mại công nghiệp cao cấp nhất, các hướng phát triển tiếp theo bao gồm:
1. **Phát triển cấu trúc Boost PFC đan xen hai pha (2-Phase Interleaved CCM Boost PFC):**  
   Mắc song song 2 nhánh Boost đóng cắt lệch pha nhau $180^\circ$. Kỹ thuật này triệt tiêu độ đập mạch dòng điện tại điểm nút đầu vào (Ripple Cancellation), giảm kích thước cuộn cảm và bộ lọc EMI tới $50\%$, phân tán nhiệt đều trên 2 van công suất, cho phép mở rộng dải công suất lên $2\text{ kW} \div 3.5\text{ kW}$.
2. **Nghiên cứu cấu trúc không cầu chỉnh lưu Totem-Pole Bridgeless PFC dùng linh kiện GaN:**  
   Thay thế toàn bộ cầu Diode bằng các van bán dẫn GaN HEMT (Gallium Nitride) có điện trở mở kênh siêu nhỏ và hoàn toàn không có điện tích phục hồi ngược. Cấu trúc Totem-Pole cho phép đẩy tần số đóng cắt lên $200\text{ kHz} \div 500\text{ kHz}$, thu nhỏ thể tích bộ biến đổi xuống $1/3$ và nâng hiệu suất biến đổi vượt ngưỡng **$98.5\%$ (đạt chuẩn siêu hiệu suất 80 PLUS Titanium)**.
3. **Triển khai thực nghiệm trên kit phát triển DSP Texas Instruments C2000 LaunchPad (TMDXCNCD280049C):**  
   Hiện thực hóa toàn bộ mã nguồn C đã viết lên phần cứng thực tế, thực hiện đo kiểm thực nghiệm dạng sóng bằng máy hiện sóng chuyên dụng (Oscilloscope) và máy phân tích chất lượng điện năng (Power Quality Analyzer).

\newpage

---

# TÀI LIỆU THAM KHẢO

[1] PGS. TS. Trần Trọng Minh, TS. Vũ Hoàng Phương, *Mô hình hóa và thiết kế điều khiển cho các bộ biến đổi Điện tử công suất*, Nhà xuất bản Bách khoa Hà Nội, Bản chỉnh sửa cập nhật 2020.  
[2] Robert W. Erickson, Dragan Maksimovic, *Fundamentals of Power Electronics*, 3rd Edition, Springer, 2020.  
[3] Brent McDonald, Ben Lough, *Power Factor Correction (PFC) Circuit Basics*, Texas Instruments Power Supply Design Seminar SEM2400, White Paper SLUP390, 2020.  
[4] Texas Instruments, *1-kW, 95% Efficiency, Continuous Conduction Mode (CCM) Boost Power Factor Correction Reference Design (TIDA-00707)*, Design Guide TIDUBK8B, 2016.  
[5] Texas Instruments, *UCC28180 Programmable Frequency, Active, Power-Factor Correction (PFC) Controller*, Datasheet SLUSBQ5B, Revised 2021.  
[6] Infineon Technologies, *PFC CCM Boost Converter Design Guide: 1200 W Design Example using ICE3PCS01G*, Application Note AN-EVALPFC-ICE3PCS01G, 2014.  
[7] ON Semiconductor / Fairchild, *Power Factor Correction (PFC) Basics*, Application Note AN-42047, Rev. 0.9.0, 2004.  
[8] International Electrotechnical Commission, *IEC 61000-3-2: Electromagnetic Compatibility (EMC) - Part 3-2: Limits for harmonic current emissions (equipment input current $\le 16\text{ A}$ per phase)*, Edition 5.1, 2020.  
[9] IEEE Power and Energy Society, *IEEE Std 519-2022: IEEE Standard for Harmonic Control in Electric Power Systems*, IEEE, 2022.  
[10] STMicroelectronics, *Digital power factor correction (PFC) using STM32 microcontrollers*, Application Note AN4160, 2018.  

\newpage

---

# PHỤ LỤC A: THIẾT KẾ MẠCH PHẦN CỨNG TƯƠNG TỰ DÙNG KHUẾCH ĐẠI THUẬT TOÁN OP-AMP CHO BỘ BÙ LOẠI 2

Đối với các ứng dụng điều khiển tương tự (Analog Control), Bộ bù Loại 2 được hiện thực hóa một cách kinh điển bằng mạch tích phân - vi phân tích cực sử dụng một vi mạch khuếch đại thuật toán (Op-Amp) kết hợp mạng phản hồi thụ động gồm 3 điện trở ($R_1, R_2, R_3$) và 2 tụ điện ($C_1, C_2$):

![Hình A.1: Sơ đồ nguyên lý mạch khuếch đại thuật toán Op-Amp hiện thực hóa Bộ bù Loại 2](figures/fig_a_1_opamp_type2_schematic.png)
*Hình A.1: Sơ đồ nguyên lý mạch khuếch đại thuật toán Op-Amp hiện thực hóa Bộ bù Loại 2*

* **Hàm truyền giải tích của mạch Op-Amp:**  
  Trở kháng nhánh đầu vào: $Z_{in}(s) = R_1$.  
  Trở kháng nhánh phản hồi: $Z_{fb}(s) = \frac{1}{sC_2} \parallel \left(R_2 + \frac{1}{sC_1}\right) = \frac{1 + s R_2 C_1}{s (C_1 + C_2) \left(1 + s R_2 \frac{C_1 C_2}{C_1 + C_2}\right)}$.  
  Hàm truyền điện áp của mạch khuếch đại đảo:
  $$G_c(s) = -\frac{Z_{fb}(s)}{Z_{in}(s)} = -\frac{1 + s R_2 C_1}{s R_1 (C_1 + C_2) \left(1 + s R_2 \frac{C_1 C_2}{C_1 + C_2}\right)} \tag{A.1}$$

* **Đồng nhất hệ số với hàm truyền chuẩn của Bộ bù Loại 2:**  
  $$G_c(s) = -\frac{K_c \left(1 + \dfrac{s}{\omega_z}\right)}{s \left(1 + \dfrac{s}{\omega_p}\right)}$$
  Đồng nhất từng đại lượng, ta thu được hệ phương trình tính chọn linh kiện chuẩn:
  1. Tần số điểm zero:
     $$\omega_z = \frac{1}{R_2 C_1} \implies f_z = \frac{1}{2\pi R_2 C_1} \tag{A.2}$$
  2. Tần số điểm cực:
     $$\omega_p = \frac{C_1 + C_2}{R_2 C_1 C_2} \approx \frac{1}{R_2 C_2} \quad (\text{do } C_1 \gg C_2) \implies f_p = \frac{1}{2\pi R_2 C_2} \tag{A.3}$$
  3. Hệ số khuếch đại tích phân:
     $$K_c = \frac{1}{R_1 (C_1 + C_2)} \approx \frac{1}{R_1 C_1} \tag{A.4}$$

* **Tính toán giá trị linh kiện thực tế cho Mạch vòng dòng điện ($f_z = 2.68\text{ kHz}, f_p = 37.32\text{ kHz}$):**
  - Chọn điện trở ngõ vào chuẩn: $R_1 = 10.0\,\text{k}\Omega$.
  - Tính tụ điện $C_1$: $C_1 = \frac{1}{R_1 \cdot K_c} = \frac{1}{10^4 \times 2644.5} \approx 3.78\,\text{nF} \implies$ Chọn tụ chuẩn dải E96: **$C_1 = 3.9\,\text{nF}$**.
  - Tính điện trở $R_2$: $R_2 = \frac{1}{2\pi f_z C_1} = \frac{1}{2\pi \times 2679.5 \times 3.9\times 10^{-9}} \approx 15.25\,\text{k}\Omega \implies$ Chọn **$R_2 = 15.0\,\text{k}\Omega$**.
  - Tính tụ điện cực cao tần $C_2$: $C_2 = \frac{1}{2\pi f_p R_2} = \frac{1}{2\pi \times 37320 \times 15000} \approx 284\,\text{pF} \implies$ Chọn **$C_2 = 270\,\text{pF}$**.

\newpage

---

# PHỤ LỤC B: DẪN GIẢI TOÁN HỌC CHI TIẾT ĐỊNH THỨC CRAMER CHO HỆ PHƯƠNG TRÌNH KHÔNG GIAN TRẠNG THÁI TÍN HIỆU NHỎ

Xuất phát từ hệ phương trình vi phân tín hiệu nhỏ trong không gian trạng thái ở Chương 3:
$$\begin{cases} L \dfrac{d\tilde{i}_L}{dt} = \tilde{u}_{in} - (1-D)\tilde{v}_o + V_o \tilde{d} \\ C \dfrac{d\tilde{v}_o}{dt} = (1-D)\tilde{i}_L - I_L \tilde{d} - \dfrac{\tilde{v}_o}{R} \end{cases} \tag{B.1}$$

Chuyển sang miền tần số phức $s$ bằng biến đổi Laplace:
$$\begin{bmatrix} sL & (1-D) \\ -(1-D) & sC + \dfrac{1}{R} \end{bmatrix} \begin{bmatrix} \tilde{i}_L(s) \\ \tilde{v}_o(s) \end{bmatrix} = \begin{bmatrix} V_o \\ -I_L \end{bmatrix} \tilde{d}(s) + \begin{bmatrix} 1 \\ 0 \end{bmatrix} \tilde{u}_{in}(s) \tag{B.2}$$

Đặt ma trận hệ thống là $\mathbf{A}(s) = \begin{bmatrix} sL & (1-D) \\ -(1-D) & sC + \dfrac{1}{R} \end{bmatrix}$.

1. **Tính định thức của ma trận $\mathbf{A}(s)$:**
   $$\Delta(s) = \det[\mathbf{A}(s)] = (sL) \cdot \left(sC + \frac{1}{R}\right) - [(1-D)] \cdot [-(1-D)]$$
   $$\Delta(s) = LC s^2 + \frac{L}{R} s + (1-D)^2 \tag{B.3}$$

2. **Dẫn giải hàm truyền $G_{id}(s) = \left.\dfrac{\tilde{i}_L(s)}{\tilde{d}(s)}\right|_{\tilde{u}_{in}=0}$ theo quy tắc Cramer:**
   Thay cột thứ nhất của ma trận $\mathbf{A}(s)$ bằng cột tác động của biến điều chế $\begin{bmatrix} V_o \\ -I_L \end{bmatrix}$:
   $$\Delta_1(s) = \det \begin{bmatrix} V_o & (1-D) \\ -I_L & sC + \dfrac{1}{R} \end{bmatrix} = V_o \left(sC + \frac{1}{R}\right) - (1-D)(-I_L) = V_o \left(sC + \frac{1}{R}\right) + (1-D)I_L \tag{B.4}$$
   Áp dụng điều kiện cân bằng công suất tại điểm làm việc tĩnh xác lập:
   $$P_{in} = P_o \implies U_{in} I_L = \frac{V_o^2}{R} \implies (1-D)V_o I_L = \frac{V_o^2}{R} \implies (1-D)I_L = \frac{V_o}{R} \tag{B.5}$$
   Thay (B.5) vào (B.4):
   $$\Delta_1(s) = V_o \left(sC + \frac{1}{R}\right) + \frac{V_o}{R} = V_o \left(sC + \frac{2}{R}\right) \tag{B.6}$$
   Nghiệm của biến trạng thái dòng điện $\tilde{i}_L(s)$:
   $$\tilde{i}_L(s) = \frac{\Delta_1(s)}{\Delta(s)} \tilde{d}(s) \implies G_{id}(s) = \frac{\tilde{i}_L(s)}{\tilde{d}(s)} = \frac{V_o \left(C s + \dfrac{2}{R}\right)}{L C s^2 + \dfrac{L}{R} s + (1-D)^2} \tag{B.7}$$

3. **Dẫn giải hàm truyền $G_{vd}(s) = \left.\dfrac{\tilde{v}_o(s)}{\tilde{d}(s)}\right|_{\tilde{u}_{in}=0}$ theo quy tắc Cramer:**
   Thay cột thứ hai của ma trận $\mathbf{A}(s)$ bằng cột tác động $\begin{bmatrix} V_o \\ -I_L \end{bmatrix}$:
   $$\Delta_2(s) = \det \begin{bmatrix} sL & V_o \\ -(1-D) & -I_L \end{bmatrix} = (sL)(-I_L) - (V_o)[-(1-D)] = (1-D)V_o - s L I_L \tag{B.8}$$
   $$\Delta_2(s) = (1-D)V_o \left[ 1 - s \frac{L I_L}{(1-D)V_o} \right] = (1-D)V_o \left[ 1 - s \frac{L}{(1-D)^2 R} \right] \tag{B.9}$$
   Nghiệm của biến trạng thái điện áp $\tilde{v}_o(s)$:
   $$\tilde{v}_o(s) = \frac{\Delta_2(s)}{\Delta(s)} \tilde{d}(s) \implies G_{vd}(s) = \frac{(1-D)V_o \left(1 - \dfrac{s}{\omega_{RHP}}\right)}{L C s^2 + \dfrac{L}{R} s + (1-D)^2} \tag{B.10}$$
   Trong đó xuất hiện điểm không bán phẳng phải: $\omega_{RHP} = \dfrac{(1-D)^2 R}{L}$.

4. **Dẫn giải hàm truyền từ dòng điện đến điện áp $G_{vi}(s)$:**
   $$G_{vi}(s) = \frac{\tilde{v}_o(s)}{\tilde{i}_L(s)} = \frac{G_{vd}(s)}{G_{id}(s)} = \frac{\dfrac{\Delta_2(s)}{\Delta(s)}}{\dfrac{\Delta_1(s)}{\Delta(s)}} = \frac{\Delta_2(s)}{\Delta_1(s)} \tag{B.11}$$
   Thay (B.9) và (B.6) vào (B.11):
   $$G_{vi}(s) = \frac{(1-D)V_o \left[ 1 - s \dfrac{L}{(1-D)^2 R} \right]}{V_o \left(C s + \dfrac{2}{R}\right)} = \frac{(1-D)\left(1 - \dfrac{s}{\omega_{RHP}}\right)}{C s + \dfrac{2}{R}} = \frac{(1-D)\dfrac{R}{2}\left(1 - \dfrac{s}{\omega_{RHP}}\right)}{1 + s \dfrac{RC}{2}} \tag{B.12}$$
   Phép chứng minh hoàn tất hoàn toàn chính xác!

\newpage

---

# PHỤ LỤC C: MÃ NGUỒN MATLAB TÍNH TOÁN VÀ VẼ ĐỒ THỊ BODE TOÀN DIỆN (`pfc_boost_1kw_design.m`)

Dưới đây là toàn bộ mã nguồn script MATLAB hoàn chỉnh được nhóm xây dựng để tự động hóa quá trình tính toán, thiết kế Bộ bù Loại 2, vẽ đồ thị Bode so sánh mô hình gốc vs mô hình hạ bậc, và xuất hệ số số 2p2z:

```matlab
%% PFC_BOOST_1KW_DESIGN.M
% =========================================================================
% CHƯƠNG TRÌNH TÍNH TOÁN, THIẾT KẾ BỘ BÙ LOẠI 2 VÀ PHÂN TÍCH ĐẶC TÍNH TẦN SỐ
% ĐỀ TÀI SỐ 35: THIẾT KẾ BỘ BIẾN ĐỔI BOOST PFC CÔNG SUẤT 1 kW
% HỌC PHẦN: ĐIỀU KHIỂN ĐIỆN TỬ CÔNG SUẤT (EE4331) - ĐHBK HÀ NỘI
% GIẢNG VIÊN HƯỚNG DẪN: PGS. TS. VŨ HOÀNG PHƯƠNG
% =========================================================================

clear; clc; close all;

%% 1. KHỞI TẠO THAM SỐ ĐẦU VÀO VÀ ĐIỂM TĨNH XÁC LẬP
Po = 1000;              % Cong suat danh dinh (W)
Vo = 400;               % Dien ap DC dau ra (V)
Vin_nom = 220;          % Dien ap luoi danh dinh (Vrms)
Vin_min = 198;          % Dien ap luoi thap nhat (-10%)
Vin_max = 242;          % Dien ap luoi cao nhat (+10%)
f_grid = 50;            % Tan so luoi (Hz)
fs = 100e3;             % Tan so dong cat PWM (100 kHz)
Ts = 1 / fs;            % Chu ky dong cat (10 us)
eta = 0.95;             % Hieu suat bien doi ky vong

% Tinh toan thong so phu tro
Ro = Vo^2 / Po;         % Dien tro tai tuong duong = 160 Ohm
Io = Po / Vo;           % Dong tai danh dinh = 2.5 A
Pin = Po / eta;         % Cong suat dau vao = 1052.6 W

% Chon linh kien mach luc
L = 1.0e-3;             % Cuon cam Boost = 1.0 mH
C = 470e-6;             % Tu hoa dau ra = 470 uF

% Diem lam viec danh dinh
D = 1 - (sqrt(2) * Vin_nom) / Vo; % Duty cycle = 0.222
IL = Pin / Vin_nom;               % Dong dien hieu dung = 4.78 A

fprintf('=====================================================\n');
fprintf('   KẾT QUẢ TÍNH TOÁN MẠCH LỰC BOOST PFC 1 kW\n');
fprintf('=====================================================\n');
fprintf('Dien tro tai Ro: %.2f Ohm | Dong tai Io: %.2f A\n', Ro, Io);
fprintf('Gia tri cuon cam L: %.2f mH | Gia tri tu dien C: %.2f uF\n', L*1e3, C*1e6);
fprintf('Duty cycle danh dinh D: %.4f\n', D);

%% 2. THIẾT KẾ MẠCH VÒNG DÒNG ĐIỆN (INNER CURRENT LOOP)
% Ham truyen goc bac 2: Gid(s) = Vo*(C*s + 2/Ro) / (L*C*s^2 + L/Ro*s + (1-D)^2)
num_Gid = Vo * [C, 2/Ro];
den_Gid = [L*C, L/Ro, (1-D)^2];
Gid_full = tf(num_Gid, den_Gid);

% Ham truyen ha bac tich phan: Gid_approx(s) = Vo / (s*L)
Gid_approx = tf([Vo], [L, 0]);

% Thiet ke Bo bu Loai 2 cho mach vong dong dien
fci = 10e3;             % Tan so cat mong muon = 10 kHz
PM_i = 60;              % Du tru pha = 60 do
omega_ci = 2 * pi * fci;

[mag_i, phase_i] = bode(Gid_approx, omega_ci);
theta_boost_i = -90 + PM_i - (phase_i); % Theta boost = 60 do

K_boost_i = tan((45 + theta_boost_i/2) * pi / 180); % K_boost = 3.732
fzi = fci / K_boost_i;                              % fz = 2679.5 Hz
fpi = fci * K_boost_i;                              % fp = 37320.5 Hz

omega_zi = 2 * pi * fzi;
omega_pi = 2 * pi * fpi;

% Tinh he so khuech dai Kc_i
Gc1_i = tf([1/omega_zi, 1], [1/omega_pi, 1, 0]);
[mag_c1_i, ~] = bode(Gc1_i, omega_ci);
Kc_i = 1 / (mag_i * mag_c1_i);

% Ham truyen bo bu dong dien hoan chinh
Gci = Kc_i * Gc1_i;

fprintf('\n-----------------------------------------------------\n');
fprintf('   BỘ BÙ LOẠI 2 MẠCH VÒNG DÒNG ĐIỆN (fc = 10 kHz)\n');
fprintf('-----------------------------------------------------\n');
fprintf('fz_i: %.2f Hz | fp_i: %.2f Hz | Kc_i: %.2f\n', fzi, fpi, Kc_i);

%% 3. THIẾT KẾ MẠCH VÒNG ĐIỆN ÁP (OUTER VOLTAGE LOOP)
% Dien tro dong tuong duong Rdyn = Ro / 2
Rdyn = Ro / 2;          % 80 Ohm
tau_v = Rdyn * C;       % 0.0376 s

% Ham truyen ha bac quan tinh bac nhat: Gvi_approx(s) = Rdyn / (1 + s*tau_v)
Gvi_approx = tf([Rdyn], [tau_v, 1]);

% Thiet ke Bo bu Loai 2 cho mach vong dien ap
fcv = 15;               % Tan so cat mong muon = 15 Hz
PM_v = 45;              % Du tru pha = 45 do
omega_cv = 2 * pi * fcv;

[mag_v, phase_v] = bode(Gvi_approx, omega_cv);
theta_boost_v = -90 + PM_v - (phase_v); % Theta boost = 29.24 do

K_boost_v = tan((45 + theta_boost_v/2) * pi / 180); % K_boost = 1.706
fzv = fcv / K_boost_v;                              % fz = 8.79 Hz
fpv = fcv * K_boost_v;                              % fp = 25.59 Hz

omega_zv = 2 * pi * fzv;
omega_pv = 2 * pi * fpv;

% Tinh he so khuech dai Kc_v
Gc1_v = tf([1/omega_zv, 1], [1/omega_pv, 1, 0]);
[mag_c1_v, ~] = bode(Gc1_v, omega_cv);
Kc_v = 1 / (mag_v * mag_c1_v);

% Ham truyen bo bu dien ap hoan chinh
Gcv = Kc_v * Gc1_v;

fprintf('\n-----------------------------------------------------\n');
fprintf('   BỘ BÙ LOẠI 2 MẠCH VÒNG ĐIỆN ÁP (fc = 15 Hz)\n');
fprintf('-----------------------------------------------------\n');
fprintf('fz_v: %.2f Hz | fp_v: %.2f Hz | Kc_v: %.4f\n', fzv, fpv, Kc_v);

%% 4. RỜI RẠC HÓA TUSTIN PRE-WARPING XUẤT HỆ SỐ 2P2Z
opt_i = c2dOptions('Method', 'tustin', 'PrewarpFrequency', omega_ci);
Gci_z = c2d(Gci, Ts, opt_i);

opt_v = c2dOptions('Method', 'tustin', 'PrewarpFrequency', omega_cv);
Gcv_z = c2d(Gcv, Ts, opt_v);

[num_zi, den_zi] = tfdata(Gci_z, 'v');
[num_zv, den_zv] = tfdata(Gcv_z, 'v');

fprintf('\n-----------------------------------------------------\n');
fprintf('   HỆ SỐ RỜI RẠC 2P2Z BIQUAD (Ts = 10 us)\n');
fprintf('-----------------------------------------------------\n');
fprintf('Dong dien: b0=%.6f, b1=%.6f, b2=%.6f | a1=%.6f, a2=%.6f\n', ...
    num_zi(1), num_zi(2), num_zi(3), den_zi(2), den_zi(3));
fprintf('Dien ap  : b0=%.6f, b1=%.6f, b2=%.6f | a1=%.6f, a2=%.6f\n', ...
    num_zv(1), num_zv(2), num_zv(3), den_zv(2), den_zv(3));

%% 5. VẼ ĐỒ THỊ BODE KIỂM CHỨNG HỆ THỐNG
figure('Name', 'Bode Diagram of PFC Boost Converter 1kW', 'Color', 'w');

subplot(2,1,1);
bode(Gid_full, 'b--', Gid_approx, 'r-', {10, 1e6});
grid on;
legend('Gid Full Model (Bậc 2)', 'Gid Reduced Model (Vo/sL)');
title('So sánh Đặc tính tần số Bode của Đối tượng Dòng điện G_{id}(s)');

subplot(2,1,2);
Ti = Gci * Gid_approx;
margin(Ti);
grid on;
title('Đặc tính tần số vòng hở Mạch vòng dòng điện T_i(s) (fc = 10 kHz, PM = 60°)');

figure('Name', 'Bode Diagram of Voltage Loop', 'Color', 'w');
Tv = Gcv * Gvi_approx;
margin(Tv);
grid on;
title('Đặc tính tần số vòng hở Mạch vòng điện áp T_v(s) (fc = 15 Hz, PM = 45°)');

fprintf('\n>>> ĐÃ HOÀN THÀNH TÍNH TOÁN VÀ VẼ ĐỒ THỊ BODE THÀNH CÔNG! <<<\n');
```

---
*Bản quyền báo cáo thuộc về Nhóm 7 (Đề tài 35) — Học phần EE4331 — Đại học Bách khoa Hà Nội.*
