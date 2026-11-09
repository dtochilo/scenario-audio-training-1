# Scenario Audio Training Webpage

## Files

Keep these five files together in the same folder (the website root):

- `index.html`
- `Scenario_1_Success.m4a`
- `Scenario_2_Success.m4a`
- `Scenario_3_Success.m4a`
- `Scenario_4_Success.m4a`

The supplied package contains `index.html` and this README. The four audio assets were not available in the build workspace, so add the original `.m4a` files beside `index.html` before launching or publishing the site.

## Run locally

For the most reliable browser behavior, serve the folder over HTTP instead of opening the HTML directly:

```bash
cd training_webpage
python3 -m http.server 8000
```

Then open `http://localhost:8000` in Edge, Chrome, Firefox, or Safari.

## Included behavior

- Four audio scenarios unlock in sequence.
- The next scenario stays locked until the current audio reaches its validated end.
- Native seeking, fast-forwarding, playback-rate changes, and media-session seek commands are blocked or rolled back.
- Validated audio position, completed scenarios, quiz attempts, learner name, and completion state are saved in browser `localStorage`.
- The quiz stays locked until all four recordings are complete.
- Five questions are scored automatically and require 5/5 (100%). A failed attempt displays the score and clears all answers.
- The certificate remains locked until the audio path is complete and the quiz score is 100%.
- The certificate can be downloaded as a PNG or printed/saved as a PDF through the browser print dialog.
- A **Reset all progress** button clears local progress after confirmation.

## Customize the quiz

Open `index.html`, find `const QUESTIONS`, and edit each `prompt`, `options`, and `correct` value. The `correct` value is the zero-based option index: `0` is the first option, `1` is the second, and so on.

The included five questions are a procedural completion check because the content of the audio recordings was not available during the build. Replace them with content-specific questions if the quiz should assess the scenarios themselves.

If you change course logic or questions after learners have started, increment `COURSE_VERSION` and update `STORAGE_KEY` so old browser progress does not carry into the revised course.

## Deployment notes

- Configure the web server to serve `.m4a` as `audio/mp4` or `audio/x-m4a`.
- Progress is saved only in the current browser/profile. For cross-device tracking, centralized reporting, or LMS records, connect the page to an authenticated backend or package it as SCORM/xAPI.
- Browser-side anti-skip controls are suitable for learner guidance but are not tamper-proof against a user with developer tools. High-assurance compliance training should validate progress on a server or in an LMS.
