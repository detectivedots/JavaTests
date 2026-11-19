# Java Chapter Tests

A static, responsive multiple-choice quiz site for GitHub Pages. It reads chapter JSON files from the `tests/` folder and uses each file's `name` property as the chapter title.

## Features

- Pick a chapter by its JSON `name`.
- All choices are checkboxes, including single-answer questions.
- Original choice order is preserved; choices are never shuffled.
- Submit a response to see whether it is correct, the correct answer, and the explanation.
- Use **Give up · Show answer** to reveal the correct answer and explanation.
- A live score and completion progress remain visible during the test and after completion.
- Navigate between questions using Previous/Next or the question navigator.
- No timer.
- Question, choice, and explanation line breaks and indentation are preserved with responsive wrapping.
- `pages` and `answer_pages` are ignored. Recognizable running headers from the sample book (such as `Review Questions 95`) are removed from displayed text; ordinary whitespace and code indentation are retained.
- Questions without a usable answer key can still be completed, but are excluded from the graded score.

## Folder structure

```text
java-chapter-quiz/
├── index.html
├── README.md
└── tests/
    ├── manifest.json
    ├── chapter-2-demo.json
    ├── chapter-3.json
    └── ...
```

## Add a chapter

1. Put the chapter's JSON file inside `tests/`.
2. Add its filename to `tests/manifest.json`:

```json
{
  "tests": [
    "chapter-2.json",
    "chapter-3.json",
    "chapter-4.json"
  ]
}
```

3. Make sure each file has a `name` and a `questions` array. The app displays `name` as the chapter title.

The app uses `questions.length` for the displayed count rather than relying on `question_count`, so incomplete or stale count metadata won't break the UI.

### Supported question fields

```json
{
  "name": "Chapter 2: Operators",
  "questions": [
    {
      "number": 1,
      "question": "Question text...\n    code = stays indented;",
      "choices": {
        "A": "First choice",
        "B": "Second choice"
      },
      "answer": ["A"],
      "explanation": "Why A is correct...",
      "pages": [1],
      "answer_pages": null
    }
  ]
}
```

- `answer` may be a string such as `"A"` or an array such as `["A", "C"]`.
- `answer` can be `null` or omitted when the answer key is unavailable.
- `explanation` can be a string or empty/null.
- `pages` and `answer_pages` are not displayed or used by the app.
- Choice keys are shown in the order they appear in the JSON object.

## Run locally

From this folder, start a small local web server:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000>.

Do not open `index.html` directly with a `file://` URL. Browsers block the JSON `fetch()` requests in that mode.

## Publish with GitHub Pages

1. Create a GitHub repository and upload the contents of this folder (the `index.html` file must be at the published root).
2. Open **Settings → Pages** in the repository.
3. Choose **Deploy from a branch**, select your branch and the repository root, then save.
4. Open the published Pages URL.

The app uses relative paths, so it works both at a GitHub Pages project URL and at a custom domain.

## Score behavior

- A submitted correct or incorrect response counts in the score.
- Giving up counts as a completed incorrect attempt (the answer is revealed).
- Questions with no usable answer key count as completed but are excluded from the graded score denominator.
- The displayed score is `correct / graded questions`; completion is shown separately as `completed / total`.

Progress is held in memory while the page is open. Refreshing the page or leaving the test resets the attempt.

## Included example data

`tests/chapter-2-demo.json` contains the first three question objects supplied in the conversation, as a small demonstration. Replace it with the complete chapter JSON when ready.
"# JavaTests"  git init git add README.md git commit -m "first commit" git branch -M main git remote add origin https://github.com/detectivedots/JavaTests.git git push -u origin main
"# JavaTests"  git init git add README.md git commit -m "first commit" git branch -M main git remote add origin https://github.com/detectivedots/JavaTests.git git push -u origin main
"# JavaTests" 
