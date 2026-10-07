# Remote Jobs — Direct from Companies

Static job board that crawls remote openings directly from company career pages. No paid job boards, no recruiter gates.

## How it works

1. A Python crawler runs daily (via cron) and scrapes the companies listed in `remote_companies.txt`
2. Results are saved as JSON in `data/`
3. This static site reads the JSON and displays everything
4. Deploy to GitHub Pages or Vercel

## Deploy

### GitHub Pages
```bash
# Push this directory to a repo
git init && git add . && git commit -m "init"
git push origin main
# Enable GitHub Pages in repo settings → main branch → / (root)
```

### Vercel
```bash
vercel --prod
```

## Update data

Data files in `data/` are regenerated daily by the crawler. Copy them:

```bash
cp ~/.openclaw/workspace/job_reports/latest.json data/
cp ~/.openclaw/workspace/job_reports/new_today.json data/
cp ~/.openclaw/workspace/job_reports/removed_today.json data/
cp ~/.openclaw/workspace/remote_companies.txt data/companies.txt
```

Or run the full crawl which auto-copies:
```bash
python3 ~/.openclaw/workspace/crawl_remote_jobs.py
```

## Add companies

Edit `~/.openclaw/workspace/remote_companies.txt` (one company name per line).

Then add the company's `career_url` and job-board API mapping to `~/.openclaw/workspace/company_careers.json`, for example:

```json
"Company Name": {
  "career_url": "https://company.com/careers",
  "boards": { "greenhouse": "board-name" },
  "all_urls": ["https://company.com", "https://company.com/careers"]
}
```

Supported board keys: `ashby`, `greenhouse`, `lever`, `lever_eu` (EU-hosted Lever boards), and `recruitee`. Companies without a supported board key fall back to generic HTML scraping of `career_url`.

`data/companies.txt` is a mirror of `remote_companies.txt` and is refreshed automatically by the crawler.
# remote-jobs-app
