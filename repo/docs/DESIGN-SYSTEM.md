# Sol Design System — v1.0

Design system cho app học nhạc / luyện tai **Sol**. Dark-only, mobile-first, tiếng Việt.

## Cấu trúc

```
sol/
├── README.md                      mục lục — đọc file này trước
├── design-system/
│   ├── Sol Design System.dc.html  spec sống (mở bằng trình duyệt)
│   ├── DESIGN-SYSTEM.md           bản rút gọn — file này
│   └── tokens/
│       ├── sol-tokens.css         biến CSS + primitive
│       └── sol-tokens.json        token dạng dữ liệu
└── screens/
    ├── Sol - App hoc nhac.dc.html prototype 7 màn, chạy thật
    └── ios-frame.jsx              khung iPhone (chỉ để trình bày)
```

## File trong project

| File | Vai trò |
|---|---|
| `design-system/Sol Design System.dc.html` | Spec sống: màu, chữ, spacing, radius, elevation, 14 component (bản thật, bấm được), luật âm thanh, giọng văn, code mẫu |
| `design-system/tokens/sol-tokens.css` | Biến CSS `--sol-*` + primitive `.sol-btn` / `.sol-card` / `.sol-eyebrow` + keyframes |
| `design-system/tokens/sol-tokens.json` | Cùng giá trị dạng dữ liệu — Tailwind / React Native / Style Dictionary |
| `screens/Sol - App hoc nhac.dc.html` | Prototype tham chiếu: onboarding → lộ trình → bài học → kết quả + tab hợp âm, đàn |
| `screens/ios-frame.jsx` | Khung iPhone để trình bày prototype. Không thuộc design system |

## Dùng trong code thật

```html
<link rel="stylesheet" href="design-system/tokens/sol-tokens.css">
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

Tailwind: `require('./design-system/tokens/sol-tokens.json')` rồi map vào `theme.extend` (ví dụ đầy đủ trong spec, mục 04).

## Luật không được phá

1. **Lime = hành động & tiến độ. Violet = đang diễn ra. Green = đúng. Red = sai.** Không đổi vai.
2. **Chỉ vật bấm được có mặt đáy đặc** (`box-shadow: 0 Npx 0 <màu-press>`), nhấn thì `translateY(N-2px)`. Không dùng bóng mờ ở bất cứ đâu.
3. **Phím trắng luôn sáng hơn phím đen**, ở mọi trạng thái. Nhấn scale bằng cách *dim nốt ngoài scale*, không tô đậm nốt trong scale.
4. **Sai là lúc dạy**: mọi phản hồi sai đều kèm 1–2 câu giải thích lý thuyết ở `FeedbackFooter`, không dùng modal.
5. **Một nút lime mỗi màn.** Hành động phụ dùng ghost hoặc chip.
6. Chạm tối thiểu 44px; tên nốt trên phím ≥ 11px; chữ body ≥ 12.5px.
7. Không thêm màu ngoài bảng token. Cần sắc độ thì lấy `*-press` / `*-tint`.
8. Hai họ chữ: Baloo 2 (tiêu đề, số, nút) + Be Vietnam Pro (chữ đọc). Không thêm font thứ ba.

## Âm thanh là một phần của hệ

Một giọng đàn duy nhất: `triangle` + `sine ×2 (0.32)` + `sine ×3 (0.12)` qua lowpass 2600Hz; envelope attack 12ms → 0.24 → 0.09 → tắt dần. Nốt đơn 1.0s, hợp âm 1.4s, quãng gap 0.55s, vòng hợp âm gap 0.85s. Đúng = `[72,76,79]`, sai = `[61,60]`. Chi tiết trong `sol-tokens.json` → `audio`.

## Đổi version

Sửa token thì sửa **cả** `sol-tokens.css` và `sol-tokens.json` (hai file phải khớp), rồi tăng `$meta.version`.
