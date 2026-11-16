# CLAUDE.md

This repo holds the lecture notes, exercises and slide decks for **Lý thuyết học thống kê** (statistical learning theory; course code `statistical-learning-theory`), semester 1 of 2026–2027 (`2627-1/`), for master's students. The course belongs to the **Khoa Công nghệ thông tin** (FIT), Trường Đại học Công nghệ, ĐHQGHN, not to the Viện Trí tuệ nhân tạo like the sibling courses; pages say "Khoa Công nghệ thông tin" and the eyebrow "FIT · UET · VNU".

The workspace file `../CLAUDE.md` carries the rules shared by every course: environment, static-site rules, shared CSS, writing style, `no-ai-slop`/`quill`, the sub-agent policy, visual verification and git basics. This file holds only what is specific to this course. There is no `AGENTS.md`. Precedence: the user's instructions first, then `sources/blueprint.md` and `2627-1/planning/course-plan.md`, then this file, then `../CLAUDE.md`.

## Status

- **Ten theory lectures** (150 minutes each) defined by the user's blueprint `sources/blueprint.md`. Recitations and exams are out of scope for now.
- **Notes and exercises for 01–10 are done.** Slide decks 01–10 are built from them, one lecture after another (user request 2026-11-15); rules in § Slide decks.
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
| `2627-1/lecture-NN-<ten-bai>.html` | One RevealJS deck per lecture, built from the finished note (§ Slide decks) |
| `2627-1/lecture-style.css`, `lecture-course.css` | Shared deck stylesheet (synced copy, never edited here), then this course's deck rules (strand title slides, `lecture-deck` layout; taken from rl-plan 2026-11-15) |
| `2627-1/lecture-template.html` | Skeleton for new decks (structure only) |
| `2627-1/revealjs/`, `plugin/` | Local RevealJS runtime (copied from rl-plan 2026-11-15); KaTeX comes from `vendor/katex` |
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
# deck:      http://localhost:8765/2627-1/lecture-NN-<ten-bai>.html
../.venv/bin/python ../tools/courses/math-4-AI/2627-1/scripts/deck_check.py --url <deck URL> --out <scratchpad dir> [--shots]   # density, overflow, KaTeX, console

../.venv/bin/python ../tools/courses/statistical-learning-theory/2627-1/scripts/sync-local-materials.py          # after ANY edit to materials/*.md
../.venv/bin/python ../tools/courses/statistical-learning-theory/2627-1/scripts/sync-local-materials.py --check
git diff --check
```

Reading the PDFs: `../.venv/bin/python -I -c "import pymupdf,sys; d=pymupdf.open(sys.argv[1]); print(d[int(sys.argv[2])-1].get_text())" sources/uml/<file>.pdf <page>` (PDF page numbers as in `sources/uml-sections.md`).

## Lecture notes

- **Viewer contract:** `material-viewer.html?doc=materials/lec-NN/{lecture-note,exercises}.md`. `deck=lecture-NN-<ten-bai>.html` is optional; when a deck exists it must name the same lecture. `NN` is two digits.
- **Pipeline:** protect maths → Marked → DOMPurify → restore maths → KaTeX. Commit `material-local-data.js` with the Markdown.
- **Blocks:** `::: definition|theorem|proposition|lemma|corollary|remark|algorithm|example|application|derivation|proof|exercise|hint|solution Optional title`, closed by `:::`, not nested. `proof`, `hint`, `solution` are collapsed by default. Each file starts with one `#` heading.
- **Multi-part definitions as lists (user requirement 2026-10-30):** a definition or result with three or more components or assumptions gets a short lead sentence and a bulleted list with bold labels, not a long paragraph (`planning/van-phong.md` §3a; model: Định nghĩa 01.5).
- **Plain, direct sentences (user requirement 2026-10-30):** no convoluted phrasing — no reported-speech wrappers ("một câu trả lời … cho rằng …"), double or roundabout negation, nominalisations, abstract subjects doing a person's work, cleft or hedged constructions; a direct question that the note answers beats paraphrasing a misconception. See `planning/van-phong.md` §9a.
- **Examples step by step (user requirement 2026-10-30):** a worked example never moves too fast. One step per short paragraph or line (what is computed, which formula or numbered result, substitution, result, one sentence on what the number means); separate steps with line breaks, bold step labels or a numbered list and displayed formulas (`aligned` for multi-step calculations); no intermediate step skipped; never pack setup, several calculations and the conclusion into one paragraph. See `planning/van-phong.md` §7a. Applies to examples in notes and to solutions in exercises.
- **Define before use (user requirement 2026-10-30, after the lecture 01 pilot):** every term, symbol and numbered result is defined (or introduced with its meaning) before its first use in the body; no body text cites a later numbered block. Exceptions: the title, the learning-outcomes list (words only, no symbols or block numbers), and the closing exit-question/bridge and readings sections, which look back. Running-example objects appear where the concept they illustrate is defined, not in an early catalogue. **§2 holds the notation table and every assumption** (author decisions 2026-11-01, 2026-11-13): the assumptions form a bold-labelled list with one formula each, and the §2 notation table gives each symbol those formulas need a just-sufficient gloss (what it is, its type), so the list reads before the full definitions; the definition itself stays where the concept is introduced, and later sections cite the label only. Check with `python3 ../tools/courses/statistical-learning-theory/scripts/forward_refs.py 2627-1/materials/lec-NN/lecture-note.md` (must report 0) plus a read-through audit. This rule overrides the blueprint's component order where they conflict.
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

