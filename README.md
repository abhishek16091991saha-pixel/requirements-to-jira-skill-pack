Requirements-to-Jira Skill Pack

An AI-assisted business analysis workflow: messy meeting notes, emails and draft BRDs go in; Jira-ready user stories come out, with conflicts, vague requirements and unowned decisions flagged instead of guessed.

Abhishek Saha | Senior Analyst | LinkedIn

All data in this project is synthetic. Nothing in it comes from my employer or any client.

Start here
Document	What it covers
Case study	Problem, design choices, testing, results, what failed and how I fixed it
Results and evaluation sheet	Every scored run, scores by criterion, time comparison, limits
AI playbook	When to use the Skill, when not to, review checkpoint, failure modes, data rules
Adoption and rollout plan	Proposed pilot, demo script, metrics, risks, governance
Skill versions and changelog	The Skill instructions for v1, v2 and v3
Test packs	The two synthetic scenarios, scoring rubric and answer keys
Jira import files	The CSV files imported into Jira
Screenshots	The Jira board and tickets
At a glance

I built and tested a Claude Skill that turns raw requirements material into traceable user stories with Given/When/Then acceptance criteria, then loads them into Jira. I tested it on two synthetic scenarios with a written rubric, improved it across three versions and imported the output into Jira.

The aim was not just faster drafting. It was a workflow a BA or PMO team could trust: every story points back to its source, and nothing is invented.

The problem

Business analysts and project managers spend hours turning meeting transcripts, email threads and half-written BRDs into stories. Typing is not the real risk. The real risk is what gets missed: two stakeholders asking for incompatible things, a requirement like “it should be fast” that nobody can test, and a decision everyone agrees is needed but nobody owns. Those problems surface late and cost the most.

What I built

The story-drafter Skill (three versions). Given raw sources, it:

extracts every stated requirement and merges duplicates across sources;
writes user stories with testable acceptance criteria, a proposed priority and a status (Ready, Needs confirmation or Blocked);
flags contradictions between sources, vague requirements (with the clarifying questions to ask) and unowned decisions, and keeps affected stories separate instead of silently picking a side;
cites the exact source line for every requirement, and writes [not stated] instead of inventing numbers, owners or dates;
produces a Decisions needed list for stakeholders and a Jira import file.

A test method. Two synthetic scenarios, each with six messy sources, a hidden answer key and a 14-point rubric.

A Jira import. The generated stories were imported into Jira with priorities and status labels (needs-decision, needs-confirmation), and related stories were linked.

How I tested it
Kestrel: a bank’s digital account-opening project.
Heron: an expense-claims tool at a logistics company, never shown to the Skill during development.
Sources in each: a kickoff transcript, an email thread, a half-written BRD, operations or payroll notes, chat snippets and a steering committee note.
Planted problems in each: one contradiction, one vague requirement and one unowned decision. In Heron the contradiction was two overlapping numeric thresholds (auto-approve under £100 vs. manager approval over £50), so it could not be caught by keyword.
Rubric: seven criteria scored 0 to 2 (completeness, testable criteria, contradiction caught, vague requirement caught, missing owner caught, no invented requirements, Jira-ready output). Maximum 14.
Results
Scenario	Skill version	Sources	Score (of 14)	Planted problems caught	Skill time	Manual time
Kestrel	v1	3	12	3 of 3	12 min	about 20 min
Kestrel	v2	3	14	3 of 3	12 min	about 20 min
Kestrel	v2	6	13	3 of 3	10 min	not measured
Heron (unseen)	v3	6	14	3 of 3	14 min	25 to 30 min
Heron (unseen)	v3	6	14	3 of 3	19 min	25 to 30 min

Times are self-measured, from sending the prompt to having read the output.

Quality: every planted problem was caught in all five scored runs, and both unseen-scenario runs scored 14 of 14.
Speed: about 40% less drafting time in both scenarios.
Variation: the same prompt gave 14 and 19 minutes and 16 and 17 stories, so I report ranges, not single figures.
What went wrong, and what I changed
Version	What the test showed	What I changed
v1 to v2	v1 scored 12 of 14. It wrote a few behaviours no source stated, opened with “nothing here is invented”, had one broken cross-reference, and only offered the Jira file.	Every acceptance criterion must trace to a source; inferred behaviour goes in Notes as assumed; no self-certifying statements; a final cross-reference check; a Decisions needed section; CSV produced by default.
v2 to v3	The CSV contained literal \n characters instead of line breaks, the source did not appear inside the Jira ticket, and one transcript timestamp was cited loosely.	The CSV is built with a CSV library, with real line breaks and a Source line in every description; citations must use the exact timestamp. Checked in Jira.
Still open	On the same input, the number of stories marked Needs confirmation varied between runs (6 vs. 9).	Planned for v4: use that status only when a missing detail would change the acceptance criteria.
The Jira board

The Kestrel and Heron outputs are in two Jira spaces, with 16 and 17 work items. Each ticket holds the story, numbered acceptance criteria, notes, status and source. Contradicting stories carry the needs-decision label and are linked to each other. See the screenshots.

How this was built, and what is independent

I defined the project, ran and timed every test, imported the results into Jira and decided each change to the Skill. The Skill instructions, test scenarios, answer keys and the scoring of each run were drafted with Claude’s help, so the scoring is not independent. An independent human review of one output is pending.

Limits
Synthetic data only; two scenarios; a small number of runs.
Scored against my own rubric, with AI assistance, and by one rater.
Output varies between runs, so a human must review every result.
The Skill drafts and flags. It does not decide: conflicts and unowned items still need a stakeholder.
Text inputs only; not tested on very long documents.
What I would do next
Test a scenario with no planted problems to check that the Skill does not invent issues.
Build v4 with the status rule above, then retest.
Add a second Skill that reviews a finished set of stories for quality (INVEST, testability).
Run a two-week pilot with a small BA team and measure time per story set, rework and weekly use.
If this ran inside a bank
Use only approved AI tools, and never put confidential or customer data into an external model.
A named human signs off every story set before it enters the backlog.
Keep a standing test set and rerun it whenever the Skill or the underlying model changes.
Keep an audit trail of what the Skill produced and what the human changed.

Trying the Skill

Each Skill folder contains one SKILL.md file. To use one, zip the folder and upload it in the Skills settings of your Claude account, switch it on, then paste your source material into a new chat and ask for Jira-ready user stories. Use synthetic or approved data only.
