# Website Plan

Working notes. Add to this as we go.

## Goal

Business: Selkent Recycling Limited (registered company name; register the domain under this name).

A simple website for Dad's shop so customers can see the services and send an enquiry. Dad follows up by phone or email from his normal Yahoo account. No replying through the site.

## Decisions so far (and why)

| Decision | Why |
|---|---|
| Static site (HTML/CSS/JS) | No database or server needed, so it's cheap, fast and has little to hack |
| Hosting on GitHub Pages | Free, deploys on every push, and builds on my existing GitHub pipeline practice |
| Public repo | Shows my code and how I managed the project for a portfolio. Free Pages needs it too. No secrets or customer data go in the repo |
| Form service: Web3Forms (free plan) | Emails submissions to Dad without me running a backend. Free plan is 250 submissions a month, includes hCaptcha and a custom thank-you page. Formspree's free plan (50 a month) was too small |
| Launch with honeypot only; hCaptcha ready to switch on | Avoids CAPTCHA friction for older or stressed customers; escalate if spam appears. A phone/email fallback sits under the form |
| Submissions go to Dad's Yahoo inbox | He already uses it; no custom email needed |
| Domain bought last, in the business's name | Preview on the free GitHub address first; the business owns the domain |

## Spam protection (build this in from the start)

Why: the form's ID is visible in public code, so anyone could submit to it. Without protection, Dad's inbox gets flooded.

### The layers

1. **Honeypot field (ON at launch)**: a hidden field real people never fill in. Simple bots fill every field, so any submission with it filled in gets rejected. Invisible to customers.
2. **hCaptcha (built in, OFF at launch)**: a "prove you're human" challenge. Switched on in the Web3Forms dashboard, and the commented-out lines in `index.html` need un-commenting, only if spam becomes a problem.
3. **Restrict allowed domains (not used)**: makes the form service only accept submissions from our own site address. On Web3Forms it is a paid (Pro) feature, so it is a possible upgrade if the first two layers fail.

### Risk assessment (what the evidence says)

Sources are mostly vendors of spam or CAPTCHA tools, so they have a commercial interest, and none are specific to a small removals business. Treat as a guide, not proof.

