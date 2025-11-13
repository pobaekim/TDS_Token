# 토큰 구조 비교

## 📊 전체 비교 요약

| 항목 | 기존 (v1) | 리팩토링 후 (v2) | 개선 |
|------|-----------|-----------------|------|
| **파일 구조** | 단일 파일 (또는 2개) | 역할별 분리 (4개) | ✅ 유지보수성 향상 |
| **단위 명시** | 일부 누락 | 모두 명시 | ✅ 명확성 향상 |
| **명명 규칙** | 하이픈 구분 | 점(.) 계층 구조 | ✅ 일관성 향상 |
| **Dark Mode** | 미지원 | 완전 지원 | ✅ 기능 추가 |
| **토큰 계층** | 평면적 | Primitive → Semantic | ✅ 구조 개선 |
| **참조 체계** | 불명확 | 명확한 참조 경로 | ✅ 추적성 향상 |
| **총 토큰 수** | ~200개 | ~250개 (Dark 포함) | ✅ 완성도 향상 |

## 🔄 구조 변경 예시

### 1. Spacing 토큰

#### Before (v1)
```json
{
  "Primitive": {
    "space-0": {
      "value": "0",
      "type": "spacing"
    },
    "space-4": {
      "value": "16",
      "type": "spacing"
    }
  }
}
```

#### After (v2)
```json
{
  "primitive": {
    "spacing": {
      "0": {
        "value": "0px",
        "type": "spacing"
      },
      "4": {
        "value": "16px",
        "type": "spacing"
      }
    }
  }
}
```

**변경 사항:**
- ✅ 단위 추가 (`0` → `0px`, `16` → `16px`)
- ✅ 계층 구조화 (spacing 그룹)
- ✅ 네이밍 단순화 (`space-4` → `4`)

---

### 2. Color 토큰

#### Before (v1)
```json
{
  "Primitive": {
    "color-base-blue-600": {
      "value": "#2563eb",
      "type": "color"
    }
  }
}
```

#### After (v2)
```json
{
  "primitive": {
    "color": {
      "blue": {
        "600": {
          "value": "#2563eb",
          "type": "color"
        }
      }
    }
  }
}
```

**변경 사항:**
- ✅ 3단계 계층 구조 (color → blue → 600)
- ✅ 색상 팔레트 명확화
- ✅ 확장성 향상

---

### 3. Typography 토큰

#### Before (v1)
```json
{
  "Primitive": {
    "font-size-12": {
      "value": "12px",
      "type": "fontSizes"
    }
  }
}
```

#### After (v2)
```json
{
  "primitive": {
    "fontSize": {
      "base": {
        "value": "12px",
        "type": "fontSizes",
        "description": "Default size"
      }
    }
  }
}
```

**변경 사항:**
- ✅ 의미 있는 이름 (`font-size-12` → `base`)
- ✅ 설명 추가
- ✅ 스케일 일관성 (xs, sm, base, md, lg, xl, 2xl, 3xl, 4xl)

---

### 4. Semantic 토큰 (Light Mode)

#### Before (v1)
```json
{
  "Semantic/light": {
    "color-primary": {
      "value": "{color-base-blue-600}",
      "type": "color"
    }
  }
}
```

#### After (v2)
```json
{
  "semantic": {
    "color": {
      "action": {
        "primary": {
          "value": "{primitive.color.blue.600}",
          "type": "color",
          "description": "주요 액션 / 브랜드 Primary"
        }
      }
    }
  }
}
```

**변경 사항:**
- ✅ 의미론적 그룹화 (`action` 카테고리)
- ✅ 명확한 참조 경로 (`{primitive.color.blue.600}`)
- ✅ 역할 설명 추가

---

### 5. Dark Mode 지원 (NEW!)

#### Before (v1)
```
Dark Mode 지원 없음
```

#### After (v2)
```json
// semantic-dark.json
{
  "semantic": {
    "color": {
      "surface": {
        "default": {
          "value": "{primitive.color.slate.900}",
          "type": "color",
          "description": "기본 표면 (Dark Mode)"
        }
      },
      "text": {
        "default": {
          "value": "{primitive.color.slate.50}",
          "type": "color",
          "description": "본문 텍스트 (Dark Mode)"
        }
      }
    }
  }
}
```

**변경 사항:**
- ✅ Dark Mode 전용 토큰 파일 추가
- ✅ Light/Dark 동일한 키 구조
- ✅ 테마 전환 용이

---

## 📁 파일 구조 비교

### Before (v1)
```
/Downloads/
├── tokens.json          (Primitive만)
└── tokens2.json         (Primitive + Semantic Light)
```

### After (v2)
```
/Downloads/tokens-refactored/
├── primitive.json           # 기본 토큰
├── semantic-light.json      # Light Mode
├── semantic-dark.json       # Dark Mode (NEW!)
├── tokens-unified.json      # 통합 파일
├── README.md               # 문서
├── MIGRATION_GUIDE.md      # 마이그레이션 가이드
└── COMPARISON.md           # 이 문서
```

**개선 사항:**
- ✅ 역할별 파일 분리
- ✅ 완전한 문서화
- ✅ 마이그레이션 지원

---

## 🎨 사용 예시 비교

### CSS Variables

#### Before (v1)
```css
.button {
  background: var(--color-primary);
  padding: var(--space-4);
  font-size: var(--font-size-12);
  border-radius: var(--radius-base-8);
}
```

