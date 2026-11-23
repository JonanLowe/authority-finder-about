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
   *Amended 2026-11-17:* when the tool bundles an Act, it also asks legislation.gov.uk for
   the image files that Act's own XML names (rule 6). Nothing from the document is sent.
   *Amended 2026-11-23:* the tool also sends, built only from references the document names and never
   from its other text: a statutory instrument's number when it is named only by number (for example
   "SI 2019/859"); a Scottish citation to scotcourts.gov.uk, and a Northern Irish one to judiciaryni.uk
   once that lookup is switched on (rule 6); and, when the user asks for a bundle, the addresses of the
   judgments and statutes those references lead to. Until this date the rule named citation strings,
   statute titles and a bundled Act's image files only.

2. **We never say a case is good law.** No open data exists that could support the
   claim. The tool says "found", "not found in Find Case Law" or "outside coverage".
   It never says "correct", "valid" or "still good".
   *Amended 2026-11-23:* the tool's words have changed. For a case it says "Found in Find Case Law",
   "Not found in Find Case Law", "Before Find Case Law's coverage — not looked up" or "Court not in
   Find Case Law", and for the other sources it uses the words given in rule 6. It still never says
   "correct", "valid", "still good", "current" or "in force". Until this date the rule listed "outside
   coverage" among the tool's words.

3. **Nothing is silently dropped.** Every reference the tool extracts appears in the
   report with a status. A reference it could not resolve is a reported row, never a
   missing one.

4. **We say what we did not check.** Find Case Law holds modern judgments only, from
   2001 at the earliest, and no House of Lords, Scottish or Northern Irish courts.
   Citations outside that boundary are reported as "outside coverage", never as "not
   found", and any headline figure is given alongside the share that fell outside it.
   *Amended 2026-11-23:* the boundary has moved. House of Lords citations from 2001 to 2009 are matched
   against a saved copy of the archive's index, and Scottish citations are looked up on scotcourts.gov.uk
   (both rule 6); a Northern Ireland lookup is built but switched off. A citation outside every source is
   reported as "Before Find Case Law's coverage — not looked up" or "Court not in Find Case Law", never as
   "not found". Until this date the rule said such citations were reported as "outside coverage".

5. **Same input, same output.** The tool is deterministic. No generative model is used
   anywhere. The local classifier is pinned by hash and decoded without randomness, and
   a test checks that running it twice gives the same answer.

