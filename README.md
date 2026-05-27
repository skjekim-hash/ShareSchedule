# 🌙 우리의 달력 — 커플 공유 캘린더

남편과 아내가 함께 일정을 공유하는 심플한 웹 캘린더입니다.  
GitHub Pages에 올리고 Firebase를 연동하면 실시간으로 일정이 동기화됩니다.

---

## ✨ 기능

- 📅 월별 달력 보기 + 이전/다음 달 이동
- ➕ 이름, 날짜, 시간으로 일정 추가
- 👨 남편 / 👩 아내 / 💑 같이 — 색상으로 구분
- 🔄 Firebase 연동 시 실시간 공유 (두 기기에서 동시에 반영)
- 💾 Firebase 미설정 시 로컬 저장 모드로 동작
- 🗑️ 일정 삭제 (클릭 후 확인)

---

## 🚀 배포 방법

### 1단계 — GitHub Pages 설정

1. GitHub에 새 저장소(repository)를 만드세요.
2. `index.html`을 저장소에 업로드하세요.
3. **Settings → Pages → Source: Deploy from a branch → main / (root)** 선택
4. 잠시 후 `https://[아이디].github.io/[저장소명]/` 주소로 접속 가능!

---

### 2단계 — Firebase 설정 (실시간 공유 필수)

Firebase를 설정하면 남편과 아내 기기에서 **동시에 실시간으로** 일정이 공유됩니다.

#### 2-1. Firebase 프로젝트 만들기

1. [https://console.firebase.google.com/](https://console.firebase.google.com/) 접속
2. **프로젝트 추가** 클릭 → 이름 입력 (예: `couple-calendar`)
3. Google Analytics는 선택 사항 (꺼도 됩니다)

#### 2-2. Firestore Database 만들기

1. 왼쪽 메뉴 **Firestore Database** → **데이터베이스 만들기**
2. **테스트 모드로 시작** 선택 (나중에 보안 규칙 수정 가능)
3. 위치: `asia-northeast3 (Seoul)` 권장

#### 2-3. 웹 앱 등록 및 설정 복사

1. 프로젝트 설정(⚙️) → **앱 추가** → 웹(`</>`) 선택
2. 앱 닉네임 입력 후 **앱 등록**
3. `firebaseConfig` 코드 블록을 복사

#### 2-4. index.html에 설정 붙여넣기

`index.html` 파일에서 아래 부분을 찾아 교체:

```javascript
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",          // ← 여기 교체
  authDomain:        "YOUR_PROJECT_ID.firebaseapp.com",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID",
};
```

교체 후 GitHub에 다시 업로드(push)하면 완료!

---

### 3단계 — Firestore 보안 규칙 (선택)

테스트 모드는 30일 후 만료됩니다. 영구 사용을 원하면:

Firestore → **규칙** 탭에서 아래로 교체:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /events/{eventId} {
      allow read, write: if true;
    }
  }
}
```

> 💡 더 안전하게 하려면 Firebase Authentication을 추가해 특정 이메일만 허용할 수 있습니다.

---

## 📱 사용 방법

1. 브라우저에서 GitHub Pages 주소 열기
2. 아내에게 같은 주소 공유
3. 일정 이름 / 날짜 / 시간 입력 후 누구의 일정인지 선택 → **일정 추가하기**
4. 두 기기에서 실시간으로 반영됩니다 ✨

---

## 🛠 로컬에서 테스트하기

별도 서버 없이 `index.html`을 브라우저로 바로 열면 **로컬 저장 모드**로 동작합니다.  
(같은 기기, 같은 브라우저에서만 저장 — 공유는 안 됨)

---

## 📁 파일 구조

```
couple-calendar/
└── index.html   ← 모든 것이 하나의 파일에
└── README.md
```

---

Made with 💑
