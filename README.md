# Remote Jobs — Direct from Companies

Static job board that crawls remote openings directly from company career pages. No paid job boards, no recruiter gates.

## How it works

1. A Python crawler runs daily (via cron) and scrapes ~50 remote-friendly companies
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

Edit `data/companies.txt` and `~/.openclaw/workspace/remote_companies.txt`.

Then update the crawler's COMPANY config in `crawl_remote_jobs.py` with the new company's career URL and job board API if available.
# remote-jobs-app
