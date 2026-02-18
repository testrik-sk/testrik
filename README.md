# 🚀 테스트릭(Testrik) 배포 가이드

## 📁 프로젝트 구조
```
testrik/
├── index.html          ← 메인 웹사이트 (전체 사이트가 이 파일 하나)
├── README.md           ← 이 가이드
└── (추후 추가)
    ├── sitemap.xml     ← 검색엔진 등록용
    └── robots.txt      ← 검색엔진 크롤링 허용
```

---

## 🌐 STEP 1: 도메인 구매 (선택사항, 연 ₩11,000~)

도메인이 없어도 Vercel이 `프로젝트명.vercel.app` 주소를 무료로 제공합니다.
하지만 수익화를 위해서는 **커스텀 도메인을 강력 추천**합니다.

### 추천 도메인 등록 업체
| 업체 | 가격 (연간) | 특징 |
|------|------------|------|
| **Namecheap** | ~₩12,000 | 가장 저렴, 영문 |
| **가비아** | ~₩16,500 | 한국 업체, 한국어 지원 |
| **Cloudflare** | ~₩11,000 | 원가 판매, 가장 저렴 |

### 추천 도메인 이름
- `testrik.com` (메인)
- `testrik.co.kr` (한국 대상)
- `테스트릭.kr` (한글 도메인)

---

## 🖥️ STEP 2: Vercel에 배포하기 (무료)

### 방법 A: GitHub를 통한 배포 (추천 ⭐)

1. **GitHub 가입**: https://github.com 에서 계정 생성

2. **새 저장소 만들기**:
   - 오른쪽 상단 `+` → `New repository` 클릭
   - Repository name: `testrik`
   - Public 선택 → `Create repository` 클릭

3. **파일 업로드**:
   - `uploading an existing file` 링크 클릭
   - `index.html` 파일을 드래그해서 업로드
   - 하단 `Commit changes` 클릭

4. **Vercel 연결**:
   - https://vercel.com 접속 → `Sign Up` → `Continue with GitHub` 선택
   - `Add New Project` 클릭
   - `testrik` 저장소 선택 → `Import`
   - Framework Preset: `Other` 선택
   - `Deploy` 클릭!
   
5. **완료!** 🎉
   - 배포 완료되면 `testrik.vercel.app` 주소가 생성됩니다

### 방법 B: Vercel 직접 업로드 (더 간단)

1. https://vercel.com 가입
2. https://vercel.com/new 접속
3. 하단 `Browse` 또는 파일 드래그
4. `testrik` 폴더 전체를 업로드
5. `Deploy` 클릭 → 끝!

---

## 🔗 STEP 3: 커스텀 도메인 연결

1. Vercel 대시보드 → 프로젝트 → `Settings` → `Domains`
2. 구매한 도메인 입력 (예: `testrik.com`)
3. Vercel이 보여주는 DNS 설정을 도메인 업체에서 적용:
   ```
   A Record: 76.76.21.21
   CNAME: cname.vercel-dns.com
   ```
4. 10~30분 후 적용 완료

---

## 💰 STEP 4: 수익화 설정

### 1. Google AdSense 가입
1. https://adsense.google.com 접속
2. 웹사이트 URL 입력 (도메인 필요)
3. AdSense 코드를 `index.html` 의 `<head>` 안에 삽입
4. 승인까지 보통 1~7일 소요

**index.html에서 수정할 부분:**
```html
<!-- 이 주석을 찾아서 본인의 AdSense ID로 교체 -->
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-여기에본인ID" crossorigin="anonymous"></script>
```

> ⚠️ AdSense 승인 조건: 
> - 독자적인 콘텐츠가 있을 것
> - 개인정보처리방침 페이지가 있을 것
> - 일정 수준의 트래픽이 있을 것

### 2. 쿠팡 파트너스
1. https://partners.coupang.com 가입
2. 테스트 결과에 맞는 상품 링크 생성
3. 결과 페이지의 "스폰서" 영역에 링크 삽입

### 3. Google Analytics (트래픽 추적)
1. https://analytics.google.com 접속
2. 속성 생성 → 측정 ID 발급 (G-XXXXXXXXXX)
3. `index.html` `<head>` 에 코드 삽입:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-여기에ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-여기에ID');
</script>
```

### 4. 카카오톡 공유 기능
1. https://developers.kakao.com 가입
2. 앱 생성 → JavaScript 키 발급
3. `index.html` `<head>` 에 추가:
```html
<script src="https://t1.kakaocdn.net/kakao_js_sdk/2.7.4/kakao.min.js"></script>
<script>Kakao.init('여기에_JavaScript_키');</script>
```
4. `shareKakao()` 함수를 아래로 교체:
```javascript
function shareKakao() {
  Kakao.Share.sendDefault({
    objectType: 'feed',
    content: {
      title: '테스트릭 - ' + quiz.title,
      description: '내 결과를 확인해보세요!',
      imageUrl: 'https://testrik.com/og-image.png',
      link: { mobileWebUrl: location.href, webUrl: location.href }
    },
    buttons: [{
      title: '나도 테스트하기',
      link: { mobileWebUrl: location.href, webUrl: location.href }
    }]
  });
}
```

---

## 📈 STEP 5: 검색엔진 등록 (SEO)

### Google Search Console
1. https://search.google.com/search-console 접속
2. 도메인 추가
3. 사이트맵 제출: `https://testrik.com/sitemap.xml`

