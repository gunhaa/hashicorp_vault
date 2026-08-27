# Kong Gateway 3.10 → 3.14(LTS) 업그레이드 - Admin API 변경사항

> 이 문서는 HashiCorp Vault 학습 저장소(vault)와는 별개로, Kong Gateway 버전 업그레이드 검토를 위해
> 별도로 정리한 문서입니다. (`CLAUDE.md`의 Vault 관련 규칙과는 무관합니다.)

## 요약

- Kong Gateway **3.10.0.0**은 LTS 릴리스(2025-03-27 출시), **3.14.0.0**은 그다음 LTS 릴리스(2026-04-07 출시)로,
  3.10 → 3.14가 공식적으로 권장되는 LTS 업그레이드 경로다.
- 이 구간에서 **"Admin API" 카테고리로 명시된 breaking change는 3.13.0.0의 empty-value JSON 인코딩 수정 1건뿐**이다.
- 그 외에는 특정 플러그인(OpenID Connect, OpenTelemetry, AI 계열, Kafka Consume 등)의 설정 필드
  rename/타입 변경이 Admin API 요청 바디에 영향을 준다. deck이나 자동화 스크립트로 Admin API를 직접
  다루고 있다면 아래 필드명 변경 항목들을 먼저 점검할 것.
- Kong Gateway 3.10 이후 버전은 OSS `Kong/kong` GitHub 저장소에 태그되지 않는다(공개 저장소는 3.9.3에서 멈춤 —
  Enterprise 전용 릴리스로 전환). 따라서 GitHub CHANGELOG.md는 이 구간의 근거로 쓸 수 없고,
  공식 docs 사이트(breaking-changes 문서)가 유일하게 신뢰 가능한 소스였다.
- 공식 changelog 페이지(`/gateway/changelog/`)는 현재 3.14.0.5 이전 버전(3.10~3.13)을 이미 제거한 상태라,
  breaking-changes 문서(`/gateway/breaking-changes/`)의 버전별 섹션을 원본 HTML까지 직접 대조해 검증했다.

## 명시적으로 "Admin API" 카테고리로 분류된 항목

| 버전 | 항목 | 내용 |
|---|---|---|
| **3.13.0.0** | Admin API: empty value encoding | 빈 객체(`{}`) 기본값을 가진 record/map 필드가 이제 올바르게 JSON 객체로 인코딩된다. 이전에는 배열로 잘못 인코딩되었다. |

3.10.0.0 / 3.11.0.0 / 3.12.0.0 / 3.14.0.0 섹션에는 "Admin API"라는 이름의 항목이 별도로 존재하지 않는다.

## Admin API 요청/응답 스키마에 영향을 주는 관련 변경 (플러그인·엔티티 단위로 분류됨)

| 버전 | 항목 | 내용 |
|---|---|---|
| 3.14.0.0 | OpenID Connect: consumer claims 데이터 타입 | `config.consumer_claim` → `config.consumer_claims`로 이름 변경, 문자열 배열 → 배열의 배열로 타입 변경 |
| 3.14.0.0 | OpenID Connect: header claims 필드 | `config.upstream_headers_claims`/`upstream_headers_names` → `config.upstream_headers`, `config.downstream_headers_claims`/`downstream_headers_names` → `config.downstream_headers`로 통합 |
| 3.14.0.0 | TLS certificate verify by default | `tls_certificate_verify` 기본값이 `on`으로 변경. Traditional 모드에서 `tls_verify = false`로 Service/plugin config를 업데이트하면 **Admin API가 오류를 반환**함 |
| 3.14.0.0 | OpenTelemetry: access logs endpoint 파라미터 | `config.access_logs_endpoint` → `config.access_logs.endpoint` |
| 3.12.0.0 | Kafka Consume 플러그인: Service 스코핑 제거 | Kafka Consume 플러그인을 Service에 더 이상 붙일 수 없음(붙여도 동작하지 않음) |
| 3.11.0.0 | AI Proxy 계열: `preserve` route type deprecated | `config.route_type = preserve`가 deprecated, 3.11.0.0 이후 도입된 타입으로 전환 권장 |
| 3.10.0.0 | AI Rate Limiting Advanced 플러그인 | `config.llm_providers.window_size`, `config.llm_providers.limit`이 단일 숫자 대신 숫자 배열을 요구하도록 변경 |

## 조사 중 발견한 오귀속 정정 (참고용)

원본 페이지를 자동 요약 도구로 여러 번 읽었을 때, 다음 항목들이 잘못된 버전에 귀속되는 경우가 있었다.
실제 HTML의 `<h2>/<h3>/<h4>` 헤더 구조를 직접 대조해 아래와 같이 정정했다.

- "Consumer Groups(`/consumer_groups`)·Consumers(`/consumers`) 리스트 API가 페이지네이션되고 JSON 키가
  `data`로 변경"된 것은 3.14가 아니라 **3.6.0.0**의 변경사항이다 (`/gateway/breaking-changes/#admin-api`,
  3.6.0.0 섹션 내 `#admin-api` 앵커).
- `/vitals/reports` Admin API 엔드포인트 제거는 **3.0.0.0**의 변경사항이다
  (`/gateway/breaking-changes/#admin-api`, 3.0.0.0 섹션 내 `#admin-api` 앵커).

## 참고 링크

- [Kong Gateway breaking changes, deprecations, and known issues](https://developer.konghq.com/gateway/breaking-changes/)
  — 버전별 섹션 앵커: `#3-10-0-0`, `#3-11-0-0`, `#3-12-0-0`, `#admin-api-empty-value-encoding`(3.13.0.0), `#3-14-0-0`
- [Kong Gateway 3.10 to 3.14 LTS upgrade 가이드](https://developer.konghq.com/gateway/upgrade/lts-upgrade-310-314/)
  — 이 정확한 업그레이드 경로를 다루는 공식 문서
- [Kong Gateway changelog](https://developer.konghq.com/gateway/changelog/)
  — 3.14.0.5 이전 버전(3.10~3.13)은 이미 제거되어 있어, 최신 패치(3.14.0.x 이후) 확인용으로만 참고
