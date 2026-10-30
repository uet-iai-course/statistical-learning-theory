# CLAUDE.md

This repo holds the lecture notes and exercises for **Lý thuyết học thống kê** (statistical learning theory; course code `statistical-learning-theory`), semester 1 of 2026–2027 (`2627-1/`), for master's students. The course belongs to the **Khoa Công nghệ thông tin** (FIT), Trường Đại học Công nghệ, ĐHQGHN, not to the Viện Trí tuệ nhân tạo like the sibling courses; pages say "Khoa Công nghệ thông tin" and the eyebrow "FIT · UET · VNU".

The workspace file `../CLAUDE.md` carries the rules shared by every course: environment, static-site rules, shared CSS, writing style, `no-ai-slop`/`quill`, the sub-agent policy, visual verification and git basics. This file holds only what is specific to this course. There is no `AGENTS.md`. Precedence: the user's instructions first, then `sources/blueprint.md` and `2627-1/planning/course-plan.md`, then this file, then `../CLAUDE.md`.

## Status

- **Ten theory lectures** (150 minutes each) defined by the user's blueprint `sources/blueprint.md`. Recitations and exams are out of scope for now.
- **Lecture notes and exercises first.** Slide decks only when the user asks; until then there is no RevealJS runtime or `lecture-style.css` here.
- **Lecture 01 is the pilot** (user decision 2026-10-30): note and exercises go to the user for review before lecture 02 starts.
- **Supplementary sources for lectures 07–10** are decided with the user when those lectures start (user decision 2026-10-30). Don't download them before.

## Repo map

| Path | Contents |
|---|---|
| `sources/blueprint.md` | The user's 10-lecture blueprint: central questions, proposed results with proof depth, proof plans, original exercises, timing, readings. **Read the lecture's section in full before planning.** |
| `sources/README.md`, `sources/uml-sections.md` | Source register; UML section → PDF page index, and the solution-manual page index |
| `sources/uml/understanding-machine-learning-theory-algorithms.pdf` | **Main source**, UML (Shalev-Shwartz & Ben-David 2014), author's personal-use copy. Gitignored; never committed, published, translated or copied |
| `sources/uml/MLbookSol.pdf` | UML solution manual (instructor material). Gitignored; only for cross-checking solutions after solving independently |
| `index.html`, `index-pages.css` | Course landing page; `index-pages.css` is the shared copy (synced from `../shared/css/`, never edited here) |
| `2627-1/index.html` | Semester index: one card per lecture (all ten shown) with **Ghi chú bài giảng**, **Bài tập**, **Bài giảng**; a resource is linked only after it passed review, otherwise `Chưa có` |
| `2627-1/material-viewer.{html,js}`, `material-bootstrap.js` | Static Markdown viewer (14 block types, `DIRECTIVE_LABELS` in the JS) |
| `2627-1/material-viewer.css`, `material-index.css` | Shared copies (synced, never edited here); add `material-viewer-course.css` / `material-index-course.css` for course rules |
| `2627-1/material-local-data.js` | Generated bundle so notes open under `file://`; never edit by hand |
| `2627-1/vendor/{katex,marked,dompurify}/` | Local runtime; nothing loads from the network |
| `2627-1/materials/lec-NN/` | `lecture-note.md`, `exercises.md`; templates in `materials/_templates/` |
| `2627-1/img/lec-NN/` | SVG figures for each lecture (create when needed) |
| `2627-1/planning/course-plan.md` | The writing plan: products, standards, per-lecture workflow, order, risks |
| `2627-1/planning/ky-hieu.md`, `thuat-ngu.md`, `van-phong.md` | Course-wide notation table (UML/blueprint notation), Vietnamese–English glossary and style guide, the last two drawn from the author's *Học máy thống kê*; every note follows them and extends the glossary |
| `2627-1/planning/lec-NN/` | `outline.md`, `review-log.md` (never linked from the index) |
| `../tools/courses/statistical-learning-theory/2627-1/scripts/sync-local-materials.py` | Builds `material-local-data.js` (workspace tooling, not in this repo) |

