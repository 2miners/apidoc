# 2Miners API Documentation

[2Miners.com](https://2miners.com) — Modern cryptocurrency mining pools.

Interactive API documentation: [apidoc.2miners.com](https://apidoc.2miners.com)

## Endpoints

| Endpoint | Description |
|---|---|
| `GET /accounts/{walletid}` | Account info, hashrate, payments, rewards, workers |
| `GET /accounts/{walletid}/shares/{range}` | Account share stats by time range (`5m`, `30m`, `6h`) |
| `GET /blocks` | Pool blocks (candidates, immature, matured) |
| `GET /miners` | All active miners |
| `GET /payments` | Pool payment history |
| `GET /stats` | Pool statistics, network info, charts |
| `GET /workers/{walletid}/{workerid}/{range}` | Worker hashrate by time range (`5m`, `30m`, `6h`) |

## Supported Pools

PPLNS and SOLO pools for: ETHW, ETC, KAS, ERG, NEXA, ZEC, BTG, ZEPH, RVN, NEOX, XNA, GRIN, MWC, CTXC, AE, BEAM, CKB, BCH, QUAI.

### Coins without `apiVersion: 200`

GRIN, BEAM, AE, MWC — these coins use a different response format:

- `hashrates` / `currentHashrates` are maps keyed by algorithm number (e.g. `{"32": 506.99}`)
- `charts` are maps keyed by algorithm number
- Payments include `txFee` and `txKernelExcess` fields
- Rewards include `orphan` field
- Nodes include `minDiff`, `primaryWeight31` / `primaryWeight32` fields

## Contributing

API spec: [`2miners_api.json`](2miners_api.json) (OpenAPI 3.0)

Contributions welcome — open an issue or submit a PR at [github.com/2miners/apidoc](https://github.com/2miners/apidoc).
