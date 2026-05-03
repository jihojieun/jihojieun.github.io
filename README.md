# 모바일 청첩장 만들기 가이드

`index.html` 파일 하나로 동작하는 모바일 청첩장입니다. 네이버 지도는 **주소만 입력하면** 자동으로 위치를 찾아 핀을 꽂아줍니다.

---

## 📋 전체 순서

1. 네이버 클라우드 플랫폼에서 지도 API 키 발급 (무료)
2. `index.html`에서 내 정보로 수정
3. 사진 업로드
4. GitHub에 올리고 GitHub Pages 활성화
5. `https://내아이디.github.io/저장소이름/` 으로 청첩장 완성!

---

## 1️⃣ 네이버 지도 API 키 발급 (5분)

1. https://www.ncloud.com 가입 (휴대폰 인증 필요)
2. 결제수단(카드) 등록 — **월 1,000만 건까지 무료**라 청첩장 용도로는 절대 비용 안 나옴
3. 콘솔 → **Services → Maps → Application 등록**
4. 이름 아무거나 (예: wedding), Web Dynamic Map / Geocoding 체크
5. **서비스 URL**에 본인이 사용할 GitHub Pages 주소 등록
   - 예: `https://username.github.io`
   - localhost 테스트용으로 `http://localhost`도 같이 등록해두면 편합니다
6. 등록 후 발급된 **Client ID** 복사

`index.html` 파일 26번째 줄 근처에 있는 이 부분을 찾아서:

```html
<script src="https://oapi.map.naver.com/openapi/v3/maps.js?ncpKeyId=YOUR_CLIENT_ID&submodules=geocoder"></script>
```

`YOUR_CLIENT_ID`를 발급받은 키로 바꿔주세요.

---

## 2️⃣ 청첩장 내용 수정

`index.html` 파일을 열면 모두 한국어로 주석이 달려 있습니다. 다음 항목들을 본인 정보로 바꿔주세요.

### 주요 수정 위치
| 항목 | 위치 | 비고 |
|---|---|---|
| 신랑신부 이름 | 커버 섹션 | 영문 + 한글 둘 다 |
| 결혼식 날짜 | 여러 곳 + `CONFIG.weddingDate` | D-day 자동 계산됨 |
| 인사말 | 인사말 섹션 | |
| 부모님 성함 | 인사말, 신랑신부 섹션 | |
| 캘린더 | 6월 → 본인 결혼월로 (날짜 배치도) | |
| 예식장 정보 | `CONFIG.venue` | **주소만 정확히 넣으면 지도 자동 표시** |
| 계좌번호 | 마음 전하실 곳 섹션 | |
| 연락처 | 신랑신부 섹션 `tel:` `sms:` | |

### 지도가 핵심 — 주소만 정확히!
```javascript
const CONFIG = {
    venue: {
        name: '아주컨벤션홀',
        address: '서울특별시 강남구 테헤란로 123',  // ← 이거만 정확하면 끝
    },
};
```
도로명 주소를 정확하게 입력하면 페이지 로드 시 자동으로 좌표를 찾아 핀이 꽂힙니다. 좌표를 직접 입력할 필요가 없습니다.

---

## 3️⃣ 사진 준비

`index.html`과 같은 위치에 **`images` 폴더**를 만들고 아래 파일명으로 사진을 넣어주세요.

```
wedding/
├── index.html
└── images/
    ├── main.jpg     ← 커버 메인 사진 (세로 길쭉, 1080x1920 추천)
    ├── groom.jpg    ← 신랑 프로필 (정사각형)
    ├── bride.jpg    ← 신부 프로필 (정사각형)
    ├── g1.jpg       ← 갤러리 1 (가로형, 큰 사이즈)
    ├── g2.jpg       ← 갤러리 2 (정사각형)
    ├── g3.jpg       ← 갤러리 3 (정사각형)
    ├── g4.jpg       ← 갤러리 4 (정사각형)
    └── g5.jpg       ← 갤러리 5 (정사각형)
```

> 💡 사진이 없어도 동작합니다 — 자동으로 그라데이션 색상으로 대체돼요.
> 💡 용량은 한 장당 500KB 이하로 압축하면 로딩이 빠릅니다 ([tinypng.com](https://tinypng.com) 추천)

---

## 4️⃣ GitHub Pages 배포

### A. GitHub 저장소 만들기
1. https://github.com 가입/로그인
2. 우측 상단 **+ → New repository**
3. 이름: `wedding` (자유롭게)
4. **Public** 선택 (Pages는 무료 계정에서 Public만 가능)
5. **Create repository**

### B. 파일 업로드
1. 생성된 저장소에서 **Add file → Upload files**
2. `index.html`과 `images` 폴더 통째로 드래그
3. **Commit changes**

### C. Pages 활성화
1. 저장소 **Settings** 탭
2. 좌측 메뉴 **Pages**
3. Source: **Deploy from a branch**
4. Branch: **main** / **/(root)** 선택 → **Save**
5. 1~2분 후 위쪽에 `Your site is live at https://username.github.io/wedding/` 표시됨

### D. 네이버 API에 URL 다시 등록
처음 받은 GitHub Pages 주소를 네이버 클라우드 콘솔의 Application → 서비스 URL에 추가해 주세요. 이거 빠뜨리면 지도가 인증 오류로 안 뜹니다.

---

## 🔧 수정하고 싶을 때

GitHub 저장소에서 `index.html`을 클릭 → 연필 아이콘 → 수정 → Commit changes
→ 1분 정도 후 자동 반영됩니다.

---

## ❓ 자주 발생하는 문제

**지도가 회색으로만 나와요**
→ 네이버 클라우드 콘솔의 Application **서비스 URL**에 GitHub Pages 주소가 등록되어 있는지 확인하세요. `https://`까지 정확하게.

**지도에 핀이 잘못된 위치에 꽂혀요**
→ `CONFIG.venue.address`의 도로명 주소를 더 자세히 적어주세요. (예: "강남구" → "서울특별시 강남구 테헤란로 123")

**사진이 다 깨져요**
→ 파일명 대소문자/확장자(.jpg vs .JPG) 정확히 맞는지 확인. `images` 폴더 안에 있는지도.

**카카오톡 공유 시 미리보기가 안 떠요**
→ HTML 상단의 `og:image` 경로가 절대 URL(https://...)이어야 합니다. 배포 후 본인 도메인으로 수정하세요.

---

축하드립니다! 🎉