## Slide decks

Decks follow the shared rules NT1–NT28 in `NGUYEN-TAC-TRANG-CHIEU.md` at the repo root (a byte-identical copy of the workspace's `shared/docs/nguyen-tac-trang-chieu.md`, synced by `../tools/docs/sync_shared_docs.py`; never edit the copy here). They grew out of this course's deck build of 2026-11-15/16 and the author's decisions of 2026-11-14 (`../nhat-ky/yeu-cau-thay-doi-2026-11-13.md`, rows 1–8). The course's parameters P1–P11 are below; they and the rules after them win over the shared file where they differ, and the shared file wins over the older rl-plan deck rules.

### Course parameters for slide decks (P1–P11)

| Code | Parameter | Value for this course | Basis |
|---|---|---|---|
| P1 | Content source | `ghi chú`: the lecture note and `exercises.md` are the only source; there is no source deck | below, "Consistency with the note" |
| P2 | Terms and spelling | `planning/thuat-ngu.md`, `planning/ky-hieu.md`; "Kí hiệu", "kì vọng", "phân bố", "hàm lỗi", "lớp giả thuyết", "tập huấn luyện/xác thực/kiểm tra"; decimal comma (`0{,}05`) | `planning/van-phong.md` §12; author 2026-11-16 (dataset terms) |
| P3 | Result labels | "Giả thiết:" and "Bảo đảm:" on every formal statement; no extra labels (no "Cách khác:", "Dạng khác:", "Đầu vào:", "Đầu ra:") | below, "Labels" |
| P4 | Summary table, third column | `Ý tưởng chứng minh` | below, "Conclusion strand" |
| P5 | Extra opening slides | none | below, "Strands" |
| P6 | Timing, slide count | about 120 of 150 minutes; 45–52 slides, cap 55 with a reason in `storyboard.md` | below, "Timing" |
| P7 | Technical frame | `2627-1/lecture-template.html` (structure, RevealJS config, narrow-screen reading mode, footer "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài NN"); `data-slide-id` `LNN-k-mm`; course rules in `2627-1/lecture-course.css` | below, "Technical", "Narrow screens" |
| P8 | Outside sources | UML (Shalev-Shwartz and Ben-David 2014) by section, and the other sources the note cites; notes end with "Nguồn: ghi chú Bài NN, §k; UML §x.y." | below, "Speaker notes"; "Sources" |
| P9 | Agents | Opus 5.5, every role at effort `high` | "Sub-agents (course settings)" |
| P10 | Course checks | `deck_lint.py --course statistical-learning-theory` (shared tool in `../tools/deck/`); `sync-local-materials.py --check`; viewer links with `&deck=` | "Commands" |
| P11 | Course rules | NT-SLT-1: the learning-theory expert reviewer uses blueprint §E as a mandatory checklist. NT-SLT-2: each result slide states the type of guarantee (expectation or high probability, empirical or population, dependence on $m$, $\delta$, dimension, iterations), as in "What stays in the note" below. | below |

Decks 01–10 were built under these rules (2026-11-15/16); the rules below record this course's wording of them.

- **Consistency with the note (binding).** The deck is a companion to the note, not a second version of it:
  - same notation, symbols and assumption labels as the note (and `ky-hieu.md`), same terms (`thuat-ngu.md`), same names and numbers of results (a cited "(Định lý 03.7)" is the note's block with that number and content);
  - statements on slides keep the note's assumptions, quantifiers, constants and type of guarantee (expectation or high probability); a compact statement may drop wording, never a condition;
  - concept order follows the note's sections; a strand maps to consecutive note sections;
  - an example taken from the note keeps its data and results; a new example uses the note's notation and must not contradict any number in the note;
  - the `Mục | Bài tập` table and every exercise slide match `exercises.md` (same numbers, same results).
  - If building or reviewing the deck reveals an error or gap in the note, the deck still follows the note and the master logs a proposed note change in `review-log.md` for the author; the note is changed only with the author's approval, never silently by a deck agent.
  - The maths reviewer and the storyline reviewer each check consistency with the note slide by slide.

- **Purpose (user request 2026-11-15).** The note already carries every definition, statement and full proof. The deck explains what the note cannot show at a glance:
  - **intuition** of each main result: why it should hold, what each quantity measures, an extreme or limiting case, a picture;
  - **proof idea**: a 3–5 step roadmap, the one key inequality or trick, where each assumption enters, what breaks without it;
  - **key techniques** worth remembering across lectures (union bound, Hoeffding, symmetrisation and ghost sample, growth function, convexity and telescoping sums, replace-one stability, …), each named once on a slide labelled "Kỹ thuật." where it is first used and recalled by name afterwards;
  - **supporting examples**: small hand-computable cases, numerical bounds, a counterexample when an assumption is removed. They come from the note, or are new examples built with the note's notation; every number is re-derived and its construction logged in `review-log.md`. No claim without a basis in the note or in UML.
- **What stays in the note:** full proofs, long computations, every remark. A result slide states the result compactly with the note's two parts, "Giả thiết:" and "Bảo đảm:" (type of guarantee: expectation or high probability, empirical or population, dependence on $m$, $\delta$, dimension, iterations), and cites the note's number once ("(Định lý 03.7)"); a result the note marks *đọc thêm* [O] says so in the speaker notes. Definitions are stated briefly where needed or recalled with "Nhắc lại:".
- **Define or recall before use (as for notes):** every symbol, term, assumption and result on a slide face is introduced on an earlier slide of the same deck or recalled with "Nhắc lại:"; no slide cites a later slide's result or a later lecture (previews stay out of the face). Overview slides (cover, "Mục tiêu", "Nội dung", "Vấn đề trung tâm") are exempt and use words, not new symbols.
- **English terms:** in parentheses at first use on a content slide (overview slides exempt), every common English name and standard abbreviation as in the note.
- **Exercise slides** ("Bài tập: …") come only from `exercises.md`, with its data, wording of the question and results; worked cases from the note are "Ví dụ: …" slides. Solutions on the face are labelled "Lời giải:", never "Đáp án".
- **Concept journey for a main result:** problem → intuition ("Trực quan.") → example → statement → proof idea ("Ý tưởng chứng minh.", always its own slide, never merged with the statement) → technique or check (removed-assumption counterexample, numerical bound, "Câu hỏi:"). Steps may share a slide but are not reordered or dropped.
- **Strands:** 5–7, mapping groups of note sections. Opening strand: cover (title, one-sentence thesis, "Lý thuyết học thống kê · Năm học 2026–2027, học kỳ 1", "Khoa Công nghệ thông tin, Trường Đại học Công nghệ, ĐHQGHN"); "Tiên quyết và quy ước"; "Mục tiêu"; "Nội dung"; "Vấn đề trung tâm" with **one box stating the one core problem** (the strands' answers go to the speaker notes).
- **Strand title slides:** as in rl-plan, but the lead `p.strand-lead` is a short declarative sentence stating what the student will know or be able to do after the strand, in everyday words and concepts introduced earlier. No "Nhu cầu:", no "Muốn …, phải …".
- **No "Nhu cầu:" label** anywhere. A concept opens with a short affirmative sentence or directly with the concrete example. An example's first slide lists its data at once (objects, choices, outcomes) as a list.
- **Conclusion strand titled "Tổng kết":** summary table `Kết quả | Giả thiết không được bỏ | Ý tưởng chứng minh` (one row per main result); a slide titled "Vấn đề trung tâm" listing answers to the core problem of the whole lecture (not one line per strand); one synthesis exercise ("Bài tập: …", from `exercises.md`) with "Lời giải:" on the face; "Câu hỏi tự kiểm tra" (2–4 short questions, answers in the speaker notes, each answerable from the note alone); "Bài tập về nhà" with a `Mục | Bài tập` table pointing to `exercises.md` and a "Ghi chú bài giảng · Bài tập" viewer link; a last slide titled "Tài liệu tham khảo" (UML sections, other sources of the note) and a one-line link to the next lecture. No new concepts.
- **Titles:** natural Vietnamese noun phrases, never a word-for-word English pattern ("X như một bài toán Y" → "Ví dụ: X"). Function prefixes "Ví dụ: …", "Bài tập: …", "Chứng minh: …", "Ý tưởng chứng minh: …".
- **Labels:** with a period: Định nghĩa. Định lý. Mệnh đề. Bổ đề. Hệ quả. Nhận xét. Thuật toán. Chứng minh. Trực quan. Ví dụ. Ý tưởng chứng minh. Kỹ thuật. — with a colon: Ý nghĩa: Diễn giải: Lưu ý: Nhắc lại: Kí hiệu: Giả thiết: Bảo đảm: Kết luận: Câu hỏi: Gợi ý: Lời giải: — nothing else. A "Diễn giải:" uses only numbers shown on the same slide. The "Vấn đề trung tâm" box is one genuine question of the lecture with "Câu hỏi:", answered by the closing "Vấn đề trung tâm" slide.
- **Techniques:** a technique reused across lectures gets its own "Kỹ thuật." slide where the course first uses it (general form in one line, "Dùng khi …", where it is used); later decks recall it by name with "Nhắc lại:" in one line. A trick used in one proof only is one "Kỹ thuật." line on that proof-idea slide. The storyboard keeps a running list of techniques introduced so far.
- **Figures, formulas, tables:** SVG only (no raster without the user's approval logged in `review-log.md`); formulas, tables and pseudocode are KaTeX or HTML, never drawn into an SVG; captions state the data, never "minh họa" or "giá trị giả định"; colour is never the only signal.
- **Notation and terms** are the note's (`planning/ky-hieu.md`, `thuat-ngu.md`): "phân bố", "kì vọng", "hàm lỗi", "lớp giả thuyết", $L_D$, $L_S$, $m$, … English term in parentheses at its first use in the deck.
- **Speaker notes** carry the explanation (assumptions, reading of a formula or figure, easy confusions, the link to what follows) for the lecturer and the student, never planning matter: no slide IDs, storyboard codes ("V4", "mục 5"), workflow or provenance sentences ("dựng mới", "giữ nguyên chữ"), instructions to the author, timings, or openings like "Trang này …" and end with `<p class="note-source">Nguồn: ghi chú Bài NN, §k; UML §x.y.</p>`.
- **Technical:** file `2627-1/lecture-NN-<ten-bai>.html` (ASCII slug of the note title); structure, RevealJS config, plugins and footer as in `lecture-template.html` (footer "Lý thuyết học thống kê · Học kỳ 1, 2026–2027 · Bài NN"); `data-slide-id` `LNN-k-mm` (strand $k$, slide $mm$; strand title `LNN-k-00`); SVG figures in `img/lec-NN/` with `role="img"` and specific alt text. No `\text{}` with Vietnamese inside KaTeX (console warnings).
- **Narrow screens (≤ 760 px):** every deck uses the reading mode of `lecture-course.css` (from math-4-AI, adopted 2026-11-15 after the lecture 01 student review found the shrunken 16:9 frame unreadable at 390 px): `.slides` wrapped in `div.lecture-viewport` and the narrow-screen script of `lecture-template.html`. The narrow check scrolls each slide to its end; wide formulas and tables scroll horizontally in place, the page never does.
- **Timing:** the deck covers about 120 of the 150 minutes (target 45–52 slides, cap 55 with a reason in `storyboard.md`); timing lives in `storyboard.md` only.
- **Pipeline per deck** (sub-agent policy below): storyboard writer (plan and source analysis in one role, since the note is the only source; output `planning/lec-NN/storyboard.md` with a page → note-block table and proposed note changes) → storyboard gate (master decisions logged before drafting) → deck writer (stages of ≈ 15 slides) → five independent reviews on the frozen draft, each writing only `planning/lec-NN/reviews/deck-<vai>.md` → editor → recheck → master's final check (`deck_check.py`: console, page errors, failed requests, `.katex-error`, overflow, density recount; `deck-build/footer_check.py`: no content touching the footer or frame bottom; `deck-build/deck_lint.py`: density, strand-lead length, notes length, labels, banned phrases, repeated notes; screenshots at 1600×900 and 390×844 of every slide, the narrow ones scrolled to the end, looked at by the master; keyboard navigation: →, ↓, Space, Esc overview, `#/N` links of "Nội dung"; the viewer with `&deck=` for the note and exercises). A later one-slide edit still goes editor → maths and storyline recheck of that slide ±2 → browser check → log. Decisions go to `planning/lec-NN/review-log.md`, section "Bộ trang chiếu". Then the index card's **Bài giảng** gets the deck link, the note and exercise viewer links gain `&deck=…`, commit and push.
- **Known checker quirks:** `deck_check.py` flags OVERFLOW on the clipped SVG tail of KaTeX `\sqrt` (false positive; do not rewrite √ to silence it); editors misreport syllable counts, so the master recounts.

## Sub-agents (course settings)

The policy in `../CLAUDE.md` applies, with every sub-agent at effort `high` (`subagent_type: "general-purpose"`, `model: "opus"`, never `fork`). Writers on different files may run in parallel (user, 2026-11-04); a reviewer writes only its own report file. Each role's brief lives in `../tools/courses/statistical-learning-theory/2627-1/deck-build/` (common brief + role brief) and states role, inputs, output, write scope, done condition, `no-ai-slop` mode and "do not commit". `review-log.md` (section "Bộ trang chiếu") records, from the tool call: each agent's role, type, model and effort; the master's `chấp nhận | yêu cầu sửa | bác bỏ` with a reason for every stage output and every finding (findings are never deleted); new examples with their construction; UML pages consulted; proposed note changes for the author. Per lecture (`course-plan.md` §5): source analysis → plan (`outline.md`) → draft note (one writer, `no-ai-slop` Edit) → five independent reviews (master's student; mathematical accuracy with every proof and constant re-derived; learning-theory expert and source fidelity; academic/pedagogical with `no-ai-slop` Detect; storyline and linking) → one editor revises → recheck changed parts → exercises (writer, then maths and pedagogy reviews, then fix) → final check (viewer at 1600×900 and 390×844, print, `file://`, KaTeX errors, local-data sync, index card).

## Git (course settings)

Remote: `git@github.com:uet-iai-course/statistical-learning-theory.git` (public), branch `main`. GitHub Pages serves `main` / at http://courses.iaidev.com/statistical-learning-theory/ (enabled 2026-10-30). Commit and push without asking after each substantial edit (user decision 2026-10-30): a reviewed round of a note or exercises, a new lecture's material, a restructure, an index or rule change. Only accepted work (master approval logged in `review-log.md`, checks passed) is committed; small fixes may wait for the next substantial commit. After pushing, confirm with `git fetch` and `git branch -r --contains HEAD`.

## Done means (per lecture)

**Deck:** every blocking and serious finding of the gate, the five reviews and the recheck resolved and logged; `storyboard.md` matches the deck (IDs, strand titles, page → note-block table); the deck agrees with the note and `exercises.md` (consistency rules above); the final check passed at both sizes with no console or KaTeX errors, failed requests or real overflow; density caps held or excepted in `storyboard.md`; agents and decisions logged; index card and viewer links updated; committed and pushed.

**Note and exercises:** every blocking and serious finding resolved and logged; `outline.md` and `review-log.md` match the note; the viewer renders the note and exercises over HTTP and `file://` with no KaTeX errors or failed requests at both sizes and in print; `material-local-data.js` is in sync; the index card links the note and exercises only once they passed review.
