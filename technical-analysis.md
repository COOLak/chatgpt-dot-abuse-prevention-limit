# Evidence and technical boundaries

Last updated: **October 7, 2026**. Status: **unresolved**.

## Recorded sequence

The owner supplied a desktop screenshot showing an ongoing ChatGPT dot conversation. The relevant sequence is:

1. The dot had previously provided progress updates about an ongoing workflow.
2. Under a date divider (October 7, 12:29 UTC; divider redacted in the published screenshot), the user asked: **“What's currently going on?”**
3. The dot replied: **“Your dot is on a break. Congrats you are in the very top users and have hit our abuse prevention limit. Check back in a bit!”**
4. The user replied **“Really?”** The original screenshot shows a read indicator at 12:31 UTC (redacted in the published copy), but no subsequent useful dot response.

Screenshot times are given here in UTC; the date dividers and read indicator, which carry the device clock, are redacted in the published screenshot. They are screenshot observations, not authenticated backend event timestamps. They do not establish when a limit began or will reset.

## Observation versus inference

| Claim | Evidence status |
|---|---|
| An ordinary status request received a limit notice | Directly visible in the supplied screenshot |
| The notice mentions “abuse prevention” and “very top users” | Directly visible product wording |
| No numerical threshold, reset time or meter appears in that notice | Directly visible omission in the quoted response |
| The user actually committed abuse | **Not established** by the product wording |
| A particular quota, anti-abuse rule or entitlement fault caused the response | **Unknown**; no backend accounting readback |
| Delegated work stopped or kept running | **Unknown**; screenshot is not task-state telemetry |
| Work or state was lost | **Not established** |
| The current incident shares #51540's root cause | **Not established**; identical message supports symptom corroboration |
| Waiting, restarting or switching accounts fixes this incident | **Not verified**; no such remedy is claimed |

## Reproduction boundary

This is a minimal description of the **observed sequence**, not a fresh isolated reproduction:

1. Use a ChatGPT dot during an ongoing workflow.
2. Ask for a status update.
3. Observe whether the quoted availability notice replaces the response.

No required consumption threshold, number of turns or elapsed work duration is known. The report does not ask other users to exhaust capacity deliberately or to circumvent an anti-abuse control.

## Public corroboration

[openai/codex#51540](https://github.com/openai/codex/issues/51540), by a different user, records the same notice on October 6 in America/New_York. Its author reports later useful responses, but those times describe that user's observation and are **not a reset policy for this incident**.

The issue was verified open on October 7 with the labels `enhancement`, `rate-limits`, `app` and `dots`. An issue label is a triage signal, not a backend diagnosis. The existing Codex App template asks users to consolidate matching reports; this incident will contribute its own evidence to that thread rather than claim a newly proven defect mechanism.

## Product documentation

The official [dot guide](https://learn.chatgpt.com/docs/dots) distinguishes dot conversations from deeper work and from work using ChatGPT Work or Codex allowances. The report does not equate those allowances or assert unlimited computation.

The relevant gap is the notice's failure to identify which allowance or restriction applies, how users can inspect its state, and when useful interaction can resume.

## Diagnostics

The public diagnostic packet excludes raw application logs and message bodies; the screenshot is published unchanged except for redacted date-divider and read-indicator rows, including earlier visible progress context. A bounded local diagnostic found 26 Orbit response-header records with HTTP 200 during 12:25–12:34 UTC. A dot messaging send in the screenshot’s corresponding minute was recorded at 12:29:29.416 UTC, with the first-response event marked successful at 12:29:31.604 UTC, about 2.19 seconds later.

HTTP success and a successful first-response event do not establish a useful semantic answer: a product limit notice can be carried by a successfully delivered response. Association with the status request is inferred from timing because the logs contain no message text. These records do not identify the applicable limit or prove that delegated work continued. App version and OS are verified in the linked diagnostic packet. Plan, limit accounting and reset time remain unverified.

Support can investigate account-specific accounting through its authenticated channel. Public reporting needs a bounded, privacy-safe finding: affected product/build, applicable limit family, impact on active work, supported recovery and remediation status.

## Resolution criteria

A useful resolution supplies an authoritative explanation of the applicable limit and its recovery, together with verifiable restoration or a product change addressing the missing availability information. A temporary return of responses establishes observed recovery at that time; it does not alone establish a permanent fix.

No root cause, workaround, reset time, task-continuation guarantee or engineering fix is verified at this checkpoint.


## Collected technical packet

[App version, OS, event timings, missing backend data and reviewed log excerpts](evidence/TECHNICAL-DIAGNOSTICS.md). Environment: ChatGPT/Codex 26.930.61225, build 13232; macOS 27.0.1 build 26A434, arm64.
