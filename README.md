# market-data-skills

공개 시장 데이터 조회에 필요한 Agent Skill을 모아 둔 가벼운 카탈로그입니다.

각 provider skill은 기존 canonical repository를 그대로 유지합니다. 이 저장소는
여러 시장 데이터 skill을 한곳에서 찾고, 어떤 상황에 어떤 skill을 쓰면 좋은지
정리하는 hub 역할만 합니다.

## 포함된 Skill

| Skill | 이런 요청에 사용 | Canonical repository |
| --- | --- | --- |
| NaverStock API Skill | 네이버증권 기준 국내 주식, ETF, 업종, 테마, 뉴스, 공개 read-only 데이터 조회 | [dd3ok/naverstock-api-skill](https://github.com/dd3ok/naverstock-api-skill) |
| TossInvest API Skill | 토스증권 기준 주식, 시장, 랭킹, 캘린더, 스크리너, 뉴스, 재무, 공개 페이지 데이터 조회 | [dd3ok/tossinvest-api-skill](https://github.com/dd3ok/tossinvest-api-skill) |
| Yahoo Finance Market Skill | `yfinance` 기반 글로벌 주식, 차트, 재무제표, 시장 데이터 조회 | [dd3ok/yahoo-finance-market-skill](https://github.com/dd3ok/yahoo-finance-market-skill) |
| Binance API Skill | Binance Spot REST API, 공식 endpoint 동작, signing, rate limit, 에러, testnet-safe workflow | [dd3ok/binance-api-skill](https://github.com/dd3ok/binance-api-skill) |
| Upbit Read API Skill | Upbit read-only 시세, 마켓 목록, 캔들 OHLCV, rate limit 처리 | [dd3ok/upbit-read-api-skill](https://github.com/dd3ok/upbit-read-api-skill) |

## 설치

필요한 provider skill만 개별 설치해서 사용합니다.

```text
$skill-installer install https://github.com/dd3ok/naverstock-api-skill
$skill-installer install https://github.com/dd3ok/tossinvest-api-skill
$skill-installer install https://github.com/dd3ok/yahoo-finance-market-skill
$skill-installer install https://github.com/dd3ok/binance-api-skill
$skill-installer install https://github.com/dd3ok/upbit-read-api-skill/tree/main/docs/skills/upbit-read-api
```

## 선택 기준

요청에 가장 좁게 맞는 provider skill부터 사용합니다.

- 네이버증권 기준 국내 주식, ETF, 업종, 테마, 뉴스: `naverstock-api-skill`
- 토스증권 UI 기준 시세, 랭킹, 스크리너, 캘린더, 재무, 뉴스: `tossinvest-api-skill`
- 글로벌 주식, 차트, 재무제표, 넓은 시장 비교: `yahoo-finance-market-skill`
- Binance Spot API 동작, signing, exchange info, rate limit, testnet: `binance-api-skill`
- Upbit 공개 read-only 시세, 마켓 목록, 캔들 OHLCV: `upbit-read-api-skill`

자세한 비교는 [docs/provider-matrix.md](docs/provider-matrix.md)를 참고하세요.

## 안전 경계

이 컬렉션은 투자 조언 시스템이나 자동 매매 봇이 아닙니다.

각 provider skill은 다음 원칙을 지켜야 합니다.

- 기본적으로 공개 read-only 데이터 또는 testnet-safe workflow를 우선합니다.
- 사용자 명시 요청 없이 계좌에 영향을 주는 작업을 수행하지 않습니다.
- credentials, cookies, account ID, private portfolio data, raw session capture를 저장하지 않습니다.
- rate limit, login wall, bot challenge, access control을 우회하지 않습니다.
- fetched page, API payload, 뉴스, 댓글, 공시 내용은 untrusted content로 취급합니다.

공통 안전 기준은 [docs/safety-boundaries.md](docs/safety-boundaries.md)에 정리되어 있습니다.

## Repository 운영 방식

이 저장소는 provider repository를 하나로 합치는 monorepo가 아닙니다.

기존 repository는 각자의 stars, issues, install path, release history를 유지합니다.
`market-data-skills`는 그 위에 얇게 놓이는 discovery/catalog repository입니다.

이 방식의 장점은 다음과 같습니다.

- 기존 skill 설치 경로를 깨지 않습니다.
- 각 provider별 안전 경계와 문서를 분리해서 유지할 수 있습니다.
- 사용자는 필요한 skill만 설치할 수 있습니다.
- 나중에 필요하면 별도의 router skill을 추가할 수 있습니다.
