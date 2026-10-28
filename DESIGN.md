---
version: alpha
name: Giang Anh Elevator — App nội bộ
description: Hệ thống thiết kế dùng chung cho dashboard, tool Lark và app vận hành của Thang máy Giang Anh. Đổi màu primary theo nhận diện GAE trước khi dùng.
colors:
  primary: "#0f4c81"
  primary-hover: "#0d3f6b"
  primary-active: "#0a3258"
  on-primary: "#ffffff"
  surface: "#ffffff"
  background: "#fafafa"
  on-surface: "#171717"
  on-surface-muted: "#5f6368"
  on-surface-disabled: "#b2b2b2"
  outline: "#e8e8e8"
  outline-row: "#f2f2f2"
  outline-control: "#d1d5db"
  positive: "#04250e"
  positive-container: "#dcfae5"
  warning: "#5c3a00"
  warning-container: "#fff3cd"
  error: "#831c1e"
  error-container: "#ffedea"
  info: "#0b3d5c"
  info-container: "#e6f1fa"
typography:
  headline-md: { fontFamily: "Be Vietnam Pro", fontSize: 24px, fontWeight: 600, lineHeight: 1.25 }
  title-md:    { fontFamily: "Be Vietnam Pro", fontSize: 18px, fontWeight: 600, lineHeight: 1.3 }
  body-lg:     { fontFamily: "Be Vietnam Pro", fontSize: 16px, fontWeight: 400, lineHeight: 1.55 }
  body-md:     { fontFamily: "Be Vietnam Pro", fontSize: 14px, fontWeight: 400, lineHeight: 1.5 }
  label-md:    { fontFamily: "Be Vietnam Pro", fontSize: 14px, fontWeight: 500, lineHeight: 1.4 }
  label-sm:    { fontFamily: "Be Vietnam Pro", fontSize: 12px, fontWeight: 500, lineHeight: 1.4 }
  kpi:         { fontFamily: "Be Vietnam Pro", fontSize: 28px, fontWeight: 500, lineHeight: 1.1, fontFeature: "tnum" }
rounded:
  sm: 4px
  md: 6px
  lg: 8px
  xl: 12px
  full: 9999px
spacing:
  xs: 4px
  sm: 8px
  md: 12px
  lg: 16px
  xl: 24px
  2xl: 32px
  gutter: 16px
  margin: 24px
components:
  button-primary:       { backgroundColor: "{colors.primary}", textColor: "{colors.on-primary}", typography: "{typography.label-md}", rounded: "{rounded.md}", height: 40px, padding: 0 16px }
  button-primary-hover: { backgroundColor: "{colors.primary-hover}" }
  button-secondary:     { backgroundColor: "{colors.surface}", textColor: "{colors.on-surface}", rounded: "{rounded.md}", height: 40px }
  input:                { backgroundColor: "{colors.surface}", textColor: "{colors.on-surface}", typography: "{typography.body-lg}", rounded: "{rounded.sm}", height: 40px, padding: 0 12px }
  card:                 { backgroundColor: "{colors.surface}", rounded: "{rounded.lg}", padding: "{spacing.lg}" }
  chip-positive:        { backgroundColor: "{colors.positive-container}", textColor: "{colors.positive}", rounded: "{rounded.full}", height: 20px }
  chip-error:           { backgroundColor: "{colors.error-container}", textColor: "{colors.error}", rounded: "{rounded.full}", height: 20px }
---

## Overview

Tham chiếu: **sổ điều độ sản xuất in trên giấy, được số hoá** — kẻ ô mảnh, số căn phải, một màu mực, một màu nhấn cho việc cần làm ngay. Người dùng là điều độ, kỹ thuật, kế toán, KTV và lái xe; dùng hàng chục lần mỗi ngày, nhiều khi trên điện thoại ngoài trời hoặc trong xưởng sáng. Vì vậy: quét nhanh, nhất quán, không trang trí; thương hiệu nằm ở sự chính xác.

Đặc điểm chính:
- Một màu nhấn (primary) ≤10% màn hình, chỉ cho hành động chính, mục đang chọn và trạng thái.
- Bảng trước card; KPI là chữ chia bằng kẻ 1px, không ô icon.
- Phẳng mặc định: viền 1px **hoặc** bóng nhẹ, không bao giờ cả hai; bóng chỉ cho menu/dialog.
- Chữ Be Vietnam Pro, đủ dấu, line-height ≥1.5, số dạng tabular.

## Colors

