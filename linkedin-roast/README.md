# linkedin-roast

A Claude skill that has five reviewers (a recruiter, a hiring manager, a founder, an expert in your field and a peer) roast a LinkedIn profile, each one working alone. It then rewrites the headline, the About section and every experience entry, and makes a banner and a headshot prompt.

This is a modified copy of [alexyc9381/linkedin-roast-skill](https://github.com/alexyc9381/linkedin-roast-skill) (MIT, © Alex Chen). It lives in its own folder and is not part of the 11-skill `linkedin-skills` bundle in this repository.

## What changed from the original

The original reads a profile from a PDF, pasted text or a screenshot only. This version also accepts a **profile link** (`linkedin.com/in/...`):

1. **Signed-in browser first.** If a browser tool is available (Claude in Chrome or the built-in browser), it opens the profile there. It reads the main page plus the `/details/experience/`, `/details/education/` and `/details/skills/` pages, because the main page cuts those sections short.
2. **Read only.** It never clicks Connect, Message, Follow, Edit or Like, and never opens other profiles. If LinkedIn asks you to sign in, you do it yourself; the skill never types or asks for your password.
3. **Plain fetch, then fall back.** With no browser, it tries one plain fetch. LinkedIn usually blocks that, so the skill then asks for the PDF instead and does not guess.
4. The five reviewers always get the cleaned text, never the link.

## Use

Install the skill from `skills/linkedin-roast/SKILL.md`, then run:

```
/linkedin-roast https://www.linkedin.com/in/your-handle/
```

or attach your LinkedIn PDF (desktop: Me → View profile → More → Save to PDF).

## Example

[`examples/haggai-akumbom/`](examples/haggai-akumbom/) holds a real run on 18 Nov 2026:

| File | What it is |
|---|---|
| `roasts.md` | The five reviews, what they agree on, and the scores (average 4.2/10) |
| `new-profile.md` | New headline and alternates, the About, the keyword table, every experience entry before and after, and the open `[ADD YOUR NUMBER]` questions |
| `banner.png` / `banner.svg` | 1584 × 396 LinkedIn banner |
| `headshot-prompt.md` | Prompt for an image tool, to use with your own photo |

The reviewers are one model playing five roles. Their reviews are a structured second opinion, not career advice, and nothing here guarantees interviews or a job.
