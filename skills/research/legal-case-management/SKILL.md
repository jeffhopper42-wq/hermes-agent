---
name: legal-case-management
description: Research and interact with open-source legal case management systems. Search court records via CourtListener/RECAP, look up case law, manage legal documents, and track case information using free public APIs and open-source tools.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [Research, Legal, Case Management, Law, Court Records, CourtListener]
    related_skills: [domain-intel, duckduckgo-search]
---

# Legal Case Management Research

Research legal cases, search court records, and interact with open-source legal case management platforms. Uses free public APIs (CourtListener, RECAP) and open-source tools -- no API keys required for basic searches.

## Quick Reference

| Action | Command |
|--------|---------|
| Search court opinions | `curl "https://www.courtlistener.com/api/rest/v4/search/?q=QUERY&type=o"` |
| Search PACER/RECAP dockets | `curl "https://www.courtlistener.com/api/rest/v4/search/?q=QUERY&type=r"` |
| Get specific opinion | `curl "https://www.courtlistener.com/api/rest/v4/opinions/OPINION_ID/"` |
| Search by court | `curl "https://www.courtlistener.com/api/rest/v4/search/?q=QUERY&type=o&court=scotus"` |
| Search by date range | `curl "https://www.courtlistener.com/api/rest/v4/search/?q=QUERY&type=o&filed_after=2024-01-01&filed_before=2025-01-01"` |
| Look up a judge | `curl "https://www.courtlistener.com/api/rest/v4/people/?name_last=Roberts"` |
| Browse court jurisdictions | `curl "https://www.courtlistener.com/api/rest/v4/courts/"` |

## CourtListener API (Free Law Project)

