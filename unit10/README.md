# Unit 10 — It's a Mystery

## Current release: secure teacher-testing stage

The Year 6 four-skills assessment is available at [the Unit 10 page](https://mohammaddhameri-blip.github.io/Year-6-Topical-Assessment/unit10/). Registered `TST-###` tester codes can begin or resume one attempt on the same device. **Official `Y6-###` access remains disabled** in the backend until the school confirms appropriate pupil authentication and authorises official release.

Assessment sections: Reading 8 MCQs; Listening 4 complete-sentence answers based on an original community-park script played through the device's text-to-speech engine, with playback speeds; Reading–Writing 2 subjective notice questions; Writing 4 dialogue choices and 5 original dialogue lines; Speaking 3 microphone recordings.

### What works now

- Server-controlled attempts tied to the existing `students` roster; existing school assessment records remain untouched.
- Answers save on-device and automatically sync to a private database when connected. When offline, local answers persist until the next successful sync.
- Voice recordings save in the browser's IndexedDB and upload to a **private** Supabase Storage bucket. Failed voice uploads can be retried at final submission.
- Final submission locks the attempt; server checks that every answer and all 3 recordings are present.
- Teacher reviews require **Supabase Auth + an explicit allowlist entry**, not a pupil code. The dashboard at [teacher review](https://mohammaddhameri-blip.github.io/Year-6-Topical-Assessment/unit10/teacher/) supports viewing recordings, written answers, objective-item evidence, separate scores out of 25, TP 1–6, CEFR indicators, approval, and retake permission.
- No scores are revealed automatically to pupils. AI marking is **not yet connected**; teacher judgement and approval are required.

### One-time teacher setup

1. In the school's Supabase project, create or invite the teacher as a Supabase **Auth user** with an email and password. A Supabase Dashboard account alone is not the same as an Auth user.
2. A database administrator must explicitly authorise that Auth user's UUID. From the SQL Editor, substitute the appropriate school-verified teacher email:
   ```sql
   insert into public.y6_unit10_teacher_access (user_id, active)
   select id, true from auth.users where email = 'verified-teacher@example.com'
   on conflict (user_id) do update set active = excluded.active;
   ```
3. The teacher can then sign in at `unit10/teacher/` and review actual tester submissions. No teacher passwords or private audio URLs belong in GitHub.
4. Official pupil codes remain blocked while `public.y6_unit10_settings.official_enabled = false`. Do **not** enable them until stronger pupil identity checks and the school's privacy and consent practices are confirmed.

### Known limitations

- Pupil codes alone are not strong authentication and could be guessed. Same-device session recovery works, but lost browser storage requires teacher-assisted recovery.
- Audio is synthesized by the device and requires a working speech engine; the original MP3 asset has not yet been hosted.
- Speech transcripts, AI-assisted provisional scoring, full CEFR moderation and teacher-controlled public results release are future steps.
- Camera/microphone permission is necessary; network loss during upload means retry from the same device.
- No end-of-assessment time limit is enforced: the 20–30 minutes is an estimate.

Backend Edge Function: `year6-unit10`; private tables: `y6_unit10_attempts`, `y6_unit10_settings`, `y6_unit10_teacher_access`, `y6_unit10_retake_permits`; private bucket `y6-unit10-speaking`. No service-role secret is placed in browser files.
