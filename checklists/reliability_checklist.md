# Reliability Checklist — FIT4110 Lab 03

Team: team-core (A6 — Core Business)
Ngay: 24/05/2026

## 1. Functional tests

- [x] Co test cho endpoint health — TC01 GET /health tra 200 status=ok
- [x] Co test happy path cho endpoint chinh — TC02 POST /events, TC03 POST /alerts
- [x] Co kiem tra status code 2xx — TC02 201, TC03 201, TC04 200, TC05 200, TC06 200, TC07 200
- [x] Co kiem tra field quan trong trong response — eventId, acceptedAt, id, status, locationId
- [x] Co it nhat 1 test doc du lieu danh sach hoac chi tiet — TC04 GET /alerts, TC05 GET /alerts/recent, TC06 GET /alerts/{id}

## 2. Auth tests

- [x] Co test thieu token — TC09 missing token tra 401/403 (skip tren mock, chay tren local)
- [x] Co test sai token hoac token rong — TC10 invalid token (skip tren mock)
- [x] Endpoint public duoc khai bao ro neu khong can auth — GET /health co security: []
- [x] Test the hien dung expected status 401/403 — TC09, TC10 expect [401,403]

## 3. Negative tests

- [x] Co test thieu field bat buoc — TC11 POST /alerts thieu sourceService va message
- [x] Co test sai kieu du lieu — TC13 POST /events sai eventType discriminator
- [x] Co test sai enum hoac gia tri ngoai mien — TC12 alertType=INVALID_TYPE
- [x] Loi tra ve theo cung mot error model — ProblemDetails voi title+status+detail

## 4. Boundary tests

- [x] Co test min/max hoac du lieu sat nguong — TC16 limit=100 (max), TC17 limit=101 (over max)
- [x] Co test limit/pagination neu endpoint co danh sach — TC16, TC17 GET /alerts
- [x] Co test payload lon hoac metadata thieu — TC15 THRESHOLD_EXCEEDED event day du field
- [x] Co ghi chu ky vong xu ly du lieu bien — limit>100 tra 422, THRESHOLD_EXCEEDED tra 201

## 5. Reliability tests co ban

- [x] Co kiem tra response time — TC22, TC23 (skip tren mock, chay tren local)
- [x] Co mo ta timeout mong muon — SLA 500ms p95 ghi trong openapi info description
- [x] Co test hoac ghi chu retry/idempotency neu phu hop — POST /events co eventId lam idempotency key
- [x] Co consumer-side smoke test voi it nhat 1 mock cua nhom khac — TC19 IoT mock, TC20+TC21 AI Vision mock

## 6. Evidence

- [x] Collection export JSON — postman/collections/team-core.postman_collection.json
- [x] Environment mock export JSON — postman/environments/team-core_mock.postman_environment.json
- [x] Environment local export JSON — postman/environments/team-core_local.postman_environment.json
- [x] Newman report XML — reports/newman-report-mock.xml
- [x] Newman report HTML — reports/newman-report.html
- [x] Contract lint report — reports/contract-lint-report.txt (No errors found)
- [x] Test-case matrix da dien — templates/test-case-matrix.csv (23 test cases)
- [x] Bien ban handshake da dien — templates/consumer-provider-handshake.md
