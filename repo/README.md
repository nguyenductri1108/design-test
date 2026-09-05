# Sol — Design System & Prototype

App học nhạc / luyện tai. Dark-only, mobile-first, tiếng Việt (thuật ngữ Anh trong ngoặc).

```
tokens/
  sol-tokens.css          biến CSS --sol-* + primitive (.sol-btn, .sol-card)
  sol-tokens.json         cùng giá trị dạng dữ liệu (Tailwind / RN / Style Dictionary)
docs/
  DESIGN-SYSTEM.md        8 luật không được phá — đọc trước khi code
  design-system.html      spec sống: 5 nhóm màu, 11 bậc chữ, 14 component bấm được
prototype/
  index.html              app chạy thật — 18 màn, 10 dạng câu hỏi, tiếng đàn WebAudio
  ios-frame.jsx           khung iPhone — chỉ để trình bày, không mang vào code
```

Mở `docs/design-system.html` và `prototype/index.html` trực tiếp bằng trình duyệt, không cần build.

## 18 màn trong prototype

Onboarding (mục tiêu · thời lượng) · Home lộ trình · Chi tiết bài học ·
Bài học · Kết quả · Ôn lại câu sai (+ màn rỗng) · Thư viện bài hát ·
Hợp âm · Đàn tự do · Hồ sơ · Thành tích · Cài đặt · Nhắc nhở hàng ngày ·
4 trạng thái rọng: đang tải, mất mạng, chặn âm thanh, ôn rỗng.

## 10 dạng câu hỏi

Nghe ra nốt (bấm phím) · nhận quãng · đọc nốt trên khuông · điền nốt lên khuông ·
trưởng vs thứ · đoán hợp âm tiếp theo · xếp vòng 4 hợp âm · ghép tên với thế bấm ·
vỗ nhịp · hát lại (mic + đo cent).

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

## Âm thanh là một phần của hệ

Một giọng đàn duy nhất: `triangle` + `sine ×2 (0.32)` + `sine ×3 (0.12)` qua lowpass 2600Hz;
envelope attack 12ms → 0.24 → 0.09 → tắt dần. Nốt đơn 1.0s · hợp âm 1.4s · quãng gap 0.55s ·
vòng hợp âm gap 0.85s. Đúng = `[72,76,79]`, sai = `[61,60]`.
Thông số đầy đủ: `tokens/sol-tokens.json` → `audio`.

## Đổi token

Sửa **cả** `.css` và `.json` cho khớp, rồi tăng `$meta.version` trong JSON.
