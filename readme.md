# 2Miners API Documentation

[2Miners.com](https://2miners.com): cryptocurrency mining pools.

Interactive API documentation: [apidoc.2miners.com](https://apidoc.2miners.com)

## Base URL

Every pool has its own host:

- PPLNS: `https://<pool>.2miners.com/api`
- SOLO: `https://solo-<pool>.2miners.com/api`

Pools: `ae`, `bch`, `beam`, `ckb`, `erg`, `etc`, `ethw`, `grin`, `kas`, `mwc`, `nexa`, `prl`, `qtc`, `quaikawpow`, `quaisha`, `rvn`, `xna`, `zec`, `zeph` (PPLNS and SOLO each), and `solo-btc`.

## Endpoints

| Endpoint | Description |
|---|---|
| `GET /stats` | Pool hashrate, miners, block counters, round luck, node state |
| `GET /stats/region` | Pool hashrate by miners' country |
| `GET /miners` | Online miners |
| `GET /blocks` | Blocks found: candidates, immature, matured; luck over recent blocks |
| `GET /finders` | Latest blocks with their finders |
| `GET /payments` | Latest pool payouts and totals |
| `GET /accounts/{login}` | One miner: hashrate, workers, balances, payouts, rewards, payout settings |
| `GET /accounts/{login}/stats` | Balances and payout settings only |
| `GET /check/{login}` | Is the address known to the pool, last share |
| `GET /accounts/{login}/hashrates/{bucket}` | Account hashrate chart |
| `GET /accounts/{login}/shares/{bucket}` | Account shares chart (valid, invalid, stale) |
| `GET /accounts/{login}/settings` | Payout threshold and allowed range |
| `POST /accounts/{login}/settings` | Change the payout threshold (`{"ip", "key": "minPayout", "value"}`) |
| `GET /workers/{login}` | Workers with hashrate and share counters |
| `GET /workers/{login}/lastbeat` | Last share time per worker |
| `GET /workers/{login}/{worker}/hashrates/{bucket}` | Worker hashrate chart (measured and reported) |
| `GET /workers/{login}/{worker}/shares/{bucket}` | Worker shares chart |

`{bucket}` is `5m`, `30m` or `6h`.

## Things to know

- Amounts are integers in the coin's base unit (10^8 for most coins; see the table on the docs page).
- Node fields in `/stats` and some block rewards are strings: parse them as numbers.
- Hashrates are in H/s. Timestamps are Unix seconds, except `now` and `updatedAt` (milliseconds).
- Empty lists may come back as `null`.
- GRIN and MWC return `hashrate`, `currentHashrate` and the share counters as objects keyed by algorithm (`{"32": 192.56}`) and accept an optional `/{algo}` suffix on the chart endpoints.
- Every response carries `apiVersion: 200`. The old pre-200 format is gone from all pools.

## Contributing

API spec: [`2miners_api.json`](2miners_api.json) (OpenAPI 3.0).

Contributions welcome: open an issue or submit a PR at [github.com/2miners/apidoc](https://github.com/2miners/apidoc).
