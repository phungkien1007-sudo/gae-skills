---
name: gae-marketing-page
description: Thiết kế trang web giới thiệu, landing page, trang đại lý, trang sản phẩm thang máy Giang Anh (chế độ "Persuade") — trang để đọc/cuộn, không phải app để làm việc. Dùng khi xây hoặc sửa website, landing, hero, trang chiến dịch.
---

# Trang marketing Giang Anh — chế độ "Persuade"

Tổng hợp từ taste-skill, hallmark, impeccable, Emil/GSAP skills, React Bits, Canvas UI, Scroll World. Mục tiêu: trang **trông như được làm riêng** cho GAE, không thể đổi tên sang công ty khác mà vẫn đúng. Với app/dashboard → dùng skill `gae-app-ui`.

## 1. Quy trình (chạy đúng thứ tự)

1. **Kiểm kê 8–12 điều chỉ GAE có**: nhà máy ở đâu, công suất, loại thang, chứng nhận (vd. cửa EI), số năm, khách hàng/đại lý thật, ảnh xưởng thật, con số thật. Không có → hỏi, không bịa.
2. **Lập luận**: mỗi section **một khẳng định**; trang là chuỗi lập luận, không phải "hero → 3 tính năng → CTA → footer".
3. **Hướng thẩm mỹ**: chọn 1 trong 3 phương án viết ra (tham chiếu cụ thể, không tính từ: "bản vẽ kỹ thuật xanh Prussian", "nhà xưởng bê tông Formwork", "tạp chí công nghiệp Đức 1970"). Tham khảo theme hallmark hợp ngành: Blueprint, Formwork, Console, Wayfind, Almanac, Coral, Furrow. Tránh Inter/Roboto/Poppins/Open Sans làm chữ hiển thị; chữ hiển thị vẫn phải đủ dấu tiếng Việt.
4. **Câu ý tưởng** "X trở thành Y" + bài kiểm tra đối thủ (đổi logo đối thủ vào có vẫn đúng không? → làm lại) + **một yếu tố tương tác sống** (vd. chọn kích thước hố thang → xem mặt cắt).
5. **Copy deck** trước khi dựng: tiêu đề ≤2 dòng mọi bề rộng (~32 ký tự, ~5 từ), 1 h1 ở màn đầu, mỗi section có heading, ~80 từ/màn hình.
6. **Dựng với motion tắt** → qua cổng kiểm tra → xem ảnh chụp ở 1440/768/390, tối đa 3 vòng sửa → **thêm chuyển động sau cùng**.

## 2. Sàn bắt buộc (không miễn trừ)

- Mọi màu/font qua token; không #000/#fff ngoài token; không literal ngoài khối token.
- Hero vừa 1280×800: headline, lede, CTA và hình đều thấy; hero không dùng `vh` (dùng `dvh/svh`); ở 1920 container 1360–1520, gutter ≥120.
- `overflow-x: clip` trên html/body, không `100vw`; không cuộn ngang 320→1920; grid dùng `minmax(0,1fr)`; heading `overflow-wrap:break-word; min-width:0`.
- `:focus-visible` mọi nơi, hiện ngay; reduced-motion fallback; nội dung thấy được khi tắt JS; không 2 `sticky top:0`.
- Không eyebrow, không nhãn uppercase tracked ≤15px, không chuỗi "a · b · c", không mũi tên dính chữ link, không chấm trang trí, không in nghiêng một từ.
- Không gradient tím/xanh/pink, không cyan trên nền tối, không card lồng card, không emoji icon, không khung trình duyệt/điện thoại giả, không mock sản phẩm giả khi sản phẩm thật tồn tại (chụp cái thật).
- **Không số liệu, testimonial, logo bịa**; không "Gửi thành công" giả nếu không có request thật.
- Copy: không từ sáo ("liền mạch", "đột phá", "nâng tầm", "đẳng cấp", "giải pháp toàn diện"), không nút phụ "Tìm hiểu thêm"/"Bắt đầu", không mở đầu rỗng, hạn chế gạch dài, không lặp một ý ở ≥3 section ("Không X. Chỉ Y.").
- Nhãn nút & nav chính không bao giờ xuống dòng.

## 3. Chữ, màu, bố cục trang

- ≤2 typeface (thường 1). 2–3 cỡ thấy được, tối đa 5. Display: tracking −0.02…−0.05em, leading 0.85–1.05, tối đa 6rem; h2 ≥40px. Body 16–20px, leading 1.45–1.6, 45–75 ký tự/dòng, căn trái. ≤3 weight.
- **Một nền, một mực, một màu nhấn**; accent trên hành động + tối đa một thứ nữa; ≤5% khung nhìn (8% là lỗi). Chữ chạy dùng mực đậm, không xám. Tách bề mặt bằng bậc tông, không bằng kẻ. Không xám zero-chroma khi trang có sắc neo.
- Nút phẳng: vuông **hoặc** tròn hẳn; bo 9–16px là mặc định của trang yếu. Nav = wordmark + 3–5 link + 1 hành động.
- Lề ngoài bằng nhau; section cách 120–240px và **khác nhau**; không khoảng trống > nửa màn; khoảng trên heading ≥2× dưới; không section nào mỏng; không mọi section ngăn cách cùng một kiểu.
- Không bóng trên phần tử đứng yên; bóng chỉ cho thứ nổi. Không glow/aura/blob. Không ảnh tường (ảnh ≤1/3 trang), không SVG minh hoạ vẽ tay, không ô ảnh gradient rỗng, không 24+ dấu tích đếm.
- Ảnh: xưởng, máy, người thật của GAE; có `alt`, có credit; LCP không lazy-load; video autoplay phải muted + poster.
- Tooltip 800–1000ms; auto-rotate dừng khi hover/focus + nút dừng; không toast cho việc đã thấy; không bounce.

