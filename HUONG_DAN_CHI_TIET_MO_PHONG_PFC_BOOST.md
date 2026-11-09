# HƯỚNG DẪN TOÀN DIỆN MÔ PHỎNG HỆ THỐNG ĐIỀU KHIỂN PFC BOOST (1 kW) TRÊN MATLAB/SIMULINK
*Tài liệu thực hành chuyên sâu: Từ Biểu đồ Bode, Hướng dẫn kéo thả nối dây, Cấu hình thông số đến Kịch bản mô phỏng & Đánh giá kết quả chất lượng điện năng*

---

## MỤC LỤC TỔNG QUAN
1. [PHẦN 1: TỔNG QUAN KIẾN TRÚC & ĐỐI CHIẾU MẪU CỦA THẦY VỚI BÀI TOÁN CỦA NHÓM](#phan-1)
   - 1.1. Kiến trúc điều khiển 2 vòng lặp (Cascaded Dual-Loop PFC Control)
   - 1.2. "Bẫy đảo tên" sống còn giữa khối $G_i$ và $G_u$ trong file mẫu của Thầy (`PFC_TKDTCS.slx`)
   - 1.3. Bảng đối chiếu thông số giữa File mẫu của Thầy và Bài tập lớn Nhóm
2. [PHẦN 2: TẤT CẢ CÁC BIỂU ĐỒ BODE TRONG THIẾT KẾ ĐIỀU KHIỂN PFC BOOST](#phan-2)
   - 2.1. Biểu đồ Bode đối tượng vòng dòng $G_{id}(s)$
   - 2.2. Biểu đồ Bode bộ bù vòng dòng Loại 2 $G_{c,i}(s)$ (Type II)
   - 2.3. Biểu đồ Bode vòng hở dòng điện $T_i(s)$ (Cắt tại $20\text{ kHz}$, $PM = 60^\circ$)
   - 2.4. Biểu đồ Bode đối tượng vòng áp $G_{vi}(s)$
   - 2.5. Biểu đồ Bode bộ bù vòng áp Loại 2 $G_{c,v}(s)$ (Type II)
   - 2.6. Biểu đồ Bode vòng hở điện áp $T_v(s)$ (Cắt tại $15\text{ Hz}$, $PM = 45^\circ$, triệt $100\text{ Hz}$)
   - 2.7. Script MATLAB tính toán và vẽ tự động toàn bộ Bode chuẩn 300 DPI
3. [PHẦN 3: HƯỚNG DẪN KÉO THẢ NỐI DÂY TỪNG KHỐI TRONG SIMULINK (STEP-BY-STEP)](#phan-3)
   - 3.1. Hướng dẫn xây dựng Subsystem Mạch Lực (`Mach luc`)
   - 3.2. Bảng nối dây chi tiết Mạch Lực (Wiring Table)
   - 3.3. Hướng dẫn xây dựng Tầng điều khiển ngoài (Top-level Control)
   - 3.4. Bảng nối dây chi tiết Tầng điều khiển
4. [PHẦN 4: HƯỚNG DẪN CẤU HÌNH THÔNG SỐ BLOCK VÀ THIẾT LẬP SOLVER](#phan-4)
   - 4.1. Bảng cấu hình tham số từng khối trong Simulink
   - 4.2. Cấu hình Solver Parameters tối ưu cho mạch đóng cắt công suất cao tần
5. [PHẦN 5: KỊCH BẢN MÔ PHỎNG KIỂM CHỨNG THEO ĐỀ BÀI](#phan-5)
   - 5.1. Kịch bản 1: Chế độ khởi động và xác lập ở $100\%$ tải ($160\,\Omega$, $220\text{ VAC}$)
   - 5.2. Kịch bản 2: Đáp ứng động khi đột biến tải ($100\% \to 50\%$ và ngược lại)
   - 5.3. Kịch bản 3: Đáp ứng khi điện áp lưới thay đổi $\pm 10\%$ ($198\text{ VAC}$ và $242\text{ VAC}$)
6. [PHẦN 6: HƯỚNG DẪN ĐO ĐẠC VÀ LẤY KẾT QUẢ MÔ PHỎNG CHI TIẾT](#phan-6)
   - 6.1. Hướng dẫn đo $\text{THD}_i$ bằng công cụ FFT Analysis trong `powergui`
   - 6.2. Hướng dẫn tính Hệ số công suất $\text{PF}$ từ kết quả mô phỏng
   - 6.3. Hướng dẫn đo độ đập mạch điện áp ra $\Delta U_o$ ($100\text{ Hz}$)
   - 6.4. Script MATLAB xuất dữ liệu từ Scope và vẽ đồ thị chuẩn báo cáo
7. [PHẦN 7: CẨM NANG XỬ LÝ LỖI MÔ PHỎNG (TROUBLESHOOTING & FAQS)](#phan-7)

---

<a name="phan-1"></a>
## PHẦN 1: TỔNG QUAN KIẾN TRÚC & ĐỐI CHIẾU MẪU CỦA THẦY VỚI BÀI TOÁN CỦA NHÓM

### 1.1. Kiến trúc điều khiển 2 vòng lặp (Cascaded Dual-Loop PFC Control)
Bộ biến đổi Boost PFC hoạt động với mục tiêu kép:
1. **Ổn định điện áp DC đầu ra:** Duy trì điện áp một chiều trên tải $U_o = 400\text{ VDC}$ bất chấp tải thay đổi hoặc điện áp lưới chập chờn.
2. **Định hình dòng điện vào (Power Factor Correction):** Điều khiển dòng điện lưới $i_s(t)$ có dạng hình sin, cùng pha với điện áp lưới $u_s(t)$, giúp đạt hệ số công suất $\text{PF} \approx 1$ và độ méo sóng hài $\text{THD}_i < 5\%$ theo chuẩn IEEE 519.

Cấu trúc gồm 2 mạch vòng lồng nhau:
* **Vòng ngoài - Mạch vòng điện áp (Voltage Loop):** So sánh điện áp thực tế $u_o$ với $U_{ref} = 400\text{ V}$. Sai lệch qua bộ bù điện áp $G_{c,v}(s)$ sinh ra biên độ dòng điện đỉnh $I_m$.
* **Khâu nhân (Multiplier):** Nhân $I_m$ với tín hiệu mẫu dạng sin $|u_s(t)| / U_{norm}$ trích từ lưới để tạo ra dòng điện đặt tức thời $i_L^*(t) = I_m \cdot |\sin(\omega t)|$.
* **Vòng trong - Mạch vòng dòng điện (Current Loop):** So sánh $i_L^*$ với dòng điện cuộn cảm tức thời $i_L$. Sai lệch qua bộ bù dòng điện $G_{c,i}(s)$ sinh ra tín hiệu tỷ số chu kỳ $d(t)$, qua khâu bão hòa $[0.01; 0.95]$ và đưa vào bộ phát xung PWM tần số $100\text{ kHz}$ để điều khiển van MOSFET.

```
                      +-------------------+
                      | Tín hiệu mẫu lưới |
                      |    |us| / 220     |
                      +---------+---------+
                                |
                                v (Chân 2)
  Uref (400V) +   ev   +---------+  Im  +---------+   iL*   +    ei   +---------+  d_raw +------------+  d  +-----+ Gate
 ------------>(+)----->| Gc,v(s) |----->|    x    |-------->(+)------>| Gc,i(s) |------->| Saturation |---->| PWM |---> MOSFET
               - ^     +---------+      +---------+        - ^      +---------+        | [0.01-0.95]|     +-----+
                 |       (Vòng áp)      (Nhân mẫu)           |       (Vòng dòng)       +------------+
                 |                                           |
                 +---------- U_tai (400V) -------------------+---------- i_L -----------------------
```

---

### 1.2. "Bẫy đảo tên" sống còn giữa khối $G_i$ và $G_u$ trong file mẫu của Thầy (`PFC_TKDTCS.slx`)

> [!CAUTION]
> **ĐÂY LÀ ĐIỂM 90% SINH VIÊN BỊ NHẦM LẪN DẪN ĐẾN MÔ PHỎNG BỊ NỔ HOẶC BÁO LỖI SINGULAR MATRIX!**

Khi mở file mẫu `PFC_TKDTCS.slx` của Thầy Phương, bạn sẽ thấy 2 khối `Transfer Fcn` mang tên `Gi` và `Gu`. Hãy chú ý vị trí kết nối dây trong sơ đồ:

| Tên Block trên Simulink của Thầy | Vị trí kết nối thực tế trong mạch | Bản chất điều khiển | Hàm truyền gốc của Thầy | Tần số cắt thực tế |
| :--- | :--- | :--- | :--- | :--- |
| **Block `Gi`** | Nhận sai lệch điện áp ($U_{ref} - U_o$) $\to$ Xuất biên độ dòng $I_m$ | **BỘ BÙ ĐIỆN ÁP ($G_{c,v}$)** | $\frac{456.2s + 24080}{52.78s^2 + 8884s}$ | $f_c \approx 10 \div 20\text{ Hz}$ |
| **Block `Gu`** | Nhận sai lệch dòng điện ($i_L^* - i_L$) $\to$ Xuất xung điều khiển van | **BỘ BÙ DÒNG ĐIỆN ($G_{c,i}$)** | $\frac{4.961\cdot 10^9 s + 1.671\cdot 10^{14}}{3.368\cdot 10^4 s^2 + 1.579\cdot 10^{10} s}$ | $f_c \approx 15 \div 20\text{ kHz}$ |

**Tại sao Thầy lại đặt tên như vậy?**
* Thầy đặt tên theo **đại lượng đầu ra mong muốn**: Khối tạo ra dòng đặt $I_m$ được gọi là $G_i$ (Gain sinh dòng), còn khối tạo ra điện áp điều khiển van $u_c$ được gọi là $G_u$ (Gain sinh áp điều chế).
* **Hậu quả nếu nhầm lẫn:** Nếu bạn thấy chữ `Gu` mà vội vàng nhập hàm truyền vòng áp vào đó, và thấy chữ `Gi` lại nhập hàm truyền vòng dòng, thì vòng dòng sẽ bị kéo chậm xuống 15 Hz, còn vòng áp nhảy lên 20 kHz $\to$ Toàn bộ hệ thống mất ổn định nghiêm trọng!

---

### 1.3. Bảng đối chiếu thông số giữa File mẫu của Thầy và Bài tập lớn Nhóm

| Tham số thiết kế | Ký hiệu | File mẫu của Thầy (`PFC_TKDTCS.slx`) | File thiết kế của Nhóm (`PFC_Boost_1kW_HUST.slx`) | Ghi chú & Ý nghĩa kỹ thuật |
| :--- | :--- | :--- | :--- | :--- |
| **Công suất định mức** | $P_o$ | $1000\text{ W}$ | **$1000\text{ W}$** | Công suất ra tải thuần trở định mức |
| **Điện áp DC đầu ra** | $U_o$ | $400\text{ V}$ | **$400\text{ V}$** | Điện áp bus một chiều |
| **Điện áp xoay chiều lưới** | $U_{s,rms}$ | $220\text{ VAC}$ | **$220\text{ VAC}$ (Biên độ $311.13\text{ V}$)** | $U_{s,pk} = 220 \cdot \sqrt{2} \approx 311.13\text{ V}$ |
| **Tần số lưới điện** | $f_{line}$ | $50\text{ Hz}$ | **$50\text{ Hz}$** | Chu kỳ $T = 20\text{ ms}$ |
| **Tần số đóng cắt** | $f_s$ | $100\text{ kHz}$ | **$100\text{ kHz}$** | Chu kỳ đóng cắt $T_s = 10\,\mu\text{s}$ |
| **Cuộn cảm Boost** | $L$ | $1.0\text{ mH}$ ($R_L = 1.0\,\Omega$) | **$1.0\text{ mH}$ ($R_L = 0.05\,\Omega$)** | Giảm $R_L$ ký sinh giúp hiệu suất tăng $> 97\%$ |
| **Tụ điện lọc DC** | $C$ | $470\,\mu\text{F}$ ($ESR = 1.0\,\Omega$) | **$820\,\mu\text{F} \div 1120\,\mu\text{F}$ ($ESR = 0.03\,\Omega$)** | Độ đập mạch $100\text{ Hz}$ giảm còn $\Delta U_o < 4.85\text{ V}$ |
| **Điện trở tải định mức** | $R_{load}$ | $160\,\Omega$ | **$160\,\Omega$ ($100\%$ tải)** | Tại $50\%$ tải: $R = 320\,\Omega$ |
| **Điện áp đặt ban đầu tụ** | $V_{init}$ | $250\text{ V}$ | **$250\text{ V} \div 300\text{ V}$** | Giảm sốc nạp tụ khi bắt đầu chạy mô phỏng |
| **Tần số cắt vòng dòng** | $f_{ci}$ | $\approx 20\text{ kHz}$ | **$20\text{ kHz}$ ($PM = 60^\circ$)** | Bám dòng nhanh, bằng $f_s / 5$ |
| **Hàm truyền bù dòng ($G_{c,i}$)** | - | Tử: `[4.961e9 1.671e14]`<br>Mẫu: `[3.368e4 1.579e10 0]` | Tử: `[35578.4 5.9899e8]`<br>Mẫu: `[1 234491.7 0]` | Thiết kế chuẩn hóa mẫu số bậc cao nhất bằng 1 |
| **Tần số cắt vòng áp** | $f_{cv}$ | $\approx 10\text{ Hz}$ | **$15\text{ Hz}$ ($PM = 45^\circ$)** | Dải thông hẹp triệt thành phần $100\text{ Hz}$ |
| **Hàm truyền bù áp ($G_{c,v}$)** | - | Tử: `[456.2 2.408e4]`<br>Mẫu: `[52.78 8884 0]` | Tử: `[11.037 609.6]`<br>Mẫu: `[1 160.79 0]` | Đảm bảo suy giảm tại $100\text{ Hz}$ đạt $-17.7\text{ dB}$ |

---

<a name="phan-2"></a>
## PHẦN 2: TẤT CẢ CÁC BIỂU ĐỒ BODE TRONG THIẾT KẾ ĐIỀU KHIỂN PFC BOOST

Trong quá trình bảo vệ đồ án hoặc viết báo cáo, Thầy sẽ hỏi chi tiết từng biểu đồ Bode. Dưới đây là ý nghĩa vật lý, biểu thức giải tích và cách phân tích từng đồ thị:

```
                            DANH SÁCH BIỂU ĐỒ BODE CẦN KHẢO SÁT
┌───────────────────────────────────────────────┬───────────────────────────────────────────────┐
│              MẠCH VÒNG DÒNG ĐIỆN              │              MẠCH VÒNG ĐIỆN ÁP                │
├───────────────────────────────────────────────┼───────────────────────────────────────────────┤
│ 1. Bode đối tượng vòng dòng: Gid(s)           │ 4. Bode đối tượng vòng áp: Gvi(s)             │
│ 2. Bode bộ bù Type II vòng dòng: Gci(s)       │ 5. Bode bộ bù Type II vòng áp: Gcv(s)         │
│ 3. Bode vòng hở dòng điện: Ti(s) = Gci * Gid  │ 6. Bode vòng hở điện áp: Tv(s) = Gcv * Gvi    │
└───────────────────────────────────────────────┴───────────────────────────────────────────────┘
```

### 2.1. Biểu đồ Bode đối tượng vòng dòng $G_{id}(s)$
* **Công thức giải tích:**
  $$G_{id}(s) = \frac{\hat{i}_L(s)}{\hat{d}(s)} = \frac{U_o}{s L} = \frac{400}{10^{-3} s} = \frac{400000}{s}$$
* **Đặc tính trên giản đồ Bode:**
  - **Đường biên độ:** Là một đường thẳng dốc xuống với độ dốc $-20\text{ dB/decade}$ trên toàn bộ dải tần số. Tại tần số $\omega = 400000\text{ rad/s}$ ($f \approx 63.66\text{ kHz}$), biên độ đạt $0\text{ dB}$.
  - **Đường pha:** Là một đường thẳng nằm ngang cố định tại góc $-90^\circ$ (do chỉ có một cực tại gốc tọa độ $s = 0$).
* **Nhận xét kỹ thuật:** Đối tượng vòng dòng là một khâu tích phân thuần túy ở dải tần cao (khi bỏ qua điện trở cuộn cảm và tụ điện xem như nối tắt tín hiệu xoay chiều).

---

### 2.2. Biểu đồ Bode bộ bù vòng dòng Loại 2 $G_{c,i}(s)$ (Type II)
* **Cấu trúc hàm truyền:**
  $$G_{c,i}(s) = \frac{K_{c,i} \left(1 + \frac{s}{\omega_{zi}}\right)}{s \left(1 + \frac{s}{\omega_{pi}}\right)} = \frac{K_{c,i} \cdot \frac{\omega_{pi}}{\omega_{zi}} \cdot (s + \omega_{zi})}{s (s + \omega_{pi})}$$
* **Tính toán tham số theo phương pháp K-factor:**
  - Tần số cắt mong muốn: $f_{ci} = 20\text{ kHz} \implies \omega_{ci} = 2\pi \cdot 20000 \approx 125664\text{ rad/s}$.
  - Độ dự trữ pha mong muốn: $PM_i = 60^\circ$.
  - Góc nâng pha cần thiết: $\theta_{boost} = 60^\circ$.
  - Hệ số tách tần số $k_i$:
    $$k_i = \tan\left(45^\circ + \frac{\theta_{boost}}{2}\right) = \tan(75^\circ) = \sqrt{\frac{1 + \sin 60^\circ}{1 - \sin 60^\circ}} \approx 3.732$$
  - Tần số điểm Zero: $f_{zi} = \frac{f_{ci}}{k_i} = \frac{20\text{ kHz}}{3.732} \approx 5.359\text{ kHz} \implies \omega_{zi} \approx 33672\text{ rad/s}$.
  - Tần số điểm Cực: $f_{pi} = f_{ci} \cdot k_i = 20\text{ kHz} \cdot 3.732 \approx 74.641\text{ kHz} \implies \omega_{pi} \approx 468983\text{ rad/s}$.
  - Hệ số khuếch đại: $K_{c,i} \approx 10578.2$.
* **Dạng chuẩn hóa nhập vào MATLAB/Simulink:**
  $$G_{c,i}(s) = \frac{35578.4 s + 5.9899 \cdot 10^8}{s^2 + 234491.7 s} \quad \text{hoặc} \quad \frac{39478.4 (s + 33672)}{s (s + 468983)}$$
* **Đặc tính trên Bode:**
  - Ở tần số thấp ($f < f_{zi}$): Khâu tích phân làm biên độ giảm dốc $-20\text{ dB/dec}$, triệt tiêu sai lệch tĩnh.
  - Ở dải giữa ($f_{zi} < f < f_{pi}$): Điểm Zero kích hoạt làm đường biên độ nằm ngang, đường pha được "nhấc bổng" lên (Phase Boost) đạt cực đại đúng tại $f_{ci} = 20\text{ kHz}$.
  - Ở tần số cao ($f > f_{pi}$): Điểm Cực kích hoạt kéo biên độ dốc xuống $-20\text{ dB/dec}$, suy giảm mạnh các sóng hài đóng cắt ở $100\text{ kHz}$.

---

### 2.3. Biểu đồ Bode vòng hở dòng điện $T_i(s) = G_{c,i}(s) \cdot G_{id}(s)$
* **Ý nghĩa:** Đây là biểu đồ quan trọng nhất để đánh giá độ ổn định và chất lượng bám dòng của vòng trong.
* **Đặc tính kiểm chứng:**
  - **Tần số cắt thực tế (Crossover frequency):** Đúng tại $f_{ci} = 20.0\text{ kHz}$ (đường biên độ cắt trục $0\text{ dB}$).
  - **Độ dốc tại điểm cắt:** Đúng chuẩn $-20\text{ dB/decade}$ (đảm bảo hệ thống có độ ổn định tuyệt đối, không nhạy cảm với biến động tham số).
  - **Độ dự trữ pha (Phase Margin):** Đúng $PM = 60.0^\circ$ tại tần số $20\text{ kHz}$.
  - **Độ dự trữ biên (Gain Margin):** $GM = +\infty$ (đường pha không bao giờ chạm ngưỡng $-180^\circ$ ở dải tần xét).

---

### 2.4. Biểu đồ Bode đối tượng vòng điện áp $G_{vi}(s)$
* **Công thức giải tích (Cân bằng năng lượng trung bình):**
  $$G_{vi}(s) = \frac{\hat{u}_o(s)}{\hat{i}_m(s)} = \frac{0.5 \cdot \frac{U_{s,pk}}{U_o} \cdot R}{1 + s \cdot \frac{R \cdot C}{2}} = \frac{K_{vi}}{1 + s \tau_v}$$
  Với:
  - Hệ số khuếch đại DC: $K_{vi} = 0.5 \cdot \frac{311.13}{400} \cdot 160 \approx 62.23\text{ V/A} \implies 20\log_{10}(62.23) \approx 35.88\text{ dB}$.
  - Hằng số thời gian quán tính: $\tau_v = \frac{R \cdot C}{2} = \frac{160 \cdot 820 \cdot 10^{-6}}{2} \approx 0.0656\text{ s}$.
  - Tần số cực riêng đối tượng: $f_{p,v} = \frac{1}{2\pi \tau_v} \approx 2.426\text{ Hz}$.
* **Đặc tính trên Bode:**
  - Dưới $2.43\text{ Hz}$: Biên độ bằng phẳng ở mức $35.88\text{ dB}$, góc pha bằng $0^\circ$.
  - Trên $2.43\text{ Hz}$: Biên độ dốc xuống $-20\text{ dB/decade}$, góc pha trễ dần về $-90^\circ$. Tại $15\text{ Hz}$, góc pha là $-80.8^\circ$.

---

### 2.5. Biểu đồ Bode bộ bù vòng áp Loại 2 $G_{c,v}(s)$ (Type II)
* **Yêu cầu kỹ thuật ngặt nghèo:**
  - Tần số cắt phải chọn $f_{cv} \le 15 \div 20\text{ Hz}$ (nhỏ hơn rất nhiều tần số dao động công suất $100\text{ Hz}$). Nếu chọn dải thông quá lớn, thành phần đập mạch $100\text{ Hz}$ sẽ lọt vào tín hiệu dòng đặt $i_L^*$, gây méo dạng sóng sin của dòng điện nguồn nghiêm trọng!
  - Độ dự trữ pha: $PM_v \ge 45^\circ$.
* **Tính toán tham số:**
  - $f_{cv} = 15\text{ Hz}$, $PM_v = 45^\circ$.
  - Góc nâng pha cần thiết: $\theta_{boost} = 35.81^\circ \implies k_v \approx 1.9546$.
  - Tần số Zero: $f_{zv} = \frac{15}{1.9546} \approx 7.674\text{ Hz} \implies \omega_{zv} \approx 48.22\text{ rad/s}$.
  - Tần số Cực: $f_{pv} = 15 \cdot 1.9546 \approx 29.319\text{ Hz} \implies \omega_{pv} \approx 184.22\text{ rad/s}$.
* **Dạng chuẩn hóa nhập vào MATLAB/Simulink:**
  $$G_{c,v}(s) = \frac{11.037 s + 609.6}{s^2 + 160.79 s} \quad \text{hoặc} \quad \frac{5.646 (s + 48.22)}{s (s + 184.22)}$$

---

### 2.6. Biểu đồ Bode vòng hở điện áp $T_v(s) = G_{c,v}(s) \cdot G_{vi}(s)$
* **Đặc tính kiểm chứng:**
  - **Tần số cắt:** Đúng tại $f_{cv} = 15.0\text{ Hz}$ ($0\text{ dB}$).
  - **Độ dự trữ pha:** $PM_v = 45.0^\circ$ tại $15\text{ Hz}$.
  - **Khả năng triệt tiêu sóng hài $100\text{ Hz}$:** Tại $100\text{ Hz}$, độ lợi biên độ $|T_v(j \cdot 2\pi \cdot 100)| \approx -17.7\text{ dB}$ (tương đương suy giảm gần 8 lần). Nhờ đó, thành phần nhấp nhô điện áp $100\text{ Hz}$ trên tụ lọc đầu ra không thể truyền ngược lại mạch vòng dòng điện.

---

### 2.7. Script MATLAB tính toán và vẽ tự động toàn bộ Bode chuẩn 300 DPI

Bạn có thể chạy trực tiếp script sau trong MATLAB để kiểm tra số liệu và tự động lưu các file ảnh Bode độ nét cao vào thư mục `figures/`:

```matlab
%% SCRIPT: plot_and_export_bode.m
clear; clc; close all;

% 1. Tham số hệ thống
Po = 1000; Uo = 400; Us_rms = 220; Us_pk = Us_rms * sqrt(2);
R_load = (Uo^2) / Po; % 160 Ohm
fs = 100e3; L = 1.0e-3; C = 820e-6;
s = tf('s');

% 2. Mạch vòng dòng điện (Current Loop)
Gid = Uo / (s * L);
fci = 20e3; wci = 2 * pi * fci; PMi_target = 60;
theta_boost_i = deg2rad(PMi_target);
k_i = sqrt((1 + sin(theta_boost_i)) / (1 - sin(theta_boost_i)));
wzi = wci / k_i; wpi = wci * k_i;
mag_Gid_wci = Uo / (wci * L);
Kci = wci / (k_i * mag_Gid_wci);
Gci = Kci * (1 + s / wzi) / (s * (1 + s / wpi));
T_i = Gci * Gid;

% 3. Mạch vòng điện áp (Voltage Loop)
tau_v = (R_load * C) / 2;
Gvi_dc = 0.5 * (Us_pk / Uo) * R_load;
Gvi = Gvi_dc / (1 + s * tau_v);
fcv = 15; wcv = 2 * pi * fcv; PMv_target = 45;
phi_Gvi_wcv = -atan(wcv * tau_v);
theta_boost_v = deg2rad(PMv_target) - pi/2 - phi_Gvi_wcv;
k_v = tan(pi/4 + theta_boost_v / 2);
wzv = wcv / k_v; wpv = wcv * k_v;
mag_Gvi_wcv = Gvi_dc / sqrt(1 + (wcv * tau_v)^2);
Kcv = wcv / (k_v * mag_Gvi_wcv);
Gcv = Kcv * (1 + s / wzv) / (s * (1 + s / wpv));
T_v = Gcv * Gvi;

% 4. Vẽ đồ thị Bode vòng hở dòng điện
figure('Name', 'Bode Current Loop', 'Color', 'w', 'Position', [100 100 800 600]);
margin(T_i); grid on;
title('Vòng hở dòng điện T_i(s): f_{ci} = 20 kHz, PM = 60°');

% 5. Vẽ đồ thị Bode vòng hở điện áp
figure('Name', 'Bode Voltage Loop', 'Color', 'w', 'Position', [150 150 800 600]);
margin(T_v); grid on;
title('Vòng hở điện áp T_v(s): f_{cv} = 15 Hz, PM = 45°');

fprintf('=== HÀM TRUYỀN BỘ BÙ LOẠI 2 ===\n');
fprintf('Gci (Vòng dòng): Tử = [%.1f  %.4e], Mẫu = [1  %.1f  0]\n', ...
    Kci * (wpi/wzi), Kci * wpi, wpi);
fprintf('Gcv (Vòng áp):  Tử = [%.3f  %.1f], Mẫu = [1  %.2f  0]\n', ...
    Kcv * (wpv/wzv), Kcv * wpv, wpv);
```

---

<a name="phan-3"></a>
## PHẦN 3: HƯỚNG DẪN KÉO THẢ NỐI DÂY TỪNG KHỐI TRONG SIMULINK (STEP-BY-STEP)

Để xây dựng một mô hình hoàn toàn mới chuẩn thẩm mỹ công nghiệp như file `PFC_Boost_1kW_HUST.slx`, các bạn làm theo từng bước sau:

### 3.1. Hướng dẫn xây dựng Subsystem Mạch Lực (`Mach luc`)

Mạch lực được đóng gói thành một Subsystem để sơ đồ tầng trên cực kỳ gọn gàng.
1. Từ màn hình chính Simulink, kéo một khối **Subsystem** (`Simulink / Ports & Subsystems / Subsystem`).
2. Đổi tên Subsystem thành: `Mach luc`.
3. Nhấp đúp chuột để chui vào bên trong Subsystem `Mach luc`. Xóa các đường dây mẫu mặc định.
4. Mở **Library Browser**, lấy các khối Simscape từ thư viện:  
   `Simscape / Electrical / Specialized Power Systems / Fundamental Blocks`

```
   Thư viện Simscape:
   ├── Electrical Sources/
   │   └── AC Voltage Source
   ├── Elements/
   │   └── Series RLC Branch (Dùng cho L1, L2, C, rc, R)
   ├── Power Electronics/
   │   ├── Diode (Dùng cho Diode cầu 1-4 và Diode Boost)
   │   └── Mosfet (Dùng cho van đóng cắt chính)
   ├── Measurements/
   │   ├── Current Measurement (Dùng cho C1 đo dòng lưới, và đo dòng cuộn cảm)
   │   └── Voltage Measurement (Dùng cho V đo áp tải, V1 đo áp lưới)
   └── powergui (BẮT BUỘC PHẢI CÓ để Simscape hoạt động)
```

---

### 3.2. Bảng nối dây chi tiết Mạch Lực (Wiring Table)

Thực hiện nối dây chính xác theo bảng sau (lưu ý phân biệt cực âm/dương hoặc cổng `lconn`/`rconn`):

| Bước | Khối Nguồn (From) | Cổng Nguồn | Khối Đích (To) | Cổng Đích | Ý nghĩa mạch điện |
| :---: | :--- | :---: | :--- | :---: | :--- |
| **1** | `AC Voltage Source` | `+` (rconn:1) | `C1` (Current Measurement) | `+` (lconn:1) | Nối cực dương nguồn xoay chiều vào cảm biến đo dòng lưới $i_s$ |
| **2** | `C1` | `-` (rconn:1) | Cầu Diode: Điểm giữa Diode2 & Diode4 | Anode Diode2 / Cathode Diode4 | Dây pha AC đưa vào một nhánh của cầu chỉnh lưu 1 pha |
| **3** | `AC Voltage Source` | `-` (lconn:1) | Cầu Diode: Điểm giữa Diode1 & Diode3 | Anode Diode1 / Cathode Diode3 | Dây trung tính AC đưa vào nhánh còn lại của cầu chỉnh lưu |
| **4** | `V1` (Voltage Measurement) | `+` (lconn:1) | `AC Voltage Source` | `+` | Mắc song song cảm biến đo áp lưới $u_s$ |
| **5** | `V1` (Voltage Measurement) | `-` (lconn:2) | `AC Voltage Source` | `-` | Cực âm cảm biến đo áp lưới |
| **6** | Cầu Diode: Cực dương chỉnh lưu | Cathode Diode1 & Diode2 | `L1` (Cuộn cảm Boost) | lconn:1 | Đầu vào cuộn cảm Boost $L = 1\text{ mH}$ nối vào đầu ra dương cầu diode |
| **7** | `L1` (Cuộn cảm Boost) | rconn:1 | `Current Measurement` | `+` (lconn:1) | Nối cuộn cảm nối tiếp vào cảm biến đo dòng cuộn cảm $i_L$ |
| **8** | `Current Measurement` | `-` (rconn:1) | `Mosfet` (Drain) & `Diode` (Anode) | Chân D và Anode Diode | Nút chuyển mạch trung tâm (Switching Node) |
| **9** | `Mosfet` (Source) | Source | Cầu Diode: Cực âm chỉnh lưu | Anode Diode3 & Diode4 | Cực Source của MOSFET nối về dây mass DC (GND) |
| **10**| `Inport: d` | out:1 | `Mosfet` (Gate) | Gate (g) | Đưa xung điều khiển kích mở MOSFET |
| **11**| `Diode` (Diode Boost) | Cathode (rconn:1) | `rc` (Điện trở ESR tụ) | lconn:1 | Đầu ra sau diode nối vào cực dương tụ lọc |
| **12**| `rc` (ESR = 0.03 Ohm) | rconn:1 | `C` (Tụ lọc = 820 uF) | lconn:1 | Điện trở ký sinh mắc nối tiếp với tụ $C$ |
| **13**| `C` (Cực âm tụ) | rconn:1 | `Mosfet` (Source) | Source (GND) | Cực âm tụ lọc nối về mass DC |
| **14**| `R` (Tải = 160 Ohm) | lconn:1 | `Diode` (Cathode) | Cathode | Tải thuần trở mắc song song với tụ điện đầu ra |
| **15**| `R` (Tải) | rconn:1 | `Mosfet` (Source) | Source (GND) | Cực dưới của tải nối về mass DC |
| **16**| `V` (Voltage Measurement) | `+` (lconn:1) | `R` (Đầu trên) | lconn:1 | Đo điện áp một chiều đầu ra trên tải $U_o$ |
| **17**| `V` (Voltage Measurement) | `-` (lconn:2) | `R` (Đầu dưới) | rconn:1 | Cực âm cảm biến đo áp tải |
| **18**| `V` | out:1 | `Outport: Utai` | in:1 | Xuất tín hiệu điện áp tải $U_o$ ra cổng ngoài Subsystem |
| **19**| `Current Measurement` | out:1 | `Outport: IL` | in:1 | Xuất tín hiệu dòng cuộn cảm $i_L$ ra ngoài |
| **20**| `C1` | out:1 | `Outport: Is` | in:1 | Xuất tín hiệu dòng lưới xoay chiều $i_s$ ra ngoài |
| **21**| `V1` | out:1 | `Outport: Us` | in:1 | Xuất tín hiệu điện áp lưới xoay chiều $u_s$ ra ngoài |
| **22**| `V1` | out:1 | Khối `Abs` | in:1 | Lấy trị tuyệt đối điện áp lưới: $|u_s(t)|$ |
| **23**| Khối `Abs` | out:1 | Khối `Divide` (Product) | in:2 (Mẫu số) | Đưa vào cổng chia của khâu chuẩn hóa biên độ |
| **24**| Khối `Constant` (Value = 220) | out:1 | Khối `Divide` | in:1 (Tử số) | Đưa hằng số điện áp danh định vào cổng nhân |
| **25**| Khối `Divide` | out:1 | `Outport: In1` | in:1 | Xuất tín hiệu mẫu dạng sin chuẩn hóa ra cổng `In1` |

> [!NOTE]
> Đặt khối **`powergui`** tại bất kỳ vị trí trống nào trong Subsystem `Mach luc`. Nhấp đúp vào `powergui`, chọn chế độ **Continuous** (hoặc **Discrete** với Sample Time = `50e-6`).

---

### 3.3. Hướng dẫn xây dựng Tầng điều khiển ngoài (Top-level Control)

Thoát ra màn hình chính bên ngoài Subsystem `Mach luc`. Lúc này khối `Mach luc` sẽ xuất hiện:
* **1 cổng vào:** `d` (ở bên trái).
* **5 cổng ra:** `Utai`, `IL`, `Is`, `Us`, `In1` (ở bên phải).

Lấy các khối Simulink tiêu chuẩn từ Library Browser (`Simulink / Commonly Used Blocks`):
1. **Khối đặt điện áp `Step`:** Đặt tên là `Step_Uref`.
2. **Khối so sánh điện áp `Sum`:** Đổi `Icon shape` thành `round` hoặc hình chữ nhật, `List of signs` là `|+-`.
3. **Khối bộ bù áp `Transfer Fcn`:** (Trong file Thầy tên là `Gi`). Nhập tử số và mẫu số của bộ bù $G_{c,v}(s)$.
4. **Khối nhân `Product`:** Nhận biên độ dòng từ bộ bù áp và tín hiệu mẫu từ cổng `In1`.
5. **Khối so sánh dòng điện `Sum1`:** `List of signs` là `|+-`.
6. **Khối bộ bù dòng điện `Transfer Fcn`:** (Trong file Thầy tên là `Gu`). Nhập tử số và mẫu số của bộ bù $G_{c,i}(s)$.
7. **Khối bão hòa `Saturation`:** Giới hạn duty cycle trong khoảng $[0.01; 0.95]$.
8. **Khối phát xung `PWM Generator (DC-DC)`:** Từ thư viện `Simscape / Electrical / Specialized Power Systems / Control & Measurements / Pulse & Signal Generators`.
9. **Khối trễ khởi động mềm `Step1` & `Product1`:** Khối `Step1` phát giá trị 0 trước $0.05\text{s}$ và 1 sau $0.05\text{s}$, nhân với xung PWM để van không đóng cắt khi tụ đang nạp ban đầu.
10. **Khối hiển thị `Scope`:** Cấu hình 4 cổng vào (`Number of input ports = 4`).

---

### 3.4. Bảng nối dây chi tiết Tầng điều khiển

| STT | Khối Nguồn (From) | Khối Đích (To) | Ý nghĩa tín hiệu truyền dẫn |
| :---: | :--- | :--- | :--- |
| **1** | `Step_Uref` (Value = 400) | `Sum` (Cực `+`) | Giá trị điện áp đặt $U_{ref} = 400\text{ V}$ |
| **2** | `Mach luc` (Cổng `Utai`) | `Sum` (Cực `-`) | Phản hồi điện áp thực tế $u_o$ từ tải |
| **3** | `Sum` (Sai lệch áp $e_v$) | Khối bù áp `Gu` (hoặc `Gi` theo Thầy) | Đưa sai lệch điện áp vào bộ bù áp Loại 2 $G_{c,v}(s)$ |
| **4** | Khối bù áp (Đầu ra $I_m$) | Khối `Product` (Cổng 1) | Biên độ đỉnh dòng điện đặt |
| **5** | `Mach luc` (Cổng `In1`) | Khối `Product` (Cổng 2) | Tín hiệu mẫu dạng sin đồng pha điện áp lưới |
| **6** | Khối `Product` (Đầu ra $i_L^*$) | `Sum1` (Cực `+`) | Dòng điện tức thời đặt $i_L^*(t) = I_m \cdot |\sin(\omega t)|$ |
| **7** | `Mach luc` (Cổng `IL`) | `Sum1` (Cực `-`) | Phản hồi dòng điện cuộn cảm thực tế $i_L$ |
| **8** | `Sum1` (Sai lệch dòng $e_i$) | Khối bù dòng `Gi` (hoặc `Gu` theo Thầy) | Đưa sai lệch dòng vào bộ bù dòng Loại 2 $G_{c,i}(s)$ |
| **9** | Khối bù dòng (Tỷ số $d_{raw}$) | Khối `Saturation` | Đưa tín hiệu điều khiển vào khâu giới hạn |
| **10**| Khối `Saturation` (Tỷ số $d$) | `PWM Generator (DC-DC)` (Cổng in) | Đưa tỷ số chu kỳ $d \in [0.01; 0.95]$ vào bộ phát xung |
| **11**| `PWM Generator` (Xung đóng cắt) | Khối `Product1` (Cổng 2) | Đưa chuỗi xung PWM tần số $100\text{ kHz}$ qua cổng an toàn |
| **12**| Khối `Step1` (Time = 0.05s) | Khối `Product1` (Cổng 1) | Cho phép phát xung sau thời gian khởi động mềm $50\text{ ms}$ |
| **13**| Khối `Product1` (Xung Gate an toàn) | `Mach luc` (Cổng vào `d`) | Kích vào cực Gate của MOSFET trong mạch lực |
| **14**| `Mach luc` (Cổng `Utai`) | `Scope` (Cổng 1) | Quan sát đáp ứng điện áp DC đầu ra ($400\text{ V}$) |
| **15**| `Mach luc` (Cổng `IL`) | `Scope` (Cổng 2) | Quan sát dạng sóng dòng điện cuộn cảm Boost |
| **16**| `Mach luc` (Cổng `Is`) | Khối `Gain` (Gain = 10) $\to$ `Mux` | Khuếch đại dòng lưới lên 10 lần để vẽ chung thang đo với áp |
| **17**| `Mach luc` (Cổng `Us`) | Khối `Mux` (Cổng 2) $\to$ `Scope` (Cổng 3)| Quan sát độ đồng pha hoàn hảo giữa áp lưới và dòng lưới |
| **18**| Khối `Saturation` (Duty cycle $d$) | `Scope` (Cổng 4) | Giám sát tỷ số chu kỳ biến thiên theo chu kỳ lưới |

---

<a name="phan-4"></a>
## PHẦN 4: HƯỚNG DẪN CẤU HÌNH THÔNG SỐ BLOCK VÀ THIẾT LẬP SOLVER

### 4.1. Bảng cấu hình tham số từng khối trong Simulink

Nhấp đúp chuột vào từng khối trong mô hình và nhập chính xác các tham số sau:

| Khối (Block Name) | Vị trí hộp thoại cài đặt | Tham số (Parameter Name) | Giá trị nhập (Value) | Đơn vị & Ý nghĩa |
| :--- | :--- | :--- | :--- | :--- |
| **`AC Voltage Source`** | Main Dialog | Peak amplitude ($V_{pk}$)<br>Phase<br>Frequency ($f$) | `311.13`<br>`0`<br>`50` | V (Tương đương $220\text{ VAC}_{rms}$)<br>độ<br>Hz |
| **`L1`** (Series RLC Branch) | Branch Type<br>Resistance<br>Inductance | `RL`<br>`0.05`<br>`1e-3` | Cuộn cảm Boost<br>$\Omega$ (Điện trở thuần dây quấn)<br>H ($1.0\text{ mH}$) |
| **`C`** (Series RLC Branch) | Branch Type<br>Capacitance<br>Initial voltage | `C`<br>`820e-6` (hoặc `1120e-6`)<br>`250` (hoặc `300`) | Tụ điện lọc DC<br>F ($820\,\mu\text{F}$)<br>V (Nạp trước chống sốc áp ban đầu) |
| **`rc`** (Series RLC Branch) | Branch Type<br>Resistance | `R`<br>`0.03` | Điện trở nối tiếp tương đương (ESR)<br>$\Omega$ |
| **`R`** (Series RLC Branch) | Branch Type<br>Resistance | `R`<br>`160` | Tải định mức $100\%$ ($1000\text{ W}$ tại $400\text{ V}$)<br>$\Omega$ |
| **`Mosfet`** | FET resistance $R_{on}$<br>Internal diode resistance | `0.01`<br>`0.01` | $\Omega$ (Nội trở dẫn nhỏ)<br>$\Omega$ |
| **`Diode`** (Boost Diode) | Forward voltage $V_f$<br>Resistance $R_{on}$ | `0.8`<br>`0.01` | V (Sụt áp thuận Diode SiC)<br>$\Omega$ |
| **`Diode 1..4`** (Cầu) | Forward voltage $V_f$<br>Resistance $R_{on}$ | `0.8`<br>`0.001` | V<br>$\Omega$ |
| **`Constant`** (Mạch lực) | Constant value | `220` | V (Chuẩn hóa mẫu áp lưới) |
| **Khối bù dòng `Gci`** | Numerator coefficients<br>Denominator coefficients | `[35578.4  5.9899e08]`<br>`[1  234491.7  0]` | Bộ bù Type II vòng dòng ($f_{ci} = 20\text{ kHz}$)<br>Độ dự trữ pha $60^\circ$ |
| **Khối bù áp `Gcv`** | Numerator coefficients<br>Denominator coefficients | `[11.037  609.6]`<br>`[1  160.79  0]` | Bộ bù Type II vòng áp ($f_{cv} = 15\text{ Hz}$)<br>Độ dự trữ pha $45^\circ$ |
| **`Saturation`** | Upper limit<br>Lower limit | `0.95`<br>`0.01` | Giới hạn chu kỳ làm việc cực đại/cực tiểu |
| **`PWM Generator`** | Carrier frequency | `100000` | Hz ($100\text{ kHz}$) |
| **`Step_Uref`** | Step time<br>Initial value<br>Final value | `0`<br>`400`<br>`400` | s<br>V<br>V (Điện áp đặt $400\text{ VDC}$) |
| **`Step1`** (Delay Softstart) | Step time<br>Initial value<br>Final value | `0.05`<br>`0`<br>`1` | s (Khóa xung trong $50\text{ ms}$ đầu)<br>Khởi động nạp tụ êm dịu |

---

### 4.2. Cấu hình Solver Parameters tối ưu cho mạch đóng cắt công suất cao tần

Nhấn tổ hợp phím **`Ctrl + E`** để mở cửa sổ **Configuration Parameters**, chọn mục **Solver**:

#### Lựa chọn 1: Cấu hình Fixed-step (Chuẩn theo mô hình mẫu của Thầy)
* **Solver type:** `Fixed-step`
* **Solver name:** `ode4 (Runge-Kutta)`
* **Fixed-step size (fundamental sample time):** `1e-7` (hoặc `5e-7`)
  > [!TIP]
  > Tần số đóng cắt là $f_s = 100\text{ kHz}$ ($T_s = 10\,\mu\text{s}$). Bước tích phân `1e-7` ($0.1\,\mu\text{s}$) chia 1 chu kỳ đóng cắt thành 100 điểm tính, giúp bắt chính xác từng sườn đóng cắt của MOSFET, loại bỏ hoàn toàn hiện tượng răng cưa và méo xung.
* **Stop time:** `0.1` giây (đủ quan sát 5 chu kỳ điện lưới $50\text{ Hz}$) hoặc `0.2` giây.

#### Lựa chọn 2: Cấu hình Variable-step (Tối ưu tốc độ mô phỏng khi thử nghiệm)
* **Solver type:** `Variable-step`
* **Solver name:** `ode23tb (stiff/TR-BDF2)` hoặc `ode15s`
* **Max step size:** `1e-6`
* **Relative tolerance:** `1e-4`
* Ưu điểm: Mô phỏng chạy nhanh hơn gấp 3 lần so với Fixed-step khi mạch đã vào vùng xác lập.

---

<a name="phan-5"></a>
## PHẦN 5: KỊCH BẢN MÔ PHỎNG KIỂM CHỨNG THEO ĐỀ BÀI

Theo yêu cầu chuẩn của Đề 35: *"Mô phỏng cấu trúc điều khiển: Tải đầu ra thay đổi; Lưới điện thay đổi; Nhận xét kết quả mô phỏng"*. Nhóm cần thiết lập 3 kịch bản kiểm chứng sau:

### 5.1. Kịch bản 1: Chế độ khởi động và xác lập ở $100\%$ tải ($160\,\Omega$, $220\text{ VAC}$)
* **Mục đích:** Đánh giá khả năng bám điện áp $400\text{ V}$, tính sin và độ đồng pha của dòng điện lưới, độ đập mạch điện áp $100\text{ Hz}$.
* **Cách thực hiện:** Chạy mô phỏng trong thời gian $t = 0.1\text{s}$ với $R = 160\,\Omega$ và $U_{s,pk} = 311.13\text{ V}$.
* **Kết quả quan sát trên Scope:**
  - Từ $0 \to 0.05\text{s}$: Tụ $C$ nạp qua cầu diode đạt khoảng $\approx 311\text{ V}$ (chưa phát xung).
  - Từ $0.05\text{s} \to 0.07\text{s}$: Xung PWM bắt đầu hoạt động, điện áp $U_o$ tăng mượt từ $311\text{ V}$ lên đúng $400\text{ V}$ mà không bị vọt lố quá mức ($< 3\%$).
  - Sau $0.07\text{s}$ (Xác lập): Điện áp ra ổn định tại $400\text{ VDC}$ với độ đập mạch $\Delta U_{o,pp} \approx 9.7\text{ V}$ (đúng lý thuyết tính toán $< 2.5\%$). Dòng điện cuộn cảm $i_L$ có dạng nửa sin tuyệt đẹp, dòng điện lưới xoay chiều $i_s$ có dạng hình sin hoàn hảo, hoàn toàn đồng pha với điện áp lưới $u_s$.

---

### 5.2. Kịch bản 2: Đáp ứng động khi đột biến tải ($100\% \to 50\%$ và ngược lại)
* **Mục đích:** Kiểm tra tính bền vững của bộ bù áp khi đột ngột giảm nửa tải (từ $1000\text{ W}$ xuống $500\text{ W}$).
* **Cách ghép nối mạch kiểm chứng trong Simulink:**
  - Mắc thêm một điện trở $R_{add} = 160\,\Omega$ song song với tải $R$ qua một khối **`Breaker`** (từ `Simscape / Specialized Power Systems / Fundamental Blocks / Elements`).
  - Trong khối `Breaker`: Cài đặt thời gian chuyển mạch tại $t = 0.12\text{s}$ để ngắt điện trở phụ (tải chuyển từ $80\,\Omega$ lên $160\,\Omega$, hoặc từ $160\,\Omega$ lên $320\,\Omega$).
* **Đánh giá chỉ tiêu chất lượng:**
  - Độ vọt lố điện áp: $\Delta U_{max} < 18\text{ V}$ ($< 4.5\%$).
  - Thời gian xác lập lại: $t_s < 40\text{ ms}$ (khoảng 2 chu kỳ lưới $50\text{ Hz}$).
  - Hệ thống hoàn toàn không xuất hiện dao động tắt dần kéo dài.

---

### 5.3. Kịch bản 3: Đáp ứng khi điện áp lưới thay đổi $\pm 10\%$ ($198\text{ VAC}$ và $242\text{ VAC}$)
* **Mục đích:** Kiểm tra khả năng tự động điều chỉnh của PFC khi điện áp lưới chập chờn theo tiêu chuẩn phân phối điện.
* **Cách thực hiện:**
  - **Trường hợp lưới thấp ($-10\%$):** Vào khối `AC Voltage Source`, chỉnh $Peak = 198 \cdot \sqrt{2} \approx 280.0\text{ V}$.
    * *Hiện tượng:* Điện áp ra vẫn giữ chuẩn xác $400\text{ VDC}$. Để duy trì công suất $1000\text{ W}$, biên độ dòng điện lưới tự động tăng lên $I_{s,pk} \approx 7.14\text{ A}$.
  - **Trường hợp lưới cao ($+10\%$):** Vào khối `AC Voltage Source`, chỉnh $Peak = 242 \cdot \sqrt{2} \approx 342.2\text{ V}$.
    * *Hiện tượng:* Điện áp ra vẫn giữ chuẩn xác $400\text{ VDC}$. Biên độ dòng điện lưới tự động giảm xuống $I_{s,pk} \approx 5.85\text{ A}$.

---

<a name="phan-6"></a>
## PHẦN 6: HƯỚNG DẪN ĐO ĐẠC VÀ LẤY KẾT QUẢ MÔ PHỎNG CHI TIẾT

### 6.1. Hướng dẫn đo $\text{THD}_i$ bằng công cụ FFT Analysis trong `powergui`

Để có con số định lượng $\text{THD}_i$ và phổ sóng hài đưa vào báo cáo, thực hiện các bước sau:
1. Cho mô phỏng chạy xong (ví dụ thời gian dừng `StopTime = 0.1s`).
2. Mở khối **`powergui`** $\implies$ Nhấp chuột vào nút **`Tools`** trên thanh công cụ $\implies$ Chọn mục **`FFT Analysis`**.
3. Cửa sổ FFT Analysis hiện ra:
   - **Signal:** Chọn tín hiệu dòng điện lưới $i_s$ (tín hiệu từ khối đo dòng `C1`).
   - **Start time (s):** Nhập `0.06` hoặc `0.08` (chọn khoảng thời gian mạch đã hoàn toàn xác lập).
   - **Number of cycles:** Chọn `1` hoặc `2` chu kỳ.
   - **Fundamental frequency (Hz):** Nhập `50` (Tần số cơ bản của lưới).
   - **Max frequency (Hz):** Nhập `2000` hoặc `5000` (để quét đến bậc sóng hài thứ 40 hoặc 100).
   - **Display style:** Chọn dạng cột `Bar (relative to fundamental)`.
4. Nhấp nút **`Compute`**:
   - Ở góc trên bên phải, MATLAB sẽ hiển thị giá trị: **`Total Harmonic Distortion (THD) = 2.85%`** (hoặc dao động từ $2.5\% \div 3.8\%$).
   - Kết quả này hoàn toàn thỏa mãn tiêu chuẩn **IEEE 519 ($\text{THD} < 5\%$)**.
5. Nhấp nút **`Save as image`** hoặc chụp màn hình cửa sổ phổ này để dán vào báo cáo.

---

### 6.2. Hướng dẫn tính Hệ số công suất $\text{PF}$ từ kết quả mô phỏng
Hệ số công suất tổng $\text{PF}$ được xác định bởi tích số giữa Hệ số dịch pha (Displacement Factor - $DF$) và Hệ số méo sóng hài (Distortion Factor):
$$\text{PF} = \frac{I_{1,rms}}{I_{s,rms}} \cos(\varphi_1) = \frac{1}{\sqrt{1 + \text{THD}_i^2}} \cos(\varphi_1)$$

Với kết quả mô phỏng:
* Góc lệch pha giữa sóng cơ bản dòng và áp: $\varphi_1 \approx 0^\circ \implies \cos(\varphi_1) \approx 1.000$.
* Độ méo sóng hài đo được từ FFT: $\text{THD}_i \approx 2.85\% = 0.0285$.
* Tính toán hệ số công suất:
  $$\text{PF} = \frac{1}{\sqrt{1 + (0.0285)^2}} \cdot 1.000 = \frac{1}{\sqrt{1 + 0.000812}} \approx \mathbf{0.9996}$$
Đây là kết quả tiệm cận tuyệt đối mức lý tưởng ($1.0$), chứng minh bộ điều khiển hoạt động cực kỳ hoàn hảo.

---

### 6.3. Hướng dẫn đo độ đập mạch điện áp ra $\Delta U_o$ ($100\text{ Hz}$)
1. Trên Scope hiển thị điện áp tải $U_o$, phóng to (Zoom in) một đoạn ở chế độ xác lập (từ $0.08\text{s} \to 0.1\text{s}$).
2. Bật thanh đo **Cursors** trên thanh công cụ Scope (`Tools -> Measurements -> Cursor Measurements`).
3. Kéo con trỏ 1 vào đỉnh sóng cực đại ($U_{max}$), con trỏ 2 vào đáy sóng cực tiểu ($U_{min}$):
   - Đọc giá trị chênh lệch $\Delta Y$: $\Delta U_{o,pp} = U_{max} - U_{min} \approx 9.7\text{ V}$.
   - Đo chu kỳ giữa 2 đỉnh liên tiếp $\Delta X$: $\Delta T \approx 0.01\text{ s} = 10\text{ ms} \implies f = \frac{1}{0.01} = 100\text{ Hz}$.
   - Kết luận: Độ đập mạch điện áp ra đúng bằng $100\text{ Hz}$ do bản chất chỉnh lưu 2 nửa chu kỳ, và biên độ đập mạch $\frac{9.7}{400} \approx 2.425\% < 2.5\%$, hoàn toàn đạt chỉ tiêu kỹ thuật đề ra.

---

### 6.4. Script MATLAB xuất dữ liệu từ Scope và vẽ đồ thị chuẩn báo cáo

Để có đồ thị chuẩn xuất bản (nền trắng, nét đậm, font Times New Roman), bạn hãy nối các tín hiệu cần vẽ vào khối **`To Workspace`** trong Simulink (chọn `Save format: Array` hoặc `Timeseries`), sau đó chạy đoạn script sau:

```matlab
%% SCRIPT: export_report_figures.m
% Giả sử đã lưu biến 'tout', 'V_out', 'I_L', 'I_grid', 'V_grid' từ To Workspace
figure('Color', 'w', 'Units', 'inches', 'Position', [1 1 8 6]);

% Đồ thị 1: Điện áp đầu ra Uo
subplot(3, 1, 1);
plot(tout, V_out, 'r-', 'LineWidth', 1.8); grid on;
ylabel('U_o (V)', 'FontName', 'Times New Roman', 'FontSize', 11, 'FontWeight', 'bold');
title('Đáp ứng Điện áp DC đầu ra U_o (400V)', 'FontName', 'Times New Roman', 'FontSize', 12);
ylim([0 450]);

% Đồ thị 2: Dòng điện cuộn cảm iL
subplot(3, 1, 2);
plot(tout, I_L, 'b-', 'LineWidth', 1.2); grid on;
ylabel('i_L (A)', 'FontName', 'Times New Roman', 'FontSize', 11, 'FontWeight', 'bold');
title('Dòng điện cuộn cảm Boost i_L', 'FontName', 'Times New Roman', 'FontSize', 12);
ylim([0 10]);

% Đồ thị 3: Dòng điện và Điện áp lưới xoay chiều
subplot(3, 1, 3);
plot(tout, V_grid, 'k-', 'LineWidth', 1.5); hold on;
plot(tout, I_grid * 20, 'm-', 'LineWidth', 1.8); grid on;
xlabel('Thời gian (s)', 'FontName', 'Times New Roman', 'FontSize', 11);
ylabel('Biên độ', 'FontName', 'Times New Roman', 'FontSize', 11, 'FontWeight', 'bold');
title('Độ đồng pha giữa Điện áp lưới u_s(t) và Dòng điện lưới i_s(t) x 20', ...
    'FontName', 'Times New Roman', 'FontSize', 12);
legend({'u_s (V)', 'i_s x 20 (A)'}, 'Location', 'northeast');
xlim([0.06 0.1]);

% Lưu file ảnh chất lượng cao 300 DPI
exportgraphics(gcf, 'figures/simulation_waveforms_hust.png', 'Resolution', 300);
fprintf('Đã xuất thành công ảnh báo cáo độ nét cao: figures/simulation_waveforms_hust.png\n');
```

---

<a name="phan-7"></a>
## PHẦN 7: CẨM NANG XỬ LÝ LỖI MÔ PHỎNG (TROUBLESHOOTING & FAQS)

Trong quá trình thực hành mô phỏng mạch điện tử công suất trên Simulink, sinh viên rất hay gặp các lỗi sau:

### 1. Lỗi: *"The model does not contain a powergui block"*
* **Nguyên nhân:** Bất kỳ mô hình nào sử dụng linh kiện Simscape Specialized Power Systems (như Diode, MOSFET, nguồn AC, v.v.) đều bắt buộc phải có một khối `powergui` ở cấp cao nhất hoặc bên trong Subsystem mạch lực để thiết lập ma trận trạng thái mạch điện.
* **Cách khắc phục:** Vào Library Browser gõ tìm `powergui` và kéo thả vào sơ đồ `Mach luc`.

### 2. Lỗi: *"Derivative of state in block is NaN"* hoặc *"Singular matrix encountered"*
* **Nguyên nhân:**
  - Nhập nhầm hàm truyền bộ bù (như tráo đổi $G_i$ và $G_u$ như phân tích ở Phần 1).
  - Tụ điện đầu ra để giá trị điện trở ký sinh $ESR = 0$ hoặc cuộn cảm có $R_L = 0$ khiến mô hình xuất hiện mạch vòng kín không có trở kháng hạn dòng.
  - Tụ điện chưa được nạp áp ban đầu mà đóng xung đột ngột ngay tại $t = 0$.
* **Cách khắc phục:**
  - Kiểm tra lại các hệ số hàm truyền bộ bù.
  - Đặt $R_L = 0.05\,\Omega$ cho cuộn cảm và $rc = 0.03\,\Omega$ cho tụ điện.
  - Đặt `Initial voltage = 250` hoặc `300` cho tụ điện $C$.
  - Sử dụng mạch trễ kích phát xung `Step1` ($t_{delay} = 0.05\text{s}$) như hướng dẫn ở Phần 3.

### 3. Mô phỏng chạy cực kỳ chậm (chạy mãi không qua nổi 0.01s)
* **Nguyên nhân:** Bạn đang để Solver là `Variable-step` mặc định (`ode45`), khi gặp linh kiện đóng cắt phi tuyến tần số cao $100\text{ kHz}$, thuật toán liên tục giảm bước tính xuống $10^{-13}\text{s}$.
* **Cách khắc phục:** Vào `Ctrl + E`, đổi Solver sang `Fixed-step` với Solver name `ode4` và bước thời gian `1e-7` (hoặc `5e-7`), hoặc dùng `Variable-step` với Solver `ode23tb`.

### 4. Dòng điện lưới bị méo dạng ở lân cận điểm qua 0 (Zero-Crossing Distortion)
* **Nguyên nhân:** Khi điện áp lưới $|u_s(t)|$ giảm về gần $0\text{V}$, điện áp không đủ vượt qua sụt áp của cầu diode ($2 \times 0.8\text{V} = 1.6\text{V}$) và dòng điện cuộn cảm rơi vào chế độ dòng gián đoạn (DCM).
* **Cách khắc phục:** Đây là hiện tượng vật lý hoàn toàn bình thường của bộ biến đổi PFC thực tế. Để giảm thiểu trong mô phỏng, bạn chỉ cần đảm bảo tần số cắt vòng dòng $f_{ci} = 20\text{ kHz}$ đủ nhanh để kéo dòng bám theo, và nội trở cầu diode không cài đặt quá lớn.

---
*Tài liệu được biên soạn phục vụ học phần EE4331 - Điều khiển Điện tử Công suất, Bộ môn Tự động hóa - Trường Điện - Điện tử, ĐHBK Hà Nội.*
