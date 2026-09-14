# expense-capture 报销捕获

Receipts become ledger rows — with every field traceable to the source image and nothing guessed.

收据变成账本行——每个字段都能追溯到原图，绝不脑补。

## Why / 为什么

Expense entry has one expensive failure mode: **invention**. A misread total, a guessed merchant name, a tax amount assumed from the subtotal — each one is a small reconciliation nightmare and, in an audit, a credibility problem. The discipline is mechanical: transcribe what is visible, flag what is not, reconcile the batch at the end.

报销录入只有一种昂贵的失败：**编造**。看错总额、猜商家名、从小计倒推税额——每一个都是一次对账噩梦，在审计里是信用问题。纪律是机械的：看见什么抄什么，看不见的标记，最后整体对账。

## Field discipline / 字段纪律

| Field | Rule |
|---|---|
| date | as printed; different formats resolved explicitly |
| merchant | exactly as shown; abbreviations kept, expansions marked as guesses |
| amount | the charged amount as printed; the currency symbol travels with it |
| currency | stated explicitly; mixed-currency batches convert with the rate and rate date shown |
| tax | only when the receipt separates it; assuming tax from a total is a flagged guess |
| category | from the ledger's own category list; unclear cases ask, never improvise |

## The batch loop / 批处理闭环

1. Transcribe each receipt into a row, flags inline (`unclear: merchant`).
2. Reconcile: row count == receipt count; sum of rows == sum read from the receipts (stated both ways).
3. Re-verify flagged fields against the image once more before submitting; a flag that cannot be resolved stays a flag for the user.
4. Ledger writes happen after approval, in the ledger's own format — and a row that fails to write is reported, not retried blind (blind retries create duplicates).

## Install / 安装

```bash
npx skills add ChenneyZhuang/expense-capture
```

Per-agent paths: [COMPATIBILITY.md](COMPATIBILITY.md). MIT. v0.1.0.

各 agent 安装路径见 COMPATIBILITY.md。MIT 许可，v0.1.0。
