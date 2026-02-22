# PROJECT

## 1) 프로젝트 개요
- 프로젝트명: `ml-study` (Obsidian Digital Garden 기반 개인 지식 사이트)
- 목적: Obsidian Vault 노트를 GitHub로 퍼블리시하고 Eleventy(11ty)로 정적 사이트를 빌드해 Vercel/Netlify에 배포
- 핵심 경로:
  - 노트 소스(배포 대상): `src/site/notes`
  - Eleventy 설정: `.eleventy.js`
  - 노트 공통 데이터 계산: `src/site/notes/notes.11tydata.js`
  - 배포 설정: `vercel.json`, `netlify.toml`

## 2) 실행/빌드
- 요구 Node 버전: `22.x` (`package.json`의 `engines.node`)
- 주요 스크립트:
  - 로컬 개발: `npm run start`
  - 프로덕션 빌드: `npm run build`
  - Eleventy만 빌드: `npm run build:eleventy`

## 3) 퍼블리시/배포 흐름
1. Obsidian Digital Garden 플러그인으로 Vault 노트를 GitHub에 커밋 (`Published multiple files`)
2. 커밋된 노트가 `src/site/notes/**/*.md`에 반영됨
3. Vercel이 `npm run build` 실행
4. Eleventy가 frontmatter의 `permalink`를 기준으로 출력 경로 생성

## 4) 최근 장애 기록 (중요)
- 장애 시점: 2026-02-23 (KST)
- 증상: Vercel 빌드 실패
  - 에러: `DuplicatePermalinkOutputError`
  - 원인: 여러 노트가 동일 `permalink`를 가져 같은 출력 경로로 충돌
- 관련 커밋:
  - `a972c99` (2026-02-23 00:23:56 +0900) `Published multiple files`
  - `d460f55` (2026-02-23 00:42:11 +0900) `Published multiple files`
  - `3c38dde` (2026-02-23 00:48:37 +0900) `Published multiple files`

## 5) 근본 원인 분석
- Obsidian Vault 플러그인 설정의 `slugifyEnabled: true` 때문에,
  - 한글/비ASCII 경로가 slugify 과정에서 비거나 손실되어
  - `///`, `//.../`, `/ml//.../` 같은 permalink가 생성됨
- 그 결과 서로 다른 노트가 동일 permalink로 수렴해 Eleventy 빌드가 실패함
- 실제 원인 설정 파일:
  - `C:\Users\shj\Documents\Obsidian Vault\.obsidian\plugins\digitalgarden\data.json`

## 6) 확정 해결책
- 필수 설정:
  - `slugifyEnabled`를 `false`로 고정
- 적용 이유:
  - 퍼블리시 시 경로 slugify 손실을 막아 permalink 중복 재발 방지
- 추가 운영 원칙:
  - `src/site/notes`의 `permalink`를 수동 수정하더라도, 다음 Obsidian 퍼블리시에서 다시 덮일 수 있으므로
  - 반드시 Vault 플러그인 설정을 먼저 고정할 것

## 7) 재발 방지 체크리스트
- 퍼블리시 전:
  - Vault 설정에서 `slugifyEnabled=false` 확인
- 퍼블리시 후:
  - `src/site/notes` 내 permalink 중복 검사
  - 특히 `///`, `/...//.../` 패턴 여부 확인
- 배포 전:
  - `npm run build:eleventy` 로컬 선검증 (가능한 환경에서)

## 8) 알려진 주의사항
- 로컬 Node 버전이 22 미만이면 스크립트/의존성 이슈가 발생할 수 있음
- Obsidian 플러그인 설정 파일에 토큰이 평문 저장될 수 있으므로 보안 관리 필요
