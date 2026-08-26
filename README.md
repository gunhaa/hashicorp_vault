# HashiCorp Vault 학습 저장소

HashiCorp Vault(시크릿 관리 / 암호화 도구)를 공식문서 기준으로 학습하며 정리하는 저장소입니다.

## 구조

```
notes/    # 학습 노트 (번호 순서대로, 폴더 분리 없이 단일 파일)
qna/      # notes/와 번호·이름이 1:1 대칭되는 질문/답변 기록
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
| 02 | [인증방식](./notes/02_인증방식.md) | Auth Method 개념, Token/AppRole/Userpass/LDAP/Kubernetes/AWS, Token TTL·갱신 |
| 03 | [시크릿엔진](./notes/03_시크릿엔진.md) | Static/Dynamic Secrets, KV, Database, PKI, Transit |
| 04 | [정책](./notes/04_정책.md) | ACL Policy, Capabilities, Templated Policy, Sentinel |
| 05 | [운영](./notes/05_운영.md) | 설치, Seal/Unseal, HA, 백업/복구 |

> 일부 번호는 실제 프로젝트의 민감한 구현 정보를 포함한 비공개 학습 문서로 `.gitignore` 처리되어 있어 이 저장소에는 포함되지 않을 수 있습니다.
