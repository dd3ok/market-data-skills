# market-data-skills

A lightweight catalog of Agent Skills for public market data workflows.

Each provider skill stays in its own canonical repository and can be installed
independently. This repository is a hub for discovery, routing, and shared
safety boundaries.

## Skills

| Skill | Use when | Canonical repository |
| --- | --- | --- |
| NaverStock API Skill | Korean stocks, ETFs, sectors, themes, news, and public read-only Naver Finance data | [dd3ok/naverstock-api-skill](https://github.com/dd3ok/naverstock-api-skill) |
| TossInvest API Skill | TossInvest public read-only stock, market, ranking, calendar, screener, news, and financial page data | [dd3ok/tossinvest-api-skill](https://github.com/dd3ok/tossinvest-api-skill) |
| Yahoo Finance Market Skill | Global market data through `yfinance`, including prices, charts, and financial statements | [dd3ok/yahoo-finance-market-skill](https://github.com/dd3ok/yahoo-finance-market-skill) |
| Binance API Skill | Binance Spot REST API work, official endpoint behavior, signing, rate limits, errors, and testnet-safe workflows | [dd3ok/binance-api-skill](https://github.com/dd3ok/binance-api-skill) |

## Install

Install only the provider skills you need.

```text
$skill-installer install https://github.com/dd3ok/naverstock-api-skill
$skill-installer install https://github.com/dd3ok/tossinvest-api-skill
$skill-installer install https://github.com/dd3ok/yahoo-finance-market-skill
$skill-installer install https://github.com/dd3ok/binance-api-skill
```

## Routing

Use the narrowest provider skill that matches the request:

- Korean public stock pages: start with NaverStock or TossInvest.
- TossInvest UI-specific market views: use TossInvest.
- Global equity and broad market data: use Yahoo Finance.
- Binance Spot API behavior, signing, and exchange metadata: use Binance.

See [docs/provider-matrix.md](docs/provider-matrix.md) for a fuller comparison.

## Safety

This collection is not an investment-advice system and is not a trading bot.

Provider skills should:

- prefer public or testnet-safe workflows by default
- avoid account-impacting actions unless a provider-specific skill explicitly
  supports them and the user explicitly asks
- avoid storing credentials, cookies, account IDs, private portfolio data, or raw
  session captures
- stop instead of bypassing rate limits, login walls, bot challenges, or access
  controls

See [docs/safety-boundaries.md](docs/safety-boundaries.md).

## Repository model

This hub intentionally does not merge the provider repositories into one
monorepo. Existing provider repositories keep their stars, issues, install
paths, and release history. This repository only explains how they fit together.
