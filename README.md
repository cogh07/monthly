# 선적비용 대조 툴

영천항운 SAS 파일과 콘솔사 인보이스 파일을 업로드하면  
AI(Claude API)가 자동으로 선적 건을 추출하여 금액을 비교해주는 웹 툴입니다.

## 배포 방법 (GitHub Pages)

### 1단계 — GitHub 저장소 만들기
1. [github.com](https://github.com) 로그인
2. 우측 상단 `+` → **New repository**
3. Repository name: `shipping-comparator` (또는 원하는 이름)
4. **Public** 선택 (GitHub Pages 무료 사용 조건)
5. **Create repository** 클릭

### 2단계 — 파일 업로드
1. 저장소 페이지에서 **Add file** → **Upload files** 클릭
2. `index.html` 파일을 드래그하여 업로드
3. **Commit changes** 클릭

### 3단계 — GitHub Pages 활성화
1. 저장소 상단 **Settings** 탭 클릭
2. 좌측 메뉴 **Pages** 클릭
3. Source: **Deploy from a branch**
4. Branch: **main** / **/ (root)** 선택 후 **Save**
5. 약 1~2분 후 URL 자동 생성됨

> URL 형식: `https://[GitHub아이디].github.io/shipping-comparator/`

---

## 사용 방법

### API 키 설정 (최초 1회)
1. 페이지 우측 상단 **API 키 설정** 클릭
2. [Anthropic Console](https://console.anthropic.com) → API Keys에서 키 발급
3. `sk-ant-...` 형식의 키 입력 후 **저장**
4. 키는 브라우저 로컬 스토리지에 저장됨 (다음 방문 시 재입력 불필요)

### 파일 비교
1. 왼쪽: SAS 파일 (영천항운 AP LIST PDF) 업로드
2. 오른쪽: 콘솔사 인보이스 파일 (INVOICE LIST PDF) 업로드
3. **비교 분석하기** 클릭
4. AI가 두 파일을 분석하여 결과 표시 (약 20~30초 소요)

### 결과 해석
| 상태 | 의미 |
|------|------|
| 일치 | 양쪽 금액 동일 |
| 불일치 | 같은 B/L인데 금액 차이 있음 |
| 콘솔사만 | 콘솔사 인보이스에 있으나 SAS에 없음 |
| SAS만 | SAS에 있으나 콘솔사 인보이스에 없음 |

결과 우측 하단 **CSV 내보내기**로 엑셀에서 활용 가능

---

## 업데이트 방법
코드 수정이 필요할 경우:
1. GitHub 저장소에서 `index.html` 클릭 → 연필 아이콘(Edit) 클릭
2. 내용 수정 후 **Commit changes**
3. 수 분 내 자동 반영

---

## 기술 스택
- 순수 HTML/CSS/JavaScript (프레임워크 없음)
- Anthropic Claude API (`claude-sonnet-4-20250514`)
- PDF → base64 변환 후 AI로 데이터 추출
- 매칭 키: SAS의 M.B/L No = 콘솔사의 House No
