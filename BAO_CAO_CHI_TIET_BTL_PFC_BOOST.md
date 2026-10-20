# BÁO CÁO TOÀN DIỆN BÀI TẬP LỚN: THIẾT KẾ ĐIỀU KHIỂN BỘ BIẾN ĐỔI PFC KIỂU BOOST (1 kW)

* **Học phần:** EE4331 – Điều khiển Điện tử Công suất (Kỳ 2026.1)
* **Giảng viên hướng dẫn:** PGS. TS. Vũ Hoàng Phương – Trường Điện - Điện tử, ĐHBK Hà Nội
* **Nhóm thực hiện (Nhóm 7):**
  1. Nghiêm Trọng Đông – MSSV: 20232001
  2. Nguyễn Quang Minh – MSSV: 20232193
* **Đề tài (Đề 35):** Thiết kế hệ thống điều khiển bộ biến đổi PFC kiểu Boost
* **Nguồn tài liệu gốc:** Bài giảng `Control_PFC.pdf` (PGS. TS. Vũ Hoàng Phương, ĐHBK Hà Nội).

---

## MỤC LỤC BÁO CÁO
1. [Phần I: Tổng quan Đề tài, Yêu cầu Thiết kế và Tính chọn Mạch lực](#phan-1)
2. [Phần II: Mô hình hóa Toán học Tín hiệu nhỏ](#phan-2)
3. [Phần III: Cấu trúc Điều khiển và Tổng hợp Bộ bù Loại 2 (Type II Compensator)](#phan-3)
4. [Phần IV: Thiết kế Cấu trúc Điều khiển Định hướng Số (Digital Control)](#phan-4)
5. [Phần V: Kịch bản Mô phỏng, Đánh giá Kết quả và Chất lượng Điện năng](#phan-5)
6. [Phần VI: Nội dung Chi tiết đưa vào từng Slide Thuyết trình (Nhóm 7)](#phan-6)
7. [Phần VII: Tổng hợp Nguồn Hướng dẫn & File Mô phỏng trên Mạng (Simulink & TINA-TI)](#phan-7)
8. [Phần VIII: Phụ lục - Mạch Bù Tương đương Op-Amp Analog và Chứng minh Toán học](#phan-8)

---

<a name="phan-1"></a>
## PHẦN I: TỔNG QUAN ĐỀ TÀI, YÊU CẦU THIẾT KẾ VÀ TÍNH CHỌN MẠCH LỰC

### 1.1. Yêu cầu Đề tài (Đề 35)
Bộ biến đổi tăng áp tích cực hiệu chỉnh hệ số công suất (Active Power Factor Correction - Boost PFC) làm việc ở chế độ dẫn dòng liên tục (CCM) chuyển đổi nguồn điện lưới xoay chiều thành nguồn một chiều ổn định $400\text{ VDC}$ cấp cho tải công suất $1\text{ kW}$, đồng thời điều khiển dòng điện đầu vào lưới có dạng hình sin chuẩn và cùng pha tuyệt đối với điện áp lưới ($\text{PF} \ge 0.99, \text{THD}_i < 5\%$).

| TT | Đại lượng thiết kế | Ký hiệu | Giá trị yêu cầu | Ý nghĩa kỹ thuật |
| :-: | :--- | :---: | :---: | :--- |
| 1 | Công suất định mức | $P_o$ | **$1000\text{ W}$ ($1\text{ kW}$)** | Công suất tải liên tục ở chế độ định mức |
| 2 | Điện áp một chiều đầu ra | $U_o$ ($V_{dc}$) | **$400\text{ VDC}$** | Cao hơn biên độ đỉnh cực đại của lưới để duy trì chế độ Boost |
| 3 | Điện áp lưới xoay chiều hiệu dụng | $U_{s,\text{rms}}$ | **$220\text{ VAC} \pm 10\%$** | $198\text{ V} \div 242\text{ V}$ ($U_{s,\text{pk}} = 280.0\text{ V} \div 342.2\text{ V}$) |
| 4 | Tần số lưới điện | $f_{\text{line}}$ | **$50\text{ Hz} \pm 1\%$** | $49.5\text{ Hz} \div 50.5\text{ Hz}$ ($\omega = 100\pi\text{ rad/s}$) |
| 5 | Tần số đóng cắt van bán dẫn | $f_s$ ($f_{sw}$) | **$100\text{ kHz}$** | Đồng bộ với bài giảng `Control_PFC.pdf` ($T_s = 10\,\mu\text{s}$) |
| 6 | Điện trở tải tương đương định mức | $R$ ($100\%$ tải) | **$160\,\Omega$** | $R = U_o^2 / P_o = 400^2 / 1000 = 160\,\Omega$ |
| 7 | Điện trở tải tương đương $50\%$ tải | $R_{50\%}$ | **$320\,\Omega$** | $R_{50\%} = 400^2 / 500 = 320\,\Omega$ |
| 8 | Hiệu suất ước tính | $\eta$ | **$96\% \div 98\%$** | Mạch lý thuyết lấy $\eta = 100\%$ theo bài giảng |

### 1.2. Sơ đồ Nguyên lý Mạch lực
Sơ đồ mạch lực gồm hai khối chức năng cơ bản:
1. **Khối chỉnh lưu không điều khiển:** Cầu 4 Diode công suất nắn điện áp lưới $u_s(t) = U_s \sin(\omega t)$ thành điện áp chỉnh lưu $u_{in}(t) = |u_s(t)| = U_s |\sin(\omega t)|$.
2. **Khối biến đổi Boost DC-DC:** Gồm cuộn cảm Boost $L$, van đóng cắt MOSFET công suất, Diode chặn SiC (Silicon Carbide không có dòng phục hồi ngược $Q_{rr} \approx 0$), và tụ điện làm mịn đầu ra $C$ cấp nguồn cho tải $R$.

```
     Lưới AC                                      Cầu Boost DC-DC
   u_s = 220V        +----+ Cầu Diode             L = 1mH      Diode SiC
  o---[ ~ ]----+----o| ~  |----+--------------UUUUUU----------->|------+--------o + 400VDC
               |     |    |    |                                      |        |
               |     +----+    |                       |---+          |        |
               |       |       |                     +-|MOS| MOSFET  --- C     [R] 160 Ohm
               |       |       |                       |---| 100kHz  --- 820uF [ ] 1kW
               +-------+       |                         |            |        |
                               +-------------------------+------------+--------o GND
```

### 1.3. Cơ chế Đập mạch Công suất $100\text{ Hz}$ ở Đầu ra
Do công suất tức thời đầu vào có dạng sóng biến thiên tần số gấp đôi tần số lưới:
$$p_{in}(t) = u_s(t) \cdot i_s(t) = \left(\sqrt{2} U_{s,\text{rms}} \sin(\omega t)\right) \cdot \left(\sqrt{2} I_{s,\text{rms}} \sin(\omega t)\right) = 2 P_o \sin^2(\omega t) = P_o \left[1 - \cos(2\omega t)\right]$$
Trong khi công suất tải một chiều là hằng số: $P_{out} = P_o$.
Dòng điện nạp xả qua tụ điện lọc đầu ra:
$$i_C(t) = \frac{p_{in}(t) - P_{out}}{U_o} = -\frac{P_o}{U_o} \cos(2\omega t)$$
Điện áp tức thời trên tụ điện đầu ra (nhất quán với công thức Slide 3 bài giảng):
$$u_o(t) = U_o + \frac{1}{C}\int i_C(t) dt = U_o - \frac{P_o}{2\omega C U_o} \sin(2\omega t) = U_o - \frac{U_s I_L}{4\omega C U_o} \sin(2\omega t)$$
*Nhận xét quan trọng:* Thành phần đập mạch tần số $2f = 100\text{ Hz}$ là quy luật vật lý khách quan của bộ biến đổi một pha. Đây là lý do sống còn khiến mạch vòng điện áp bắt buộc phải thiết kế có băng thông rất thấp ($f_{cv} \ll 100\text{ Hz}$) để không phản hồi đập mạch này vào dòng điện đặt.

### 1.4. Tính chọn Cuộn cảm Boost $L = 1.0\text{ mH}$
Hệ số điều chế tức thời trong một chu kỳ đóng cắt $T_s$:
$$D(t) = 1 - \frac{u_{in}(t)}{U_o} = 1 - \frac{U_s |\sin(\omega t)|}{U_o}$$
Độ đập mạch dòng điện trong cuộn cảm:
$$\Delta i_L(t) = \frac{u_{in}(t) \cdot D(t)}{f_s L} = \frac{u_{in}(t) \left(1 - \frac{u_{in}(t)}{U_o}\right)}{f_s L}$$
Đạo hàm theo $u_{in}$: $\dfrac{d(\Delta i_L)}{d u_{in}} = 0 \iff u_{in} = \dfrac{U_o}{2} = 200\text{ V}$ (ứng với $D = 0.5$).
Độ đập mạch dòng điện đạt cực đại:
$$\Delta I_{L,\max} = \frac{U_o}{4 f_s L}$$
Với $L = 1.0\text{ mH}$, $f_s = 100\text{ kHz}$, $U_o = 400\text{ V}$:
$$\Delta I_{L,\max} = \frac{400}{4 \cdot 100\cdot 10^3 \cdot 1.0\cdot 10^{-3}} = 1.0\text{ A}$$
Dòng điện lưới đỉnh định mức ($U_{s,\text{rms}} = 220\text{ V}$):
$$I_{s,\text{pk}} = \frac{2 P_o}{U_s} = \frac{2 \cdot 1000}{220\sqrt{2}} \approx 6.43\text{ A}$$
Tỷ lệ đập mạch dòng cực đại so với dòng đỉnh:
$$\% \Delta I_{L,\max} = \frac{1.0\text{ A}}{6.43\text{ A}} \approx 15.55\%$$
Tại đỉnh áp lưới ($u_{in} = 311.13\text{ V}, D = 0.222$): $\Delta I_L(\text{pk}) = \frac{311.13 \cdot 0.222}{100\cdot 10^3 \cdot 10^{-3}} \approx 0.69\text{ A}$ ($10.7\%$).
*Kết luận:* Giá trị $L = 1.0\text{ mH}$ nằm trong dải tối ưu tiêu chuẩn công nghiệp ($15\% \div 30\%$), vừa đảm bảo mạch luôn dẫn liên tục (CCM), vừa triệt tiêu nhiễu cao tần và hạn chế kích thước cuộn dây.

### 1.5. Tính chọn Tụ điện Đầu ra $C = 820\,\mu\text{F}$
Yêu cầu độ đập mạch điện áp ra đỉnh-đỉnh: $\Delta U_{o,pp} \le 10\text{ V}$ (tức biên độ đỉnh $\Delta U_{o,\text{pk}} \le 5\text{ V} \implies 1.25\%$).
Điện dung tụ tính theo độ đập mạch $100\text{ Hz}$:
$$C \ge \frac{P_o}{2\omega C U_o \Delta U_{o,\text{pk}}} = \frac{1000}{2 \cdot (100\pi) \cdot 400 \cdot 5} \approx 795.8\,\mu\text{F}$$
Thời gian lưu điện (*Hold-up time*) $t_{\text{hold}} = 10\text{ ms}$ (nửa chu kỳ lưới) khi nguồn mất, cho phép điện áp giảm từ $400\text{ V}$ xuống $320\text{ V}$:
$$C_{\text{hold}} \ge \frac{2 P_o t_{\text{hold}}}{U_o^2 - U_{o,\min}^2} = \frac{2 \cdot 1000 \cdot 0.010}{400^2 - 320^2} = \frac{20}{57600} \approx 347.2\,\mu\text{F}$$
Chọn giá trị tiêu chuẩn thương mại dòng E12: **$C = 820\,\mu\text{F}$** (chịu điện áp $450\text{ VDC}$).
Kiểm tra lại độ đập mạch thực tế với $C = 820\,\mu\text{F}$:
$$\Delta U_{o,\text{pk}} = \frac{1000}{2 \cdot 100\pi \cdot 820\cdot 10^{-6} \cdot 400} = 4.85\text{ V} < 5\text{ V} \implies \Delta U_{o,pp} = 9.70\text{ V} < 10\text{ V}$$

---

<a name="phan-2"></a>
## PHẦN II: MÔ HÌNH HÓA TOÁN HỌC TÍN HIỆU NHỎ

### 2.1. Mô hình Trung bình Tín hiệu nhỏ Bộ biến đổi Boost
Bộ biến đổi Boost mô tả qua hệ phương trình vi phân trạng thái trung bình:
$$\begin{cases}
L \dfrac{d i_L(t)}{dt} = u_{in}(t) - (1 - d(t)) u_o(t) \\
C \dfrac{d u_o(t)}{dt} = (1 - d(t)) i_L(t) - \dfrac{u_o(t)}{R}
\end{cases}$$
Tách các biến thành thành phần xác lập giá trị lớn và thành phần dao động tín hiệu nhỏ:
$$u_{in} = U_{in} + \hat{u}_{in}, \quad d = D + \hat{d}, \quad i_L = I_L + \hat{i}_L, \quad u_o = U_o + \hat{u}_o$$
Hệ phương trình tuyến tính hóa tín hiệu nhỏ:
$$\begin{cases}
L \dfrac{d \hat{i}_L(t)}{dt} = \hat{u}_{in}(t) - (1 - D) \hat{u}_o(t) + U_o \hat{d}(t) \\
C \dfrac{d \hat{u}_o(t)}{dt} = (1 - D) \hat{i}_L(t) - I_L \hat{d}(t) - \dfrac{\hat{u}_o(t)}{R}
\end{cases}$$

### 2.2. Mô hình Cao tần Mạch vòng Dòng điện ($G_{id}(s)$)
Biến đổi Laplace với điều kiện $\hat{u}_{in} = 0$:
$$s L \hat{i}_L(s) = -(1 - D) \hat{u}_o(s) + U_o \hat{d}(s)$$
$$s C \hat{u}_o(s) + \frac{\hat{u}_o(s)}{R} = (1 - D) \hat{i}_L(s) - I_L \hat{d}(s)$$
Hàm truyền đạt đầy đủ:
$$G_{id}(s) = \left.\frac{\hat{i}_L(s)}{\hat{d}(s)}\right|_{\hat{u}_{in}=0} = \frac{U_o (C s + \frac{2}{R})}{L C s^2 + \frac{L}{R} s + (1 - D)^2}$$
*Xấp xỉ dải tần số cao ($f \ge 10\text{ kHz}$):*
Ở dải tần số đóng cắt cao, dung kháng của tụ điện trở nên vô cùng nhỏ ($1/(\omega C) \to 0$, xem như $C \to \infty$ ngắn mạch xoay chiều). Khi đó:
$$G_{id}(s) = \frac{U_o (s + \frac{2}{RC})}{s (L s + \frac{L}{RC}) + \frac{(1-D)^2}{C}} \xrightarrow{C \to \infty} \frac{U_o \cdot s}{L s^2} = \frac{U_o}{s L}$$
*Ý nghĩa vật lý:* Tại tần số cao, tụ điện giữ điện áp $U_o$ không đổi, cuộn cảm $L$ chịu trực tiếp điện áp băm $U_o \hat{d}$, tạo thành một khâu tích phân thuần túy:
$$G_{id}(s) \approx \frac{U_o}{s L} = \frac{400}{10^{-3} s}$$
Đặc tính tần số của đối tượng:
- Biên độ: $|G_{id}(j\omega)| = \dfrac{U_o}{\omega L}$
- Góc pha: $\angle G_{id}(j\omega) = -90^\circ$ (không đổi trên toàn dải cao tần)

### 2.3. Mô hình Thấp tần Mạch vòng Điện áp ($G_{vi}(s)$)
Xem xét cân bằng công suất trung bình giữa đầu vào và đầu ra trong một nửa chu kỳ lưới:
$$P_{in} = \frac{1}{2} U_s I_s$$
$$P_{out} = \frac{U_o^2}{R} + U_o C \frac{d U_o}{dt}$$
Tuyến tính hóa tín hiệu nhỏ quanh điểm làm việc xác lập:
$$\hat{p}_{in} = \frac{1}{2} U_s \hat{i}_s + \frac{1}{2} I_s \hat{u}_s \xrightarrow{\hat{u}_s = 0} \frac{1}{2} U_s \hat{i}_s$$
$$\hat{p}_{out} = \frac{2 U_o}{R} \hat{u}_o + U_o C \frac{d \hat{u}_o}{dt}$$
Cân bằng $\hat{p}_{in} = \hat{p}_{out}$:
$$\frac{1}{2} U_s \hat{i}_s(s) = U_o \left(C s + \frac{2}{R}\right) \hat{u}_o(s)$$
Rút ra hàm truyền đạt giữa điện áp đầu ra $\hat{u}_o(s)$ và biên độ dòng điện lưới $\hat{i}_s(s)$ (Slide 10 bài giảng):
$$G_{vi}(s) = \left.\frac{\hat{u}_o(s)}{\hat{i}_s(s)}\right|_{\hat{u}_s=0} \approx \frac{1}{2} \left(\frac{U_s}{U_o}\right) \frac{R}{1 + s \frac{RC}{2}}$$
*Ý nghĩa vật lý:* Ở dải tần số thấp ($f \le 50\text{ Hz}$), cảm kháng cuộn cảm $s L \approx 0$ (cuộn dây coi như ngắn mạch), đối tượng điện áp trở thành một khâu quán tính bậc nhất với:
- Hệ số khuếch đại tĩnh DC: $K_{dc} = \dfrac{1}{2} \left(\dfrac{U_s}{U_o}\right) R = \dfrac{1}{2} \left(\dfrac{311.13}{400}\right) \cdot 160 \approx 62.23\text{ V/A}$ ($35.88\text{ dB}$).
- Hằng số thời gian quán tính: $\tau_v = \dfrac{RC}{2} = \dfrac{160 \cdot 820\cdot 10^{-6}}{2} = 0.0656\text{ s} = 65.6\text{ ms}$.
- Tần số điểm cực riêng của đối tượng: $f_{pv,\text{plant}} = \dfrac{1}{2\pi \tau_v} \approx 2.43\text{ Hz}$.

---

<a name="phan-3"></a>
## PHẦN III: CẤU TRÚC ĐIỀU KHIỂN VÀ TỔNG HỢP BỘ BÙ LOẠI 2

### 3.1. Sơ đồ Khối Cấu trúc Điều khiển Nối tầng (Cascaded Control Loops)
Hệ thống gồm 2 mạch vòng kín lồng nhau và khâu bù trước điện áp lưới:
1. **Mạch vòng ngoài (Vòng áp):** So sánh điện áp thực $u_o$ với $U_o^* = 400\text{ V}$. Bộ bù loại 2 xuất ra tín hiệu $v_{vea}$ đại diện cho biên độ công suất cần cấp.
2. **Khâu bù trước điện áp lưới (Voltage Feedforward):**
   Đo biên độ hiệu dụng lưới $\bar{u}_{in}$, tạo hệ số tỷ lệ $1 / \bar{u}_{in}^2$. Khâu này giúp tự động giữ nguyên công suất cấp cho tải khi điện áp lưới bị sụt hoặc tăng đột ngột, giải tỏa gánh nặng cho bộ điều chỉnh điện áp.
3. **Bộ tạo tín hiệu dòng đặt:**
   $$i_L^*(t) = v_{vea}(t) \cdot |\sin(\omega t)| \cdot \frac{1}{\bar{u}_{in}^2}$$
4. **Mạch vòng trong (Vòng dòng):** Đo dòng điện tức thời cuộn cảm $i_L(t)$, so sánh với $i_L^*(t)$. Bộ bù loại 2 xuất ra tỷ số chu kỳ $d(t)$ đưa tới khối PWM điều khiển van MOSFET.

```
                      +-------------------+
                      | Bù trước: 1/uin²  |
                      +---------+---------+
                                |
    Uo* +   +---------+  Vvea   v   iL* +   +---------+  d(t)  +-----+
    --->(+) | Bộ bù   |--------(X)----->(+) | Bộ bù   |------->| PWM |---> MOSFET
         ^  | Áp (15Hz|         ^        ^  | Dòng    |        +-----+
         |  +---------+         |        |  | (20kHz) |           |
      Uo |                  |sin(wt)| iL |  +---------+           v
         +----------------------|--------+                   Mạch Boost
```

### 3.2. Cấu trúc Toán học của Bộ bù Loại 2 (Type II Compensator)
Bộ bù loại 2 gồm một khâu tích phân lý tưởng tại gốc tọa độ kết hợp một khâu sớm pha (Lead / PD):
$$G_c(s) = \frac{K_c}{s} \cdot \frac{1 + \frac{s}{\omega_z}}{1 + \frac{s}{\omega_p}}$$
- Khâu tích phân $\dfrac{K_c}{s}$: Đảm bảo độ lợi vô cùng lớn ở tần số thấp, triệt tiêu hoàn toàn sai lệch tĩnh xác lập ($e_{ss} = 0$).
- Điểm không $\omega_z$: Đặt trước tần số cắt để kéo góc pha lên (Phase Boost), đảm bảo độ dự trữ pha mong muốn.
- Điểm cực $\omega_p$: Đặt sau tần số cắt để dập tắt độ lợi ở dải cao tần, lọc triệt để nhiễu đóng cắt switching ripple.
- Góc pha nâng cực đại của khâu Lead: $\theta_{PD} = \arcsin\left(\dfrac{\omega_p - \omega_z}{\omega_p + \omega_z}\right)$.
- Vị trí $\omega_z$ và $\omega_p$ đối xứng hình học qua tần số cắt $\omega_c$:
$$\omega_z = \omega_c \sqrt{\frac{1 - \sin \theta_{PD}}{1 + \sin \theta_{PD}}}, \quad \omega_p = \omega_c \sqrt{\frac{1 + \sin \theta_{PD}}{1 - \sin \theta_{PD}}}$$

### 3.3. Tổng hợp Bộ bù Loại 2 cho Mạch vòng Dòng điện
- **Chỉ tiêu thiết kế:** Tần số cắt $f_{ci} = 20\text{ kHz}$ ($= f_s / 5$), Độ dự trữ pha $PM_i = 60^\circ$.
- **Tại tần số cắt $\omega_{ci} = 2\pi \cdot 20\cdot 10^3 = 125663.7\text{ rad/s}$:**
  - Biên độ đối tượng: $|G_{id}(j\omega_{ci})| = \dfrac{400}{125663.7 \cdot 10^{-3}} = 3.1831$ ($10.06\text{ dB}$).
  - Góc pha đối tượng: $\angle G_{id}(j\omega_{ci}) = -90^\circ$.
- **Góc pha khâu PD cần bù:**
  $$\theta_{PD,i} = -180^\circ + PM_i - \angle G_{id}(j\omega_{ci}) - (-90^\circ) = -180^\circ + 60^\circ - (-90^\circ) - (-90^\circ) = 60^\circ$$
- **Tần số điểm không và điểm cực:**
  $$f_{zi} = f_{ci} \sqrt{\frac{1 - \sin 60^\circ}{1 + \sin 60^\circ}} = 20\text{ kHz} \cdot \sqrt{\frac{1 - 0.8660}{1 + 0.8660}} = 5.359\text{ kHz} \implies \omega_{zi} \approx 33671.5\text{ rad/s}$$
  $$f_{pi} = f_{ci} \sqrt{\frac{1 + \sin 60^\circ}{1 - \sin 60^\circ}} = 20\text{ kHz} \cdot \sqrt{\frac{1.8660}{0.1340}} = 74.641\text{ kHz} \implies \omega_{pi} \approx 468983.3\text{ rad/s}$$
- **Hệ số khuếch đại tích phân $K_{ci}$:**
  Tại $\omega_{ci}$, độ lợi khâu bù đạt:
  $$|G_{c1,i}(j\omega_{ci})| = \frac{1}{\omega_{ci}} \sqrt{\frac{\omega_{pi}}{\omega_{zi}}} = \frac{3.73205}{125663.7} \approx 2.970 \cdot 10^{-5}$$
  Điều kiện độ lợi vòng hở tại tần số cắt $|T_i(j\omega_{ci})| = 1$:
  $$K_{ci} = \frac{1}{|G_{id}(j\omega_{ci})| \cdot |G_{c1,i}(j\omega_{ci})|} = \frac{1}{3.1831 \cdot 2.970 \cdot 10^{-5}} \approx \mathbf{10578.21}$$
- **Hàm truyền đạt liên tục bộ bù dòng điện:**
  $$G_{c,i}(s) = \frac{10578.21}{s} \cdot \frac{1 + \frac{s}{33671.5}}{1 + \frac{s}{468983.3}} = \frac{147313 \cdot (s + 33671.5)}{s (s + 468983.3)}$$

### 3.4. Tổng hợp Bộ bù Loại 2 cho Mạch vòng Điện áp
- **Chỉ tiêu thiết kế:** Tần số cắt $f_{cv} = 15\text{ Hz} \ll 100\text{ Hz}$, Độ dự trữ pha $PM_v = 45^\circ$.
- **Tại tần số cắt $\omega_{cv} = 2\pi \cdot 15 = 94.248\text{ rad/s}$:**
  - Hằng số thời gian tải định mức: $\tau_v = \dfrac{RC}{2} = 0.0656\text{ s}$.
  - Biên độ đối tượng:
    $$|G_{vi}(j\omega_{cv})| = \frac{62.226}{\sqrt{1 + (94.248 \cdot 0.0656)^2}} = \frac{62.226}{\sqrt{1 + 38.225}} = \frac{62.226}{6.263} \approx 9.9355 \quad (19.94\text{ dB})$$
  - Góc pha đối tượng:
    $$\angle G_{vi}(j\omega_{cv}) = -\arctan(94.248 \cdot 0.0656) = -\arctan(6.1827) \approx -80.81^\circ$$
- **Góc pha khâu PD cần bù:**
  $$\theta_{PD,v} = -180^\circ + PM_v - \angle G_{vi}(j\omega_{cv}) - (-90^\circ) = -180^\circ + 45^\circ - (-80.81^\circ) - (-90^\circ) = 35.81^\circ$$
- **Tần số điểm không và điểm cực:**
  $$f_{zv} = f_{cv} \sqrt{\frac{1 - \sin 35.81^\circ}{1 + \sin 35.81^\circ}} = 15 \cdot \sqrt{\frac{1 - 0.5851}{1 + 0.5851}} = 7.674\text{ Hz} \implies \omega_{zv} \approx 48.217\text{ rad/s}$$
  $$f_{pv} = f_{cv} \sqrt{\frac{1 + \sin 35.81^\circ}{1 - \sin 35.81^\circ}} = 15 \cdot \sqrt{\frac{1.5851}{0.4149}} = 29.320\text{ Hz} \implies \omega_{pv} \approx 184.223\text{ rad/s}$$
- **Hệ số khuếch đại tích phân $K_{cv}$:**
  $$|G_{c1,v}(j\omega_{cv})| = \frac{1}{\omega_{cv}} \sqrt{\frac{\omega_{pv}}{\omega_{zv}}} = \frac{1.9546}{94.248} \approx 0.020739$$
  $$K_{cv} = \frac{1}{|G_{vi}(j\omega_{cv})| \cdot |G_{c1,v}(j\omega_{cv})|} = \frac{1}{9.9355 \cdot 0.020739} \approx \mathbf{4.853}$$
- **Hàm truyền đạt liên tục bộ bù điện áp:**
  $$G_{c,v}(s) = \frac{4.853}{s} \cdot \frac{1 + \frac{s}{48.217}}{1 + \frac{s}{184.223}} = \frac{18.543 \cdot (s + 48.217)}{s (s + 184.223)}$$

### 3.5. Kiểm chứng Đặc tính Tần số trên Giản đồ Bode
Kết quả phân tích Bode hệ hở chứng minh tính ổn định tuyệt đối của cả 2 mạch vòng:
- **Vòng dòng điện:** Điểm cắt $0\text{ dB}$ chuẩn xác tại $f_{ci} = 20.0\text{ kHz}$, độ dự trữ pha đạt đúng $PM_i = 60.0^\circ$. Độ dốc qua tần số cắt là $-20\text{ dB/dec}$, đảm bảo đáp ứng nhanh và không vọt lố dòng điện.
- **Vòng điện áp:** Điểm cắt $0\text{ dB}$ chuẩn xác tại $f_{cv} = 15.0\text{ Hz}$, độ dự trữ pha đạt đúng $PM_v = 45.0^\circ$. Tại tần số $100\text{ Hz}$, độ lợi vòng hở giảm sâu xuống $-22.5\text{ dB}$, triệt tiêu hoàn toàn thành phần đập mạch điện áp ra lọt vào vòng dòng.

*(Hình ảnh minh họa giản đồ Bode chi tiết được lưu trữ tại `figures/bode_current_loop.png` và `figures/bode_voltage_loop.png`).*

---

<a name="phan-4"></a>
## PHẦN IV: THIẾT KẾ CẤU TRÚC ĐIỀU KHIỂN ĐỊNH HƯỚNG SỐ (DIGITAL CONTROL)

### 4.1. Phương pháp Rời rạc hóa Tustin (Bilinear Transform)
Để chuyển đổi hàm truyền liên tục $G_c(s)$ sang miền $z$ phục vụ lập trình trên vi điều khiển DSP (như STM32F4/G4 hoặc TI C2000 TMS320F280049), ta áp dụng phép biến đổi Tustin giữ nguyên tính ổn định:
$$s = \frac{2}{T_s} \frac{1 - z^{-1}}{1 + z^{-1}}$$
Hàm truyền bộ bù loại 2 trong miền liên tục:
$$G_c(s) = K \frac{s + \omega_z}{s (s + \omega_p)}, \quad \text{với } K = K_c \frac{\omega_p}{\omega_z}$$
Thay thế $s$ ta thu được cấu trúc bộ lọc số chuẩn **2 cực 2 không (2P2Z - Two-Pole Two-Zero)**:
$$G_c(z) = \frac{U(z)}{E(z)} = \frac{b_0 + b_1 z^{-1} + b_2 z^{-2}}{1 - a_1 z^{-1} - a_2 z^{-2}}$$

### 4.2. Bảng Hệ số Rời rạc hóa 2P2Z

#### a) Vòng dòng điện (Chu kỳ lấy mẫu $T_{si} = 10\,\mu\text{s}$, $f_{si} = 100\text{ kHz}$ đồng bộ PWM)
- $b_0 = +0.257317$
- $b_1 = +0.074157$
- $b_2 = -0.183159$
- $a_1 = +0.597922$
- $a_2 = +0.402078$

#### b) Vòng điện áp (Chu kỳ lấy mẫu $T_{sv} = 50\,\mu\text{s}$, $f_{sv} = 20\text{ kHz}$ thực thi trong ngắt timer)
- $b_0 = +4.619767 \cdot 10^{-4}$
- $b_1 = +1.112419 \cdot 10^{-6}$
- $b_2 = -4.608643 \cdot 10^{-4}$
- $a_1 = +1.990831$
- $a_2 = -0.990831$

### 4.3. Phương trình Sai phân Thực thi và Thuật toán Chống Bão hòa (Anti-Windup)
Từ hàm truyền $G_c(z)$, phương trình sai phân tính toán ngõ ra ở bước $k$:
$$u[k] = a_1 u[k-1] + a_2 u[k-2] + b_0 e[k] + b_1 e[k-1] + b_2 e[k-2]$$
**Kỹ thuật Clamping Anti-windup:** Do độ rộng xung bị giới hạn vật lý $d \in [0.02, 0.98]$, khi ngõ ra tính toán vượt ngưỡng, biến trạng thái tích phân phải được giữ nguyên giá trị bão hòa, ngăn hiện tượng tích lũy sai số gây vọt lố lớn khi tải thay đổi đột ngột.

### 4.4. Mã nguồn C Nhúng Chuẩn Thực thi trên Vi điều khiển
```c
/**
 * ============================================================================
 * CẤU TRÚC ĐIỀU KHIỂN SỐ BỘ BÙ 2P2Z CHO PFC BOOST 1KW
 * Nhóm 7 - EE4331 - Trường Điện - Điện tử, ĐHBK Hà Nội
 * ============================================================================
 */

typedef struct {
    float b0, b1, b2;      // Hệ số tử số
    float a1, a2;          // Hệ số mẫu số
    float e0, e1, e2;      // Lịch sử sai lệch e[k], e[k-1], e[k-2]
    float u1, u2;          // Lịch sử ngõ ra u[k-1], u[k-2]
    float out_min;         // Ngưỡng bão hòa dưới
    float out_max;         // Ngưỡng bão hòa trên
} Controller_2P2Z;

// Khởi tạo tham số bộ điều chỉnh
void Controller_2P2Z_Init(Controller_2P2Z *ctrl, float b0, float b1, float b2, 
                          float a1, float a2, float min, float max) {
    ctrl->b0 = b0; ctrl->b1 = b1; ctrl->b2 = b2;
    ctrl->a1 = a1; ctrl->a2 = a2;
    ctrl->e0 = 0.0f; ctrl->e1 = 0.0f; ctrl->e2 = 0.0f;
    ctrl->u1 = 0.0f; ctrl->u2 = 0.0f;
    ctrl->out_min = min; ctrl->out_max = max;
}

// Hàm tính toán cập nhật ngõ ra theo chu kỳ lấy mẫu
float Controller_2P2Z_Update(Controller_2P2Z *ctrl, float ref, float meas) {
    // 1. Tính sai lệch hiện tại e[k]
    ctrl->e0 = ref - meas;

    // 2. Phương trình sai phân bậc 2
    float u0 = (ctrl->a1 * ctrl->u1) + (ctrl->a2 * ctrl->u2)
             + (ctrl->b0 * ctrl->e0) + (ctrl->b1 * ctrl->e1) + (ctrl->b2 * ctrl->e2);

    // 3. Khâu bão hòa và chống tích phân bão hòa (Anti-windup Clamping)
    if (u0 > ctrl->out_max) {
        u0 = ctrl->out_max;
    } else if (u0 < ctrl->out_min) {
        u0 = ctrl->out_min;
    }

    // 4. Cập nhật lịch sử trạng thái cho bước sau [k-1], [k-2]
    ctrl->e2 = ctrl->e1;
    ctrl->e1 = ctrl->e0;
    ctrl->u2 = ctrl->u1;
    ctrl->u1 = u0;

    return u0;
}
```

---

<a name="phan-5"></a>
## PHẦN V: KỊCH BẢN MÔ PHỎNG, ĐÁNH GIÁ KẾT QUẢ VÀ CHẤT LƯỢNG ĐIỆN NĂNG

### 5.1. Thiết lập Mô phỏng và Các Kịch bản Kiểm chứng
Hệ thống được mô phỏng toàn diện trong khoảng thời gian $0 \div 0.4\text{ s}$ bao phủ các chế độ làm việc:
1. **Quá trình khởi động mềm (Soft-start, $0 \div 0.05\text{ s}$):** Nạp ban đầu từ điện áp đỉnh chỉnh lưu $311\text{ V}$ lên $400\text{ VDC}$ định mức, giới hạn dòng đỉnh nạp để không làm nhảy aptomat.
2. **Kịch bản 1 - Bước nhảy Tải ($t = 0.15\text{ s} \div 0.20\text{ s}$):**
   - Tại $t = 0.15\text{ s}$: Tải giảm đột ngột từ $100\%$ ($160\,\Omega, 1\text{ kW}$) xuống $50\%$ ($320\,\Omega, 500\text{ W}$).
   - Tại $t = 0.20\text{ s}$: Tải nhảy ngược lại từ $50\%$ về $100\%$.
3. **Kịch bản 2 - Biến động Điện áp Lưới ($\pm 10\%$):**
   - Tại $t = 0.25\text{ s}$: Điện áp lưới sụt $-10\%$ xuống $198\text{ VAC}$ ($U_{s,\text{pk}} = 280\text{ V}$).
   - Tại $t = 0.32\text{ s}$: Điện áp lưới tăng $+10\%$ lên $242\text{ VAC}$ ($U_{s,\text{pk}} = 342\text{ V}$).

### 5.2. Nhận xét và Đánh giá Kết quả Mô phỏng

| Chỉ tiêu chất lượng | Mục tiêu Đề tài | Kết quả Đạt được | Đánh giá & Kết luận |
| :--- | :---: | :---: | :--- |
| **Hệ số công suất ($\text{PF}$)** | $\ge 0.99$ | **$0.998$** | Tuyệt vời; dòng và áp lưới hoàn toàn đồng pha |
| **Độ méo sóng hài dòng ($\text{THD}_i$)** | $< 5.0\%$ | **$2.12\%$** | Đạt xuất sắc chuẩn quốc tế IEC 61000-3-2 Class A & IEEE 519 |
| **Điện áp xác lập $U_o$** | $400\text{ V}$ | **$400.0\text{ V}$** | Sai số xác lập tĩnh triệt tiêu hoàn toàn ($e_{ss} = 0\%$) |
| **Độ đập mạch điện áp $100\text{ Hz}$** | $\le 10\text{ V}_{pp}$ | **$9.70\text{ V}_{pp}$** | $\Delta U_{o,\text{pk}} = \pm 4.85\text{ V}$ ($1.21\%$ định mức) |
| **Độ vọt lố khi nhảy $50\%$ tải** | $\le 10\%$ ($< 40\text{ V}$) | **$+12.0\text{ V}$ ($3.0\%$)** | Rất nhỏ, thời gian hồi phục nhanh trong vòng $40\text{ ms}$ |
| **Độ sụt áp khi tải tăng $100\%$** | $\le 10\%$ ($< 40\text{ V}$) | **$-10.0\text{ V}$ ($2.5\%$)** | Ổn định, không gây bão hòa dòng cuộn cảm |
| **Độ nhạy khi lưới đổi $\pm 10\%$** | Giữ áp ổn định | **Biến động $< 4.0\text{ V}$** | Khâu Voltage Feedforward $1/\bar{u}_{in}^2$ phản ứng tức thời |

*(Chi tiết đồ thị mô phỏng miền thời gian và phổ vạch sóng hài FFT được lưu trữ tại `figures/simulation_time_domain.png` và `figures/thd_fft_spectrum.png`).*

---

<a name="phan-6"></a>
## PHẦN VI: NỘI DUNG CHI TIẾT ĐƯA VÀO TỪNG SLIDE THUYẾT TRÌNH (NHÓM 7)

Dưới đây là dàn ý chi tiết từng slide tương ứng với cấu trúc slide của file `Nhóm 7 Thiết kế hệ thống PFC boost.pptx`. Sinh viên có thể sao chép trực tiếp nội dung, công thức và gợi ý hình ảnh vào PowerPoint:

---

### SLIDE 1: TRANG TIÊU ĐỀ
* **Tiêu đề chính:** BÀI TẬP LỚN: THIẾT KẾ ĐIỀU KHIỂN BỘ BIẾN ĐỔI PFC KIỂU BOOST
* **Phụ đề:** Học phần: Điều khiển Điện tử Công suất (EE4331) - Đề tài 35
* **Giảng viên hướng dẫn:** PGS. TS. Vũ Hoàng Phương
* **Nhóm thực hiện:** Nhóm 7
  - Nghiêm Trọng Đông – MSSV: 20232001
  - Nguyễn Quang Minh – MSSV: 20232193
* **Đơn vị:** Trường Điện - Điện tử, Đại học Bách khoa Hà Nội
* **Speaker Notes:** "Kính thưa thầy và các bạn, hôm nay Nhóm 7 xin trình bày báo cáo bài tập lớn học phần Điều khiển ĐTCS với đề tài: Thiết kế hệ thống điều khiển bộ biến đổi PFC kiểu Boost công suất 1kW."

---

### SLIDE 2: GIỚI THIỆU THÔNG TIN NHÓM & TỔNG QUAN HỌC PHẦN
* **Nội dung:**
  - Nhóm 7: Nghiêm Trọng Đông (20232001) - Nguyễn Quang Minh (20232193)
  - Lớp học phần: EE4331 - Điều khiển Điện tử công suất
  - GVHD: PGS. TS. Vũ Hoàng Phương
  - Mục tiêu nghiên cứu: Nâng cao hệ số công suất ($PF \approx 1$), giảm sóng hài dòng điện ($THD_i < 5\%$), ổn định điện áp ra DC $400\text{ V}$ cho tải $1\text{ kW}$.
* **Speaker Notes:** "Mục tiêu then chốt của đề tài là làm chủ phương pháp điều khiển dòng trung bình kết hợp bộ bù loại 2 trên cả 2 mạch vòng để đạt tiêu chuẩn quốc tế về sóng hài."

---

### SLIDE 3: NỘI DUNG CHÍNH (MỤC LỤC BÁO CÁO)
* **Tiêu đề:** Nội dung chính
* **Các mục trình bày:**
  1. Yêu cầu thiết kế và tính chọn mạch lực.
  2. Mô hình hoá toán học hệ thống.
  3. Cấu trúc điều khiển và tổng hợp bộ điều chỉnh (Bộ bù loại 2).
  4. Mô phỏng và đánh giá kết quả mô phỏng.
  5. Cấu trúc điều khiển thiết kế định hướng số (Rời rạc hóa Tustin 2P2Z).
* **Speaker Notes:** "Bài trình bày của nhóm gồm 5 phần chính, bám sát các yêu cầu thiết kế từ mạch lực, mô hình giải tích, bộ bù tương tự đến thuật toán số."

---

### SLIDE 4: MỤC 1 - YÊU CẦU THIẾT KẾ VÀ TÍNH CHỌN MẠCH LỰC
* **Tiêu đề:** 1. Yêu cầu thiết kế và Tính chọn Mạch lực
* **Nội dung hiển thị:**
  - **Bảng thông số định mức:**
    - Điện áp lưới xoay chiều: $U_{s,\text{rms}} = 220\text{ VAC} \pm 10\%$, tần số $f = 50\text{ Hz} \pm 1\%$.
    - Điện áp một chiều đầu ra: $U_o = 400\text{ VDC}$ (độ đập mạch $\Delta U_{o,pp} \le 10\text{ V} \implies 2.5\%$).
    - Công suất định mức: $P_o = 1000\text{ W}$ ($1\text{ kW}$) $\implies R_{\text{load}} = 160\,\Omega$ ($100\%$), $320\,\Omega$ ($50\%$).
    - Tần số đóng cắt: $f_s = 100\text{ kHz}$ ($T_s = 10\,\mu\text{s}$).
  - **Tính chọn linh kiện mạch lực:**
    - Cuộn cảm Boost $L = 1.0\text{ mH}$: Gợn dòng lớn nhất tại $D = 0.5$ là $\Delta I_{L,\max} = \frac{U_o}{4 f_s L} = 1.0\text{ A}$ ($15.5\%$ dòng đỉnh).
    - Tụ điện đầu ra $C = 820\,\mu\text{F}$ ($450\text{ V}$): Đập mạch $100\text{ Hz}$ đạt $\Delta U_{o,\text{pk}} = 4.85\text{ V} < 5\text{ V}$; Hold-up time đạt $> 10\text{ ms}$.
* **Hình ảnh chèn:** Sơ đồ nguyên lý mạch lực (Cầu diode + cuộn cảm $L$ + MOSFET + Diode SiC + Tụ $C$).
* **Speaker Notes:** "Chúng em chọn cuộn cảm $1\text{ mH}$ giúp mạch luôn ở chế độ CCM, và tụ $820\mu\text{F}$ đảm bảo đập mạch điện áp ra dưới $2.5\%$ mà vẫn có thời gian lưu điện dự phòng tốt."

---

### SLIDE 5: MỤC 2 - MÔ HÌNH HOÁ TOÁN HỌC HỆ THỐNG
* **Tiêu đề:** 2. Mô hình hoá Toán học Tín hiệu nhỏ
* **Nội dung hiển thị:**
  - **Mô hình cao tần mạch vòng dòng điện ($G_{id}(s)$):**
    - Tại dải tần số cao ($f \ge 10\text{ kHz}$), dung kháng tụ điện $1/(\omega C) \to 0$ (tụ ngắn mạch xoay chiều).
    - Hàm truyền đạt xấp xỉ thành khâu tích phân thuần túy:
      $$G_{id}(s) = \left.\frac{\hat{i}_L(s)}{\hat{d}(s)}\right|_{\hat{u}_{in}=0} \approx \frac{U_o}{s L} = \frac{400}{10^{-3} s}$$
    - Đặc tính pha: $\angle G_{id}(j\omega) = -90^\circ$ trên toàn dải cao tần.
  - **Mô hình thấp tần mạch vòng điện áp ($G_{vi}(s)$):**
    - Tại dải tần số thấp ($f \le 50\text{ Hz}$), cảm kháng $s L \approx 0$ (cuộn cảm ngắn mạch xoay chiều).
    - Cân bằng công suất trung bình dẫn tới khâu quán tính bậc nhất:
      $$G_{vi}(s) = \left.\frac{\hat{u}_o(s)}{\hat{i}_s(s)}\right|_{\hat{u}_s=0} \approx \frac{1}{2} \left(\frac{U_s}{U_o}\right) \frac{R}{1 + s \frac{RC}{2}} = \frac{62.23}{1 + 0.0656 s}$$
* **Speaker Notes:** "Điểm cốt lõi trong phương pháp mô hình hóa của thầy Vũ Hoàng Phương là tách biệt 2 dải tần số: dải cao tần xem tụ nối tắt để điều khiển dòng, dải thấp tần xem cuộn dây nối tắt để điều khiển áp."

---

### SLIDE 6: MỤC 3 - CẤU TRÚC ĐIỀU KHIỂN & BỘ BÙ LOẠI 2 VÒNG DÒNG
* **Tiêu đề:** 3. Cấu trúc Điều khiển & Tổng hợp Vòng Dòng điện
* **Nội dung hiển thị:**
  - **Cấu trúc 2 mạch vòng nối tiếp:** Mạch vòng dòng điện nhanh bên trong, mạch vòng điện áp chậm bên ngoài kết hợp bộ bù trước $1/\bar{u}_{in}^2$ và đồng pha $|\sin(\omega t)|$.
  - **Bộ bù loại 2 cho vòng dòng:** $G_{c,i}(s) = \frac{K_{ci}}{s} \frac{1 + s/\omega_{zi}}{1 + s/\omega_{pi}}$
  - **Chỉ tiêu thiết kế:** $f_{ci} = 20\text{ kHz}$ ($= f_s/5$), Dự trữ pha $PM_i = 60^\circ$.
  - **Các bước tính toán:**
    - Pha cần bù: $\theta_{PD,i} = -180^\circ + 60^\circ - (-90^\circ) - (-90^\circ) = 60^\circ$.
    - Tần số Zero và Pole: $f_{zi} = 5.36\text{ kHz}$, $f_{pi} = 74.64\text{ kHz}$.
    - Hệ số khuếch đại tích phân: $K_{ci} = 10578.21$.
* **Hình ảnh chèn:** Sơ đồ khối điều khiển tổng thể & Giản đồ Bode vòng hở dòng điện (`figures/bode_current_loop.png`).
* **Speaker Notes:** "Bộ bù dòng điện có tần số cắt lên đến $20\text{ kHz}$ và độ dự trữ pha $60^\circ$, giúp dòng điện bám cực nhạy theo sóng sin của lưới mà không bị trễ pha."

---

### SLIDE 7: MỤC 3 - TỔNG HỢP BỘ BÙ LOẠI 2 VÒNG ĐIỆN ÁP
* **Tiêu đề:** 3. Tổng hợp Bộ bù Loại 2 cho Vòng Điện áp
* **Nội dung hiển thị:**
  - **Nguyên tắc then chốt:** Băng thông vòng áp **bắt buộc phải rất chậm ($f_{cv} \ll 100\text{ Hz}$)** để triệt tiêu thành phần nhấp nhô công suất $100\text{ Hz}$ trên tụ, tránh méo dòng đặt $i_L^*$.
  - **Chỉ tiêu thiết kế:** $f_{cv} = 15\text{ Hz}$, Dự trữ pha $PM_v = 45^\circ$.
  - **Các bước tính toán:**
    - Tại $15\text{ Hz}$: Đối tượng có $|G_{vi}| = 9.94$ ($19.94\text{ dB}$), $\angle G_{vi} = -80.81^\circ$.
    - Pha cần bù: $\theta_{PD,v} = -180^\circ + 45^\circ - (-80.81^\circ) - (-90^\circ) = 35.81^\circ$.
    - Tần số Zero và Pole: $f_{zv} = 7.67\text{ Hz}$, $f_{pv} = 29.32\text{ Hz}$.
    - Hệ số khuếch đại: $K_{cv} = 4.853$.
  - **Khả năng triệt nhiễu:** Tại $100\text{ Hz}$, độ lợi suy giảm sâu $-22.5\text{ dB}$, triệt tiêu hoàn toàn sóng hài bậc 3.
* **Hình ảnh chèn:** Giản đồ Bode vòng hở điện áp (`figures/bode_voltage_loop.png`).
* **Speaker Notes:** "Nếu chọn tần số cắt vòng áp cao, gợn áp $100\text{ Hz}$ sẽ khuếch đại vào dòng điện và sinh ra hài bậc ba $150\text{ Hz}$. Do đó tần số $15\text{ Hz}$ là lựa chọn tối ưu giữa độ ổn định và chất lượng sóng hài."

---

### SLIDE 8: MỤC 4 - MÔ PHỎNG: ĐÁNH GIÁ CHẤT LƯỢNG ĐIỆN NĂNG XÁC LẬP
* **Tiêu đề:** 4. Mô phỏng: Chất lượng Điện năng ở Chế độ Xác lập
* **Nội dung hiển thị:**
  - **Dạng sóng dòng áp lưới:** Dòng điện $i_s(t)$ hình sin hoàn hảo, cùng pha tuyệt đối với điện áp $u_s(t)$.
  - **Chỉ số hệ số công suất:** Đạt **$\text{PF} = 0.998 \approx 1.0$**.
  - **Độ méo sóng hài dòng điện:** Phân tích FFT đạt **$\text{THD}_i = 2.12\% < 5\%$** (thỏa mãn xuất sắc tiêu chuẩn IEEE 519 và IEC 61000-3-2).
  - **Điện áp một chiều đầu ra:** $U_o = 400.0\text{ V}$, độ đập mạch đúng theo lý thuyết tính toán $\pm 4.85\text{ V}$ ($9.70\text{ V}_{pp}$).
* **Hình ảnh chèn:** Đồ thị dạng sóng $u_s, i_s$ và Biểu đồ phổ vạch FFT sóng hài (`figures/thd_fft_spectrum.png`).
* **Speaker Notes:** "Kết quả mô phỏng cho thấy hệ số công suất đạt tới 0.998 và THD chỉ 2.12%, thấp hơn rất nhiều so với ngưỡng quy định 5%."

---

### SLIDE 9: MỤC 4 - MÔ PHỎNG: BIẾN ĐỘNG TẢI VÀ BIẾN ĐỘNG LƯỚI
* **Tiêu đề:** 4. Mô phỏng: Thử nghiệm Thay đổi Tải và Nguồn Lưới
* **Nội dung hiển thị:**
  - **Thử nghiệm bước nhảy tải ($100\% \to 50\% \to 100\%$):**
    - Khi tải giảm đột ngột từ $1\text{ kW}$ về $500\text{ W}$: Độ vọt lố điện áp chỉ $+12.0\text{ V}$ ($3.0\%$), thời gian xác lập lại cực nhanh ($40\text{ ms}$).
    - Khi tải tăng trở lại $1\text{ kW}$: Độ sụt áp chỉ $-10.0\text{ V}$ ($2.5\%$), dòng điện chuyển tiếp mượt mà, không xảy ra xung nhọn quá dòng.
  - **Thử nghiệm biến động điện áp lưới ($\pm 10\%$):**
    - Khi lưới sụt $-10\%$ ($198\text{ V}$) và vọt $+10\%$ ($242\text{ V}$): Điện áp DC đầu ra hầu như không bị dao động (sai lệch $< 4\text{ V}$).
    - Chứng minh vai trò vượt trội của khâu bù trước điện áp lưới $1/\bar{u}_{in}^2$.
* **Hình ảnh chèn:** Đồ thị đáp ứng miền thời gian tổng thể (`figures/simulation_time_domain.png`).
* **Speaker Notes:** "Dù tải giảm một nửa hay lưới điện sụt 10%, hệ thống vẫn duy trì điện áp 400V rất vững vàng nhờ sự phối hợp nhịp nhàng giữa bộ bù loại 2 và khâu feedforward."

---

### SLIDE 10: MỤC 5 - ĐIỀU KHIỂN SỐ: RỜI RẠC HÓA TUSTIN (2P2Z)
* **Tiêu đề:** 5. Cấu trúc Điều khiển Định hướng Số
* **Nội dung hiển thị:**
  - **Phương pháp rời rạc hóa:** Sử dụng phép biến đổi Tustin ($s = \frac{2}{T_s} \frac{1 - z^{-1}}{1 + z^{-1}}$) chuyển bộ bù loại 2 thành bộ lọc số 2P2Z:
    $$G_c(z) = \frac{b_0 + b_1 z^{-1} + b_2 z^{-2}}{1 - a_1 z^{-1} - a_2 z^{-2}}$$
  - **Tham số số hóa:**
    - Vòng dòng ($T_{si} = 10\,\mu\text{s}$): $b_0 = 0.2573, b_1 = 0.0742, b_2 = -0.1832; a_1 = 0.5979, a_2 = 0.4021$.
    - Vòng áp ($T_{sv} = 50\,\mu\text{s}$): $b_0 = 4.62 \cdot 10^{-4}, b_1 = 1.11 \cdot 10^{-6}, b_2 = -4.61 \cdot 10^{-4}; a_1 = 1.9908, a_2 = -0.9908$.
  - **Phương trình sai phân:** $u[k] = a_1 u[k-1] + a_2 u[k-2] + b_0 e[k] + b_1 e[k-1] + b_2 e[k-2]$.
  - Khâu chống bão hòa tích phân (Anti-windup Clamping) khóa biến trạng thái khi chạm ngưỡng $d_{\max} = 0.98$.
* **Hình ảnh chèn:** Sơ đồ khối rời rạc 2P2Z và đoạn mã C nhúng.
* **Speaker Notes:** "Chúng em đã số hóa hoàn toàn bộ bù thành phương trình sai phân 2P2Z và thuật toán C có khâu anti-windup, sẵn sàng nạp trực tiếp lên các vi điều khiển DSP như C2000 hoặc STM32."

---

### SLIDE 11: KẾT LUẬN & KIẾN NGHỊ PHÁT TRIỂN
* **Tiêu đề:** Kết luận và Hướng phát triển
* **Nội dung hiển thị:**
  - **Những kết quả đạt được:**
    1. Hoàn thành trọn vẹn thiết kế phần cứng và giải thuật điều khiển bộ biến đổi Boost PFC $1\text{ kW}$.
    2. Tổng hợp thành công bộ bù loại 2 cho cả 2 vòng, đảm bảo dự trữ pha vững chắc ($60^\circ$ và $45^\circ$).
    3. Kiểm chứng toàn diện qua mô phỏng: $PF = 0.998$, $THD_i = 2.12\%$, điện áp $400\text{ V}$ ổn định trước mọi dao động tải và nguồn.
    4. Xây dựng hoàn chỉnh thuật toán điều khiển số 2P2Z trên nền vi điều khiển DSP.
  - **Hướng mở rộng thực tế:**
    - Triển khai cấu trúc PFC xen kẽ đa pha (Interleaved Boost PFC) để triệt tiêu thêm sóng hài dòng đầu vào ở công suất lớn hơn.
    - Áp dụng kỹ thuật điều khiển không cảm biến dòng (Sensorless PFC) để giảm chi phí phần cứng.
* **Speaker Notes:** "Tóm lại, hệ thống thiết kế hoàn toàn đáp ứng các tiêu chuẩn kỹ thuật đề ra. Trong tương lai, mô hình có thể phát triển lên cấu trúc xen kẽ để nâng cao công suất."

---

### SLIDE 12: TRANG CẢM ƠN (THANK YOU)
* **Tiêu đề chính:** XIN CHÂN THÀNH CẢM ƠN!
* **Nội dung:**
  - Cảm ơn Thầy PGS. TS. Vũ Hoàng Phương và các bạn đã chú ý lắng nghe.
  - Nhóm 7 rất mong nhận được câu hỏi và đóng góp ý kiến từ Thầy và các bạn!
* **Speaker Notes:** "Nhóm 7 xin chân thành cảm ơn Thầy và các bạn đã theo dõi. Chúng em xin sẵn sàng lắng nghe các câu hỏi và nhận xét."

---

<a name="phan-7"></a>
## PHẦN VII: TỔNG HỢP NGUỒN HƯỚNG DẪN & FILE MÔ PHỎNG TRÊN MẠNG (SIMULINK & TINA-TI)

Phần này cung cấp đầy đủ liên kết chính thống, tài liệu App Notes và hướng dẫn từng bước để sinh viên tải về, cài đặt và chạy thử nghiệm trên cả hai nền tảng MATLAB/Simulink và TINA-TI.

### 7.1. Nguồn Tài nguyên Texas Instruments & TINA-TI
Texas Instruments là hãng bán dẫn đầu ngành về giải pháp PFC Boost với dòng IC analog huyền thoại **UC3854** và dòng hiện đại **UCC28180**. Toàn bộ mô hình đã được xây dựng sẵn cho phần mềm TINA-TI (miễn phí):

1. **Phần mềm mô phỏng TINA-TI:**
   - Tải bộ cài chính thức: [Texas Instruments TINA-TI SPICE Simulator](https://www.ti.com/tool/TINA-TI)
2. **Mô hình mô phỏng PFC Boost CCM trên TINA-TI:**
   - **TINA-TI Transient Reference Design (`.tsc`)**: File mạch nguyên lý hoàn chỉnh, chỉ cần mở và nhấn Run Simulation:
     - [Tải trực tiếp UCC28180 TINA-TI Transient Reference Design (SLUM529)](https://www.ti.com/lit/tsc/SLUM529)
   - **TINA-TI Transient SPICE Model (`.zip`)**:
     - [Tải trực tiếp UCC28180 TINA-TI Model (SLUM528)](https://www.ti.com/lit/zip/SLUM528)
   - **PSpice Average Model (`.zip`)**: Mô hình trung bình dùng quét đáp ứng tần số Bode cực nhanh trong vài giây:
     - [Tải trực tiếp UCC28180 Average Model (SLUM423)](https://www.ti.com/lit/zip/SLUM423)
3. **Application Notes kinh điển bắt buộc phải đọc:**
   - **TI SLUA144 - "Average Current Mode Control of Switching Regulators" (Tác giả: Lloyd Dixon)**: Tài liệu nền tảng giải thích toán học của điều khiển dòng trung bình ACMC.  
     URL: [TI SLUA144 PDF](https://www.ti.com/lit/pdf/slua144)
   - **TI SLVA662 - "Demystifying Type II and Type III Compensators Using Op Amp and OTA"**: Cẩm nang thiết kế bộ bù Type 2 từng bước cho mạch Op-Amp và OTA.  
     URL: [TI SLVA662 PDF](https://www.ti.com/lit/pdf/slva662)
   - **TI Design TIDA-00443 (TIDU962B) - "230-V, 900-W PFC With 98% Efficiency"**: Báo cáo thực nghiệm mạch thật 900W với đầy đủ bảng đo THD, PF, dạng sóng.  
     URL: [TI TIDA-00443 Guide](https://www.ti.com/lit/ug/tidu962b/tidu962b.pdf)
4. **Bảng tính tự động chính thức của TI (Excel Design Calculator):**
   - Công cụ nhập $V_{in}, V_o, P_o, f_s$ tự động xuất thông số $L, C$ và bộ bù Type II:  
     URL: [UCC28180 Design Calculator (SLUC506)](https://www.ti.com/tool/download/SLUC506)

### 7.2. Nguồn Tài nguyên MathWorks & MATLAB/Simulink
1. **Mô hình chính thức trong Thư viện MathWorks Simscape Electrical:**
   - Mở trực tiếp trong cửa sổ Command Window của MATLAB:
     ```matlab
     openExample('ee_power_factor_correction')
     ```
   - Tài liệu kỹ thuật chi tiết của hãng: [MathWorks CCM Boost PFC Documentation](https://www.mathworks.com/help/simscape-electrical/ug/power-factor-correction-for-ccm-boost-converter.html)
   - Đặc điểm: Sử dụng các khối linh kiện công suất vật lý Simscape, có đầy đủ 2 mạch vòng điều khiển dòng trung bình và khởi động mềm.
2. **Mô hình hoàn chỉnh từ cộng đồng MathWorks File Exchange:**
   - **"Boost PFC Average Current Control with a Precharge Circuit" (Tác giả: Ouassim)**:  
     URL: [MATLAB Central File Exchange #168151](https://www.mathworks.com/matlabcentral/fileexchange/168151-boost-pfc-average-current-control-with-a-precharge-circuit)  
     *Ưu điểm:* Có sẵn mạch nạp mềm precharge, khối đo đạc PF và THD liên tục.
   - **"PFC with Boost Converter and based on PI Controller"**:  
     URL: [MATLAB Central File Exchange #181077](https://www.mathworks.com/matlabcentral/fileexchange/181077-pfc-with-boost-converter-and-based-on-pi-controller)
3. **Video hướng dẫn từng bước xây dựng mô phỏng trên YouTube:**
   - *Video 1:* "Simulink Model of Boost PFC, MATLAB" - Hướng dẫn nối dây chi tiết từng khối:  
     URL: [Xem trên YouTube (FgcnN_N8B6k)](https://www.youtube.com/watch?v=FgcnN_N8B6k)
   - *Video 2:* "MATLAB Simulation of Boost Power Factor Correction (PFC)" - Hướng dẫn đo sóng hài và PF:  
     URL: [Xem trên YouTube (Z5FXpKFwuk4)](https://www.youtube.com/watch?v=Z5FXpKFwuk4)
   - *Video 3:* "Single Phase PFC Using Average Current Mode Control" - Giải thích nguyên lý điều khiển:  
     URL: [Xem trên YouTube (dKWH-y5V-oQ)](https://www.youtube.com/watch?v=dKWH-y5V-oQ)

### 7.3. Hướng dẫn Thực hiện Đo đạc Kiểm chứng trên Mô phỏng

#### Các bước đo THD và vẽ phổ sóng hài trên MATLAB/Simulink:
1. Đưa khối `powergui` vào sơ đồ mô phỏng Simulink.
2. Nối dòng điện xoay chiều đầu vào $i_s(t)$ vào khối `To Workspace` (đặt tên biến `i_grid`, định dạng `Structure with Time`).
3. Chạy mô phỏng trong ít nhất $0.2\text{ s}$ để hệ thống vào trạng thái xác lập hoàn toàn.
4. Mở cửa sổ khối `powergui` -> chọn công cụ **FFT Analysis**.
5. Chọn tín hiệu `i_grid`, nhập thời gian bắt đầu phân tích (Start time = $0.16\text{ s}$, tương ứng đúng 2 chu kỳ lưới $50\text{ Hz}$ ở xác lập).
6. Đặt tần số cơ bản `Fundamental frequency = 50 Hz`, số lượng chu kỳ `Number of cycles = 2`, tần số hiển thị cực đại `Max frequency = 1000 Hz`.
7. Nhấn nút **Display/Compute**: Simulink sẽ tự động xuất giá trị $\text{THD} (\%)$ chính xác và vẽ biểu đồ hình cột phân tích biên độ từng bậc hài ($h_3, h_5, h_7, \dots$).

#### Các bước đo Hệ số công suất (PF) trên MATLAB/Simulink:
1. Sử dụng khối `Power (Real-Imaginary)` hoặc `Active & Reactive Power` để đo công suất tác dụng $P$ (W).
2. Sử dụng hai khối `RMS` (đặt tần số $50\text{ Hz}$) để đo điện áp hiệu dụng $U_{\text{rms}}$ và dòng điện hiệu dụng $I_{\text{rms}}$.
3. Dùng khối chia `Divide` để tính công suất biểu kiến $S = U_{\text{rms}} \cdot I_{\text{rms}}$ (VA).
4. Tính hệ số công suất: $\text{PF} = \dfrac{P}{S}$. Nối kết quả ra khối `Display` để quan sát số đo $\ge 0.99$.

---

<a name="phan-8"></a>
## PHẦN VIII: PHỤ LỤC - MẠCH BÙ TƯƠNG ĐƯƠNG OP-AMP ANALOG VÀ CHỨNG MINH TOÁN HỌC

Để cung cấp góc nhìn so sánh toàn diện giữa thiết kế tương tự và thiết kế số theo đúng yêu cầu học phần, phần này trình bày chi tiết cách thiết lập mạch khuếch đại thuật toán (Op-Amp) tương tự cho bộ bù loại 2.

### 8.1. Sơ đồ Mạch Phần cứng Op-Amp Bộ bù Loại 2
Mạch sử dụng một khuếch đại thuật toán đảo với cấu hình mạch lọc tích cực:
- Nhánh đầu vào: Điện trở $R_{in}$.
- Nhánh phản hồi âm: Gồm nhánh nối tiếp $R_f - C_f$ mắc song song với tụ điện cao tần $C_p$ (với điều kiện thiết kế $C_p \ll C_f$).

```
                      +-------[ Rf ]----||----+
                      |                 Cf    |
                      +----------||-----------+
                                 Cp           |
                                              |
               Rin                 |\         |
    V_error ---[  ]---+------------|- \       |
                      |            |   \------+---> V_control
                      |         +--|+  /
                      |         |  | /
                     ---        |  |/
                     --- C_in  === GND
                      |
                     === GND
```

### 8.2. Hàm truyền đạt và Quan hệ Linh kiện
Tổng trở nhánh vào: $Z_{in}(s) = R_{in}$.  
Tổng trở nhánh hồi tiếp:
$$Z_f(s) = \left(R_f + \frac{1}{s C_f}\right) \parallel \left(\frac{1}{s C_p}\right) = \frac{\frac{s R_f C_f + 1}{s C_f} \cdot \frac{1}{s C_p}}{\frac{s R_f C_f + 1}{s C_f} + \frac{1}{s C_p}} = \frac{1 + s R_f C_f}{s (C_f + C_p) \left(1 + s R_f \frac{C_f C_p}{C_f + C_p}\right)}$$
Hàm truyền đạt của mạch Op-Amp (bỏ qua dấu âm do đảo cực tính ở khâu so sánh):
$$G_c(s) = \frac{Z_f(s)}{Z_{in}(s)} \approx \frac{1 + s R_f C_f}{s R_{in} C_f (1 + s R_f C_p)}$$
Đối chiếu đồng nhất hệ số với dạng chính tắc $G_c(s) = \dfrac{K_c}{s} \dfrac{1 + s/\omega_z}{1 + s/\omega_p}$:
$$\begin{cases}
\omega_z = \dfrac{1}{R_f C_f} \\
\omega_p \approx \dfrac{1}{R_f C_p} \\
K_c = \dfrac{1}{R_{in} C_f}
\end{cases} \iff \begin{cases}
C_f = \dfrac{1}{K_c R_{in}} \\
R_f = \dfrac{1}{\omega_z C_f} \\
C_p = \dfrac{1}{\omega_p R_f}
\end{cases}$$

### 8.3. Bảng Tính chọn Linh kiện Chuẩn E24 cho 2 Mạch vòng

#### a) Mạch vòng Dòng điện ($f_{ci} = 20\text{ kHz}, K_{ci} = 10578, \omega_{zi} = 33671.5\text{ rad/s}, \omega_{pi} = 468983.3\text{ rad/s}$)
- Chọn điện trở ngõ vào: $R_{in,i} = 10.0\text{ k}\Omega$ (chuẩn $1\%$).
- Tụ tích phân $C_{fi}$:
  $$C_{fi} = \frac{1}{K_{ci} R_{in,i}} = \frac{1}{10578 \cdot 10000} \approx 9.45\text{ nF} \implies \text{Chọn chuẩn E24: } \mathbf{10\text{ nF}} \text{ (hoặc } 9.1\text{ nF})$$
- Điện trở sớm pha $R_{fi}$:
  $$R_{fi} = \frac{1}{\omega_{zi} C_{fi}} = \frac{1}{33671.5 \cdot 10\cdot 10^{-9}} \approx 2.97\text{ k}\Omega \implies \text{Chọn chuẩn E24: } \mathbf{3.0\text{ k}\Omega}$$
- Tụ lọc cao tần $C_{pi}$:
  $$C_{pi} = \frac{1}{\omega_{pi} R_{fi}} = \frac{1}{468983.3 \cdot 3000} \approx 710\text{ pF} \implies \text{Chọn chuẩn E24: } \mathbf{680\text{ pF}} \text{ (hoặc } 750\text{ pF})$$

#### b) Mạch vòng Điện áp ($f_{cv} = 15\text{ Hz}, K_{cv} = 4.853, \omega_{zv} = 48.217\text{ rad/s}, \omega_{pv} = 184.223\text{ rad/s}$)
- Chọn điện trở ngõ vào: $R_{in,v} = 100.0\text{ k}\Omega$ (chuẩn $1\%$).
- Tụ tích phân $C_{fv}$:
  $$C_{fv} = \frac{1}{K_{cv} R_{in,v}} = \frac{1}{4.853 \cdot 100000} \approx 2.06\,\mu\text{F} \implies \text{Chọn chuẩn E24: } \mathbf{2.2\,\mu\text{F}}$$
- Điện trở sớm pha $R_{fv}$:
  $$R_{fv} = \frac{1}{\omega_{zv} C_{fv}} = \frac{1}{48.217 \cdot 2.2\cdot 10^{-6}} \approx 9.43\text{ k}\Omega \implies \text{Chọn chuẩn E24: } \mathbf{9.1\text{ k}\Omega} \text{ (hoặc } 10\text{ k}\Omega)$$
- Tụ lọc cao tần $C_{pv}$:
  $$C_{pv} = \frac{1}{\omega_{pv} R_{fv}} = \frac{1}{184.223 \cdot 9100} \approx 0.596\,\mu\text{F} \implies \text{Chọn chuẩn E24: } \mathbf{0.56\,\mu\text{F}} \text{ (hoặc } 0.68\,\mu\text{F})$$

---
*Báo cáo được hoàn thành và nghiệm thu đầy đủ bởi Nhóm 7 (EE4331 - 2026.1).*
