# aircheck-admin

오늘공기 Admin Dashboard (Turborepo 모노레포)

## 프로젝트 구조

```
aircheck-admin/
├── apps/
│   └── admin/              # Next.js Admin 앱
├── packages/
│   ├── api-client/         # API 클라이언트
│   ├── ui/                 # 공통 UI 컴포넌트
│   ├── eslint-config/      # ESLint 설정
│   └── typescript-config/  # TypeScript 설정
├── package.json            # 워크스페이스 루트
└── turbo.json              # Turborepo 설정
```

## 프로젝트 생성

```bash
npx create-turbo@latest aircheck-admin --package-manager npm
```

## 의존성 설치

```bash
npm install
```

## 개발 서버 실행

```bash
npm run dev
```

Admin 앱: http://localhost:3000

## 기술 스택

| 패키지 | 기술 | 용도 |
|--------|------|------|
| `apps/admin` | Next.js 16, React 19 | Admin 웹앱 |
| `packages/api-client` | TypeScript | API 통신 |
| `packages/ui` | React | 공통 컴포넌트 |

## 모노레포 구조

### 왜 Turborepo?

| 장점 | 설명 |
|------|------|
| **모듈 분리** | 패키지 간 명시적 의존성 |
| **빌드 캐싱** | 변경된 패키지만 재빌드 |
| **일관성** | 공유 설정 (ESLint, TS) |

### 패키지 의존성

```
apps/admin
├── @repo/ui          # 공통 UI
├── @repo/api-client  # API 클라이언트
└── next, react

packages/api-client
└── (의존성 없음 - 순수 TypeScript)

packages/ui
└── react
```

## 스크립트

| 명령어 | 설명 |
|--------|------|
| `npm run dev` | 모든 앱 개발 서버 실행 |
| `npm run build` | 모든 앱/패키지 빌드 |
| `npm run lint` | 전체 린트 검사 |

## API 연동

### 환경 변수 설정

```bash
# apps/admin/.env.local
NEXT_PUBLIC_API_URL=https://api.todaygonggi.com
NEXT_PUBLIC_API_KEY=your-api-key
```

### 사용 예시

```typescript
import { createApiClient } from '@repo/api-client';

const api = createApiClient(process.env.NEXT_PUBLIC_API_KEY!);
const result = await api.get('/admin/stats');
```

## TODO

- [ ] 대시보드 페이지
- [ ] 캐시 관리 페이지
- [ ] 로그 조회 페이지
- [ ] 환경 변수 설정
