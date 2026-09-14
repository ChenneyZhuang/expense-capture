---
name: expense-capture
description: |
  Turn receipts and invoices into ledger-ready expense rows without
  invention: transcribe each field (date, merchant, amount, currency, tax)
  exactly as the source shows it, flag unclear fields instead of guessing,
  state currency explicitly and show any conversion rate with its date,
  never assume tax from a total, and end the batch with a reconciliation —
  row count equals receipt count, stated totals equal recomputed totals.
  Use when processing receipts for bookkeeping or reimbursement, importing
  an expense batch into a ledger, splitting a shared bill, or auditing
  existing expense rows against their source images.
  触发词：报销 / 收据录入 / 记账凭证 / expense。
license: MIT
metadata:
  version: "0.1.0"
---

# Expense Capture: transcribe, flag, reconcile

The expensive failure in expense entry is invention — a misread total, a
guessed merchant, a tax assumed from a subtotal. Every field traces to the
source, or it is flagged.

## Rules

1. **Transcribe what is visible; flag what is not.** An unclear field
   becomes `unclear: <field>` inline — a visible flag beats an invisible
   guess, every time.
2. **The currency travels with the amount.** Amounts carry their symbol or
   currency code; conversions show the rate and the rate's date; a batch
   mixing currencies never reports one silent total.
3. **Tax is read, never derived.** Where the receipt separates tax, record
   it; where it does not, the tax field stays empty or flagged — deriving
   tax from a total invents a number the source never contained.
4. **Category from the ledger's own list.** The ledger's categories govern;
   an expense that fits none is a question for the user, not an improvised
   label that pollutes reports.
5. **Reconcile the batch before submitting.** Row count equals receipt
   count; the stated total equals the total recomputed from the rows; both
   are stated, so a mismatch is visible instead of discovered in audit.
6. **Writes happen after approval and are verified.** Ledger writes land in
   the ledger's own format after the user approves; a failed write is
   reported — a blind retry is how duplicate rows are born.

## Steps

1. **Inventory the sources.** List every receipt/invoice image with an ID;
   state the count. Done when: the count is explicit and no source is
   uncited.
2. **Transcribe.** One row per source: date, merchant, amount, currency,
   tax (as shown), category, flags. Done when: every row's fields trace to
   its source and every unclear field is flagged inline.
3. **Reconcile.** Recompute the batch total from the rows; compare against
   the sum read from the sources; state row count vs receipt count.
   Done when: both counts match and both totals match, or every mismatch
   is named with its row.
4. **Resolve or surface flags.** Re-check flagged fields against the image
   once; flags that survive go to the user as one batched question list.
   Done when: zero flags remain unresolved-and-unstated.
5. **Write and verify.** After approval, write the rows in the ledger's
   format and read them back. Done when: each approved row has a verified
   ledger result or an explicit failure report.

## Done when

Every row traces to a source image, zero fields were invented, the batch
reconciles on count and total, flags were surfaced rather than guessed
through, and approved rows are verified in the ledger.
