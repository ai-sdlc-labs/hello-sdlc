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

## Status

Status follows the intent's pull requests, so no extra "flip the status" commit is needed:

- **proposed**: the PR adding `intent.md` is open. Write `Status: accepted` in the file.
  That only becomes true if the PR is merged.
- **accepted**: a product owner approved the PR and it was merged. Every intent on `main` is accepted.
- **rejected**: the PR was closed without merging, so nothing reaches `main`.
- **closed**: a later PR sets `Status: closed` (done or abandoned) and says why.

Every decision therefore has a reviewer, a timestamp, and a discussion thread. Per `.github/CODEOWNERS`,
changes under `intent/` need approval from `@ai-sdlc-labs/product-owners`.
