# intent/

Every idea starts here, as Stage 1 (Plan) of the
[AI-Native SDLC Playbook](https://claude.com/resources/articles/the-ai-native-sdlc-playbook).

## Convention

Each idea gets its own folder, `intent/NNNN-short-slug/` (e.g. `intent/0001-hello-world/`),
where `NNNN` is the next free four-digit number. The folder grows as the idea moves through the stages:

| File        | Stage | Answers                     |
|-------------|-------|-----------------------------|
| `intent.md` | 1     | Why, and what outcome?      |
| `spec.md`   | 2     | What exactly will we build? |
| `plan.md`   | 3     | How will we build it?       |

Start a new idea by copying [`TEMPLATE.md`](TEMPLATE.md) to `intent/NNNN-short-slug/intent.md`.

## Status changes

An intent's status (`proposed` → `accepted` → `closed`) changes **only through a pull request**.
That gives every decision a reviewer, a timestamp, and a discussion thread. Per `.github/CODEOWNERS`,
changes under `intent/` need approval from `@ai-sdlc-labs/product-owners`.
