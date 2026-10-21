# Year 6 Topical Assessment

This repository is a GitHub Pages static webapp. The homepage lists topical English assessments; **Unit 10: It’s a Mystery** is available at `unit10/`.

## Installation / deployment

1. Extract `Year6_Topical_Assessment_GitHub_Upload.zip`.
2. **Do not upload the ZIP itself**. In GitHub, open this repository, choose **Add file → Upload files**, and drag in the contents of the `year6_topical_publish` folder: `index.html`, `.nojekyll`, `unit10/` and `README.md`. GitHub's browser UI may need directory upload support; if it flattens directories, use GitHub Desktop or `git` to commit the extracted folder structure.
3. Under **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then Save.
4. The default URL should be `https://mohammaddhameri-blip.github.io/Year-6-Topical-Assessment/` after GitHub Pages finishes publishing. Only treat it as live after checking it loads.

## Unit 10 functionality

- Original mystery Reading passage with 8 multiple-choice questions.
- Original listening narration (`unit10/audio/vandalism.mp3`) with 4 short answers.
- Subjective reading-and-writing comprehension and individual dialogue writing.
- Speaking requires 3 browser microphone recordings, with a microphone test and replay.
- Typed responses autosave using localStorage; audio saves using IndexedDB; offline-capable after initial load.
- Tester codes `TST-###` only. No server verification; **this is NOT an official exam**.
- The submission screen says **Awaiting teacher review** but **no actual submission leaves the device**.

## Production requirements still outstanding

A secure backend must verify existing `Y6-###` accounts against the shared student roster, enforce one official attempt with teacher-authorised retakes, securely upload audio and written responses, prevent loss across devices, run AI-assisted marking, and require teacher approval before pupils can view TP or CEFR-indicative reports. **Never expose the teacher answer scheme in this public repository.**

## Teacher blueprint

A private teacher blueprint is provided separately as `Year6_Unit10_Assessment_Blueprint.md`. It must **not** be committed to this public repository because it contains answer keys and scoring details.
