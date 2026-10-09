---
name: invoice-checker
description: Checks incoming vendor invoices for missing mandatory fields, wrong VAT calculations and possible duplicates before they are booked, and returns a short pass/fail report. Use when the user shares an invoice (PDF, image or text) or asks to check, validate or review one.
---

# Invoice Checker

Review a vendor invoice and report what is wrong before it gets booked.

## Checks

**1. Mandatory fields** (Dutch invoice requirements)
- Invoice number (unique, sequential) and invoice date
- Supplier name, address, VAT number (BTW-id) and KvK number
- Apolix's name and address as the customer
- Description and quantity of goods or services, and date of delivery
- Amount excl. VAT, VAT rate, VAT amount and total
- For reverse charge (EU B2B): the customer's VAT number and the text "BTW verlegd" / "VAT reverse charged"

**2. Calculations**
- Each line: quantity × unit price = line total
- VAT amount = net amount × rate, using 21%, 9% or 0% (round per line or per invoice, but consistently)
- Net + VAT = total

**3. Duplicates and red flags**
- Same supplier + same invoice number or same amount and date as an invoice the user has mentioned
- Bank account (IBAN) different from earlier invoices of the same supplier, which is a common fraud signal
- Missing PO number when the user says one is required

## Output

Start with one line: **✅ Ready to book** or **⚠️ Needs attention**. Then a short table of issues (field, problem, what to do). Only list problems; don't repeat fields that are fine. If the invoice is unreadable or a page is missing, say so instead of guessing.
