# 디자인 토큰 리팩토링 v2.0

## 📋 개요

기존 토큰 구조를 분석하고 효율적으로 재구성한 디자인 토큰 시스템입니다.

## 🎯 주요 개선사항

### 1. **파일 구조 개선**
- 단일 파일에서 역할별로 분리된 구조로 변경
- Primitive, Semantic (Common/Light/Dark) 토큰 분리
- 공통 속성과 테마별 색상 분리로 중복 제거
- 유지보수성 및 확장성 향상

### 2. **단위 명시**
- 모든 spacing, fontSize, borderRadius 값에 단위(px) 추가
- 혼란 방지 및 명확한 값 정의

### 3. **명명 규칙 통일**
```
Before: font-size-10, space-0-5, color-base-blue-600
After:  fontSize.xs, spacing.0.5, color.blue.600
```

### 4. **Dark Mode 지원**
- semantic-dark.json 파일 추가
- Light/Dark 모드 간 일관된 토큰 키 구조

### 5. **계층 구조 명확화**
```
Primitive (기본 값)
    ↓ 참조
Semantic (의미론적 토큰)
    ↓ 참조  
Component (컴포넌트별 토큰)
```

### 6. **Semantic 토큰 최적화**
- 테마 독립적 속성(typography, spacing, radius, border)을 `semantic-common.json`으로 분리
- 테마 의존적 속성(color)만 `semantic-light.json`, `semantic-dark.json`에 정의
- 중복 코드 제거 및 관리 포인트 최소화

## 📁 파일 구조

```
tokens-refactored/
├── primitive.json          # 기본 토큰 (색상, 간격, 타이포그래피 등)
├── semantic-common.json    # 공통 의미론적 토큰 (typography, spacing, radius, border)
├── semantic-light.json     # 라이트 모드 색상 토큰
├── semantic-dark.json      # 다크 모드 색상 토큰
├── tokens.json            # 통합 파일 (Light + Dark) - 자동 생성
├── $themes.json           # Tokens Studio 테마 설정
├── $metadata.json         # Tokens Studio 메타데이터
└── README.md              # 이 문서
```

## 🔍 토큰 구조

### Primitive 토큰

기본적인 디자인 값들을 정의합니다.

#### Spacing
- `primitive.spacing.0` ~ `primitive.spacing.32`
- 4px 기본 단위 (0.5 = 2px, 1 = 4px, 2 = 8px, ...)

#### Typography
- **Font Size**: xs(10px) ~ 4xl(40px)
- **Line Height**: xs(14px) ~ 4xl(48px)
- **Font Weight**: regular(400), medium(500), semibold(600)
- **Font Family**: sans(Mona Sans), mono(Menlo)

#### Colors
- **Neutral**: white, black, slate, gray
- **Brand/Accent**: blue, red, green, orange, yellow
- 각 색상은 50~900 스케일로 정의

#### Border
- **Radius**: sm(4px), md(6px), lg(8px), xl(16px), full(999px)
- **Width**: hairline(0.5px), 0~3px
- **Style**: solid, dashed

#### Opacity
- 0%, 4%, 8% ~ 100%

### Semantic 토큰

의미론적 역할을 정의합니다. 효율성을 위해 **공통 토큰**과 **테마별 토큰**으로 분리되어 있습니다.

#### semantic-common.json (테마 독립적)
모든 테마에서 공통으로 사용하는 속성들:

**Typography**
```json
{
  "semantic.typography.heading.h1": "히어로/대형 타이틀",
  "semantic.typography.body.md": "본문 기본",
  "semantic.typography.button": "버튼 텍스트"
}
```

**Spacing**
- **Component**: 3xs(2px) ~ xl(32px) - 컴포넌트 내부 간격
- **Layout**: 2xl(48px) ~ 5xl(128px) - 레이아웃 간격

**Radius**
- sm(4px), smPlus(6px), md(8px), lg(16px), full(999px)

**Border**
- 다양한 상태별 보더 스타일 정의 (구조만, 색상은 테마별)
- default, primary, success, warning, danger, focus, disabled 등

#### semantic-light.json / semantic-dark.json (테마 의존적)
각 테마별로 다른 색상만 정의:

**Color**
```json
{
  "semantic.color.action.primary": "주요 액션",
  "semantic.color.text.default": "본문 텍스트",
  "semantic.color.surface.default": "기본 배경",
  "semantic.color.state.success.default": "성공 상태"
}
```

## 🎨 Light vs Dark Mode

### Light Mode (`semantic-light.json`)
- 밝은 배경 + 어두운 텍스트
- `color.surface.default` → white
- `color.text.default` → slate.900
- `color.action.primary` → blue.600

### Dark Mode (`semantic-dark.json`)
- 어두운 배경 + 밝은 텍스트
- `color.surface.default` → slate.900
- `color.text.default` → slate.50
- `color.action.primary` → blue.500

## 🚀 사용 방법

### 1. Tokens Studio (Figma Plugin) 사용

프로젝트에 `$themes.json` 파일이 포함되어 있어 Tokens Studio에서 바로 사용 가능합니다.

**사용 단계:**
1. Figma에서 Tokens Studio 플러그인 실행
2. Settings → Token Storage → JSON Files
3. 이 폴더를 선택하여 토큰 로드
4. Theme 탭에서 "Light Theme" 또는 "Dark Theme" 선택

**테마 구성:**
- **Light Theme**: primitive + semantic-common + semantic-light
- **Dark Theme**: primitive + semantic-common + semantic-dark

### 2. 통합 파일 사용 (권장)

