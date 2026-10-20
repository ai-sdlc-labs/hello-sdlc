# Intent: Hello, world in a random language

| Field      | Value        |
|------------|--------------|
| ID         | 0001         |
| Originator | @river-lake  |
| Date       | 2026-10-20   |

## Problem
I want to learn the AI-native SDLC by running every stage of it end to end on GitHub. For that I need a
product small enough not to distract from the process, but real enough to exercise it: a public page,
stored data, staging and production, and a feedback loop back to the agent. No visitor has a pain today;
the product is a vehicle for practice.

## Proposed outcome
A public web page greets each visitor with "Hello, world" in one of 5 human languages, chosen at random,
with the language name and a pronunciation hint. Visitors can rate the greeting 👍/👎 and report a problem
or request a new language by picking from predefined options only. Feedback is stored privately; the agent
reads it and proposes fixes as pull requests that a human approves.

## Affected users and systems
- **Visitors:** only the originator (the link is not shared) and bots or crawlers that find the page.
- **Originator (@river-lake):** reads all feedback in the Cloudflare dashboard; approves the agent's PRs.
- **Agent (`ai-sdlc-agent`):** reads ratings and selected options (read-only) and turns them into PRs.
- **Systems:** Cloudflare Workers (staging and production), free-tier Cloudflare storage for feedback,
  this GitHub repository and its CI.

## Constraints
- $0 budget: free tiers only. The app must never exceed a free-tier limit or cost money, even under bot traffic.
- Cloudflare Workers with separate staging and production, on the free `*.workers.dev` address.
- Public GitHub repository: no secrets, feedback, or visitor data in code, issues, PRs, CI output, or logs.
- One human (@river-lake) plays every human role.
- Feedback is select-only. The server accepts only values from a predefined allow-list and rejects the rest.
- The agent never sees visitor data (timestamp, browser) and changes production only through an approved PR.
- No deadline.

## Success signals
Measured on production over the 24 h after each production deploy:
- p95 page load time < 1 s.
- < 5% of visits end in 👎 and ≥ 20% of visits end in 👍.

At all times:
- 0 days over any free-tier limit.

## Out of scope
- User accounts or login of any kind.
- Showing feedback, ratings, or counts on the public page.
- An admin page for reading feedback (the Cloudflare dashboard is enough).
- Applying or merging suggestions without human approval on a PR.
- Free-text feedback of any kind.
- Audio pronunciation (text hints only).
- Letting the visitor choose a language (random only).
- Translating the page's own interface (labels, buttons).
- A custom domain.
- Analytics beyond what the success signals need.

## Open questions
- Minimum number of page loads before a 24 h p95 counts? (Stage 2, @river-lake)
- Should ratings from suspected bots be excluded from the 👍/👎 ratio, and how do we tell? (Stage 2)
- Which 5 languages, and which source verifies each greeting and pronunciation hint? (@river-lake)
- Which predefined list do visitors pick a new language from (e.g. ISO 639)? (Stage 2)
- Store the full browser user-agent string, or only the browser family? (Stage 2, security review)
- How does the agent get read-only access to feedback without exposing it in the public repo? (Stage 2)

## Initial risk notes
- **Data handled:** per feedback record: the greeting shown, 👍/👎, the selected problem or requested
  language, a timestamp, and the browser (user-agent). No names, emails, IP addresses, or free text.
- **Who can reach it:** anyone on the internet, bots included, can submit feedback. Only @river-lake can
  read all fields. The agent can read ratings and selected options only, read-only.
- **What could go wrong:**
  - Bots flood the feedback endpoint, exhaust a free-tier quota, and take the page down or incur cost.
  - Forged requests skip the form and send arbitrary values. Without the server-side allow-list these would
    be stored and could reach the agent as prompt injection.
  - The agent proposes a wrong greeting or pronunciation hint, and it ships unless the human reviewer checks it.
  - Feedback or visitor data leaks into the public repository (issues, PR text, CI logs).
  - The agent's read credential leaks or is scoped wider than ratings and selected options.
  - Full user-agent strings help fingerprint visitors; keep no more than the spec needs.
