# Bộ skill thiết kế giao diện Giang Anh — cách cài & dùng

Tổng hợp từ 12 repo trong bài "12 GitHub repo giúp Claude Code và Codex tạo giao diện đẹp hơn" (Việt Nguyễn AI, 27/10/2026).

## Có gì trong thư mục này

| File | Dùng cho |
|---|---|
| `gae-app-ui/SKILL.md` | App nội bộ: dashboard, tool Lark, app vận hành, web mobile KTV/lái xe. **Skill chính.** |
| `gae-marketing-page/SKILL.md` | Website, landing, trang đại lý, trang sản phẩm. |
| `DESIGN.md` | Hệ thống thiết kế mẫu cho app GAE (chuẩn Google design.md). Copy vào gốc mỗi dự án, đổi màu primary theo nhận diện. |

## Cài vào Claude Code / Codex

```bash
# Claude Code (dùng chung mọi dự án)
mkdir -p ~/.claude/skills
cp -r gae-app-ui gae-marketing-page ~/.claude/skills/
# hoặc chỉ cho một dự án
cp -r gae-app-ui gae-marketing-page <du-an>/.claude/skills/

# Codex: cùng cấu trúc, thư mục ~/.codex/skills/ (hoặc <du-an>/.codex/skills/)
# Mỗi dự án: copy DESIGN.md vào gốc, sửa màu, rồi
npx @google/design.md lint DESIGN.md
```

Trong claude.ai: hai skill đã được đề xuất qua thẻ "Lưu skill" trong cuộc trò chuyện.

## Nên cài trực tiếp repo nào? (trả lời câu "cài hết hay cài một cái")

Không cài hết — chúng chồng chéo và một số đẩy về kiểu "AI slop". Hai skill ở trên đã gói phần đáng dùng. Nếu muốn có thêm công cụ chạy tự động (lint/kiểm tra bằng trình duyệt):

| Repo | Có nên cài | Lý do |
|---|---|---|
| **pbakaus/impeccable** | Nên (1 cái duy nhất nếu chỉ chọn 1) | 24 lệnh (`/impeccable audit`, `critique`, `polish`, `harden`, `document`) + bộ dò 60+ dấu hiệu AI slop chạy sau mỗi lần sửa UI. `npx impeccable install --providers=claude,codex` |
| google-labs-code/design.md | Nên (chỉ CLI lint) | `npx @google/design.md lint DESIGN.md` bắt contrast, token mồ côi. |
| Leonxlnx/taste-skill | Có thể | Chương "app screens" rất tốt (đã gói vào gae-app-ui); script `inspect.mjs` chụp 1440/768/390 cần Node 22 + Chrome. |
| nutlope/hallmark | Chỉ cho website | 50 theme + sloplint cho trang landing; không dùng cho app. |
| emilkowalski/skills | Có thể | `animate` / `review-animations` / `break-ui` — đã gói quy tắc; cài nếu muốn lệnh riêng. `npx skills@latest add emilkowalski/skills` |
| greensock/gsap-skills | Chỉ khi dự án dùng GSAP | Tài liệu chính chủ, thiên vị GSAP. |
| nextlevelbuilder/ui-ux-pro-max-skill | **Không** | Phần quy tắc UX ổn (đã gói), nhưng dữ liệu style/palette đẩy về gradient, bóng màu, glass, indigo — đúng như bình luận trong bài. |
| VoltAgent/awesome-design-md | Tham khảo | Xem DESIGN.md của Supabase/Wise để học cách viết, không copy phong cách. |
| nexu-io/open-design | Không cần | App desktop riêng; các skill bên trong phần lớn là bản sao của emil/gsap. |
| DavidHDev/react-bits | Cài từng component khi cần | `npx shadcn@latest add @react-bits/<Name>-TS-TW`; danh sách component hợp app ở mục 10 của gae-app-ui. |
| DavidHDev/canvas-ui, oso95/scroll-world | Chỉ cho landing | Hiệu ứng WebGL / video 3D cuộn; tốn GPU và credit trả phí. |

## Quy ước ngắn nhất (nếu chỉ nhớ 5 điều)

1. Mỗi màn hình một câu hỏi; việc hay làm nhất cách 1 click.
2. Một màu nhấn ≤10%, màu đặt lên dữ liệu không lên khung; không gradient/glow/glass.
3. Bảng trước card; KPI là chữ, số tabular, tên tiếng Việt dài có dấu không bị cắt.
4. Mọi control đủ trạng thái; mọi vùng dữ liệu đủ loading/empty/error/success.
5. Chuyển động chỉ để báo trạng thái, <300ms, transform/opacity; dữ liệu không nhúc nhích vì đẹp.