### 네이버 서치어드바이저
1. https://searchadvisor.naver.com 접속
2. 사이트 등록
3. `<meta>` 태그 인증

### SEO 체크리스트
- [x] `<title>` 태그 설정 ✅
- [x] `<meta description>` 설정 ✅
- [x] Open Graph 태그 설정 ✅
- [ ] `sitemap.xml` 생성 (추후 테스트 추가 시)
- [ ] OG 이미지 제작 (결과 공유용 이미지)

---

## 📱 STEP 6: 트래픽 확보 전략

### 초기 (0~1개월)
1. **카카오톡/인스타그램 공유 최적화** — 결과 이미지가 핵심
2. **에브리타임/디시인사이드** — 대학생 커뮤니티에 공유
3. **인스타그램 릴스** — 테스트 결과를 영상으로 제작

### 성장기 (1~3개월)
4. **네이버 블로그** — "심리테스트 추천" 키워드로 SEO 글 작성
5. **틱톡** — 테스트 결과 리액션 영상
6. **트위터/스레드** — 테스트 결과 공유 바이럴

### 확장기 (3개월~)
7. **새 테스트 주 1회 추가** — 신규 트래픽의 핵심
8. **시즌 테스트** — 크리스마스, 밸런타인 등 이벤트성
9. **브랜드 협업** — 기업 맞춤 테스트 제작 수주

---

## 🔧 유지보수 & 업데이트

### 새 테스트 추가하는 법
`index.html` 의 `tests` 배열에 새 객체를 추가하면 자동으로 카드가 생성됩니다:

```javascript
{
  id: 'new-test-id',
  cat: '심리',              // 카테고리
  badge: 'new',            // hot, new, ai, pop
  badgeText: '✨ NEW',
  gradient: 'linear-gradient(135deg, #색상1, #색상2)',
  icon: '🎭',
  title: '새로운 테스트 제목',
  desc: '테스트 설명',
  plays: '0만',
  time: '2분',
  introDesc: '인트로 설명...',
  questions: [
    { q: '질문 내용', opts: [
      { t: '선택지 텍스트', s: 'result_key' },
      // ...
    ]}
  ],
  results: {
    result_key: {
      icon: '🎭',
      type: '결과 유형 이름',
      sub: '부제목',
      tags: ['태그1', '태그2'],
      text: '결과 설명...',
      good: '잘 맞는 유형',
      bad: '주의할 유형'
    }
  }
}
```

---

## 💡 핵심 수익화 포인트 정리

| 수익원 | 예상 시기 | 월 예상 수익 |
|--------|-----------|-------------|
| Google AdSense | 1~2개월 후 | 일 트래픽 1만 기준 ₩30~100만 |
| 쿠팡 파트너스 | 즉시 가능 | ₩5~30만 |
| 프리미엄 결과 유료화 | 트래픽 확보 후 | 구매율 1% 기준 ₩10~50만 |
| 브랜드 협업 | 3개월 후 | 건당 ₩200~500만 |

> 수익은 트래픽에 비례합니다. 핵심은 **바이럴되는 콘텐츠**를 꾸준히 만드는 것!

---

## ❓ FAQ

**Q: 코딩을 몰라도 운영할 수 있나요?**
A: 네! 위 가이드대로 따라하면 배포 가능합니다. 새 테스트 추가 시에는 Claude에게 질문 데이터를 만들어달라고 요청하면 됩니다.

**Q: 서버 비용이 드나요?**
A: Vercel 무료 플랜으로 월 100GB 대역폭까지 무료입니다. 일반적인 테스트 사이트라면 충분합니다.

**Q: AdSense 승인이 안 되면?**
A: 개인정보처리방침 페이지 추가, 콘텐츠 양 증가 (테스트 10개 이상), 일정 기간 운영 후 재신청하세요.

**Q: 모바일에서도 잘 보이나요?**
A: 네, 반응형으로 제작되어 모바일/태블릿/PC 모든 환경에서 최적화됩니다.

---

*이 가이드는 테스트릭 프로젝트를 위해 작성되었습니다.*
*추가 질문은 Claude에게 언제든 물어보세요! 🤖*
