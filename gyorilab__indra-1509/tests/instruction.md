# Issue

**Title:** Pubmed and pmc clients updates

## Description

This PR updates the PubMed and PMC clients.

### PubMed client updates

First, the pubmed client is updated with the following:
- The Pubmed medline XML downloading process (sourcing data from https://ftp.ncbi.nlm.nih.gov/pubmed/) has been updated to allow more flexibility so that downstream repositories can adopt the pubmed client's download process instead of implementing their own
- After testing parallel download, it was determined that a speedup of _at least_ 2-4x was possible with a modest amount of 4 workers, which greatly reduces the time it takes to download the full XML dump from scratch. Because of this, the possibility to run downloads in parallel is added, with a default of serial download (i.e. `max_workers=1`).

### PMC client updates

Second, the PMC client is updated after observing the following behaviors on the server:
- The old base URL, `https://www.ncbi.nlm.nih.gov/pmc/oai/oai.cgi` now redirects to `https://pmc.ncbi.nlm.nih.gov/api/oai/v1/mh/`
- The new endpoint accepts the same parameters as the previous endpoint
- The new endpoint is heavily throttled: only 3 requests per second are allowed (see https://pmc.ncbi.nlm.nih.gov/tools/oai/), and on top of that, throttling is sometimes more restrictive than that leading to disruptions when making requests.

With the new S3 based datasets from PMC (see https://pmc.ncbi.nlm.nih.gov/tools/pmcaws/) being able to replace a lot of the functions, the following updates to the code base has been made:
- The main client function that interacts with `https://pmc.ncbi.nlm.nih.gov/api/oai/v1/mh/` has been updated to do an exponential back-off when a 429 is encountered.
- Functions that can use the S3 based client in indra have been updated to do that
- Skip tests that use the throttled API as the tests cannot reliably run
- Add tests for the S3 based client

#### Other updates:
- Remove unsued import (`lru_cache` in `indra/literature/__init__.py`)
- Remove test skip for rlimsp processor tests as the webservice is _not_ down any more

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `040f9efe5657`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.