# CKD News Monitor - GitHub Pages 초기 구축

## 1. GitHub 저장소 생성

1. GitHub에서 새 repository 생성
2. 예: `ckd-news-public`
3. Public repository 권장
4. 아래 파일 업로드
   - `index.html`
   - `data/public_news.json`

## 2. GitHub Pages 켜기

Repository → Settings → Pages

- Source: Deploy from a branch
- Branch: `main`
- Folder: `/root`
- Save

## 3. GitHub Token 생성

Fine-grained personal access token 권장.

필요 권한:

- Repository access: 방금 만든 repository 1개만 선택
- Contents: Read and write

토큰은 절대 GitHub Pages 파일이나 public_news.json에 넣지 말고, Apps Script Script Properties에만 저장.

## 4. Apps Script Exporter 생성

새 Apps Script 프로젝트 생성 후 `apps_script_export_public_news.gs` 전체 붙여넣기.

처음 실행 순서:

1. `setupPublicNewsExporter`
2. Script Properties 입력
3. `testBuildPublicNewsJson`
4. `exportPublicNewsToGitHub`
5. `createPublicNewsExportHourlyTrigger`

## 5. Script Properties

필수:

```text
GITHUB_TOKEN = GitHub fine-grained PAT
GITHUB_OWNER = GitHub 아이디 또는 조직명
GITHUB_REPO = ckd-news-public
GITHUB_BRANCH = main
PUBLIC_JSON_PATH = data/public_news.json
FAMILY_SHEET_ID = 가족사 뉴스 Google Sheet ID
PORTFOLIO_SHEET_ID = 피투자사 뉴스 Google Sheet ID, 없으면 빈칸
```

선택:

```text
FAMILY_KEYWORDS = 종근당,종근당홀딩스,종근당건강,종근당바이오,경보제약
PORTFOLIO_KEYWORDS = BIOMX,LYELL,OPUS,Opus Genetics,이엔셀,ENCell,앱클론,AbClon
PUBLIC_MAX_ITEMS = 500
```

## 6. 공개 데이터에 포함되는 필드

- category
- companies
- title
- summary
- source
- link
- publishedAt
- publishedText
- sentAt

아래 정보는 공개 JSON에 포함하지 않음.

- gemini_reason
- matched_issue_id
- 메일 수신자/참조자
- Script Properties
- API Key / GitHub Token
