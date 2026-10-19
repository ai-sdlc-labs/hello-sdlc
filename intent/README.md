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

`intent.md` has no status field. The status is the state of the pull request that adds it:

| Pull request           | Intent status |
|------------------------|---------------|
| open                   | proposed      |
| merged                 | accepted      |
| closed without merging | closed        |

Per `.github/CODEOWNERS`, the PR needs approval from `@ai-sdlc-labs/product-owners` before it can merge.
So every intent on `main` is accepted, and every decision has a reviewer, a timestamp, and a discussion thread.
