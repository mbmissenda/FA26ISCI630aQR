# FA26ISCI630aQR
# Student Questions Archive: Faculty Guide
 
This guide explains how to run the anonymous Q&A archive for a course, from first setup through each weekly update and each new semester.
 
**What it is:** a single web page (`student-questions-archive.html`) that shows every anonymous student question and your answer, grouped by module. Students can search it, see what is new this week, and browse the whole course archive.
 
**What you need:**
- The HTML file
- A place to host it (GitHub Pages works well)
- A text editor, or optionally a Google Sheet
- Access to edit your course in CourseArc
---
 
## 1. One-time setup
 
### Step 1: Host the page
1. Create a GitHub repository (for example `course-qa`) and upload the HTML file. Rename it `index.html` if you want a short link.
2. In the repository, go to **Settings > Pages**, choose your main branch, and save.
3. GitHub gives you a web address for the page. Open it and confirm it loads.
### Step 2: Add it to CourseArc
1. Try adding the page to a CourseArc page as an **embed** (iframe) using the web address.
2. If CourseArc does not allow embeds on your account, add a **link** that opens the page in a new tab instead. Students get the same experience.
3. Test it on a phone as well as a computer.
### Step 3: Name your modules
1. Open the HTML file in a text editor.
2. Find the block marked **EDIT THIS BLOCK** near the top of the script.
3. Under `modules`, set an `id` (a number) and a `title` for each module. The number is what you type when you file a question under that module.
4. Change `title` and `subtitle` to suit your course.
---
 
## 2. Weekly routine (about 15 minutes)
 
1. **Collect.** Copy the new questions out of CourseArc.
2. **Review for anonymity.** Edit each question so it cannot point to one student or one situation (see Section 5).
3. **Answer.** Write your answer. Short paragraphs read best. Link to course material when it helps.
4. **Add the entry.** Choose one of two methods.
### Method A: Edit the file directly
Add one line per question in the `ENTRIES` list:
 
```js
{ module: 3, date: "2026-09-17",
  question: "Can St. John's wort interfere with other medicines?",
  answer: "Yes. It can speed up how the body clears many medications...\n\nAsk a pharmacist before combining it with prescriptions." },
```
 
Rules that keep the page working:
- `module` is the number from your module list.
- `date` is `YYYY-MM-DD`. The date controls the "New" badge and the sort order (newest first).
- Put quotation marks around the question and answer. If your text contains a double quote, type it as `\"`.
- Use `\n\n` in the answer to start a new paragraph.
- Keep the comma at the end of each entry.
Save the file and upload it to GitHub (drag the new version into the repository and commit). The page updates within a minute or two.
 
### Method B: Use a Google Sheet (recommended if you add many questions)
Set this up once, and after that you only edit the sheet. The page reads it automatically.
 
1. Make a sheet with two tabs.
2. **Tab 1, "Inbox"** (private, never published), with these columns:
   `Module | Date | Question | Answer | Publish | Original`
   - Paste the raw student question into `Original`.
   - Put your edited version into `Question`.
   - Write your answer into `Answer`. Type `Y` in `Publish` when it is ready.
3. **Tab 2, "Public"** (this is the one you publish):
   - In row 1 type the headers: `Module | Date | Question | Answer`
   - In cell A2 enter: `=FILTER(Inbox!A2:D, Inbox!E2:E="Y")`
4. Publish only the Public tab: **File > Share > Publish to web**, choose the **Public** tab, choose **Comma-separated values (.csv)**, and publish.
5. Copy the link into `sheetCsvUrl` in the HTML file, near the top. Save and upload the file once.
**Why two tabs:** anyone who has the published link can read everything on the published tab, including rows the page does not display. The Public tab contains only your edited, approved text. Never publish the Inbox tab, because it holds raw student wording.
 
**Note:** the sheet method works when the page is hosted on your own site (like GitHub Pages). It will not work in a preview or on a file opened from your computer.
 
If the sheet cannot be reached, the page shows the entries saved in the file and a short notice. Keeping a recent copy of the entries in the file is a good backup.
 
---
 
## 3. Starting a new semester
 
Do this before the term opens, so students never see last term's questions.
 
1. **Archive last term.** In your repository, copy the finished page into a folder named for the term (for example `fall-2026/`). Its address stays available if you or students want to look back.
2. **Start fresh.** Make a copy of the HTML file for the new term (for example `spring-2027/`).
3. **Clear the entries.** Delete the sample or old entries inside `ENTRIES`, leaving the empty list: `const ENTRIES = [ ];`
4. **Update the modules and title** if the course changed.
5. **New sheet (Method B only).** Make a new copy of the sheet for the term, publish its Public tab, and paste the new link into `sheetCsvUrl`. Do not reuse last term's link.
6. **Update CourseArc.** Point the embed or link to the new term's address.
7. **Test.** Open the page and search for a word to confirm it works.
### Reusing good questions
Some questions come up every term. Once a semester ends, look through the archive and copy any that are broadly useful into the new term's list as a starting set. Give them the date of the first day of the term, and check that the answers are still current.
 
---
 
## 4. What students see
 
- A list of modules on the left (or across the top on a phone), with a count of questions in each.
- All modules together, or one module at a time.
- Each question above its answer, with the date.
- A "New" badge for 7 days (change `newDays` in the file to adjust).
- A search box that looks across all modules.
---
 
## 5. Anonymity and content guidelines
 
- Tell students in the course, before they ask, that questions may be lightly edited before they are posted.
- Remove names, and remove any detail about a person's illness, family, workplace, or other situation that could identify them.
- Small classes are the greatest risk. When in doubt, generalize the question ("Is it safe to combine an herb with a prescription?").
- Do not post anything that gives individual medical advice. Answer in terms of the course content and refer students to their own clinician or pharmacist.
- Check that every answer is accurate and up to date before publishing. Dietary supplement and herb-drug guidance changes.
- Keep the raw student text out of anything public.
---
 
## 6. Troubleshooting
 
| Problem | What to check |
|---|---|
| The page is blank or shows no entries | A missing comma, a stray quotation mark, or a missing bracket in `ENTRIES`. Compare against the example above. |
| An entry does not appear | Its `module` number does not match any `id` in `modules`. |
| An entry appears in the wrong order | Check the date format is `YYYY-MM-DD`. |
| Sheet entries are not loading | Confirm the link is the published **CSV** link for the **Public** tab, the headers are exactly `Module, Date, Question, Answer`, and the page is hosted online. |
| The "New" badge never appears | The entry's date is more than `newDays` old. |
| CourseArc will not show the page | Use a link that opens the page in a new tab, or ask CourseArc support whether embeds from your GitHub address are allowed. |
| An answer runs together | Use `\n\n` between paragraphs. |
 
---
 
## 7. Quick reference
 
| Task | Where |
|---|---|
| Change page title and description | `CONFIG.title`, `CONFIG.subtitle` |
| Name and order the modules | `CONFIG.modules` |
| Change how long "New" shows | `CONFIG.newDays` |
| Connect a Google Sheet | `CONFIG.sheetCsvUrl` |
| Add questions by hand | `ENTRIES` |
 
If you get stuck, save a copy of your file before making changes, so you can go back to a working version.
 