- Primary (`{colors.primary}` — #0f4c81): nút chính, mục nav đang chọn, link. Không dùng cho nền lớn, không dùng cho trạng thái "thành công".
- Nền (`{colors.background}` — #fafafa) và bề mặt (`{colors.surface}` — #ffffff): tách nhau bằng bậc tông, không kẻ. Sidebar dùng màu nền, không tối.
- Chữ: `{colors.on-surface}` cho nội dung, `{colors.on-surface-muted}` cho phụ, `{colors.on-surface-disabled}` chỉ cho disabled.
- Ngữ nghĩa: positive / warning / error / info mỗi màu có bản đậm (chữ, icon) và bản `-container` (nền chip). Luôn kèm nhãn chữ — màu không bao giờ là tín hiệu duy nhất.
- Biểu đồ: tối đa 4 sắc/màn hình; một series = một sắc; chỉ ở đây mới xuất hiện màu ngoài hệ.
- Cấm: gradient, glow, glass/blur, tím-indigo, cyan trên nền tối, bóng màu.

## Typography

| Cấp | Cỡ | Weight | Line-height | Dùng cho |
|---|---|---|---|---|
| headline-md | 24 | 600 | 1.25 | Tiêu đề trang (danh từ) |
| title-md | 18 | 600 | 1.3 | Tiêu đề khối, dialog |
| body-lg | 16 | 400 | 1.55 | Nội dung, input (sàn mobile) |
| body-md | 14 | 400 | 1.5 | Bảng, mô tả phụ |
| label-md | 14 | 500 | 1.4 | Nhãn field, nút |
| label-sm | 12 | 500 | 1.4 | Header bảng, nhãn nhóm nav |
| kpi | 28 | 500 | 1.1 | Giá trị KPI (tnum) |

Nguyên tắc: một họ chữ, ≤3 weight một màn hình; sentence case; không uppercase tracked; không chữ <12px (chức năng <11px). Dự phòng font: Inter, Noto Sans, system-ui — đều phủ dấu tiếng Việt.

## Layout

- Thang 4/8: 4, 8, 12, 16, 24, 32, 48. Gutter lưới 16px, lề trang 24px (16px ≤480px).
- Breakpoint: 768 (bảng → hàng 2 dòng, bottom nav ≤5 mục), 1024 (sidebar 240px hiện), 1440 (container tối đa 1360).
- Mỗi màn hình một câu hỏi; khối trả lời câu hỏi đó ở trên cùng; khoảng trên tiêu đề ≥2× dưới.

## Elevation & Depth

| Mức | Cách thể hiện | Dùng cho |
|---|---|---|
| L0 | Phẳng, viền `{colors.outline}` 1px | Card, bảng, panel |
| L1 | `0 1px 3px rgba(0,0,0,.06)` | Dropdown, popover |
| L2 | `0 8px 24px rgba(0,0,0,.08)` | Sheet, drawer |
| L3 | `0 16px 48px rgba(0,0,0,.12)` | Modal |

Luật phẳng-mặc-định: bóng chỉ xuất hiện như phản ứng với trạng thái "nổi", không bao giờ ở trạng thái nghỉ.

## Shapes

Hệ bo chặt: input 4, nút 6, card 8, modal 12, chip 9999. Không trộn hệ chặt với hệ mềm (16–24) trong một màn hình.

## Components

- **Buttons**: primary (đầy màu, 1 cái/khung nhìn), secondary (viền), ghost (chỉ chữ), destructive (đỏ, tách riêng, cuối). Cao 40px (32px trong thanh lọc). Nhãn = động từ + đối tượng, không xuống dòng. Đủ hover/focus/active/disabled/loading.
- **Inputs**: 40px, viền `{colors.outline-control}` cố định, focus bằng outline 2px primary, nhãn trên field, lỗi dưới field.
- **Cards**: nền surface, viền 1px, bo 8, padding 16; không lồng card.
- **Navigation**: top bar 56px; sidebar 240px cùng nền, hàng 32px, mục active = pill xám; ≤5 mục cấp 1; mobile bottom nav ≤5.
- **Table**: hàng 40px, header 12px xám, kẻ `{colors.outline-row}`, số căn phải tnum.
- **Chip trạng thái**: 20px, nền container + chữ đậm cùng sắc, kèm chữ.
- **Signature**: thẻ "Tình trạng thang" — mã thang, trạng thái, lần bảo trì tới — một chip, một dòng, dùng giống nhau ở mọi app.

## Do's and Don'ts

Do: token hoá mọi màu; skeleton đúng kích thước khi tải; empty state có một câu + một hành động; Hoàn tác thay vì hỏi lại; giữ dữ liệu người dùng khi lỗi; test tên dài có dấu.
Don't: gradient/glow/glass; card lồng card; sọc viền màu bên; emoji icon; số bịa; animation vào trang; sidebar tối; màu accent làm màu thành công.

## Motion

```yaml
motion:
  press: 120ms
  state: 150ms
  overlay: 250ms
  easing-out: cubic-bezier(0.23, 1, 0.32, 1)
  easing-in-out: cubic-bezier(0.77, 0, 0.175, 1)
  max: 300ms
  reduced-motion: giữ opacity/màu, bỏ translate/scale
```
Chuyển động chỉ để báo trạng thái; không có gì dài hơn 300ms; không animate dữ liệu đang đọc.
