---
name: gae-app-ui
description: Thiết kế & kiểm tra giao diện cho app nội bộ Giang Anh (dashboard, tool tích hợp Lark, app vận hành, web mobile cho KTV/lái xe/xưởng). Dùng khi xây mới, sửa, hoặc review UI của bất kỳ app nào không phải trang marketing.
---

# Giao diện app nội bộ Giang Anh — chế độ "Operate"

Tổng hợp từ 12 repo (impeccable, Google design.md, taste-skill, hallmark, Emil Kowalski skills, GSAP skills, ui-ux-pro-max, react-bits…). Nguyên tắc gốc: app vận hành được dùng hàng chục–hàng trăm lần/ngày → **quét nhanh, nhất quán, không phô diễn**. Thương hiệu nằm ở chi tiết chính xác, không ở hiệu ứng.

## 0. Trước khi code

1. Xác định chế độ: **Operate** (app, dashboard, tool, form) → skill này. Trang landing/giới thiệu → dùng skill `gae-marketing-page`.
2. Đọc `DESIGN.md` ở gốc dự án nếu có; token trong đó là luật. Nếu chưa có → tạo theo khung ở mục 12 rồi mới code.
3. Đọc `package.json` để biết stack đang dùng. Không đổi thư viện đang có.
4. Mỗi màn hình trả lời **một câu hỏi** và nêu **một phát hiện** (vd: "Hôm nay xưởng 2 chậm tiến độ 3 đơn"). Việc làm nhiều nhất phải cách 1 click.
5. Liệt kê dữ liệu thật & các job của người dùng trước khi vẽ. Không lorem ipsum, không số bịa, không "Acme".

## 1. Token mặc định (khi DESIGN.md chưa quy định)

```css
:root {
  /* Nền & chữ */
  --bg: #fafafa;          /* ground — không dùng #fff tinh */
  --surface: #ffffff;     /* card, bảng */
  --ink: #171717;         /* chữ chính — không #000 */
  --ink-2: #5f6368;       /* chữ phụ */
  --ink-3: #6b6b6b;       /* xám nhạt nhất còn đạt 4.5:1 */
  --ink-disabled: #b2b2b2;
  --line: #e8e8e8;        /* viền */
  --line-row: #f2f2f2;    /* kẻ dòng bảng */
  --line-control: #d1d5db;/* viền input */
  /* Màu nhấn: MỘT màu, ≤5–10% diện tích màn hình */
  --accent: #0f4c81;      /* đổi theo brand GAE; tránh indigo/violet Tailwind */
  --accent-hover: #0d3f6b;
  --accent-active: #0a3258;
  --on-accent: #ffffff;
  /* Ngữ nghĩa — bộ riêng, không trùng màu accent */
  --ok: #04250e;   --ok-bg: #dcfae5;
  --warn: #5c3a00; --warn-bg: #fff3cd;
  --bad: #831c1e;  --bad-bg: #ffedea;
  --info: #0b3d5c; --info-bg: #e6f1fa;
  /* Bo góc: một "hệ" — chặt (4–8) hoặc mềm (16–24), không ở giữa */
  --r-input: 4px; --r-button: 6px; --r-card: 8px; --r-modal: 12px; --r-pill: 9999px;
  /* Khoảng cách: thang 4/8 */
  --s-1: 4px; --s-2: 8px; --s-3: 12px; --s-4: 16px; --s-6: 24px; --s-8: 32px; --s-12: 48px;
  /* Độ cao: L0 phẳng + viền; L1–L3 chỉ cho thứ "nổi" (menu, dialog) */
  --shadow-1: 0 1px 3px rgba(0,0,0,.06);
  --shadow-2: 0 8px 24px rgba(0,0,0,.08);
  --shadow-3: 0 16px 48px rgba(0,0,0,.12);
  /* Chữ */
  --font: "Be Vietnam Pro", "Inter", "Noto Sans", system-ui, sans-serif; /* phải đủ dấu tiếng Việt */
  --font-mono: "JetBrains Mono", ui-monospace, monospace; /* CHỈ cho mã/code, không để "trông kỹ thuật" */
  /* Chuyển động */
  --ease-out: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
  --t-press: 120ms; --t-state: 150ms; --t-overlay: 250ms;
}
```

