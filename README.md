# CiteCheck: APA 7 & MLA 9 Academic Citation Auditor

CiteCheck is a skill, written as a single Markdown file (`SKILL.md`), that guides a language-model assistant in auditing the citations of an academic paper written in **APA 7** or **MLA 9**. It extracts the in-text citations and the reference entries, matches them in both directions, checks formatting against the chosen style and reports the results in a structured academic report. When tools and source texts are available, it can also verify publications, DOIs and URLs and assess whether a source supports the claim made about it.

**Author:** Aditya Kumar
**Semester:** Monsoon Semester 2026
**Affiliation:** Department of Humanities and Social Sciences, Indian Institute of Technology (Indian School of Mines), Dhanbad

**Project webpage:** https://adityakumar190.github.io/citecheck-academic-auditor/

## Design question

How can a language-model assistant audit the citations of an academic paper in APA 7 or MLA 9 carefully, without inventing bibliographic details or overstating what it has checked?

## Repository contents

| File | Description |
|---|---|
| `SKILL.md` | The skill: purpose, 14 switches, resolution rules, 8 modules, style-specific checks, report design, workflow and reliability rules |
| `index.html` | Project webpage (published with GitHub Pages) |
| `README.md` | This file |

## The two styles

| | APA 7 | MLA 9 |
|---|---|---|
| In-text citation | Author–date, e.g. (Smith, 2022) | Author–page, e.g. (Smith 45), or a shortened title |
| Source list | References | Works Cited |

The two styles are kept strictly separate. APA rules are never applied to an MLA paper, or the reverse, and a paper is never converted silently from one style to the other. If the style is mixed or cannot be determined, the skill reports this and asks which style is intended.

## The eight modules

| No. | Module | Runs under |
|---|---|---|
| 1 | Citation extraction | `/audit`, `/all` |
| 2 | Reference extraction | `/audit`, `/all` |
| 3 | Citation matching | `/audit`, `/all` |
| 4 | Audit reporting | `/audit`, `/all` |
| 5 | Publication verification | `/verify`, `/all` |
| 6 | DOI verification | `/verify`, `/all` |
| 7 | URL verification | `/verify`, `/all` |
| 8 | Claim–source support assessment | `/claim-check`, `/all` |

Modules 1 to 4 form the core audit. Modules 5 to 8 are optional and depend on the evidence and tools available.

## The fourteen switches

Switches are written as slash commands at the start of the message.

| Group | Switches |
|---|---|
| Citation style | `/detect`, `/apa7`, `/mla9` |
| Audit and verification | `/audit`, `/verify`, `/claim-check`, `/all` |
| Report | `/report`, `/brief` |
| Control and export | `/strict`, `/no-web`, `/explain`, `/pdf`, `/docx` |

With no command, the skill detects the style and runs the core audit (modules 1 to 4). External verification is off unless `/verify`, `/claim-check` or `/all` is requested. `/apa7` and `/mla9` conflict, `/brief` takes precedence over `/report`, and `/no-web` overrides every external check.

## Usage

Add the skill to an assistant that supports skills, or give it the contents of `SKILL.md` as instructions. Then place the commands at the start of the message, followed by the paper:

```
/audit /apa7 /explain
[paste or upload the paper]

/all /strict /docx
[paste or upload the paper and, for claim checks, the cited sources]
```

Verification and export depend on the tools available on the platform. If a tool is missing, the skill marks the module "Not checked" and completes the checks that remain possible.

## Reliability rules

- Report only what the supplied document and the sources actually consulted support.
- Never invent an author, title, date, DOI, URL, quotation or database result, and never repair a reference with guessed information.
- Never claim that a search, lookup, URL inspection or file export took place when it did not.
- Keep apart *not found* and *does not exist*, *inaccessible* and *invalid*, *DOI resolves* and *metadata matches*, and *source located* and *claim supported*.
- Do not treat a citation mismatch as proof of plagiarism or misconduct.
- Give no quality score, percentage or pass or fail grade.

## Limitations

- The skill is a set of instructions. It does not provide a browser, a DOI resolver, a database connection or a document exporter.
- Claim–source assessment needs the relevant source content, not only a title, abstract or snippet.
- Style detection is qualitative, and short samples may be inconclusive.
- The audit covers only the material supplied, and lost formatting in extracted text cannot be assessed.
- The documentation describes the design of the skill and does not report a test of its accuracy on real papers.

## Citation

Kumar, A. (2026). *CiteCheck: APA 7 & MLA 9 Academic Citation Auditor*. Department of Humanities and Social Sciences, IIT (ISM) Dhanbad.
