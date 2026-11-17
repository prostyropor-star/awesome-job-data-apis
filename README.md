# Awesome Job Data APIs [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of **free, public job posting APIs and feeds**: where job data actually comes from, with example endpoints. Useful for job boards, job alerts, salary research, recruiting tools and hiring-signal lead generation.

Contributions welcome. Please open a pull request.

## Contents

- [Applicant tracking systems (company job boards)](#applicant-tracking-systems-company-job-boards)
- [Remote job boards](#remote-job-boards)
- [Community job threads](#community-job-threads)
- [Government job APIs](#government-job-apis)
- [Ready-made scrapers and datasets](#ready-made-scrapers-and-datasets)
- [Tips](#tips)

## Applicant tracking systems (company job boards)

Most tech companies host their careers page on an ATS that exposes a public JSON feed. Replace `{slug}` with the company's board name (usually visible in its careers URL).

| ATS | Public endpoint | Notes |
|---|---|---|
| Greenhouse | `https://boards-api.greenhouse.io/v1/boards/{slug}/jobs?content=true` | Very common among startups and scale-ups. |
| Lever | `https://api.lever.co/v0/postings/{slug}?mode=json` | Includes team, location, commitment. |
| Ashby | `https://api.ashbyhq.com/posting-api/job-board/{slug}?includeCompensation=true` | Often includes salary ranges. |
| SmartRecruiters | `https://api.smartrecruiters.com/v1/companies/{slug}/postings` | Paginated with `offset`/`limit`. Large enterprises. |
| Personio | `https://{slug}.jobs.personio.de/xml` | XML feed; popular in Germany/Austria. |
| Recruitee | `https://{slug}.recruitee.com/api/offers/` | Popular in Europe. |
| Breezy HR | `https://{slug}.breezy.hr/json` | Small and mid-size companies. |
| Workable | `https://apply.workable.com/api/v1/widget/accounts/{slug}` | Widget feed; rate-limited, go slow. |

**Finding which ATS a company uses** is the hard part. The [Company ATS Detector](https://apify.com/mistlike_potato/company-ats-detector) looks up 34,000+ companies, and a free sample is in [job-board-starter](https://github.com/prostyropor-star/job-board-starter). The full list is available as a CSV/Excel dataset: [Company Careers Directory](https://prostyropor.gumroad.com/l/jxsju).

## Remote job boards

| Source | Endpoint | Terms |
|---|---|---|
| Remote OK | `https://remoteok.com/api` | Must link back and credit Remote OK. |
| We Work Remotely | `https://weworkremotely.com/remote-jobs.rss` | RSS, all categories. |
| Himalayas | `https://himalayas.app/jobs/api?limit=20&offset=0` | Paginated JSON. |
| Remotive | `https://remotive.com/api/remote-jobs` | Must credit Remotive; do not submit to Google Jobs or other aggregators. |
| Working Nomads | `https://www.workingnomads.com/api/exposed_jobs/` | JSON. |
| Jobicy | `https://jobicy.com/api/v2/remote-jobs` | JSON, filter by `tag`, `geo`. |

## Community job threads

| Source | Endpoint | Notes |
|---|---|---|
| Hacker News "Who is hiring?" | `https://hn.algolia.com/api/v1/search_by_date?tags=story,author_whoishiring` then `https://hn.algolia.com/api/v1/items/{id}` | ~250 startup job posts per month, free text. Parsed version: [HN Who is Hiring Jobs Scraper](https://apify.com/mistlike_potato/hn-who-is-hiring-jobs-parser). Monthly stats: [hn-who-is-hiring-report](https://github.com/prostyropor-star/hn-who-is-hiring-report). |

## Government job APIs

| Source | Endpoint | Notes |
|---|---|---|
| USAJOBS (US federal) | `https://data.usajobs.gov/api/search` | Free API key required. |
| Bundesagentur für Arbeit (Germany) | `https://rest.arbeitsagentur.de/jobboerse/jobsuche-service/pc/v4/jobs` | Send header `X-API-Key: jobboerse-jobsuche`; see [bundesAPI/jobsuche-api](https://github.com/bundesAPI/jobsuche-api). |
| EURES (EU) | `https://europa.eu/eures/portal/` | Search portal; check terms before automated use. |
| Adzuna | `https://developer.adzuna.com/` | Free API key; aggregated jobs in 16+ countries. |

## Ready-made scrapers and datasets

- [Career Site Jobs Scraper](https://apify.com/mistlike_potato/career-site-jobs-scraper): jobs from 34,000+ company boards on Greenhouse, Lever, Ashby, SmartRecruiters and more in one run, with an "only new jobs" mode.
- [Remote Jobs Aggregator](https://apify.com/mistlike_potato/remote-jobs-aggregator): Remote OK, We Work Remotely, Himalayas and Remotive merged and deduplicated, with attribution fields.
- [job-board-starter](https://github.com/prostyropor-star/job-board-starter): minimal Node script that turns job data into a static job board page.

## Tips

- **Be polite**: cache responses, add a delay between requests, set a descriptive User-Agent.
- **Respect terms**: several feeds require attribution or forbid redistribution to aggregators (see the Terms column).
- **Deduplicate**: the same job often appears on several boards. Company + title + location is a good key.
- **Track new jobs only**: store job IDs between runs, so alerts contain only new postings.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
