# 토큰 마이그레이션 가이드

## 📌 개요

기존 `tokens.json`과 `tokens2.json`에서 새로운 리팩토링된 토큰 구조로 마이그레이션하는 방법을 안내합니다.

## 🔄 전체 매핑 테이블

### Font Size

| 기존 | 새 구조 |
|------|---------|
| `font-size-10` | `primitive.fontSize.xs` |
| `font-size-11` | `primitive.fontSize.sm` |
| `font-size-12` | `primitive.fontSize.base` |
| `font-size-14` | `primitive.fontSize.md` |
| `font-size-16` | `primitive.fontSize.lg` |
| `font-size-18` | `primitive.fontSize.xl` |
| `font-size-24` | `primitive.fontSize.2xl` |
| `font-size-32` | `primitive.fontSize.3xl` |
| `font-size-40` | `primitive.fontSize.4xl` |

### Spacing

| 기존 | 새 구조 | 값 |
|------|---------|-----|
| `space-0` | `primitive.spacing.0` | 0px |
| `space-0-5` | `primitive.spacing.0.5` | 2px |
| `space-1` | `primitive.spacing.1` | 4px |
| `space-1-5` | `primitive.spacing.1.5` | 6px |
| `space-2` | `primitive.spacing.2` | 8px |
| `space-2-5` | `primitive.spacing.2.5` | 10px |
| `space-3` | `primitive.spacing.3` | 12px |
| `space-4` | `primitive.spacing.4` | 16px |
| `space-5` | `primitive.spacing.5` | 20px |
| `space-6` | `primitive.spacing.6` | 24px |
| `space-8` | `primitive.spacing.8` | 32px |
| `space-12` | `primitive.spacing.12` | 48px |
| `space-16` | `primitive.spacing.16` | 64px |
| `space-24` | `primitive.spacing.24` | 96px |
| `space-32` | `primitive.spacing.32` | 128px |

### Colors

| 기존 | 새 구조 |
|------|---------|
| `color-base-white` | `primitive.color.white` |
| `color-base-black` | `primitive.color.black` |
| `color-base-slate-50` | `primitive.color.slate.50` |
| `color-base-slate-100` | `primitive.color.slate.100` |
| `color-base-slate-200` | `primitive.color.slate.200` |
| ... | ... |
| `color-base-blue-600` | `primitive.color.blue.600` |
| `color-base-red-500` | `primitive.color.red.500` |

### Border Radius

| 기존 | 새 구조 | 값 |
|------|---------|-----|
| `radius-base-4` | `primitive.radius.sm` | 4px |
| `radius-base-6` | `primitive.radius.md` | 6px |
| `radius-base-8` | `primitive.radius.lg` | 8px |
| `radius-base-16` | `primitive.radius.xl` | 16px |
| `radius-base-999` | `primitive.radius.full` | 999px |

### Font Weight

| 기존 | 새 구조 |
|------|---------|
| `font-weight-regular` | `primitive.fontWeight.regular` |
| `font-weight-medium` | `primitive.fontWeight.medium` |
| `font-weight-semibold` | `primitive.fontWeight.semibold` |

### Line Height

| 기존 | 새 구조 |
|------|---------|
| `line-height-14` | `primitive.lineHeight.xs` |
| `line-height-16` | `primitive.lineHeight.sm` |
| `line-height-18` | `primitive.lineHeight.base` |
| `line-height-20` | `primitive.lineHeight.md` |
| `line-height-24` | `primitive.lineHeight.lg` |
| `line-height-28` | `primitive.lineHeight.xl` |
| `line-height-32` | `primitive.lineHeight.2xl` |
| `line-height-36` | `primitive.lineHeight.3xl` |
| `line-height-48` | `primitive.lineHeight.4xl` |

## 🎨 Semantic 토큰 매핑

### Typography

