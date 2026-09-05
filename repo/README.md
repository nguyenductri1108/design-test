# Sol — Design System & Prototype

App học nhạc / luyện tai. Dark-only, mobile-first, tiếng Việt.

```
tokens/
  sol-tokens.css          biến CSS --sol-* + primitive (.sol-btn, .sol-card)
  sol-tokens.json         cùng giá trị dạng dữ liệu (Tailwind / RN / Style Dictionary)
docs/
  DESIGN-SYSTEM.md        8 luật không được phá — đọc trước khi code
  design-system.html      spec sống, mở trực tiếp bằng trình duyệt
prototype/
  index.html              app chạy thật, 8 màn, có tiếng đàn (WebAudio)
  ios-frame.jsx           khung iPhone — chỉ để trình bày
```

## Dùng token

```html
<link rel="stylesheet" href="tokens/sol-tokens.css">
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@500;600;700;800&family=Be+Vietnam+Pro:wght@400;500;600;700&display=swap" rel="stylesheet">
```

```css
.card {
  background: var(--sol-surface);
  border-radius: var(--sol-radius-xl);
  padding: var(--sol-space-4);
  font: var(--sol-text-body);
  color: var(--sol-ink);
}
```

## Luật cốt lõi

1. Lime = hành động & tiến độ · Violet = đang diễn ra · Green = đúng · Red = sai. Không đổi vai.
2. Chỉ vật bấm được có mặt đáy đặc (`box-shadow: 0 Npx 0 <màu-press>`), nhấn thì `translateY(N-2px)`. Không bóng mờ.
3. Phím trắng luôn sáng hơn phím đen. Nhấn scale bằng cách *dim nốt ngoài scale*.
4. Sai là lúc dạy — mọi phản hồi sai kèm 1–2 câu giải thích. Không dùng modal.
5. Một nút lime mỗi màn.
6. Chạm ≥ 44px · tên nốt ≥ 11px · chữ body ≥ 12.5px.
7. Không thêm màu ngoài token. Cần sắc độ thì dùng `*-press` / `*-tint`.
8. Hai họ chữ: Baloo 2 (tiêu đề, số, nút) + Be Vietnam Pro (chữ đọc).

Chi tiết: `docs/DESIGN-SYSTEM.md`.

## Đổi token

Sửa **cả** `.css` và `.json` cho khớp, rồi tăng `$meta.version` trong JSON.