- **Likelihood of spam: probably high enough to plan for.** Akismet says spambots target sites of all sizes regardless of traffic. Netlify reported almost half of processed form submissions in its tests were spam (2019, platform-wide). Some sources say new forms get hit within days.
- **Honeypot alone is weak against targeted bots.** Formspree says a script written for your specific form ignores honeypots, and Justia notes many bots fill in as few fields as possible. It still stops the simplest bots at no cost to customers.
- **hCaptcha has a real cost to customers.** A 2023 UC Irvine study found image challenges took 15-26 seconds with 71-85% human accuracy. Visual puzzles are hostile to low-vision users. No published study gives a universal conversion loss for a form like ours. Web3Forms' own docs say hCaptcha can be hard to solve.
- **Impact of spam: low to moderate.** Nuisance and real enquiries buried in junk, plus the 250 submissions a month cap. Nothing private is exposed (the access key can only send emails to Dad's inbox, per the Web3Forms FAQ).

### Decision

Launch with the honeypot and Web3Forms' built-in spam filtering. Expect spam, watch for it, and switch hCaptcha on if Dad starts getting a high level. Keep a clear "contact us by phone or email instead" box right under the form, so anyone who struggles with a form or the CAPTCHA can still reach him.

### Escalation steps

1. Dad (or I) notices junk enquiries arriving: note roughly how many a week.
2. Switch hCaptcha on in the Web3Forms dashboard, un-comment the hCaptcha lines in `index.html`, and push the change.
3. Test the form on a phone, and ask someone less techy to try it.
4. If spam still gets through, consider Web3Forms Pro for domain restriction, or another CAPTCHA option.

### Interview talking points

- Risk-based decision: I weighed how likely spam is, how bad it would be, and the cost of CAPTCHA friction for real customers, many of whom may be older or in a stressful situation.
- Start with the low-friction control, monitor, and escalate. Defence in depth is built in, with the stronger layer ready to switch on.
- Accessibility fallback: a visible phone and email option so nobody is locked out.
- The form key is public by design, so protection comes from filtering and restrictions, not hiding it.
- I checked the claims against vendor docs and independent studies, and noted where sources had a commercial interest.

## Page sections

- Header with business name and phone number
- Hero: what we do, one clear call to action
- Services: removals, clearances, furniture and white goods, social services support (deep cleaning, decluttering for vulnerable customers; wording to be agreed with Dad)
- Photos (need real ones from Dad)
- Contact details
- Enquiry form: name, address, email, preferred date, services needed, extra details
- Footer with privacy notice

## Privacy and data

- Form collects names, addresses and emails, so add a short privacy notice (what's collected, why, who sees it, how long it's kept)
- Keep it minimal: only ask for what Dad needs to follow up
- No customer data stored in the repo
- Check the form service's data handling and where it stores submissions

## Phase 2: admin form for Dad

Goal: let Dad update text and photos himself without touching code.

- Option: a Git-based CMS such as Decap CMS or Pages CMS. It gives a form-style editor and saves changes to the repo, which redeploys the site automatically. Free.
- Until then: Dad sends photos and wording and I update the repo.
- Build phase 1 so this is easy to add: photos in one folder, services kept in one clearly labelled section or data file, no content buried in the layout.
- Security: give Dad a limited account, never my main login. Keep branch protection on `main` so changes can be reviewed.
- To decide later: which CMS, how login works, whether changes go live straight away or need my approval.

### Phase 2 maybe: before and after photos (?)

- Idea: a few anonymous before-and-after photos for deep cleaning and decluttering (e.g. a bathroom and a kitchen), neutral captions, no mention of vulnerable customers next to them.
- Open question: how many customers would agree to their photos being used? Only go ahead if enough say yes.
- If we do it: get the customer's permission, crop out anything personal (post, documents, family photos, recognisable window views), and strip photo location data before uploading, because the repo is public.

## Still to decide

- Final business name and domain name
- Photos and which services to feature
- Wording for the social services section
- Licence for the repo

## Checklist

- [ ] Create the GitHub repo (public) and add README and PLAN
- [ ] Turn on two-factor login and branch protection on `main`
- [ ] Build the page locally (Live Server)
- [ ] Add the form with honeypot and CAPTCHA
- [ ] Deploy on GitHub Pages
- [ ] Test the form, including the Yahoo spam folder
- [ ] Create the Web3Forms access key (with Dad's Yahoo address); leave hCaptcha off for now
- [x] Fill in the phone number and email in the "contact us directly" box under the form (done from the business card)
- [x] Opening hours added (Monday to Friday, 8am to 4pm)
- [x] Registered office added to the footer (Erith, from Companies House)
- [x] Company number added to the footer (08772642)
- [ ] Footer shows the registered office as it appears on Companies House (Erith). If the real office is the Gillingham shop, Dad updates it with Companies House, then the footer changes to match
- [ ] Tell Dad: Companies House shows accounts overdue (were due 30 Sept 2026) and a confirmation statement due 27 Nov 2026
- [ ] Ask Dad/accountant whether to update the SIC code (currently electrical appliance retail) to cover removals and clearances
- [ ] Monitor for spam after launch; switch hCaptcha on if it becomes a problem (see Escalation steps)
- [ ] Optional: restrict form submissions to the site's address (paid Web3Forms feature)
- [ ] Check with Dad: waste carrier registration (get the number; it can be checked on the Environment Agency register). If he has it, add it to the About section and consider the footer
- [ ] Check with Dad: any accreditations (e.g. British Association of Removers, Move Assured, Road Haulage Association). Do NOT mention any on the site unless confirmed
- [ ] Get Dad's insurance details (type of cover, e.g. public liability and goods in transit, and the certificate). The site currently just says "Insured". Add details only if he's happy to
- [ ] Ask Dad: should "assembly available for a fee" be mentioned? Left out for now, along with the social services set-up fee
- [x] Privacy notice (`privacy.html`) written
- [ ] Confirm the 12-month enquiry retention period with Dad (the figure used in the notice)
- [ ] When creating the Web3Forms key, check the dashboard shows 30 days of submission history (the figure used in the notice)
- [ ] Dad or the accountant: take the ICO data protection fee self-assessment (ico.org.uk/fee-checker)
- [ ] Optional: GitHub Actions check (HTML validation or link checker) before deploy
- [ ] Register the domain in the business's name, with auto-renew
- [ ] Connect the domain, then update the form's allowed domain
- [ ] Set up a free Google Business Profile
- [ ] Phase 2: add an admin form (CMS) so Dad can edit text and photos
- [ ] Phase 2 maybe: before and after photos, if customers agree
