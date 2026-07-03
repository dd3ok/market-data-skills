# Provider matrix

Use this table to pick the narrowest market-data skill for a request.

| Request shape | Prefer | Why |
| --- | --- | --- |
| Korean stock quote, ETF, sector, theme, domestic market news | NaverStock API Skill | Naver Finance is a natural source for Korean market pages and public stock context. |
| TossInvest quote, ranking, screener, calendar, theme, public page endpoint re-check | TossInvest API Skill | TossInvest page data and observed public web endpoints are provider-specific. |
| US/global stock prices, charts, fundamentals, broad market comparisons | Yahoo Finance Market Skill | `yfinance` is convenient for global market data and non-provider-specific research. |
| Binance Spot REST endpoint behavior, exchange info, rate limits, signing, testnet | Binance API Skill | Binance has its own official API model, request signing, filters, and error semantics. |
| Upbit current ticker prices, quote-currency market lists, candles/OHLCV, rate-limit handling | Upbit Read API Skill | Upbit quotation endpoints have their own market-code shape, candle behavior, and `Remaining-Req` rate-limit header. |
| Cross-provider comparison | Start with the provider that owns the most specific source, then corroborate with another skill if needed | Avoid mixing source semantics before the primary source is clear. |

## Provider notes

### NaverStock

- Best for Korean market pages and public read-only Naver Finance data.
- Keep it separate from TossInvest because page structure, identifiers, and
  endpoint stability differ.

### TossInvest

- Best for TossInvest UI-specific data and observed public read-only endpoints.
- Keep unofficial web endpoint safety rules close to this provider skill.

### Yahoo Finance

- Best for broad global market data where a single exchange-specific provider is
  not required.
- Treat `yfinance` behavior as library-mediated data access, not an official
  broker API.

### Binance

- Best for exchange API behavior, signing rules, filters, and testnet-safe
  workflows.
- Keep Binance separate because it can cross from public data into signed,
  account-impacting API surfaces if boundaries are weak.

### Upbit

- Best for Upbit read-only quotation data: current ticker snapshots, quote-market
  ticker lists, and candle OHLCV.
- Keep it separate from Binance because Upbit uses different market codes,
  endpoint groups, candle retention behavior, and rate-limit headers.
- Current canonical repository: `dd3ok/upbit-read-api-skill`.

## Collection rule

This hub should stay a catalog. If a provider needs scripts, references, tests,
or safety policy, place them in that provider's canonical repository.
