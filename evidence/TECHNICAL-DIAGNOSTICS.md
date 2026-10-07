# ChatGPT / Codex dot restriction: focused diagnostics

Collected from the installed desktop app and its local diagnostic logs on 7 October 2026.

## Environment

- App display name: ChatGPT; bundle identifier: `com.openai.codex`.
- App version: **26.930.61225**; build: **13232**.
- macOS **27.0.1**, build **26A434**; architecture **arm64**.
- Incident screenshot time: approximately **12:29 UTC** on 7 October 2026.
- Log extraction window: **12:25–12:34 UTC**.

## Observed local messaging events

The supplied screenshot shows a dot responding to a normal status question with an abuse-prevention limit warning. The local dot messaging pipeline records these events in the same minute:

| UTC | Stage | Logged outcome | Duration |
|---|---|---|---|
| 12:29:29.416 | `client.http_send` | started | — |
| 12:29:30.903 | `client.http_send` | success | 1486.7 ms |
| 12:29:31.604 | `client.first_response` | success | 2187.4 ms |
| 12:29:31.604 | `client.round_trip` | success | 2187.4 ms |
| 12:31:30.206 | `client.http_send` | started | — |
| 12:31:31.582 | `client.http_send` | success | 1376.2 ms |
| 12:31:32.399 | `client.first_response` | success | 2192.8 ms |

Every one of the **26** recorded `host.response_headers` events in the extraction window has `httpStatus=200` and `outcome=success`. No explicit abuse/quota/rate-limit event or non-200 Orbit response-header status appears in that selected window.

This is evidence that the desktop messaging transport completed. It does **not** establish which backend limit fired, that the account was wrongly classified, that delegated work stopped, or that the issue is resolved. Request-to-screenshot correspondence is inferred from time because the logs do not contain message text.

## Missing diagnostic information

The selected local logs do not expose the abuse-prevention decision, quota, reset timestamp, or upstream error code. A focused query of existing macOS unified logs in the same window produced no relevant dot/Orbit/abuse-limit event. The root cause therefore remains unconfirmed and requires OpenAI's backend investigation.

## Public evidence handling

The attached JSON uses allowlist extraction: timestamps, severity, component, stage, outcome, measurement, HTTP status and duration. It excludes message bodies, request/trace/client identifiers, account or conversation identifiers, URLs, local source paths, tokens, cookies, settings, session stores and unrelated events. The supplied screenshot was preserved unchanged except for redacted date-divider and read-indicator rows; its other visible conversation text is separate from this log packet.

No app settings, authentication, permissions, services or app state were changed. No native GUI control of ChatGPT/Codex was attempted.

## Official documentation context

OpenAI's [Meet dots documentation](https://learn.chatgpt.com/docs/dots), retrieved on 7 October 2026, states that dot conversations do not consume ChatGPT usage limits, while Work/Codex tasks use their respective product limits. That distinction does not by itself rule out separate abuse-prevention safeguards. The report asks OpenAI to explain the actual restriction, its reset and whether delegated work continues.
