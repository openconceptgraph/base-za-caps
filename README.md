# OpenConceptGraph: CAPS Mathematics

An open concept graph of South Africa's Curriculum and Assessment Policy Statement (CAPS) for Mathematics, built to the [OpenConceptGraph specification](https://github.com/openconceptgraph/spec) and reviewed in the [OpenConceptGraph platform](https://github.com/openconceptgraph/platform).

**Status: early. Nothing here has been reviewed or released yet.** Grade 8 Term 1, Numbers (topics 1.1 Whole numbers, 1.2 Exponents and 1.3 Integers), is transcribed word for word from CAPS Mathematics Grades 7–9 and checked against the published PDF, and so are the Grade 7 topics it builds on: 1.1 Whole numbers (Term 1) and 1.3 Integers (Term 4). Two teaching plans place those topics: CAPS 2011's own terms and hours, for both grades, and the 2026 Annual Teaching Plan's terms, weeks and hours, for Grade 8. Concepts, prerequisite links and typical mistakes are drafted and reviewed in the platform, and appear here only when a release includes them.

## What a base holds

Two layers, kept apart:

- **Transcription:** what the Department of Basic Education published, word for word, with its page. The framework, its documents and their headings, the curriculum statements (content, clarification notes, worked examples, statements of what is different from the grade before), and teaching plans with their placements (terms, weeks, hours). This layer is the curriculum's own; it is not an interpretation.
- **Interpretation:** our reading of it. Concepts, families, typical mistakes and the links between them, each with a source and a review status. Only confirmed objects and links reach a release.

## Layout

```
mathematics/
  framework.json                  the framework and its grades
  release.json                    release settings: title, licence, credit lines, review policy
  documents/<document>.json       an official document, its headings and the PDF it was checked against
  teaching-plans/<plan>.json      a teaching plan and its placements
  statements/grade-<n>/<topic>.json one topic's statements for one grade, in the document's order
  concepts/ families/ misconceptions/ links/ sources/
                                  the interpretation, filled by releases
```

Every object has a permanent UUID, never reused; a statement also has a code such as `8/1.3/c04` (grade, topic, column, number). Where a printed page also holds topics not yet transcribed, the topic's file gives the region of the page it occupies (`regions`, in PDF points from the page's top left), and the check reads only that part: Grade 7 Integers ends on page 68, above Grade 7's Term 4 patterns and functions. Statements keep the original exactly, including its errors, with a transcriber's note where one is found. Notation is in Unicode (2³, aᵐ⁺ⁿ, √, ∛). A fraction is written numerator⁄denominator with the fraction slash, and brackets stand for a root's bar or a fraction line where those cover more than one term. A statement whose order a PDF's text layer cannot confirm is marked `eyeChecked`: its order was checked against the printed page by eye.

A teaching plan's placements are terms, weeks and hours, checked by eye against the printed plan. The 2026 Annual Teaching Plan (`teaching-plans/atp-2026.json`) schedules CAPS's own topics, so its placements name the CAPS document and keep the plan's heading for each topic as printed. It places only the topics transcribed so far; the rest follow as their headings are. Where a cell in the printed table does not line up with its week columns, the weeks follow the hours at four and a half hours a week: in Term 2, Exponents has 9 hours, weeks 1–2.

The platform's pipeline checks every statement against the PDF and loads the transcription into its working database:

```sh
pnpm base check ../base-za-caps/mathematics --pdf <CAPS Mathematics Grades 7-9 PDF> --record
pnpm base import ../base-za-caps/mathematics
```

A release is built from the working database to the [specification](https://github.com/openconceptgraph/spec)'s layout and checked with its validator. It holds the whole transcription and only the interpretation two reviewers have confirmed (`release.json`'s review policy):

```sh
pnpm base release ../base-za-caps/mathematics --version 0.1.0 --out <folder>
```

## Licence and attribution

The data in this repository are licensed under [CC BY 4.0](LICENSE). Credit OpenConceptGraph, and the Department of Basic Education for the curriculum text: curriculum statements quoted from CAPS, and teaching plan terms, weeks and hours from the 2026 Annual Teaching Plans, © Department of Basic Education.

Contributions are signed off under the [Developer Certificate of Origin](https://developercertificate.org/) (`git commit -s`).
