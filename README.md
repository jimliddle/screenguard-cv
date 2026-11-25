# ScreenGuard CV

##ScreenGuard came out of working with some young people on how quickly their CV's where getting rejected by AI screening software when they were submitting an application for a job. ScreenGuard CV checks a CV against a job advert before application, and itt shows how well you match the job, which requirements your CV doesn't yet prove, and whether hiring software is likely to read the file properly. It can also tailor the CV to the job (but it won't let anything untrue into it).

As with a lot of the Apps I create, it's a single web page that runs in the browser. There's nothing to install and no account to create and you can access it at:



## What it does

- **Checks the file.** Flags scanned or picture only PDFs, two column layouts, Word tables, images, missing contact details and text that has lost its line breaks. A CV that hiring software can't read is never seen by a person.
- **Scores your match with the job (Job Fit).** Picks out the job's hard requirements, such as years of experience, a degree, tools, the right to work and location, and shows the line of your CV that proves each one. It also points out where your CV uses different words from the job advert, since recruiters usually search for the advert's exact terms.
- **Scores the CV itself (CV Readiness).** Looks at layout, whether your results have numbers behind them, and clear writing. This is kept separate from Job Fit.
- **Checks seniority and dates.** Compares your latest job title with the role, and looks for gaps of more than 6 months, overlapping jobs and dates without months.
- **Asks about gaps.** When the job wants something your CV doesn't show, it asks whether you have done it, where and what you did. Only your answers go into the CV.
- **Tailors the CV.** Reorders and rewords your CV in the job's language, using only your original CV and your answers. After AI tailoring, every line is checked against those sources. Anything the AI added that isn't there is taken out, or your original sentence is put back, and you can restore anything that is true.
- **Tracks your applications.** Saves the exact CV you sent for each job, with its scores, and lets you record what happened. After 8 results it works out which scores led to interviews for you.
- **Exports** to Word, PDF (through your browser's print dialog), plain text or the clipboard, after warning you about placeholders and anything you haven't confirmed.

## Using it

Open `index.html` in a browser. If GitHub Pages is switched on for this repository, you can also use it at the Pages address.

1. Upload your CV (PDF or Word) or paste it in. Click **Load Sample CV** to try it with an example.
2. Click **Screen CV Now** for a first check.
3. Go to **Job & Tailor**, paste the job advert, and screen again to see Job Fit and the must-haves.
4. Answer the gap questions that apply to you, then click **Tailor with My Answers**.
5. Look through the **Truth Check**, then export from the **Export** tab and save the application in the **Tracker**.

The app needs an internet connection to load its styling and the PDF and Word readers.

## AI providers

ScreenGuard works without an API key in **Local mode**, which runs everything in the browser. For a fuller written assessment and AI tailoring, open **AI Settings** (top right) and add a key for one of:

- Claude (Anthropic): `claude-sonnet-5-5` or `claude-haiku-5-5`
- ChatGPT (OpenAI): `gpt-5.4-mini` or `gpt-5.4`
- Gemini (Google): `gemini-3.8-flash` or `gemini-3.7-flash`

Requests go straight from your browser to the provider you choose. You pay that provider for what you use.

## Privacy

Your CV, job adverts, answers and Tracker stay in your browser's storage. They're only sent anywhere if you use an AI provider, and then only to that provider.

API keys are saved in the browser too. They're encrypted, but the key needed to read them is stored in the same place, so this only stops someone casually looking. On a shared computer, choose **Session only** in AI Settings and click **Clear Data** when you've finished.

## What I've tested

I tested the scoring and the tailoring on public data. The results are fairly modest.

**Job Fit.** It scored 1,759 pairs of CVs and job adverts that someone had labelled as a good, possible or poor match. Take two CVs for the same job, one labelled good and one poor: Job Fit scored the good one higher about two times in three. A coin toss would manage one in two. It didn't work well for comparing scores across different jobs, so by default the app says Strong, Partial or Weak match rather than predicting an interview. The dataset doesn't say who labelled it or how, so treat these results as rough.

**Tailoring.** It took 100 CVs that were close to matching their job. Claude Haiku tailored them and GPT-5.4 mini judged them, without knowing which version was which. Honest AI tailoring raised the judge's match score by about 1.5 points out of 100 and made almost no difference to how many CVs were put through to a phone screen: 8 before tailoring and 9 after. The app's offline tailoring made no difference.

An earlier version without the truth check did better in a similar test, but about one tailored CV in ten included a skill, qualification or figure the person didn't have. A stricter prompt now cuts those additions by about 80%, and the truth check removes the rest. On the earlier results it removed every invented item we had found by hand and kept 96% of the content.

In practice, rewording a CV won't get you through an AI screener on its own. Applying for jobs you match, meeting the must haves and adding real experience matter the most when combatting AI screeners. The gap questions are the part I expect to help most in the App.

## The benchmark

`benchmark.html` You can rerun the tailoring test with your own API keys.

1. Download `test.csv` from the [resume-job-description-fit dataset](https://huggingface.co/datasets/cnamuangtoun/resume-job-description-fit) on Hugging Face (Files and versions tab) and choose it on the page. The file is only read in your browser.
2. Choose a judge provider, model and key. To test AI tailoring, tick **Also test AI tailoring** and pick a different provider for tailoring, so a model isn't marking its own work.
3. Pick **Near the line** and the number of pairs, then click **Run benchmark**. Settings are locked while it runs.

Each pair is judged twice (three times with AI tailoring), in random order, against its job advert. The page reports how many CVs were put through to a phone screen in each version, how many changed in each direction, the average change in match score with a 95% range, and how much the truth check removed. You can download every result as a CSV, including the tailored CVs. A run of 100 pairs with AI tailoring makes about 400 API calls. With small models that costs a few dollars, but check your providers' prices.

## Limits

ScreenGuard can't see an employer's own screening questions (such as visa sponsorship, location or salary), whether a job is already meant for someone, or how many people have applied, so there are some things no CV changes can fix. As an example, in a well known study, identical CVs got different numbers of callbacks depending only on the name at the top! ScreenGuard can help you avoid rejections you can prevent and focus on jobs where you stand a chance, but it cannot of course guarantee an interview.

## Data and credits

- The labelled CV and job pairs come from [cnamuangtoun/resume-job-description-fit](https://huggingface.co/datasets/cnamuangtoun/resume-job-description-fit). No licence is stated for that dataset, so it isn't included here.
- The callback study is Bertrand and Mullainathan (2004), "Are Emily and Greg More Employable than Lakisha and Jamal?". I used the version published in the [OpenIntro](https://github.com/OpenIntroStat/openintro) R package.
- The app uses [Tailwind CSS](https://tailwindcss.com), [Lucide](https://lucide.dev) icons, [PDF.js](https://mozilla.github.io/pdf.js/) and [Mammoth](https://github.com/mwilliamson/mammoth.js), loaded from public CDNs.

## Licence

MIT. See [LICENSE](LICENSE).
