# Consumer–Provider Handshake

## Thong tin chung

- Lab: FIT4110 Lab 03
- Ngay: 24/05/2026
- Provider team: team-core (A6 — Core Business)
- Consumer team: team-vision (A4 — AI Vision) va team-iot (A1 — IoT Ingestion)
- Provider service: Core Business API
- Consumer service: AI Vision API (consumer smoke), IoT Ingestion API (consumer smoke)

---

## Handshake 1 — Core Business (Provider) voi AI Vision (Consumer)

### Contract

- Contract file: contracts/core-business.openapi.yaml
- Mock base URL: http://localhost:4010
- Auth method: Bearer token (Authorization: Bearer {{authToken}})
- Endpoint duoc test: POST /events, POST /alerts, GET /alerts, GET /alerts/recent, GET /alerts/{alertId}, PATCH /alerts/{alertId}, GET /devices/{deviceId}

### Consumer smoke test — Core goi AI Vision mock

#### Request

```http
POST /detect
Authorization: Bearer lab-token
Content-Type: application/json
```

```json
{
  "camera_id": "CAM01",
  "image_url": "https://example.com/frame.jpg"
}
```

#### Expected response

```json
{
  "detections": [],
  "camera_id": "CAM01",
  "processed_at": "2026-05-24T08:00:01Z"
}
```

### Ket qua

- [x] Consumer goi mock thanh cong — TC21 POST /detect tra 200
- [x] Consumer parse duoc ket qua detection tu AI Vision
- [x] Consumer hieu loi 4xx/5xx provider tra ve — ProblemDetails shape
- [x] Co Newman report — reports/newman-report-mock.xml TC21 Pass

---

## Handshake 2 — Core Business (Consumer) voi IoT Ingestion (Provider)

### Contract

- Contract file: contracts/iot-ingestion.openapi.yaml (mau) / openapi.yaml Lab 02 (A1)
- Mock base URL: http://localhost:4012
- Auth method: Bearer token
- Endpoint duoc test: GET /health

### Consumer smoke test — Core goi IoT Ingestion mock

#### Request

```http
GET /health
```

#### Expected response

```json
{
  "status": "ok",
  "service": "iot-ingestion",
  "version": "0.3.0"
}
```

### Ket qua

- [x] Consumer goi mock thanh cong — TC19 GET /health tra 200
- [x] Consumer parse duoc field can dung — status=ok
- [x] Consumer hieu loi 4xx/5xx provider tra ve — ProblemDetails shape
- [x] Co Newman report — reports/newman-report-mock.xml TC19 Pass

---

## Ghi chu thay doi hop dong

| Noi dung | Truoc | Sau | Nguoi dong y |
|---|---|---|---|
| POST /events them oneOf discriminator | Khong co | SENSOR_READING / THRESHOLD_EXCEEDED | A6 + A1 |
| Alert schema flat thay vi allOf | allOf + additionalProperties | flat schema | A6 |
| union type null cho note field | oneOf nullable | type: [string, null] | A6 |

## Xac nhan

- Provider representative (A6 — Core Business): Nglo Quang Huy
- Consumer representative (A4 — AI Vision): Dai dien Nhom A4
- Consumer representative (A1 — IoT Ingestion): Dai dien Nhom A1
- Ngay: 24/05/2026