- Mọi màu/font/khoảng cách đi qua token; không hex thô trong component.
- Viền **hoặc** bóng, không cả hai trên cùng phần tử.
- Dark mode (nếu cần) là bảng màu riêng, không đảo ngược; giảm bão hoà, không dùng màu tinh.

## 2. Màu

- **Một "sự kiện màu"**: accent chỉ cho hành động chính, mục đang chọn, trạng thái. Mọi thứ khác đi trên thang xám. Trong app, màu đặt lên **dữ liệu** (trạng thái, delta), không lên khung.
- Một nút primary đầy màu mỗi khung nhìn. Nút primary tối (#1d1f20) cũng tốt khi accent đã dùng cho dữ liệu.
- Sidebar/toolbar dùng **lớp xám thứ hai**, cùng tông với nền — không sidebar tối hoặc bão hoà trên nền sáng.
- Màu không bao giờ là tín hiệu duy nhất: kèm nhãn, icon hoặc vị trí.
- Delta: màu theo **tốt/xấu**, không theo tăng/giảm (chi phí tăng = xấu). 0 = xám. Luôn nêu mốc so sánh ("so với 30 ngày trước").
- Cấm: gradient (đặc biệt tím→xanh, cyan trên nền tối), glow/halo, glass/backdrop-blur làm trang trí, nền kem+đất nung, bóng màu, chip trạng thái bão hoà chữ trắng.

## 3. Chữ

- Một họ sans phủ đủ tiếng Việt (Be Vietnam Pro / Inter / Noto Sans). Tối đa 2 họ, ≤3 weight/màn hình.
- Thang cố định (rem), tỉ số 1.125–1.2: 12 / 14 / 16 / 18 / 20 / 24 / 32. Không `clamp()` fluid trong app.
- Body ≥16px trên mobile (input <16px bị iOS zoom). Không chữ nào <12px; chữ chức năng <11px là lỗi. Line-height ≥1.3, body 1.5–1.6 (dấu tiếng Việt cần chỗ — không `overflow:hidden` với line-height chặt).
- Tiêu đề trang: **danh từ**, 18–32px/600 (thường 24). Không lời chào, không emoji. Có dòng phụ xám nêu phát hiện + dấu thời gian cập nhật (và nút làm mới).
- Sentence case. Không eyebrow/nhãn uppercase tracked trên tiêu đề, không đánh số 01/02/03, không in nghiêng một từ, không tô màu một từ.
- Measure 60–75ch; bảng dày đặc >120ch được phép. `text-wrap: balance` cho tiêu đề, `pretty` cho đoạn.
- Số liệu, tiền, giờ: `font-variant-numeric: tabular-nums`. Định dạng `Intl.NumberFormat('vi-VN')`, ngày `dd/MM/yyyy`.

## 4. Bố cục & khung app

- Top bar mặc định; sidebar (224–240px, cùng nền) chỉ khi >7 đích; thu gọn <1024px.
- Hàng nav 32px (pitch 34), icon outline 16px nét 1.5px, nhãn 14px; mục active = pill xám trung tính; nhãn nhóm 12–13px sentence case. Đếm số chỉ trên hàng đợi cần xử lý. ≤5 mục cấp cao nhất.
- Lưới: **một giá trị gutter**; card cùng hàng chung mép dưới; số cột theo số mục (không ô trống, không ô kéo giãn); ghi phép tính lưới ra.
- Khoảng cách: nhóm chặt, giữa nhóm rộng; **trên tiêu đề ≥2× dưới tiêu đề**; không lặp một giá trị ở mọi nơi. Padding trong hộp có viền ≥8px (12–16 tốt). Chữ cách mép màn hình ≥16px (12px nếu ≤480px).
- Không card lồng card. Không 3 card icon-trên-tiêu-đề làm cấu trúc trang. Không sọc màu viền trái/phải >1px trên card/hàng/alert.
- Dropdown/popover phải thoát `overflow:hidden`: dùng `<dialog>`, Popover API, portal hoặc `position:fixed`.
- Bộ nhớ làm việc: ≤4 lựa chọn tại mỗi điểm quyết định; 1 hành động chính + 1–2 phụ, còn lại vào menu. Modal là lựa chọn cuối, không phải đầu.

## 5. KPI, bảng, biểu đồ, trạng thái

**KPI** — là chữ, không phải "ô": một container chia bằng kẻ 1px; giá trị 24–30px/400–600 (≈1.7× nhãn), không bao giờ 48+; không vòng icon, không sparkline, không "hero metric" (số to + nhãn nhỏ + màu nhấn). Số thay đổi: không chuyển động, hoặc NumberFlow nhẹ — dữ liệu không nhúc nhích vì đẹp.

**Bảng** — bảng trước card. Hàng 36–53px; header 12px xám sentence case, không dải nền; không zebra; kẻ 1px tối hơn nền 3–7%. Số căn phải, tabular, số thập phân cố định theo chỉ số, dấu phân cách hàng nghìn, dấu ± trên mọi thay đổi, đơn vị là hậu tố xám. Thiếu = gạch xám; 0 thật = in "0". Sort có `aria-sort`; >50 hàng → virtualize; >1000 → phân trang/tổng hợp + drill-down. Tổng tính từ dòng, không nhập tay.

**Chip trạng thái** — 20px cao, nền nhạt + chữ đậm cùng sắc (`--ok-bg`/`--ok`…), một chip/hàng, `white-space:nowrap`, kèm chữ (không chỉ chấm màu). Không chấm nhấp nháy/pulse.

**Biểu đồ** — loại theo dữ liệu: line = xu hướng, bar = so sánh, pie chỉ ≤5 phần. Một series/một sắc mỗi chart, ≤4 sắc/màn hình. 3–5 gridline mờ (#e5e5e5), không trục y, 4–7 tick tròn, nhãn x không xoay; line thẳng 2px không marker, fill ≤14%; không legend cho một series; dự báo nét đứt; chú thích đỉnh bất thường kèm nguyên nhân. Có đơn vị trục, tooltip giá trị chính xác, dữ liệu ≥3:1 tương phản. Có empty/loading/error+retry. Cung cấp bảng thay thế & xuất CSV.

**Bốn trạng thái mỗi vùng dữ liệu** — loading: thanh xám đúng kích thước thật, không shimmer kéo dài, không nhảy layout (CLS<0.1); empty: giữ khung + header + một câu + một hành động, phân biệt *lần đầu* / *không có kết quả* / *đang lọc* / *không có quyền*; error: nằm trong khối lỗi, nói cái gì hỏng + dữ liệu tốt lần cuối lúc nào + Thử lại; success: xác nhận ngắn. Spinner quá 60s → chuyển sang tiến trình/huỷ.

## 6. Thành phần & trạng thái

Mỗi control có đủ: default, hover, focus-visible, active, disabled, loading, error (+ success, selected nơi cần). Không ship thiếu nửa.

- Nút: nhãn nêu hành động ("Lưu đơn", "Xuất CSV"), không "OK/Có/Không/Submit"; nhãn không bao giờ xuống dòng; primary 1 kiểu duy nhất; destructive màu đỏ, tách riêng, đặt cuối, confirm **nêu tên đối tượng và hậu quả**; ưu tiên Hoàn tác hơn hỏi xác nhận.
- Input: 38–40px (filter 32px), viền cố định + outline khi focus, cùng chiều cao nút bên cạnh; nhãn **trên** field 14px/500, placeholder chỉ là ví dụ; đánh dấu bắt buộc; đúng `type`/`inputmode` để lên đúng bàn phím mobile; autocomplete; validate khi blur (không từng phím); lỗi dưới field, `aria-describedby`, nói **cái gì sai – vì sao – sửa thế nào**; submit lỗi → focus vào lỗi đầu; giữ nguyên dữ liệu đã nhập; disable nút + spinner khi đang gửi (chống gửi đôi); form dài tự lưu nháp; nhiều bước có tiến trình.
- Disabled: opacity .38–.5 + cursor + thuộc tính thật; read-only trông khác disabled; **giải thích vì sao** bị khoá/không có quyền thay vì giấu.
- Focus ring 2–4px, ≥3:1, hiện ngay (không fade), không bị sticky che. Không bao giờ bỏ outline.
- Tooltip: delay 800–1000ms khi hover, 0 khi focus; tooltip kề mở ngay. Toast: 3–5s tự tắt, `aria-live=polite`, không cướp focus, dùng Sonner; không toast cho việc người dùng đã thấy.
- Icon: một bộ SVG, một nét (1.5 hoặc 2px); icon-only cần `aria-label`; icon trang trí `aria-hidden`. **Không emoji làm icon.**
- Tạo kiểu cả mặc định trình duyệt từ palette: `::selection`, caret, scrollbar, focus ring.
- Giữ cùng "từ vựng" nút/form/icon trên mọi màn hình: nếu nút Lưu trông khác nhau ở hai chỗ, một chỗ sai.

## 7. Copy tiếng Việt

- Dấu đủ, sentence case, ngắn. Nút = động từ + đối tượng. Lỗi 3 phần. Không mã thô ("404") làm thông điệp.
- Cấm từ sáo: "tối ưu hoá toàn diện", "giải pháp đột phá", "đẳng cấp", "mạnh mẽ", "liền mạch", "nâng tầm", "Tìm hiểu thêm"/"Bắt đầu ngay" làm nút phụ; không lạm dụng gạch ngang dài.
- Chữ Việt dài hơn 30–40% so với bản nháp tiếng Anh: để chỗ, kiểm tra zoom 200%.

## 8. Web mobile (KTV, lái xe, xưởng)

- `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover, interactive-widget=resizes-content">`; không `user-scalable=no`; `theme-color` theo scheme.
- Input ≥16px; `touch-action: manipulation` trên nút; `-webkit-tap-highlight-color: transparent`; `user-select:none` chỉ trên control; `100dvh` cho app shell; `env(safe-area-inset-*)`.
- Mục tiêu chạm 44×44 (sàn 24), cách 8px; control quan trọng ở vùng ngón cái (dưới). Bottom nav ≤5 mục icon+nhãn; sidebar → top bar 48px + sheet.
- <640px: bảng thành hàng 2 dòng (`display:block` + `data-label`), KPI lưới 2 cột, tối đa 1 hàng control trên chart; **không bao giờ cuộn ngang**.
- Hover chỉ bật với `@media (hover:hover) and (pointer:fine)`. Phản hồi nhấn qua `:active`/`pointerdown`.
- Chọn sáng/tối theo **nơi dùng** (xưởng sáng, ngoài trời nắng → nền sáng, tương phản cao), không theo thói quen.
- Test trên Android tầm trung thật, CPU throttle 4–6×, mạng chậm.

## 9. Ngân sách chuyển động

**Cổng tần suất** (quyết định trước): >100 lần/ngày (phím tắt, tìm kiếm, bảng) → **không animation**; vài chục lần/ngày (hover, chọn hàng) → gần như không nhận ra; thỉnh thoảng (modal, drawer, toast) → chuẩn; hiếm/lần đầu (onboarding, hoàn thành) → nơi duy nhất được "delight". Hành động từ bàn phím không bao giờ animate.

**Cổng mục đích**: phải gọi tên được — phản hồi / nhất quán không gian / báo trạng thái / tránh thay đổi giật. Không gọi tên được → không làm. Dữ liệu đang đọc/thao tác không chuyển động vì kiểu.

- Thời lượng: nhấn 100–160ms; tooltip 125ms; dropdown 150–200ms; xác nhận trạng thái **150ms mặc định**; modal/sheet 200–250ms; drawer ≤500ms với `--ease-drawer`. **Không gì >300ms trong app.** Mobile ngắn hơn 20–30%. Thoát nhanh hơn vào (≈60–70%).
- Easing: vào/ra = ease-out (`--ease-out`); di chuyển/biến hình = ease-in-out; đổi màu/hover = `ease`; chuyển động liên tục = linear. **Không ease-in, không bounce/elastic** trên UI. Không tự bịa cubic-bezier.
- Chỉ animate `transform` & `opacity` (clip-path cho reveal; height chỉ cho accordion). Không `transition: all`. Không width/margin/padding/top/left. Vào từ `scale(.95–.97)` + opacity, **không `scale(0)`**. Popover theo `transform-origin` từ phía trigger (modal ở giữa, miễn).
- Dùng transition (ngắt được, retarget) thay keyframes cho thứ bắn nhanh (toast, toggle). Thoát theo đường đã vào.
- Stagger 30–80ms/mục, chỉ trang trí, không chặn tương tác. Không entrance animation cho màn hình app, không "fade-in mọi section", không chuỗi mở trang.
- `prefers-reduced-motion`: giảm & nhẹ, không về 0 — giữ opacity/màu, bỏ translate/scale/parallax (`useReducedMotion()`; GSAP: `gsap.matchMedia()`).
- Loop: carousel dừng sau 3–5 vòng; shimmer chỉ khi đang tải; >5s phải có nút dừng; ≤3 nhấp nháy/giây.
- Công cụ rẻ nhất trước: CSS transition → `@starting-style` → CSS animation → WAAPI → Motion (spring/layout/exit/gesture) → GSAP (timeline/scroll). Không cài thư viện cho một fade. Tối đa 2 thư viện chuyển động (motion + gsap).
- Hiệu năng: `will-change` chỉ sau khi thấy giật thật; không setState mỗi frame (ghi `ref.current.style`); blur animate ≤5px; Motion: dùng `transform:` string thay `x/y` nếu cần GPU; GSAP React: `useGSAP({scope})`, `contextSafe`, `autoAlpha`, register plugin một lần, client-only.

## 10. Thư viện nên dùng (React/Next)

| Nhu cầu | Chọn |
|---|---|
| Primitive (dialog, popover, menu, select) | base-ui hoặc shadcn/Radix đang có |
| Toast | sonner |
| Command palette | cmdk |
| OTP/mã | input-otp |
| Số KPI động | NumberFlow (hoặc không animate) |
| Biểu đồ | recharts; luồng live (IoT thang máy) → Liveline |
| Danh sách dài | Virtuoso |
| Kéo thả | dnd kit |
| State | zustand; class: clsx / cva |
| Theme | next-themes |
| Chuyển động | motion (spring/layout/exit); GSAP Flip cho sắp xếp lại |

React Bits — dùng chọn lọc (Micro/Components): Counter, CountUp, AnimatedList, Stepper, SwipeToast, StatusMark, LatticeLoader, SloshGauge, RubberSegment/PillNav, GlideSelect, SquishSwitch, HoldButton/SlideCommit (xác nhận hành động quan trọng), SwipeRow (mobile), SpotlightCard/MagicBento (vừa phải), SplitFlapText (màn hình xưởng), LogoLoop (đại lý). **Cấm** trong app: 63 Backgrounds WebGL, cursor effects, gallery 3D, glitch/fuzzy text, Canvas UI, Scroll World.

## 11. Kiểm tra phá UI (break-ui) trước khi giao

Dữ liệu tệ nhất có thật: tên "Nguyễn Thị Ngọc Hân Vũ Phương" (dấu bị cắt?), tên công ty 60 ký tự, mã bản vẽ/đơn dài (middle-truncate), email/URL (`overflow-wrap:anywhere`), số tiền 12 chữ số (không bao giờ cắt số/ngày), 0 hàng / 1 hàng / 1.000+ hàng, 320px / container thật / rộng nhất, zoom 200%, dark mode, RTL. Fix chuẩn: `min-width:0` cột text flex, `flex-shrink:0` avatar/icon/badge/action, `Intl.PluralRules`, `Intl.Segmenter` cho chữ cái đầu. Cắt: tên → wrap; metadata → cuối; tên file → giữa; preview → clamp. Xếp mỗi lỗi: Hỏng / Xấu / Mong manh.

## 12. Khung DESIGN.md cho mỗi app (chuẩn Google design.md)

```markdown
---
name: <Tên app GAE>
colors: { primary, on-primary, surface, on-surface, neutral, error }
typography: { headline-md, body-md, label-sm }   # fontFamily/fontSize/fontWeight/lineHeight
rounded: { sm, md, lg, full }
spacing: { xs, sm, md, lg, xl }
components: { button-primary, button-primary-hover, card, input, input-focus }
---
## Overview        # 1 tham chiếu cụ thể, không tính từ ("sổ điều độ xưởng in trên giấy A4")
## Colors          # vai trò + luật khan hiếm cho từng màu
## Typography      # bảng cấp | size | weight | line-height | dùng cho
## Layout          # thang 4/8, breakpoint 768/1024, container
## Elevation & Depth
## Shapes
## Components      # Buttons / Cards / Inputs / Navigation / Signature
## Do's and Don'ts # ngắn, có chủ đích
## Motion          # token thời lượng + easing + reduced-motion
```
Thứ tự section cố định. Kiểm tra: `npx @google/design.md lint DESIGN.md` (bắt contrast <4.5:1, token mồ côi). Kèm `PRODUCT.md` ngắn: người dùng, công việc, bối cảnh dùng (xưởng, điện thoại, nắng), ràng buộc, nguồn dữ liệu (Lark Base).

## 13. Danh sách cấm (dấu hiệu "AI làm")

Gradient / gradient text / glow / glass / blob / halo · tím-indigo-cyan · nền kem+đất nung · card lồng card · 3 card icon-trên-tiêu-đề · sọc viền màu bên · viền 1px + bóng rộng cùng lúc · bóng offset cứng 4px 4px 0 · hero-metric · vòng icon trên tiêu đề · eyebrow/nhãn uppercase · 01/02/03 · emoji làm icon · mono "cho kỹ thuật" · chấm pulse · con trỏ nhấp nháy giả · marquee · bounce · fade-in mọi section · sparkline/vòng tiến trình thay nội dung · grid-line/sọc nền · doodle SVG · modal làm ý đầu · số bịa, testimonial bịa · "Không X. Chỉ Y." · từ sáo (mục 7).

## 14. Checklist giao hàng & định dạng review

**Trước khi giao**: token hoá 100% · contrast 4.5/3:1 · focus-visible · đủ trạng thái control · 4 trạng thái vùng dữ liệu · 320→1920 không cuộn ngang · input 16px mobile · touch 44 · reduced-motion · không `transition:all` · tabular-nums · tiếng Việt đủ dấu, không cắt · không số bịa · không mục nào trong danh sách cấm.

**Khi review UI** (`/review` hoặc được hỏi "xem lại giao diện"): tự hỏi trước "che tên đi, có nhận ra đây là app của ngành này không? người dùng làm được việc không? sạch bằng chuẩn ngành chưa?". Chấm 5 trục 0–4 (Accessibility, Performance, Theming, Responsive, Integrity → /20; 18–20 xuất sắc, 10–13 chấp nhận, <10 kém). Tải nhận thức: ≤4 lựa chọn/điểm quyết định, 1 trọng tâm, nhóm rõ, tiết lộ dần. Mức độ P0 chặn / P1 lớn hoặc vi phạm WCAG AA / P2 nhỏ / P3 trau chuốt. Xuất **một bảng** `| Trước | Sau | Vì sao |`, nhóm theo mức ảnh hưởng, kết bằng **Chặn** hoặc **Duyệt**. Thứ tự sửa animation: xoá → giảm → easing → origin → ngắt được → GPU → bất đối xứng → trau chuốt → a11y.
