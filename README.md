# authority-finder

authority-finder is a small desktop tool, in development, that checks the case citations in an
English legal document against free public sources.

It runs on the user's own computer. The document never leaves that computer: only the citation
strings themselves are looked up.

## What it requests, and from where

- **Find Case Law** (The National Archives): one lookup per neutral citation the document names,
  for example `[2019] UKSC 41`. Responses are cached, so the same document never asks twice.
- **legislation.gov.uk**: when the user asks for a bundle, one title lookup and one `data.xml`
  download for each Act or SI the document names. Requests are at least 5 seconds apart, cached,
  and never `data.pdf` or `data.docx`. It does not crawl.

Requests identify themselves with the User-Agent
`authority-finder/0.1 (+https://github.com/JonanLowe/authority-finder-about)`.

It is used one document at a time, by one person, well under each service's published rate limit.

## How it is built to behave

The rules the tool is held to, in public: [code of ethics](code-of-ethics.md).

## Contact

If this tool's requests cause you any problem, please
[open an issue](https://github.com/JonanLowe/authority-finder-about/issues) and it will be
dealt with promptly.
