# 디자인 토큰 리팩토링 완료 ✅

## 📦 생성된 파일 목록

```
/Users/pobae/Downloads/tokens-refactored/
├── primitive.json           ⭐ 기본 토큰 (색상, 간격, 타이포그래피 등)
├── semantic-light.json      ⭐ 라이트 모드 의미론적 토큰
├── semantic-dark.json       ⭐ 다크 모드 의미론적 토큰
├── tokens-unified.json      ⭐ 통합 토큰 파일 (모든 토큰 포함)
├── README.md               📄 프로젝트 개요 및 사용법
├── MIGRATION_GUIDE.md      📄 마이그레이션 가이드
├── COMPARISON.md           📄 기존 vs 신규 비교
└── INDEX.md                📄 이 문서 (시작점)
```

## 🚀 빠른 시작

### 1. 파일 이해하기

#### 📌 핵심 토큰 파일 (4개)

1. **primitive.json** (기본 토큰)
   - 원시 디자인 값 정의
   - 색상 팔레트, 간격, 폰트 크기 등
   - 직접 사용보다는 Semantic에서 참조

2. **semantic-light.json** (라이트 모드)
   - 의미론적 역할 정의
   - Light 모드 색상 스키마
   - UI 컴포넌트에서 직접 사용

3. **semantic-dark.json** (다크 모드)
   - Dark 모드 색상 스키마
   - Light와 동일한 키 구조
   - 테마 전환 시 사용

4. **tokens-unified.json** (통합)
   - 모든 토큰을 하나의 파일에
   - Figma Tokens Plugin, Style Dictionary 호환
   - 테마 메타데이터 포함

#### 📚 문서 파일 (4개)

1. **README.md** - 시작은 여기서!
   - 프로젝트 개요
   - 주요 개선사항
   - 사용 방법

2. **MIGRATION_GUIDE.md** - 기존 코드 업데이트
   - 토큰 매핑 테이블
   - 자동 변환 스크립트
   - 단계별 마이그레이션

3. **COMPARISON.md** - 변경사항 비교
   - Before/After 비교
   - 구조 변경 예시
   - 이점 정리

4. **INDEX.md** - 이 문서
   - 파일 목록
   - 빠른 시작 가이드

### 2. 어떤 파일을 사용해야 하나요?

#### 시나리오별 추천

| 상황 | 추천 파일 | 이유 |
|------|----------|------|
| 새 프로젝트 시작 | `tokens-unified.json` | 모든 토큰 포함, 테마 지원 |
| 기존 프로젝트 마이그레이션 | 개별 파일 (primitive + semantic) | 점진적 전환 가능 |
| Figma Tokens 연동 | `tokens-unified.json` | Plugin 호환 |
| Style Dictionary | 개별 파일 | 빌드 타겟별 분리 |
| Light Mode만 | `primitive.json` + `semantic-light.json` | 필요한 것만 |
| Dark Mode 지원 | 모든 파일 | 완전한 테마 지원 |

### 3. 코드에서 사용하기

#### A. 통합 파일 사용 (간단)

```javascript
import tokens from './tokens-unified.json';

// Semantic 토큰 사용 (권장)
const primaryColor = tokens.semantic.color.action.primary.value;
const spacing = tokens.semantic.spacing.component.md.value;

// 테마 전환
const currentTheme = isDark ? 'dark' : 'light';
```

#### B. 개별 파일 사용 (유연)

```javascript
import primitive from './primitive.json';
import semanticLight from './semantic-light.json';
import semanticDark from './semantic-dark.json';

// 테마에 따라 선택
const semantic = isDark ? semanticDark : semanticLight;

const primaryColor = semantic.semantic.color.action.primary.value;
```

#### C. CSS Variables로 변환

```javascript
// tokens-to-css.js
import tokens from './tokens-unified.json';

function generateCSSVariables(tokens, prefix = '') {
  let css = ':root {\n';
  
  function traverse(obj, path = '') {
    for (const [key, value] of Object.entries(obj)) {
      if (value.value !== undefined) {
        const varName = `--${prefix}${path}${key}`.replace(/\./g, '-');
        css += `  ${varName}: ${value.value};\n`;
      } else if (typeof value === 'object') {
        traverse(value, `${path}${key}-`);
      }
    }
  }
  
  traverse(tokens);
  css += '}\n';
  return css;
}

const cssVars = generateCSSVariables(tokens.semantic, 'semantic-');
console.log(cssVars);
```

### 4. 주요 개선사항 요약

#### ✅ 구조 개선
- **Before**: 평면적 구조, 하이픈 구분
- **After**: 계층적 구조, 점(.) 구분

