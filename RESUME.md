# Resume data

The canonical source is [resume-data.json](resume-data.json). It contains bilingual
Russian/English career facts with stable IDs and structured metrics. This is a
custom data format, versioned by `schemaVersion`; it is not itself JSON Resume.

[resume.json](resume.json) (English) and [resume.ru.json](resume.ru.json) (Russian)
are full, unabridged generated views compatible with the JSON Resume schema.
They are not vacancy-tailored two-page documents. Standard renderers may ignore
`x-` extensions. `x-factIds` maps work highlights to the canonical facts.

## Consumer contract

- Load the canonical JSON once, select `ru` or `en`, and resolve each employment
  record's `factIds` against `facts`. Preserve the matching locale in every field.
- Keep fact IDs stable. `schemaVersion` follows semantic versioning; consumers
  should reject unsupported major versions. Ignore unknown additive fields.
- `updatedAt` is the content review date. Project `statusAsOf` records when a
  public project status was checked. Employment dates have month precision;
  omitted `endDate` means current. Do not sum overlapping jobs or boundary months
  to infer years of experience.
- `position` describes functional responsibility, not a claim about the title in
  an employment contract. Big3/A.PRO has separate role and employer timelines.
- `metrics` retains original quantities and their scope. `reportedMetrics` are
  author-reported estimates/comparisons, not independently measured results.
  Never broaden their scope or silently insert them as verified exact outcomes.
- The CPU measure is the average dashboard reading during database access under
  comparable workload; process/container/host scope is not established. The
  change 120% to 80% is about 33% relative, or 40 percentage points.
- Infrastructure cost currency and billing period are unknown (`null`). Never
  invent them. The values 7000 to 3000 support "more than halved".
- Russian compensation preference is RUB 300000 net. Do not carry it into the
  English version. Employment type listings are omitted. Initial evening work
  at VS is timeline context, not a current availability preference.
- React involvement at Rosbank/SmartDeal is limited/incidental. Do not turn
  that into ownership of a React codebase. The AI voice operator is a pilot.
- English is described through actual client communication experience; no
  certified CEFR level is asserted. Self-directed learning is not a degree.
- Only email is provided as a contact method. Project/publication links are
  portfolio evidence. No phone, visa claim, internal source documents, internal
  tracker URLs, colleague names or private review notes are published.

## Architecture

GitHub stores data only. The website and local application are independent
consumers: they select facts, render documents, and may export JSON/PDF/DOCX.
Local model-based vacancy analysis and rewriting belong in the local application.
A progress bar should distinguish downloading JSON from processing/rendering.
For unknown download size or non-measurable rendering work, show an indeterminate
state or a named stage rather than a fabricated percentage.

Stable branch URL for consumers:
`https://raw.githubusercontent.com/Codevanger/Codevanger/main/resume-data.json`

For reproducible output, pin the URL to a commit SHA and record the selected fact
IDs, locale and renderer version. Render text as text, not untrusted HTML.

## Verification

The data was reconciled against author-provided resumes and direct clarifications,
then reviewed by a separate agent before publication. This is a consistency and
source-fidelity review, not independent verification of employment or metrics.
Both standard views are validated against the official JSON Resume schema.
The canonical file also retains context useful to consumers that a standard
resume theme does not display (career progression, skill scope, preferences).