[CourtListener](https://www.courtlistener.com/) by [Free Law Project](https://free.law/) is the largest open legal data platform. It provides free access to millions of court opinions, PACER dockets (via RECAP), oral arguments, judge information, and financial disclosures.

### Search Types

| Type parameter | What it searches |
|----------------|-----------------|
| `o` | Court opinions (case law) |
| `r` | RECAP / PACER dockets and filings |
| `oa` | Oral arguments (audio) |
| `p` | People (judges, attorneys) |

### Searching Court Opinions

```bash
# Basic keyword search
curl "https://www.courtlistener.com/api/rest/v4/search/?q=fourth+amendment+digital+privacy&type=o"

# Filter by court (scotus = Supreme Court, ca1-ca11 = Circuit Courts)
curl "https://www.courtlistener.com/api/rest/v4/search/?q=fair+use&type=o&court=scotus"

# Filter by date range
curl "https://www.courtlistener.com/api/rest/v4/search/?q=artificial+intelligence&type=o&filed_after=2023-01-01"

# Filter by citation count (influential cases)
curl "https://www.courtlistener.com/api/rest/v4/search/?q=due+process&type=o&cited_gt=100"
```

### Searching RECAP Dockets (Federal Court Filings)

RECAP is a free archive of PACER federal court documents contributed by the community.

```bash
# Search dockets
curl "https://www.courtlistener.com/api/rest/v4/search/?q=antitrust+merger&type=r"

# Search by party name
curl "https://www.courtlistener.com/api/rest/v4/search/?q=party:Google&type=r"

# Search by case number
curl "https://www.courtlistener.com/api/rest/v4/search/?q=docket_number:23-cv-01234&type=r"
```

### Retrieving Specific Records

```bash
# Get a specific opinion by ID
curl "https://www.courtlistener.com/api/rest/v4/opinions/OPINION_ID/"

# Get a specific docket
curl "https://www.courtlistener.com/api/rest/v4/dockets/DOCKET_ID/"

# Get a specific court
curl "https://www.courtlistener.com/api/rest/v4/courts/scotus/"

# Get citation relationships
curl "https://www.courtlistener.com/api/rest/v4/opinions-cited/?citing_opinion=OPINION_ID"
```

### Court Identifiers (Common)

| Court ID | Court Name |
|----------|-----------|
| `scotus` | Supreme Court of the United States |
| `ca1` - `ca11` | First through Eleventh Circuit Courts |
| `cadc` | D.C. Circuit Court of Appeals |
| `cafc` | Federal Circuit Court of Appeals |
| `dcd` | U.S. District Court for D.C. |
| `nysd` | Southern District of New York |
| `cand` | Northern District of California |

### Advanced Query Syntax

CourtListener supports Solr-style queries:

```bash
# Boolean operators
curl "https://www.courtlistener.com/api/rest/v4/search/?q=(copyright+OR+trademark)+AND+software&type=o"

# Phrase search
curl "https://www.courtlistener.com/api/rest/v4/search/?q=%22reasonable+expectation+of+privacy%22&type=o"

# Exclude terms
curl "https://www.courtlistener.com/api/rest/v4/search/?q=patent+-design&type=o"

# Wildcard
curl "https://www.courtlistener.com/api/rest/v4/search/?q=discriminat*&type=o"
```

### Rate Limits & Authentication

- **Anonymous access**: 100 requests/day — sufficient for research queries
- **Free API token**: 5,000 requests/day — register at https://www.courtlistener.com/sign-in/
- **Authenticated requests**: Add header `-H "Authorization: Token YOUR_TOKEN"`

## Open-Source Legal Case Management Projects

The following open-source projects provide case management functionality for law firms and legal practitioners:

### Production-Ready

| Project | Tech Stack | Focus |
|---------|-----------|-------|
| [ArkCase](https://github.com/ArkCase/ArkCase) | Java/Spring, Angular, Solr, Alfresco | Enterprise case management (FOIA, complaints, incidents) |
| [CourtListener](https://github.com/freelawproject/courtlistener) | Python/Django, PostgreSQL, Solr | Court opinion search, PACER archive, judicial data |
| [Iuris-Soft](https://github.com/iamgilwell/Iuris-Soft) | Full-stack | Litigation, contracts, IP, document management |

### Specialized

| Project | Tech Stack | Focus |
|---------|-----------|-------|
| [LegalNexus](https://github.com/daniel-debrun/LegalNexus) | Python, React, vector DB | AI-powered legal research with per-case vector stores |
| [OpenLawOffice](https://github.com/NodineLegal/OpenLawOffice) | .NET | Law office management: cases, billing, tasking |
| [ClinicCases](https://github.com/judsonmitchell/ClinicCases) | PHP, MySQL | Law school clinic case management |
| [Worklenz](https://github.com/Worklenz/worklenz) | Node.js, PostgreSQL, Angular | Task management adaptable to legal workflows |

## Common Features in Legal Case Management

When researching or building legal case management systems, these are the core feature areas:

1. **Case Tracking** -- Lifecycle management, status tracking, categorization, priority, deadlines
2. **Document Management** -- Upload, version control, templates, search, folder organization
3. **Client/Contact Management** -- Client profiles, contact info, conflict checks, communication logs
4. **Calendar & Deadlines** -- Court dates, statute of limitations, filing deadlines, reminders
5. **Billing & Time Tracking** -- Billable hours, expense tracking, invoicing, payment records
6. **Task Management** -- Assignments, checklists, workflows, delegation
7. **Court/Docket Integration** -- PACER/RECAP access, electronic filing, docket tracking
8. **Reporting & Analytics** -- Case volume, billing summaries, outcome analysis
9. **Communication** -- Internal messaging, client portal, email integration
10. **Compliance & Security** -- Audit trails, role-based access, data encryption, GDPR/HIPAA

## When to Use This Skill vs Built-in Tools

| Task | Better tool | Why |
|------|-------------|-----|
| "Search for case law on topic X" | **This skill** | CourtListener API for structured legal search |
| "Find a court opinion by citation" | **This skill** | Direct API access to opinion database |
| "Research a company's lawsuits" | **This skill** | RECAP docket search by party name |
| "General legal news/articles" | `web_search` | News and commentary, not case law |
| "Read a specific court document" | `web_extract` | Extract content from URLs |
| "Find a lawyer/law firm" | `web_search` | General web search is better for this |
| "Draft a legal document" | Direct LLM | Use the model's language capabilities |

## Useful Legal Research URLs

- **CourtListener**: https://www.courtlistener.com/
- **Free Law Project**: https://free.law/
- **RECAP Archive**: https://www.courtlistener.com/recap/
- **Google Scholar (Case Law)**: https://scholar.google.com/ (select "Case law")
- **Cornell LII**: https://www.law.cornell.edu/
- **Justia**: https://www.justia.com/
- **PACER**: https://pacer.uscourts.gov/

## Notes

- CourtListener data skews toward federal courts; state court coverage varies
- RECAP dockets depend on community contributions -- not all PACER filings are archived
- Always verify legal citations against authoritative sources
- This skill is for legal research, not legal advice -- always recommend consulting an attorney
- Some older opinions may lack full text (only metadata available)

---

*Built for Hermes Agent by Nous Research*
