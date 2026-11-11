# Code of ethics

authority-finder checks the case citations in an English legal document against
Find Case Law, The National Archives' judgment service, and reports what it found.
This page states the rules the tool is built to, in public, so that anyone can hold
it to them. It is the code of ethics named in our Find Case Law computational
analysis licence application (November 2026). Each rule is also a constraint in the
project's engineering contract, and the automated tests enforce the ones that can be
tested.

## The rules

1. **The document stays on the user's machine.** It is never uploaded. Only the
   citation strings themselves are sent, and the titles of the Acts and statutory
   instruments the document names. Any machine-learning model the tool runs is a local
   one, with weights on disk, and there is no hosted model API, ever.
   *Amended 2026-11-09:* was "Only the citation strings themselves are sent, to Find
   Case Law and nowhere else." Statute titles now also go to legislation.gov.uk (rule 6).

2. **We never say a case is good law.** No open data exists that could support the
   claim. The tool says "found", "not found in Find Case Law" or "outside coverage".
   It never says "correct", "valid" or "still good".

3. **Nothing is silently dropped.** Every reference the tool extracts appears in the
   report with a status. A reference it could not resolve is a reported row, never a
   missing one.

4. **We say what we did not check.** Find Case Law holds modern judgments only, from
   2001 at the earliest, and no House of Lords, Scottish or Northern Irish courts.
   Citations outside that boundary are reported as "outside coverage", never as "not
   found", and any headline figure is given alongside the share that fell outside it.

5. **Same input, same output.** The tool is deterministic. No generative model is used
   anywhere. The local classifier is pinned by hash and decoded without randomness, and
   a test checks that running it twice gives the same answer.

6. **One source, used politely.** Resolution uses Find Case Law alone: one lookup per
   citation named in the user's document, every response cached so a document is never
   looked up twice, always well inside the published rate limit. Nothing is harvested
   from any other legal database, and nothing is done in bulk without the licence that
   permits it.
   *Amended 2026-11-09:* an Act or statutory instrument named by title and year in the
   user's document is also looked up on legislation.gov.uk: one title lookup each,
   cached, at least 5 seconds apart (its robots.txt crawl delay), with a named
   User-Agent, under the Open Government Licence. The tool says "found on
   legislation.gov.uk" or "not found on legislation.gov.uk", and never that a statute is
   current or in force. Case citations are still resolved against Find Case Law alone.
   Until this date the rule read "Resolution uses Find Case Law alone".
   *Amended 2026-11-11:* a treaty or convention named in the document (the European Convention on
   Human Rights, a United Nations convention, a Hague convention) is detected and listed, never
   looked up. Where the project has opened a treaty's official text by hand, the list offers a
   link to it for the user to click; the tool makes no request to any treaty site, and never says a
   treaty is in force, ratified or binding.

7. **No analysis of people.** The classifier tags citation spans in text. It does not
   select, count or profile parties, judges, counsel or anyone else, and no personal
   data is extracted, stored or output beyond the judgment text itself.

8. **Measured, not asserted.** The model is evaluated against a hand-labelled gold set,
   with results broken down by court and by kind of reference, so that a weakness on one
   court or one citation style is visible rather than averaged away. The evaluation is
   re-run whenever the weights change, and the results are available on request.

9. **Judgment text is not redistributed.** The tool shows the user the case name, date
   and court it read from a record, with the Open Justice Licence attribution, and links
   to the judgment on Find Case Law rather than copying it. Judgment text used to train
   or evaluate the model is kept on the project's own machines and is never published.
   What is distributed is the model's weights. Today those are trained on Open Government
   Licence text only, with nothing from Find Case Law; if a model is later trained on
   Find Case Law records under licence, the release notes will say so.

10. **Changes to this code are dated and kept.** A rule is never quietly removed. If one
    changes, the old wording stays here with the date it was superseded and the reason.

## History

- 2026-11-09: first version.
- 2026-11-09: rules 1 and 6 amended: statutes named in the document are looked up on
  legislation.gov.uk by title.
- 2026-11-11: rule 6 amended: treaties and conventions are listed and linked, never looked up.
