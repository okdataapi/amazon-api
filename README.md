# Amazon API: product search, product details, reviews and Best Sellers

**Amazon product data API · Amazon product search · Amazon product details · Amazon reviews · Amazon Best Sellers.**

Examples for the [okdata](https://okdata.online/?src=gh-amazon-api) Amazon API: 4 live endpoints behind one API key, pay per call from $0.006. No Amazon login, no cookies and no browser, so there is no account to get blocked.

[Sign up free ($0.10 of trial credit)](https://okdata.online/signup/?src=gh-amazon-api) · [All Amazon endpoints](https://okdata.online/apis/amazon/?src=gh-amazon-api) · [Use it from Claude, Cursor or any MCP client](https://okdata.online/mcp/?src=gh-amazon-api)

## Endpoints

| Endpoint | What it returns | Price | Path |
|---|---|---|---|
| [Amazon product search](https://okdata.online/apis/amazon/products/search/) | Search an Amazon store by keyword, as a shopper sees the results: title, price and list price, star rating, number of ratings, units bought last month, Prime, Best Seller and Amazon's Choice badges, and the photo. | $0.006 a call | `GET /v1/amazon/products/search` |
| [Amazon product details](https://okdata.online/apis/amazon/products/get/) | One Amazon product by ASIN: title, price and list price, rating and number of ratings, units bought last month, all photos, brand, the "About this item" bullets, category path and Best Sellers Rank. | $0.006 a call | `GET /v1/amazon/products/get` |
| [Amazon product reviews](https://okdata.online/apis/amazon/products/reviews/list/) | Customer reviews of an Amazon product: stars, title and text, date, the variant bought, photos, helpful votes and whether the purchase is verified. | $0.006 a call | `GET /v1/amazon/products/reviews/list` |
| [Amazon Best Sellers](https://okdata.online/apis/amazon/bestsellers/list/) | An Amazon Best Sellers list for a category, in rank order: rank, title, price, rating, number of ratings and photo. Also New Releases, Movers & Shakers, Most Wished For and Gift Ideas. | $0.006 a call | `GET /v1/amazon/bestsellers/list` |

## Quick start

1. Sign up at the [okdata console](https://okdata.online/signup/?src=gh-amazon-api) with your email and copy the key that starts with `okd_`.
2. Make a call:

```bash
export OKDATA_API_KEY=okd_...
curl -G "https://api.okdata.online/v1/amazon/products/search" \
  -H "Authorization: Bearer $OKDATA_API_KEY" \
  --data-urlencode 'query=portable espresso maker'
```

The Python version is [examples/quickstart.py](examples/quickstart.py) (standard library only, and it fetches a second page too): `python3 examples/quickstart.py`.

Every endpoint answers in the same shape: the list is in `data.items`, `page.next_cursor` goes back as `cursor` for the next page, what the call cost is in `meta.billing.amount`, and a field the platform does not provide is null with the reason in `meta.unavailable`.

## Use it from AI (MCP)

Claude Code:

```bash
claude mcp add --transport http --scope user okdata https://api.okdata.online/mcp --header "Authorization: Bearer $OKDATA_API_KEY"
```

Cursor, Windsurf, VS Code and other clients with remote MCP:

```json
{
  "mcpServers": {
    "okdata": {
      "url": "https://api.okdata.online/mcp",
      "headers": {
        "Authorization": "Bearer okd_..."
      }
    }
  }
}
```

Then ask in plain words, for example "Amazon product search: portable espresso maker". The agent uses the free `find` and `describe` tools to pick the endpoint and see its price, then `call` to fetch the data.

## FAQ

**Do I need a Amazon account?** No. The data is public content, fetched on the server; your own account is never involved.

**How is it billed?** Each endpoint has its own price, listed above for one call; endpoints billed per item count what comes back. New accounts get $0.10 to try; after that, top-ups start at $10 and never expire, with no subscription. Pricing: https://okdata.online/pricing/ · Billing details: https://okdata.online/docs/billing/

**Can I page through results?** Each page of a list is one call: pass `page.next_cursor` back as `cursor` for the next one. A cursor stays valid for 24 hours.

**What happens when a call fails?** Every error has a fixed `code`, a `message`, and says whether you were charged (`charged`) and whether to retry (`retry`). All error codes: https://okdata.online/docs/errors/

## 中文说明

**亚马逊数据 API · 亚马逊商品搜索 · 亚马逊商品详情 · 亚马逊评论采集 · 亚马逊畅销榜。**

okdata 的亚马逊接口示例：4 个接口在线可用，一个 API Key 调用，按次计费（$0.006 起），不用登录平台账号、不用 Cookie。中文文档：https://okdata.online/zh/apis/amazon/?src=gh-amazon-api · 注册：https://okdata.online/zh/signup/?src=gh-amazon-api · 接入 AI（MCP）：https://okdata.online/zh/mcp/?src=gh-amazon-api

## License

MIT. The data comes from the okdata API; its terms apply to API use.
