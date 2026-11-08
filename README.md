# Xã, phường cũ → mới sau sáp nhập 2025 (Việt Nam) — dữ liệu mở, API, MCP

Bảng đối chiếu **xã/phường/thị trấn cũ (trước 01/7/2025) → xã/phường/đặc khu mới** sau sắp xếp đơn vị hành chính 2025,
**chép và đối chiếu từng khoản** các nghị quyết của Ủy ban Thường vụ Quốc hội (1654–1687/NQ-UBTVQH15) và Nghị quyết 202/2025/QH15 (34 tỉnh).

- Trang tra cứu: https://dorabot.io/dia-chi/sap-nhap/
- Công cụ đổi địa chỉ hàng loạt (dán Excel): https://dorabot.io/dia-chi/
- API + MCP: https://dorabot.io/dia-chi/nha-phat-trien/

## Dữ liệu

| File | Nội dung |
|---|---|
| `data/tat-ca.csv`, `data/tat-ca.json` | Đủ 34 tỉnh, thành phố (12.216 dòng) |
| `data/<tinh>.csv`, `data/<tinh>.json` | Từng tỉnh |

Mỗi dòng: xã cũ, quận/huyện cũ, tỉnh cũ → xã mới, tỉnh mới, phần (`toan_bo` / `mot_phan` / `phan_con_lai`), số nghị quyết, khoản, link trang.
Xã cũ bị chia cho nhiều xã mới có nhiều dòng. Bản mới nhất luôn ở https://dorabot.io/dia-chi/sap-nhap/du-lieu/v1/index.json.

Giấy phép **CC BY 4.0** — ghi nguồn: *Dorabot (dorabot.io/dia-chi/sap-nhap), chép từ nghị quyết của Ủy ban Thường vụ Quốc hội*.

## API

```bash
# Tra 1 xã cũ (miễn phí, không khoá)
curl "https://dorabot.io/dia-chi/sap-nhap/api/v1/tra-cuu?xa=Khâm%20Thiên&huyen=Đống%20Đa&tinh=Hà%20Nội"

# Đổi hàng loạt địa chỉ đầy đủ (không khoá 20/ngày; khoá miễn phí 100/ngày)
curl -X POST https://dorabot.io/dia-chi/api/v1/doi.php \
  -H "Authorization: Bearer dk_KHOA_CUA_BAN" -H "Content-Type: application/json" \
  -d '{"addresses":["Số 12 ngõ 5, phường Khâm Thiên, quận Đống Đa, Hà Nội"]}'
```

OpenAPI: https://dorabot.io/dia-chi/sap-nhap/du-lieu/v1/openapi.json

## MCP (Claude, ChatGPT, Cursor, Claude Code)

Máy chủ MCP từ xa: `https://dorabot.io/dia-chi/mcp` — công cụ `tra_cuu_xa_cu`, `doi_dia_chi`, `danh_sach_xa_moi`, `danh_sach_tinh`.

```bash
claude mcp add --transport http dorabot-dia-chi https://dorabot.io/dia-chi/mcp
```

## Báo sai

Mở issue kèm link trang và khoản nghị quyết, hoặc bấm "Báo sai trang này" trên trang tra cứu.