6. **Specific sources, used politely.** *Amended 2026-11-17:* Resolution uses Find Case
   Law alone for UK cases: one lookup per citation named in the user's document, every
   response cached so a document is never looked up twice, always well inside the published
   rate limit. Nothing is harvested from any other legal database, and nothing
   is done in bulk without the licence that permits it.
   *Amended 2026-11-17:* The tool uses legislation.gov.uk for an Act or statutory instrument named by
   title and year in the user's document: one title lookup each, cached, at least 5 seconds apart
   (its robots.txt crawl delay), with a named User-Agent, under the Open Government Licence.
   The tool says "found onlegislation.gov.uk" or "not found on legislation.gov.uk", and never that a statute is
   current or in force. Case citations are still resolved against Find Case Law alone.
   Until this date the rule read "Resolution uses Find Case Law alone".
   *Amended 2026-11-09, recorded here 2026-11-23:* when the user asks for a bundle, the tool downloads,
   for each case found, the judgment's PDF from Find Case Law, and for each Act or statutory instrument
   found, its text as XML from legislation.gov.uk: one request each, cached. It never requests
   legislation.gov.uk's PDF or Word files, which that site's robots.txt disallows.
   *Amended 2026-11-11:* a treaty or convention named in the document (the European Convention on
   Human Rights, a United Nations convention, a Hague convention) is detected and listed, never
   looked up. Where the project has opened a treaty's official text by hand, the list offers a
   link to it for the user to click; the tool makes no request to any treaty site, and never says a
   treaty is in force, ratified or binding.
   *Amended 2026-11-16, superseded the same day:* a House of Lords citation from 2001 to 2009 was to
   be looked up in the House of Lords judgment archive on publications.parliament.uk, under the Open
   Parliament Licence: the archive's index page once, cached, then the one judgment page, at least 5
   seconds apart, with the named User-Agent, never a crawl. Superseded because parliament.uk's
   Cloudflare protection refused the tool's client.
   *Amended 2026-11-16:* the tool makes no request to parliament.uk. A copy of the archive's index
   page, recorded once by hand on 2026-11-16 (the archive closed on 30 July 2009), ships with the
   tool, and a 2001 to 2009 House of Lords citation is matched against it on the user's machine. The
   tool says "listed in the House of Lords archive" or "not listed in the House of Lords archive",
   never "found", because the judgment itself is not opened; the link to it is for the user to
   click. The bundle saves nothing from parliament.uk.
   *Added 2026-11-17.* When it bundles an Act, the tool may also download the image files that the
   Act's own XML on legislation.gov.uk names, so that the PDF it draws of the Act includes them. Only
   those files, each once, kept on your machine, at least five seconds apart, under the same named
   User-Agent. Never the site's own PDF or Word files, and never a crawl. Checked first against
   legislation.gov.uk's robots.txt and fair-use policy, neither of which disallows it.
   *Amended 2026-11-20, recorded here 2026-11-23:* a statutory instrument named only by its number ("SI
   2019/859", or a Northern Ireland "SR 2010/113") is looked up on legislation.gov.uk by that number: one
   request, cached, on the same terms as a title. A Scottish case carries a link to the Scottish Courts
   and Tribunals Service judgments search, for the user to click.
   *Amended 2026-11-22, recorded here 2026-11-23:* a Scottish citation (Court of Session or High Court
   of Justiciary, for example "[2019] CSOH 70") is looked up on scotcourts.gov.uk, the Scottish Courts
   and Tribunals Service judgments site, under the Open Government Licence its copyright policy gives.
   That site's addresses are not built from the citation, so the tool sends one search per citation,
   through the search the site's own judgments page uses, then reads the first page of at most five of
   the opinions it returns until one prints the citation; the rest are never downloaded. Cached, at
   least 5 seconds apart, with the named User-Agent. The tool says "Found on scotcourts.gov.uk" or "Not
   confirmed on scotcourts.gov.uk", never "not found", because the search is not exact. A bundle saves
   the matched opinion's PDF.
   *Amended 2026-11-22, recorded here 2026-11-23:* guidance named in the document (sentencing
   guidelines, codes of practice and of conduct, the Code for Prosecutors, practice notes and Practice
   Statements, regulators' and prosecutors' guidance) is listed, never looked up or downloaded, with no
   link, and never called current, in force or binding.
   *Amended 2026-11-23:* a Northern Ireland citation (for example "[2025] NICA 8") can be looked up on
   judiciaryni.uk, the Judiciary NI website. **This lookup is switched off and makes no request** until
   the Lady Chief Justice's Office confirms that the judgments are covered by the Open Government
   Licence; this rule will be amended again, dated, when it is switched on. Switched on, it sends one
   request for the judgment's page, whose address is built from the citation, and one search of that
   site only if the page is not there; cached, at least 5 seconds apart, with the named User-Agent; never
   the site-wide search its robots.txt disallows. It says "Found on judiciaryni.uk" or "Not found on
   judiciaryni.uk", and a bundle saves the judgment's PDF from that site.
   *Amended 2026-11-23:* a treaty may also show its United Nations Treaty Series and Council of Europe
   Treaty Series numbers, read by hand from public records and shipped with the tool as a saved list.
   The tool makes no request to any treaty site, and never says a treaty is in force, ratified or
   binding.

8. **No analysis of people.** The classifier tags citation spans in text. It does not
   select, count or profile parties, judges, counsel or anyone else, and no personal
   data is extracted, stored or output beyond the judgment text itself.

9. **Measured, not asserted.** The model is evaluated against a hand-labelled gold set,
   with results broken down by court and by kind of reference, so that a weakness on one
   court or one citation style is visible rather than averaged away. The evaluation is
   re-run whenever the weights change, and the results are available on request.

10. **Judgment text is not redistributed.** The tool shows the user the case name, date
   and court it read from a record, with the Open Justice Licence attribution, and links
   to the judgment on Find Case Law rather than copying it. Judgment text used to train
   or evaluate the model is kept on the project's own machines and is never published.
   What is distributed is the model's weights. Today those are trained on Open Government
   Licence text only, with nothing from Find Case Law; if a model is later trained on
   Find Case Law records under licence, the release notes will say so.

11. **Changes to this code are dated and kept.** A rule is never quietly removed. If one
    changes, the old wording stays here with the date it was superseded and the reason.

## History

- 2026-11-09: first version.
- 2026-11-09: rules 1 and 6 amended: statutes named in the document are looked up on
  legislation.gov.uk by title.
- 2026-11-11: rule 6 amended: treaties and conventions are listed and linked, never looked up.
- 2026-11-16: rule 6 amended: House of Lords judgments from 2001 to 2009 looked up in the
  parliament.uk archive; superseded the same day.
- 2026-11-16: rule 6 amended: no request to parliament.uk; House of Lords citations are matched
  against a saved copy of the archive's index.
- 2026-11-17: rules 1 and 6 amended: a bundled Act's own image files are downloaded from
  legislation.gov.uk to draw its PDF.
- 2026-11-23: recorded here: rule 6 amended for bundles (2026-11-09), statutory instruments by
  number and the Scottish search link (2026-11-20), the Scottish lookup and guidance (2026-11-22).
  Rules 1, 2 and 4 amended to match. Rule 6 amended: a Northern Ireland lookup, switched off, and
  treaty numbers from a saved list.
