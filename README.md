# bugbounty-brain

A curated corpus of **4,952 publicly-disclosed [HackerOne](https://hackerone.com) reports**, organized by vulnerability type. Built as training/reference material for teaching AI assistants to hunt bugs, triage findings, and write security reports.

> All reports here are already **publicly disclosed** on hackerone.com. Nothing in this dataset is private or confidential.

---

## What's inside

Every report is stored as a **pair of files**:

| File | Contents |
|------|----------|
| `<id>.json` | Full HackerOne API metadata — title, URL, reporter, target program, state, weakness type (CWE), timestamps, votes, and team/researcher summaries |
| `<id>.md` | Human-readable writeup — summary, a metadata table (severity, program, bounty, dates), and the report body |

Reports are grouped into folders by **vulnerability class**.

## Categories

| Category | Reports | | Category | Reports |
|----------|--------:|---|----------|--------:|
| `xss` | 745 | | `path-traversal` | 106 |
| `bug-hunt` | 639 | | `sqli` | 101 |
| `info-disclosure` | 586 | | `open-redirect` | 99 |
| `bac` (broken access control) | 487 | | `ssrf` | 92 |
| `hunt-rce` | 378 | | `api-testing` | 75 |
| `business-logic` | 371 | | `dom-vulns` | 53 |
| `authentication` | 298 | | `hunt-jwt` | 44 |
| `web-cache` | 242 | | `clickjacking` | 29 |
| `csrf` | 163 | | `host-header` | 24 |
| `idor` | 134 | | `request-smuggling` | 24 |
| `command-injection` | 130 | | `prototype-pollution` | 21 |
| `race-condition` | 20 | | `subdomain-takeover` | 17 |
| `password-reset` | 18 | | `deserialization` | 16 |
| `xxe` | 14 | | `file-upload` | 8 |
| `websocket` | 4 | | `cors` | 4 |
| `oauth` | 3 | | `graphql` | 3 |
| `ssti` | 2 | | | |

The machine-readable index of counts lives in [`_all_categories.json`](_all_categories.json).

## Structure

```
.
├── _all_categories.json      # category → report-count index
├── xss/
│   ├── 100829.json           # full API metadata
│   ├── 100829.md             # readable writeup
│   └── ...
├── sqli/
├── ssrf/
└── ...                       # 33 vulnerability categories
```

## Usage

Point your AI tooling, RAG pipeline, or fine-tuning job at the `.md` files for readable writeups, or the `.json` files for structured metadata. Example — list every resolved XSS report against a given program:

```bash
jq -r 'select(.team.handle=="coinbase" and .substate=="resolved") | .title' xss/*.json
```

Count reports per category:

```bash
cat _all_categories.json | jq
```

## Notes & caveats

- **Expired image links:** `.json` files may contain AWS S3 pre-signed URLs for attachments. These are time-limited and have since expired — the metadata is intact, but inline images won't load.
- **Public data only:** reporter usernames, program names, and report bodies are all as published on HackerOne.
- This is a **reference/teaching dataset**, not an exploit kit. Use it to learn vulnerability patterns and improve defensive and authorized testing work.

## License

The report content belongs to the original researchers and programs that disclosed it on HackerOne. This repository is an organized archive for educational and research use.