#### After (v2)
```css
.button {
  background: var(--semantic-color-action-primary);
  padding: var(--primitive-spacing-4);
  font-size: var(--primitive-fontSize-base);
  border-radius: var(--primitive-radius-lg);
}

/* 또는 Semantic 토큰으로 (권장) */
.button {
  background: var(--semantic-color-action-primary);
  padding: var(--semantic-spacing-component-md);
  border-radius: var(--semantic-radius-md);
}
```

---

### JavaScript/TypeScript

#### Before (v1)
```typescript
import tokens from './tokens2.json';

const buttonStyle = {
  background: tokens.Primitive['color-base-blue-600'].value,
  padding: `${tokens.Primitive['space-4'].value}px`, // 단위 수동 추가
};
```

#### After (v2)
```typescript
import tokens from './tokens-unified.json';

const buttonStyle = {
  // Primitive 사용 (직접 값)
  background: tokens.primitive.color.blue['600'].value,
  padding: tokens.primitive.spacing['4'].value, // 단위 포함됨
  
  // Semantic 사용 (권장)
  background: tokens.semantic.color.action.primary.value,
  padding: tokens.semantic.spacing.component.md.value,
};
```

---

### React/Styled Components

#### Before (v1)
```jsx
import styled from 'styled-components';
import tokens from './tokens2.json';

const Button = styled.button`
  background: ${tokens.Primitive['color-base-blue-600'].value};
  padding: ${tokens.Primitive['space-4'].value}px;
`;
```

#### After (v2)
```jsx
import styled from 'styled-components';
import { primitive, semantic } from './tokens';

const Button = styled.button`
  /* Semantic 사용 (권장) */
  background: ${semantic.color.action.primary.value};
  padding: ${semantic.spacing.component.md.value};
  border-radius: ${semantic.radius.md.value};
  
  /* Dark Mode 지원 */
  ${props => props.theme.isDark && `
    background: ${props.theme.tokens.semantic.color.action.primary.value};
  `}
`;
```

---

## 📈 이점 정리

### 1. **개발자 경험 (DX)**
- ✅ 자동완성 지원 향상 (계층 구조)
- ✅ 토큰 검색 용이
- ✅ 타입 안전성 향상 (TypeScript)

### 2. **유지보수성**
- ✅ 역할별 파일 분리로 관리 편의
- ✅ 변경 영향 범위 명확
- ✅ 버전 관리 용이

### 3. **확장성**
- ✅ 새로운 토큰 추가 용이
- ✅ 테마 확장 가능 (Light/Dark 외 추가 테마)
- ✅ 컴포넌트 토큰 레이어 추가 가능

### 4. **일관성**
- ✅ 명명 규칙 통일
- ✅ 값의 단위 명확화
- ✅ 참조 체계 표준화

### 5. **접근성**
- ✅ Dark Mode 기본 지원
- ✅ 고대비 테마 추가 가능
- ✅ 의미론적 토큰으로 역할 명확

---

## 🔄 점진적 마이그레이션

### Phase 1: 준비
```bash
✅ 새 토큰 파일 추가
✅ 기존 파일 보존 (호환성 유지)
✅ 문서 작성
```

### Phase 2: 병행 운영
```javascript
// 두 시스템 동시 지원
import oldTokens from './tokens.json';
import newTokens from './tokens-refactored/tokens-unified.json';

const tokens = USE_NEW_TOKENS ? newTokens : oldTokens;
```

### Phase 3: 완전 전환
```bash
✅ 모든 코드 업데이트
✅ 테스트 완료
✅ 기존 파일 제거
```

---

## 💡 베스트 프랙티스

### ❌ 피해야 할 패턴

```javascript
// 1. Primitive 직접 사용
color: tokens.primitive.color.blue['600'];

// 2. 하드코딩
padding: '16px'; // 토큰 사용하지 않음

// 3. 단위 중복
padding: tokens.spacing['4'].value + 'px'; // 이미 px 포함
```

### ✅ 권장 패턴

```javascript
// 1. Semantic 토큰 사용
color: tokens.semantic.color.action.primary;

// 2. 적절한 토큰 선택
padding: tokens.semantic.spacing.component.md;

// 3. 테마 지원
const themeTokens = isDark ? semanticDark : semanticLight;
```

---

## 📊 마이그레이션 진행률 추적

```markdown
- [ ] Primitive 토큰 업데이트
  - [x] Spacing
  - [x] Colors
  - [x] Typography
  - [x] Border
  
- [ ] Semantic 토큰 생성
  - [x] Light Mode
  - [x] Dark Mode
  
- [ ] 코드베이스 업데이트
  - [ ] Components
  - [ ] Pages
  - [ ] Utilities
  
- [ ] 테스트
  - [ ] Unit Tests
  - [ ] Visual Regression
  - [ ] A11y Tests
  
- [ ] 문서화
  - [x] README
  - [x] Migration Guide
  - [x] Comparison
```

---

## 🎯 결론

리팩토링된 토큰 시스템은:
- **더 명확하고** (단위, 참조 경로)
- **더 일관되며** (명명 규칙, 구조)
- **더 확장 가능하고** (Dark Mode, 미래 테마)
- **더 유지보수하기 쉽습니다** (파일 분리, 문서화)

**마이그레이션 소요 시간**: 소규모 프로젝트 1-2일, 대규모 프로젝트 1-2주 예상

---

**Version**: 2.0.0  
**Last Updated**: 2025-11-11

