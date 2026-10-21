# Year 6 Topical Assessment

GitHub Pages webapp: [Homepage](https://mohammaddhameri-blip.github.io/Year-6-Topical-Assessment/) · [Unit 10: It's a Mystery](https://mohammaddhameri-blip.github.io/Year-6-Topical-Assessment/unit10/) · [Authorised teacher review](https://mohammaddhameri-blip.github.io/Year-6-Topical-Assessment/unit10/teacher/).

## Unit 10 — four skills

- Reading: original mystery with 8 multiple-choice questions.
- Listening: narrated community-park incident using the device speech engine with speed control, then four written comprehension answers.
- Reading–Writing: two subjective questions about a community notice.
- Writing: 4 dialogue choices and 5 original dialogue lines.
- Speaking: 3 microphone recordings about someone special and 2 follow-ups.
- Intended duration 20–30 minutes, without a forced timeout.

## Release state

**Secure teacher testing only; official Year 6 pupils are not yet admitted.** The backend currently accepts registered tester codes and uses its own secure random session token. The access-code entry field is masked and does not display example tester codes.

Written responses autosave on the device and synchronize to the secure `year6-unit10` Supabase Edge Function. Voice recordings are kept locally and uploaded to a **private** storage bucket. Final submission locks the attempt. A teacher with a separately provisioned Supabase Auth account and explicit authorisation can inspect responses and recordings, enter scores, TP1–6 and CEFR-aligned indicators, approve results, and authorise a retake. Pupils only see the scored report **after teacher approval**.

No service-role credentials or answer keys are included in this public repository. The teacher blueprint remains separate and private.

### School administration still required

Teacher authorization is not self-service: an administrator must invite/create a Supabase Auth user and explicitly allowlist that account in `public.y6_unit10_teacher_access`. See [Unit 10 setup details](unit10/README.md). The official mode flag `public.y6_unit10_settings.official_enabled` must remain `false` until stronger pupil identity confirmation and appropriate safeguarding and consent procedures are in place. Pupil codes alone are not secure identity verification.

### Remaining improvements

AI-assisted marking and transcription are not connected; scores are presently teacher-entered. Narration uses device speech synthesis and is not the previously generated MP3. Interrupted attempts resume on the original device while session and locally saved recordings remain intact. Recovery from a lost device/session and full multi-device offline media synchronization require additional work.

## Deployment

The `main` branch automatically deploys via GitHub Pages Actions. `.github/workflows/unit10-smoke.yml` also checks both UIs' JavaScript syntax and verifies rejection of unauthorised API requests. 
