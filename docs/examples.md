# Examples

What a conversation with the didlogic MCP server looks like. The assistant
finds the operations itself with `search` and `get_schema`; you only describe
what you want.

## Check balance and spend

> **You:** What's my balance, and how much did I spend on calls in October?
>
> **Assistant:** Your balance is $412.80. Outbound and inbound calls in
> October cost $86.15 across 1,240 calls; the largest share, $51.30, went to
> United States destinations.

The assistant reads the balance, then pages through October's call history in
one `execute` and adds the amounts up, returning only the totals.

## Buy a number, with a price check first

> **You:** I need a London number.
>
> **Assistant:** I found 25 available London numbers. +44 20 3XXX XXXX costs
> $1.00 setup and $1.00 a month. Buying it charges your balance now. Shall I
> buy it?
>
> **You:** Yes.
>
> **Assistant:** Done. +44 20 3XXX XXXX is yours. Where should its calls go?

Purchases, SMS and calls cost money, so the assistant states the price and
waits for a yes before it acts.

## Route a number to a SIP account

> **You:** Forward my US number to the SIP account `office`.
>
> **Assistant:** +1 800 XXX XXXX now forwards to `office`. It previously had no
> destination.

## Investigate missed calls

> **You:** Show yesterday's missed calls on my German numbers.
>
> **Assistant:** 7 missed calls yesterday on your two German numbers, 5 of them
> between 12:00 and 13:00 on +49 30 XXX XXXX. Callers and times: …

## Set up a SIP account

> **You:** Create a SIP account for the Berlin office and allow only
> 203.0.113.10.
>
> **Assistant:** Created SIP account `berlin` with a generated password, and
> restricted it to 203.0.113.10. Here are the settings for your phone system: …

## Send an SMS

> **You:** Text +44 7700 900123: "The meeting moved to 3 pm."
>
> **Assistant:** This sends one SMS to the United Kingdom for $0.04. Send it?
>
> **You:** Go ahead.
>
> **Assistant:** Sent. Message ID 81234, status: delivered to the carrier.

## Answer-rate report

> **You:** Which countries had the worst answer rate this week?
>
> **Assistant:** From the ASR report for Monday to today: Nigeria 21%,
> Pakistan 34%, Bangladesh 38%. Everything else is above 50%.

Numbers, prices and IDs above are illustrative. Your assistant answers from
your own account.
