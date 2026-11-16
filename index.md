# Privacy Policy

**USC Schedule Maker** (the Chrome extension)

Effective date: 2026-11-15

USC Schedule Maker helps USC students build and compare class schedules. This policy explains what the extension does with your information, in plain language. It describes what the extension's code actually does.

USC Schedule Maker is an independent student project. It is **not affiliated with, endorsed by, or operated by the University of Southern California (USC) or RateMyProfessors.com**.

## The short version

- Your schedule plan stays in your browser. Schedules are generated and ranked on your computer.
- When you use the AI features, the extension sends what the AI needs (your interview answers, course choices and preferences, or the feedback you type) to our backend, which passes it to Anthropic's Claude model to produce a reply. We do not store the content of these requests.
- To limit abuse of the AI backend, each install gets a random, anonymous install ID, and the backend stores your IP address only as a keyed hash, never the address itself. These rate-limit records are deleted once their time window (at most 24 hours) ends, and nothing is kept longer than 48 hours.
- We do not ask for your name, email, USC ID or password, and we never see your WebReg login.
- We do not sell your data, share it with advertisers, or use it for advertising.

## What stays on your device

These are kept only in your browser's storage for the extension (`localStorage`, IndexedDB and `chrome.storage.local`). They are not sent to us unless described in the next section.

- **Your plan:** the term, required courses, pinned sections, GE or elective slots, unit cap, allowed class times, ranking priorities, interview questions and answers, the interview summary and suggested courses, and any schedule feedback you added.
- **Course data cache:** copies of the public course catalog files the extension downloads, so it can start quickly and work if the network is unavailable.
- **Install ID:** the random rate-limit ID described below, kept in `chrome.storage.local`.

The schedules themselves are generated and ranked by code running in your browser.

This data stays until you change it, clear the extension's site data, or remove the extension. Removing the extension from Chrome deletes it.

## What is sent off your device, and why

### To our AI backend (Supabase), and from there to Anthropic

The AI backend is a set of Supabase Edge Functions run by the project. The extension sends to it only when you use an AI feature. Every AI request also carries the anonymous install ID described under rate limiting.

| Feature | What is sent |
| --- | --- |
| **Interview** (each question) | Selected term, required courses, any pinned sections, your GE or elective slots, your allowed hours, and the interview questions and answers so far, including anything you typed in free text |
| **Schedule explanations** | Your interview preferences and the top schedules shown (at most 10): their courses, sections, meeting times, instructors and scores |
| **Schedule feedback** that the extension cannot interpret on its own | The text you typed, the courses being scheduled with their public section details, and the schedule you are looking at |

The backend uses this to look up matching courses in the public course catalog and sends a prompt built from it to **Anthropic**, which provides the Claude AI model. Anthropic acts as our service provider (a processor): it processes the request to generate the reply and handles API data under its own [commercial terms](https://www.anthropic.com/legal/commercial-terms) and [privacy policy](https://www.anthropic.com/legal/privacy). The AI's reply (questions, suggested courses, explanations, structured feedback) is shown to you and stored with your plan on your device.

**Our backend does not save the content of these requests or replies.** It does not log your answers. Its logs record only an error type, such as "the model call failed", or that a request was rate-limited (which feature and for how long, without the install ID or IP address). Supabase, which hosts the backend, may keep standard technical request logs under its own [privacy policy](https://supabase.com/privacy).

Please do not type sensitive personal information (such as your student ID, health details or passwords) into the interview or feedback boxes. The AI features don't need it.

If the AI service is unreachable, you can use the built-in offline interview, which sends nothing.

### Rate limiting: install ID and hashed IP address

To keep the free AI backend from being overloaded or abused, the backend limits how many AI requests can be made:

- **Install ID:** the first time it needs one, the extension generates a random ID (a UUID), keeps it on your device in `chrome.storage.local`, and sends it with each AI request in an `x-usm-install-id` header. It is not derived from or linked to your name, email, Google account, USC account, WebReg data or device, and it is not used to track you across websites.
- **IP address:** the backend reads your IP address to apply per-network limits, but stores it only as a **keyed hash** (HMAC-SHA-256 with a secret key, a one-way scrambled value), never the address itself.
- **What is stored:** counters only. Each record holds the install ID or the hashed IP address, the endpoint, the start and end of a time window (one hour or one day), and how much AI usage was counted in it. No request content is stored.
- **Retention:** each record is **deleted once its window ends** (windows last at most 24 hours), either on the next AI request or by an hourly cleanup job, which also removes anything older than 48 hours.

### To USC's public course site (classes.usc.edu)

While you view schedules, the extension asks `classes.usc.edu` for live seat counts. These requests contain only the term and course codes, for example "CSCI-103 in Spring 2027". They are sent without your cookies, so they carry no login or account information.

### Course catalog downloads (Supabase Storage)

The extension downloads public course catalog files (courses, sections, final exam times and instructor ratings) from the project's public Supabase storage. These are ordinary file downloads and contain none of your information.

## What the extension does on WebReg (webreg.usc.edu)

The extension runs a content script on `webreg.usc.edu` pages only. There, it:

- **Adds a "myScheduleMaker" tab** to WebReg's navigation and shows the app in a panel when you click it. To place the tab it reads the page's navigation links. It does not read your grades, personal details, registration status or other account information.
- **Highlights sections** that a schedule picked when you open a course from a schedule's "Register" link. This is visual only. Nothing is clicked, submitted or added.
- **Adds sections to your myCourseBin, only when you ask.** When you click **Add all to myCourseBin** on a schedule and confirm the list, the content script acts **in your own signed-in WebReg session**. For each course it loads WebReg's course page, reads the current term, checks whether each section is already in your bin, and sends the same "Add to myCourseBin" request that WebReg's own button sends, including the security token WebReg puts on that page. It never sees or stores your WebReg password.

The myCourseBin feature is limited by design. Every WebReg request the extension makes is checked against an allowlist that permits only loading a course page and adding a section to your course bin. **It cannot register you, drop or remove classes, check out, or change anything else in WebReg.** Registration remains something you do yourself in WebReg. Nothing read from WebReg is stored or sent anywhere other than back to WebReg.

## The course data pipeline

A separate scheduled job in this project (not part of the extension) collects **public** information: USC's course catalog and seat counts, the registrar's final exam schedule, and public instructor ratings from RateMyProfessors.com (through an unofficial API). It does not collect any information about the people who use the extension.

## What we don't do

- We do not sell, rent or trade your information.
- We do not use or share your information for advertising, marketing or credit decisions.
- We do not use analytics, tracking pixels or advertising SDKs.
- We do not create user accounts or ask for your name, email, USC ID or passwords.
- We do not use or transfer your information for any purpose other than providing the extension's features.

The use of information received through Chrome extension APIs follows the [Chrome Web Store User Data Policy](https://developer.chrome.com/docs/webstore/program-policies/user-data-faq), including its Limited Use requirements.

## Your choices

- **Skip the AI.** You can build schedules without the AI interview; the offline interview sends nothing.
- **Delete your local data.** Remove the extension in `chrome://extensions`, or clear its stored data, to delete everything it kept on your device.
- **Rate-limit data** is deleted once its window (at most 24 hours) ends, and never kept past 48 hours. Because it is anonymous, we cannot look it up by person. Removing the extension deletes its install ID; a new install gets a new one.

## Children

The extension is meant for university students. It is not directed at children under 13.

## Changes to this policy

If this policy changes, the new version will be published at this same address with a new effective date.

## Contact

Questions or concerns? Open an issue at <https://github.com/TheOligarch/usc-schedule-maker-privacy/issues>.