## Commands

```bash
../.venv/bin/python -m reloadserver 8765          # from repo root
# note:      http://localhost:8765/2627-1/material-viewer.html?doc=materials/lec-NN/lecture-note.md
# exercises: http://localhost:8765/2627-1/material-viewer.html?doc=materials/lec-NN/exercises.md

../.venv/bin/python ../tools/courses/statistical-learning-theory/2627-1/scripts/sync-local-materials.py          # after ANY edit to materials/*.md
../.venv/bin/python ../tools/courses/statistical-learning-theory/2627-1/scripts/sync-local-materials.py --check
git diff --check
```

Reading the PDFs: `../.venv/bin/python -I -c "import pymupdf,sys; d=pymupdf.open(sys.argv[1]); print(d[int(sys.argv[2])-1].get_text())" sources/uml/<file>.pdf <page>` (PDF page numbers as in `sources/uml-sections.md`).

## Lecture notes

- **Viewer contract:** `material-viewer.html?doc=materials/lec-NN/{lecture-note,exercises}.md`. `deck=lecture-NN-<ten-bai>.html` is optional; when a deck exists it must name the same lecture. `NN` is two digits.
- **Pipeline:** protect maths → Marked → DOMPurify → restore maths → KaTeX. Commit `material-local-data.js` with the Markdown.
- **Blocks:** `::: definition|theorem|proposition|lemma|corollary|remark|algorithm|example|application|derivation|proof|exercise|hint|solution Optional title`, closed by `:::`, not nested. `proof`, `hint`, `solution` are collapsed by default. Each file starts with one `#` heading.
- **Plain, direct sentences (user requirement 2026-10-30):** no convoluted phrasing — no reported-speech wrappers ("một câu trả lời … cho rằng …"), double or roundabout negation, nominalisations, abstract subjects doing a person's work, cleft or hedged constructions; a direct question that the note answers beats paraphrasing a misconception. See `planning/van-phong.md` §9a.
- **Define before use (user requirement 2026-10-30, after the lecture 01 pilot):** every term, symbol and numbered result is defined (or introduced with its meaning) before its first use in the body; no body text cites a later numbered block. Exceptions: the title, the learning-outcomes list (words only, no symbols or block numbers), and the closing exit-question/bridge and readings sections, which look back. Running-example objects appear where the concept they illustrate is defined, not in an early catalogue; assumptions are stated where first needed. Check with `python3 ../tools/courses/statistical-learning-theory/scripts/forward_refs.py 2627-1/materials/lec-NN/lecture-note.md` (must report 0) plus a read-through audit. This rule overrides the blueprint's component order where they conflict.
- **Structure:** the 15 components of blueprint §A, in order, with Vietnamese headings (see `course-plan.md` §3 and `materials/_templates/lecture-note.md`). Worked examples sit between results, not all at the end. Long technical proofs go to a "Phụ lục" section at the end.
- **Results:** labelled by role (Bổ đề = proof tool, Mệnh đề = focused fact, Định lý = principal result, Hệ quả = immediate consequence). One counter per lecture, increasing in reading order, shared by definitions, results, remarks and algorithms (`Định nghĩa 01.1`, `Mệnh đề 01.5`, …); separate counters for Ví dụ and Bài tập. The blueprint's labels are mapped to these numbers in `outline.md`, not shown to students (master decision 2026-10-30, lecture 01). The block title carries number, name and proof depth: *chứng minh đầy đủ* [F], *phác thảo* [S], *đọc thêm* [O]. Every formal statement has bold "Giả thiết." and "Bảo đảm." lines (expectation or high probability; empirical or population; dependence on $m$, dimension, iterations, $\delta$, norms).
- **Proofs** start with a roadmap, name the key inequality, mark where each assumption enters, end with $\square$ and a sentence on what the result means for learning. Multi-step derivations in `aligned`, one relation per line.
- **Notation and terms:** `planning/ky-hieu.md` (from blueprint §A: $L_D$, $L_S$, $m$ sample size, $d$ VC dimension, $p$ feature dimension, …) and `planning/thuat-ngu.md`. English terms in parentheses at first use in each note.
- **A note is a self-contained textbook chapter**: problem before tool; every formula wrapped in prose; every symbol named at first use; every step justified; a concrete example before the general statement; at least one numerical bound and one "remove an assumption" counterexample per lecture; section endings in prose (no "Kết mục"/"Chuỗi suy luận" labels).
- **Voice and terms follow the author's textbook *Học máy thống kê*** (`../SML-textbook-main.zip`; style and terminology model only, never a content source; user request 2026-10-30). Writers and reviewers read `planning/van-phong.md` and `planning/thuat-ngu.md` first; terminology takes the book's majority choice ("phân bố", "kì vọng", "hàm lỗi", "tối thiểu hóa rủi ro thực nghiệm"), while notation follows `planning/ky-hieu.md`, not the book. In short: "chúng ta" for plans, needs and limits, "ta" inside calculations; the document is never the subject ("Mục này định nghĩa…" is banned); no "hãy" outside exercise statements.
- **Statistical learning theory standards** (blueprint §E is a mandatory review checklist): state the probability space, sampling scheme, loss and its range, hypothesis class, comparator and what is fixed vs random before any bound. Distinguish risk, excess risk, optimization gap, expected generalization, stationarity, regret and forgetting; expectation vs high probability; class-level vs algorithm-level guarantees. Every inequality names its tool and every constant is re-derived. Don't transfer bounded-loss results to squared or log loss, or convex results to neural networks or RL, without a new argument.
- **Teaching timings** from the blueprint go only in `outline.md`, never in student-facing text.
- **Exercises (user decision 2026-10-30):** `exercises.md` publishes the statement, one or more hints of increasing strength (each its own `::: hint` block) and a full solution (`::: solution`); hints and solutions are collapsed by default. Original prompts (blueprint) and UML exercises (number verified in the PDF) are kept apart. Solutions to UML exercises are written in our own reasoning; `sources/uml/MLbookSol.pdf` is only for cross-checking after solving independently, never copied or paraphrased closely. Written after the note passed review.
- **Sources:** UML by section (verified in `sources/uml-sections.md`); never translate or copy passages; log the sections and pages consulted in `review-log.md`. Results are course formulations with local numbers, never UML theorem numbers presented as ours.

## Sub-agents (course settings)

The policy in `../CLAUDE.md` applies, with every sub-agent at effort `high`. Per lecture (`course-plan.md` §5): source analysis → plan (`outline.md`) → draft note (one writer, `no-ai-slop` Edit) → five independent reviews (master's student; mathematical accuracy with every proof and constant re-derived; learning-theory expert and source fidelity; academic/pedagogical with `no-ai-slop` Detect; storyline and linking) → one editor revises → recheck changed parts → exercises (writer, then maths and pedagogy reviews, then fix) → final check (viewer at 1600×900 and 390×844, print, `file://`, KaTeX errors, local-data sync, index card).

## Git (course settings)

Remote: `git@github.com:uet-iai-course/statistical-learning-theory.git` (public), branch `main`. GitHub Pages serves `main` / at http://courses.iaidev.com/statistical-learning-theory/ (enabled 2026-10-30). Ask before committing or pushing, unless the user has asked for it in the current task.

## Done means (per lecture)

Every blocking and serious finding resolved and logged; `outline.md` and `review-log.md` match the note; the viewer renders the note and exercises over HTTP and `file://` with no KaTeX errors or failed requests at both sizes and in print; `material-local-data.js` is in sync; the index card links the note and exercises only once they passed review.