| 기존 | 새 구조 |
|------|---------|
| `font-heading-h1` | `semantic.typography.heading.h1` |
| `font-heading-h2` | `semantic.typography.heading.h2` |
| `font-body-md` | `semantic.typography.body.md` |
| `font-body-lg` | `semantic.typography.body.lg` |
| `font-button` | `semantic.typography.button` |
| `font-label-md` | `semantic.typography.label.md` |
| `font-code-md` | `semantic.typography.code.md` |

### Colors (Semantic)

| 기존 | 새 구조 (Light) |
|------|----------------|
| `color-primary` | `semantic.color.action.primary` |
| `color-primary-hover` | `semantic.color.action.primaryHover` |
| `color-text-default` | `semantic.color.text.default` |
| `color-text-muted` | `semantic.color.text.muted` |
| `color-surface` | `semantic.color.surface.default` |
| `color-border-default` | `semantic.color.border.default` |
| `color-success` | `semantic.color.state.success.default` |
| `color-danger` | `semantic.color.state.danger.default` |
| `color-warning` | `semantic.color.state.warning.default` |
| `color-info` | `semantic.color.state.info.default` |

### Spacing (Semantic)

| 기존 | 새 구조 |
|------|---------|
| `spacing-3xs` | `semantic.spacing.component.3xs` |
| `spacing-xxs` | `semantic.spacing.component.xxs` |
| `spacing-xs` | `semantic.spacing.component.xs` |
| `spacing-sm` | `semantic.spacing.component.sm` |
| `spacing-md` | `semantic.spacing.component.md` |
| `spacing-lg` | `semantic.spacing.component.lg` |
| `spacing-xl` | `semantic.spacing.component.xl` |
| `spacing-2xl` | `semantic.spacing.layout.2xl` |
| `spacing-3xl` | `semantic.spacing.layout.3xl` |
| `spacing-4xl` | `semantic.spacing.layout.4xl` |

### Radius (Semantic)

| 기존 | 새 구조 |
|------|---------|
| `radius-sm` | `semantic.radius.sm` |
| `radius-sm-plus` | `semantic.radius.smPlus` |
| `radius-md` | `semantic.radius.md` |
| `radius-lg` | `semantic.radius.lg` |

### Border (Semantic)

| 기존 | 새 구조 |
|------|---------|
| `border-default` | `semantic.border.default` |
| `border-subtle` | `semantic.border.subtle` |
| `border-strong` | `semantic.border.strong` |
| `border-primary` | `semantic.border.primary` |
| `border-success` | `semantic.border.success` |
| `border-warning` | `semantic.border.warning` |
| `border-danger` | `semantic.border.danger` |
| `border-focus` | `semantic.border.focus` |
| `border-field` | `semantic.border.field.default` |
| `border-field-focus` | `semantic.border.field.focus` |
| `border-field-error` | `semantic.border.field.error` |

## 🔧 자동 변환 스크립트

### JavaScript/TypeScript

```javascript
// token-migrator.js
const tokenMapping = {
  'font-size-10': 'primitive.fontSize.xs',
  'font-size-12': 'primitive.fontSize.base',
  'space-4': 'primitive.spacing.4',
  'color-primary': 'semantic.color.action.primary',
  // ... 전체 매핑 추가
};

function migrateTokens(code) {
  let result = code;
  for (const [oldToken, newToken] of Object.entries(tokenMapping)) {
    const regex = new RegExp(`\\{${oldToken}\\}`, 'g');
    result = result.replace(regex, `{${newToken}}`);
  }
  return result;
}

// 사용 예시
const oldCode = `
  color: {color-primary};
  padding: {space-4};
`;

const newCode = migrateTokens(oldCode);
console.log(newCode);
// 출력:
// color: {semantic.color.action.primary};
// padding: {primitive.spacing.4};
```

### 정규식 검색/치환

VS Code나 다른 에디터에서 정규식을 사용하여 일괄 변경:

**검색:**
```regex
\{font-size-(\d+)\}
```

**치환:**
```
{primitive.fontSize.$1}
```

## 📝 단계별 마이그레이션

### Step 1: 백업
```bash
# 기존 파일 백업
cp tokens.json tokens.json.backup
cp tokens2.json tokens2.json.backup
```