```javascript
// 모든 토큰 파일을 하나로 묶은 형태
import allTokens from './tokens.json';

// 구조: { primitive, semantic-common, semantic-light, semantic-dark }

// Light 테마 구성
const lightTheme = {
  ...allTokens.primitive,
  ...allTokens['semantic-common'],
  ...allTokens['semantic-light']
};

// Dark 테마 구성
const darkTheme = {
  ...allTokens.primitive,
  ...allTokens['semantic-common'],
  ...allTokens['semantic-dark']
};

// 테마에 따라 선택
const tokens = isDark ? darkTheme : lightTheme;
```

### 3. 분리된 파일 직접 사용 (고급)

```javascript
import primitiveTokens from './primitive.json';
import semanticCommonTokens from './semantic-common.json';
import semanticLightTokens from './semantic-light.json';
import semanticDarkTokens from './semantic-dark.json';

// 공통 토큰 + 테마별 색상 토큰 병합
const semanticColorTokens = isDark ? semanticDarkTokens : semanticLightTokens;
const semanticTokens = {
  ...semanticCommonTokens,
  ...semanticColorTokens
};
```

### 4. 토큰 참조
```css
/* Primitive 직접 사용 (권장하지 않음) */
color: #2563eb; /* primitive.color.blue.600 */

/* Semantic 토큰 사용 (권장) */
color: var(--semantic-color-action-primary);
background: var(--semantic-color-surface-default);
padding: var(--semantic-spacing-component-md);
```

## 🔄 마이그레이션 가이드

### Before → After

| Before | After |
|--------|-------|
| `{font-size-12}` | `{primitive.fontSize.base}` |
| `{color-base-blue-600}` | `{primitive.color.blue.600}` |
| `{space-4}` | `{primitive.spacing.4}` |
| `{color-primary}` | `{semantic.color.action.primary}` |
| `{spacing-md}` | `{semantic.spacing.component.md}` |

### 코드 변경 예시

**Before:**
```json
{
  "button": {
    "background": "{color-base-blue-600}",
    "padding": "{space-4}"
  }
}
```

**After:**
```json
{
  "button": {
    "background": "{semantic.color.action.primary}",
    "padding": "{semantic.spacing.component.md}"
  }
}
```

## 📊 통계

### 개선 전 (tokens.json + tokens2.json)
- 파일 수: 2개
- 총 토큰 수: ~200개
- Dark mode: 미지원
- 단위 누락: 다수
- 중복 코드: 다수

### 개선 후
- 파일 수: 4개 (소스 파일) + 1개 (통합 파일)
- 총 토큰 수: ~250개 (Dark mode 포함)
- Dark mode: 완전 지원
- 단위: 모두 명시
- 중복 제거: semantic 공통 속성 분리로 약 400줄 중복 제거
- 관심사 분리: 각 파일이 명확한 역할 담당
- 유연성: 통합 파일 / 분리 파일 - 2가지 사용 방식 제공

## 🛠️ 호환성

- ✅ Figma Tokens Plugin
- ✅ Style Dictionary
- ✅ Tokens Studio
- ✅ W3C DTCG 표준 준수

## 📝 베스트 프랙티스

1. **항상 Semantic 토큰 사용**
   - Primitive는 직접 사용하지 말 것
   - 의미론적 이름으로 역할 명확화

2. **파일 구조 선택**
   - **통합 파일** (`tokens.json`): Light + Dark 모두 포함, 간편하게 사용
   - **분리 파일**: 소스 파일들을 직접 조합하여 세밀한 제어
   - 프로젝트 상황에 맞게 선택

3. **일관된 명명 규칙**
   - 계층 구조: `semantic.category.subcategory.variant`
   - camelCase 사용

4. **테마 전환**
   - Light/Dark 토큰의 키 구조를 동일하게 유지
   - 값만 변경하여 테마 전환

5. **문서화**
   - 모든 토큰에 description 추가
   - 사용 목적 명확히 기술

## 🔧 통합 파일 생성 방법

`tokens.json` 파일은 다음 명령어로 재생성할 수 있습니다:

```bash
jq -n \
  --slurpfile primitive primitive.json \
  --slurpfile common semantic-common.json \
  --slurpfile light semantic-light.json \
  --slurpfile dark semantic-dark.json \
  '{
    primitive: $primitive[0],
    "semantic-common": $common[0],
    "semantic-light": $light[0],
    "semantic-dark": $dark[0]
  }' > tokens.json
```

**참고**: `jq` 도구가 필요합니다. Mac에서는 `brew install jq`로 설치 가능합니다.

### 빌드 스크립트

```bash
#!/bin/bash
# build-tokens.sh - 통합 파일 생성

echo "🔨 토큰 통합 파일 생성 중..."

jq -n \
  --slurpfile primitive primitive.json \
  --slurpfile common semantic-common.json \
  --slurpfile light semantic-light.json \
  --slurpfile dark semantic-dark.json \
  '{
    primitive: $primitive[0],
    "semantic-common": $common[0],
    "semantic-light": $light[0],
    "semantic-dark": $dark[0]
  }' > tokens.json

if [ $? -eq 0 ]; then
  echo "✅ tokens.json 생성 완료!"
else
  echo "❌ 생성 실패"
  exit 1
fi
```

## 🔮 향후 계획

- [ ] Component 토큰 레이어 추가
- [ ] Animation/Transition 토큰 추가
- [ ] Shadow/Elevation 토큰 추가
- [ ] Accessibility 관련 토큰 추가
- [ ] 자동화된 빌드 스크립트 작성

## 📄 라이선스

프로젝트에 맞게 라이선스를 설정하세요.

---

**Version**: 2.1.0  
**Last Updated**: 2025-11-13  
**Maintained by**: Design System Team

### Changelog
- **v2.1.0** (2025-11-13): Semantic 토큰을 common/light/dark로 분리, 중복 제거
- **v2.0.0** (2025-11-11): 초기 리팩토링 완료