#### ✅ 단위 명시
- **Before**: `"value": "16"` (단위 없음)
- **After**: `"value": "16px"` (단위 포함)

#### ✅ Dark Mode
- **Before**: 미지원
- **After**: 완전 지원 (semantic-dark.json)

#### ✅ 명명 규칙
- **Before**: `font-size-12`, `space-4`, `color-base-blue-600`
- **After**: `fontSize.base`, `spacing.4`, `color.blue.600`

#### ✅ 참조 체계
- **Before**: `{color-primary}`
- **After**: `{semantic.color.action.primary}`

## 📖 다음 단계

### 새 사용자

1. ✅ `README.md` 읽기
2. ✅ `tokens-unified.json` 프로젝트에 추가
3. ✅ 코드에서 토큰 사용 시작

### 기존 사용자 (마이그레이션)

1. ✅ `COMPARISON.md`로 변경사항 확인
2. ✅ `MIGRATION_GUIDE.md`로 마이그레이션 계획
3. ✅ 단계별 코드 업데이트
4. ✅ 테스트 및 검증

## 🎯 핵심 원칙

### 1. Semantic 토큰 우선 사용
```javascript
// ❌ Primitive 직접 사용
color: tokens.primitive.color.blue['600'];

// ✅ Semantic 사용
color: tokens.semantic.color.action.primary;
```

### 2. 의미론적 명명
```javascript
// ❌ 값 기반 명명
const blue600 = tokens.color.blue['600'];

// ✅ 역할 기반 명명
const primaryAction = tokens.semantic.color.action.primary;
```

### 3. 테마 지원
```javascript
// ✅ 테마 전환 가능한 구조
const tokens = isDark ? semanticDark : semanticLight;
```

## 📊 토큰 통계

### Primitive 토큰
- **Spacing**: 18개 (0 ~ 32)
- **Colors**: 60개 (6개 팔레트 × 10단계)
- **Typography**: 27개 (fontSize, lineHeight, fontWeight 등)
- **Border**: 15개 (radius, width, style)
- **Opacity**: 16개 (0% ~ 100%)

### Semantic 토큰
- **Typography**: 25개 (heading, body, label, code 등)
- **Colors**: 40개 (action, text, surface, border, state)
- **Spacing**: 13개 (component + layout)
- **Border**: 15개 (다양한 상태)
- **Radius**: 5개 (sm ~ full)

**총 토큰 수**: ~250개 (Light + Dark)

## 🔧 도구 호환성

- ✅ **Figma Tokens Plugin** - tokens-unified.json 직접 import
- ✅ **Style Dictionary** - 개별 파일 또는 통합 파일 사용
- ✅ **Tokens Studio** - 완벽 호환
- ✅ **Tailwind CSS** - 설정 파일로 변환 가능
- ✅ **CSS Variables** - 자동 생성 가능

## ⚡ 빠른 참조

### 자주 사용하는 토큰

```javascript
// 색상
semantic.color.action.primary          // Primary 액션 색상
semantic.color.text.default            // 기본 텍스트 색상
semantic.color.surface.default         // 기본 배경 색상

// 간격
semantic.spacing.component.md          // 컴포넌트 기본 간격 (16px)
semantic.spacing.layout.2xl            // 레이아웃 간격 (48px)

// 타이포그래피
semantic.typography.heading.h1         // H1 스타일
semantic.typography.body.md            // 본문 스타일
semantic.typography.button             // 버튼 텍스트

// Border
semantic.radius.md                     // 기본 radius (8px)
semantic.border.default                // 기본 border
```

## 🆘 문제 해결

### Q: 토큰을 찾을 수 없어요
**A**: `MIGRATION_GUIDE.md`의 매핑 테이블 참조

### Q: 단위가 이상해요
**A**: v2에서는 모든 값에 단위가 포함됩니다. 코드에서 단위를 추가하는 부분 제거 필요

### Q: Dark Mode가 안 돼요
**A**: `semantic-dark.json`을 사용하고 있는지 확인

## 📞 지원

- **문서**: 이 폴더의 markdown 파일들
- **이슈**: GitHub Issues
- **토론**: GitHub Discussions

## 🎉 리팩토링 완료!

모든 토큰이 효율적으로 재구성되었습니다:

- ✅ 4개의 토큰 파일
- ✅ 4개의 문서 파일
- ✅ ~250개의 토큰
- ✅ Light/Dark 테마 지원
- ✅ 완전한 마이그레이션 가이드

**시작하기**: `README.md`를 먼저 읽어보세요!

---

**Version**: 2.0.0  
**Date**: 2025-11-11  
**Status**: ✅ Production Ready

