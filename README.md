# HashiCorp Vault 학습 저장소

HashiCorp Vault(시크릿 관리 / 암호화 도구)를 공식문서 기준으로 학습하며 정리하는 저장소입니다.

## 구조

```
notes/    # 학습 노트 (번호 순서대로, 폴더 분리 없이 단일 파일)
labs/     # 실습용 설정/스크립트 (있을 경우)
CLAUDE.md # 이 저장소에서 답변/문서 작성 시 따르는 규칙
```

## 작성 규칙

- 답변·문서는 항상 [HashiCorp Vault 공식문서](https://developer.hashicorp.com/vault)를 검색해 근거를 확인한 뒤 작성하고, 참고 링크를 남깁니다.
- 구조/흐름을 설명할 때는 Mermaid 다이어그램을 적극 사용합니다.
- 자세한 규칙은 [`CLAUDE.md`](./CLAUDE.md)를 참고하세요.

## 노트 목록

| 번호 | 문서 | 내용 |
|---|---|---|
| 00 | [용어](./notes/00_용어.md) | Seal/Unseal, Secrets Engine, Auth Method, Token, Policy, Lease 등 핵심 용어 |
| 01 | [아키텍쳐](./notes/01_아키텍쳐.md) | 내부 컴포넌트 구조, 요청 처리 흐름, Storage Backend, HA |