## 4. Chuyển động cho trang marketing

Trang marketing **được phép** choreography — nhưng mỗi chuyển động vẫn phải có mục đích (giải thích, dẫn mắt, phản hồi). Tiêu chuẩn tối thiểu khi bật motion: ~8 phần tử chuyển động có chủ đích, không "fade-in mọi section" giống nhau.

- Reveal khi cuộn: `clip-path: inset(0 0 100% 0) → inset(0)`, ~600ms, **bắn một lần** (`useInView({once:true, margin:"-100px"})` hoặc `ScrollTrigger.batch`). Stagger 30–80ms. Vào từ `scale(.95)`+opacity, không `scale(0)`.
- Easing token: `--ease-out: cubic-bezier(0.23,1,0.32,1)`, `--ease-in-out: cubic-bezier(0.77,0,0.175,1)`; ease-in chỉ cho "thoát có lý do" trong phim, không trên UI. Spring (Motion `{type:"spring", duration:.5, bounce:.2}`) cho thứ kéo/theo chuột (`useSpring`, không gắn thẳng vào pointer).
- Thời lượng kiểu phim (chỉ cho hero/showreel): nhấn 120–220ms, phần tử tới 350–650ms, biến hình 600–1200ms, camera/reveal lớn 900–1800ms. UI điều khiển trên trang vẫn <300ms.
- GSAP khi cần timeline/scroll/pin: đơn vị **giây**, default `power2.out`; `gsap.defaults`; timeline + position (`"<"`, `">"`, `"+=0.2"`, label) thay delay; `autoAlpha` thay opacity; `stagger:{each:.1, from:"center"}`; `overwrite:"auto"`; ScrollTrigger gắn vào timeline/tween cấp cao (không tween con), không dùng `scrub` cùng `toggleActions`, `pin` animate con chứ không animate phần tử pin, `ScrollTrigger.refresh()` sau khi ảnh/font tải, cuộn ngang giả `ease:"none"`, `markers` chỉ dev. React: `useGSAP(() => {...}, {scope, dependencies, revertOnUpdate:true})`, handler bọc `contextSafe`, `gsap.matchMedia()` cho reduced-motion & breakpoint, register plugin một lần, client-only trong Next.
- `prefers-reduced-motion`: bỏ translate/scale/parallax, giữ opacity/màu; View Transitions API không tự tôn trọng → tự xử lý.
- Hiệu năng: transform/opacity; `will-change` chỉ khi thấy giật; `gsap.quickTo` cho theo chuột; kill animation ngoài màn; test Android tầm trung, CPU throttle 4×.

## 5. Thư viện & hiệu ứng (có điều kiện)

- **React Bits** (`npx shadcn@latest add @react-bits/<Name>-TS-TW`): text reveal (SplitText, BlurText, ShinyText, CountUp), AnimatedContent/FadeContent, LogoLoop (đại lý), TiltedCard/SpotlightCard, Stepper. Backgrounds WebGL (Aurora, Silk, Waves…) **chỉ** ở hero, có fallback tĩnh trên mobile/thiết bị yếu, tắt với reduced-motion, không chạy trên trang dài.
- **Canvas UI** (WebGL/WebGPU trên HTML sống): hiệu ứng wow cho hero/landing; HTML-in-canvas là thử nghiệm Chrome-only → mọi trình duyệt khác tự fallback; tốn GPU/pin; không dùng trong app. Có thể dùng "3D Object" cho mô hình cabin thang (GLB) hoặc "celebrate" cho khoảnh khắc đạt mục tiêu.
- **Scroll World** (landing 3D cuộn qua video AI): phù hợp "xưởng → dây chuyền → lắp đặt → thang hoàn thiện" (ngữ pháp camera công nghiệp: track ngang thấp dọc dây chuyền) nhưng **tốn credit video trả phí** (~$27/6 cảnh); luôn hỏi ngân sách trước; bản mobile 9:16 riêng (≈2× chi phí), không crop giữa; mẹo tái dùng: mã hoá `libx264 -crf 20 -g 8 +faststart`, nạp clip bằng Blob URL để seek không kẹt frame 0.
- Tối đa 2 thư viện chuyển động trên một trang. Lenis/smooth-scroll chỉ khi cả trang được thiết kế cho nó.

## 6. Cổng kiểm tra trước khi giao

Chụp 390 / 768 / 1440 (và 1920): hero đúng 1 màn ở 1440×900, không băng chết >160px; mỗi section 1 khẳng định rõ; đọc che logo → vẫn nhận ra GAE?; contrast 4.5/3:1; focus ring; không cuộn ngang; ảnh có alt/credit; `lang="vi"`, title, meta description; `text-wrap:balance` heading; không widow/orphan; không ô lẻ cuối grid; không >1 kiểu primary; không >3 weight; không heading nhảy cấp; không nội dung giấu trên điện thoại. Chấm 6 trục 1–5 (Triết lý, Phân cấp, Thực thi, Đặc trưng, Kiềm chế, Đa dạng) — <3 ở trục nào thì sửa trục đó rồi mới giao.
