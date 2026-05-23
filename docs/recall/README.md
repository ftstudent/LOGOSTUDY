# 문장 청킹 복습장

문장 독해 청킹 훈련을 위한 개인용 정적 웹앱 초안입니다.

## 기능

- 문장 등록: 원문, 해석, 언어, 난이도 1-4
- 여러 문장 일괄 등록: 기본 언어 선택 또는 줄별 언어 지정
- 문장 수정, 삭제
- 즐겨찾기
- 원문/해석 검색
- 추출 설정: 언어, 개수, 난이도, 즐겨찾기 필터
- 추출 기준: `reviewCount` 낮은 문장 우선, 같은 횟수 안에서는 랜덤
- 복습 화면: 원문 먼저 보기, 해석 확인, 복습 완료, 넘기기
- 복습 완료 시 `reviewCount + 1`
- 통계: 전체 문장 수, 미복습 수, 즐겨찾기 수, 최근 7일 복습 그래프, 언어/난이도별 수
- JSON 내보내기/가져오기
- GitHub Gist 자동 동기화

## 일괄 등록 형식

기본 언어를 선택한 뒤 아래 형식으로 붙여넣으면 됩니다.

```text
원문 | 해석 | 난이도
The claim depends on a hidden assumption. | 그 주장은 숨은 전제에 달려 있다. | 3
```

여러 언어를 한 번에 섞어 넣을 때는 줄 앞에 언어를 붙일 수 있습니다.

```text
es | Me di cuenta de que no era tan simple. | 그렇게 단순하지 않다는 걸 깨달았다. | 2
ja | 彼は何も言わずに部屋を出た。 | 그는 아무 말 없이 방을 나갔다. | 2
en | What matters is the condition under which it holds. | 중요한 것은 그것이 성립하는 조건이다. | 3
```

언어값은 `en`, `es`, `ja`, `fr`, `de`, `zh`, `ko`, `other` 또는 한국어 이름을 인식합니다.

## 로컬 실행

`index.html`을 브라우저로 열면 바로 사용할 수 있습니다.

```bash
cd /Users/ljw/sentence-chunk-trainer
python3 -m http.server 8080
```

그 다음 브라우저에서 `http://localhost:8080/`로 접속해도 됩니다.

## 데이터 저장과 기기 간 동기화

기본 데이터는 브라우저의 `localStorage`에 저장됩니다. 여러 기기에서 같은 문장을 이어 쓰려면 앱 안의 `GitHub 동기화` 카드를 설정하세요. 설정이 끝난 뒤에는 문장 등록, 수정, 삭제, 복습 기록이 GitHub Gist에 자동 저장되고, 페이지를 열 때 자동으로 병합됩니다.

### GitHub Gist 동기화 설정

1. GitHub에서 `Settings > Developer settings > Personal access tokens`로 이동합니다.
2. Fine-grained token 또는 classic token을 만들고, 가능한 한 `gist` 권한만 부여합니다.
3. 앱의 `GitHub 동기화` 카드에 토큰을 입력합니다.
4. 처음 쓰는 기기에서는 `새 Gist 만들기`를 누릅니다.
5. 다른 기기에서는 같은 토큰과 생성된 `Gist ID`를 한 번 입력하고 `설정 저장`을 누릅니다.

자동 동기화는 로컬 데이터와 GitHub 데이터를 병합한 뒤 다시 GitHub에 올립니다. 수동 `동기화`도 같은 동작입니다. `내려받기`는 GitHub 데이터로 현재 기기를 교체하고, `올리기`는 현재 기기 데이터로 GitHub 파일을 덮어씁니다.

토큰은 코드에 저장되지 않고 각 기기의 브라우저 `localStorage`에만 저장됩니다. 공용 기기에서는 쓰지 않는 편이 좋습니다.

중요한 문장 데이터는 가끔 화면 하단의 `JSON 내보내기`로도 백업해 두세요.

## GitHub Pages 배포

1. 이 폴더를 GitHub 저장소로 올립니다.
2. GitHub 저장소의 `Settings > Pages`로 이동합니다.
3. Source를 `Deploy from a branch`로 설정합니다.
4. Branch를 `main`, 폴더를 `/root`로 선택합니다.
5. 저장 후 표시되는 Pages 주소로 접속합니다.