### Step 2: 새 토큰 파일 복사
```bash
# 리팩토링된 토큰 파일 복사
cp tokens-refactored/* ./design-tokens/
```

### Step 3: 코드베이스 업데이트

#### A. CSS Variables
```css
/* Before */
.button {
  background: var(--color-primary);
  padding: var(--space-4);
  border-radius: var(--radius-base-8);
}

/* After */
.button {
  background: var(--semantic-color-action-primary);
  padding: var(--primitive-spacing-4);
  border-radius: var(--primitive-radius-lg);
}
```

#### B. SCSS/LESS
```scss
// Before
$primary-color: map-get($tokens, 'color-primary');
$spacing-md: map-get($tokens, 'space-4');

// After
$primary-color: map-get($tokens, 'semantic', 'color', 'action', 'primary');
$spacing-md: map-get($tokens, 'primitive', 'spacing', '4');
```

#### C. JavaScript/TypeScript
```typescript
// Before
import tokens from './tokens.json';
const primaryColor = tokens.Primitive['color-base-blue-600'].value;

// After
import tokens from './tokens-unified.json';
const primaryColor = tokens.primitive.color.blue['600'].value;
// 또는 Semantic 사용 (권장)
const primaryColor = tokens.semantic.color.action.primary.value;
```

### Step 4: 테스트
```bash
# 스타일 빌드 테스트
npm run build:styles

# 비주얼 리그레션 테스트
npm run test:visual
```

### Step 5: Dark Mode 적용
```javascript
// 테마 전환 로직
const getTokens = (isDark) => {
  if (isDark) {
    return {
      ...primitiveTokens,
      semantic: semanticDarkTokens.semantic
    };
  } else {
    return {
      ...primitiveTokens,
      semantic: semanticLightTokens.semantic
    };
  }
};
```

## ⚠️ 주의사항

### 1. 단위 변경
- 기존: `"value": "4"` (단위 없음)
- 새로운: `"value": "4px"` (단위 명시)

코드에서 단위를 별도로 추가하고 있었다면 제거 필요:

```javascript
// Before
const spacing = parseInt(tokens['space-4'].value) + 'px'; // "4" + "px" = "4px"

// After
const spacing = tokens.primitive.spacing['4'].value; // "4px" 이미 포함
```

### 2. 참조 경로 변경
```json
// Before
{
  "value": "{color-base-blue-600}"
}

// After
{
  "value": "{primitive.color.blue.600}"
}
```

### 3. Semantic 토큰 우선 사용
Primitive 토큰을 직접 사용하는 대신 Semantic 토큰을 사용하세요:

```javascript
// ❌ 나쁜 예
color: tokens.primitive.color.blue['600'];

// ✅ 좋은 예
color: tokens.semantic.color.action.primary;
```

## 🔍 검증 체크리스트

- [ ] 모든 토큰 참조가 업데이트됨
- [ ] 빌드 오류 없음
- [ ] 비주얼 리그레션 테스트 통과
- [ ] Dark Mode 정상 작동
- [ ] 단위가 올바르게 적용됨
- [ ] 문서 업데이트됨

## 🆘 문제 해결

### Q: 특정 토큰을 찾을 수 없습니다
**A:** 매핑 테이블을 참고하거나 유사한 의미의 Semantic 토큰을 사용하세요.

### Q: 기존 값과 픽셀 단위가 달라졌습니다
**A:** 원래 단위가 누락되어 있었을 수 있습니다. 디자인팀과 확인 후 올바른 값을 사용하세요.

### Q: Dark Mode에서 색상이 이상합니다
**A:** `semantic-dark.json`을 사용하고 있는지 확인하세요. Light 토큰을 그대로 사용하면 안 됩니다.

## 📞 지원

문제가 발생하거나 질문이 있으면 다음으로 연락하세요:
- Design System Team
- Slack: #design-system
- Email: design-system@company.com

---

**마이그레이션 완료 후 기존 파일은 삭제하지 말고 보관하세요.**

