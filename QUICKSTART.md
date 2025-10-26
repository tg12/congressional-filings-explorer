# Quick Start Guide

Get up and running with the Congressional Financial Disclosure Analysis Tool in under 5 minutes!

## Prerequisites Check

Python 3.8 or higher installed  
pip package manager available  
Internet connection active  

## Installation (3 steps)

### 1. Install System Dependencies

**macOS:**
```bash
brew install poppler
```

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install poppler-utils
```

### 2. Install Python Packages

```bash
cd 2025FD
pip install -r requirements.txt
```

### 3. Set OpenAI API Key

```bash
export OPENAI_API_KEY='your-api-key-here'
```

**Don't have an API key?**  
Get one at: https://platform.openai.com/api-keys

## First Run

### Test Mode (No API Key Needed)

Verify everything works:

```bash
python3 load_xml.py --test
```

Expected output:
```
================================================================================
Congressional Financial Disclosure Analysis Tool v1.0.0
================================================================================

TEST MODE ACTIVE
Running data processing only, skipping OpenAI analysis

[1/7] Loading XML metadata...
      Loaded XXX total disclosure records
...
```

### Full Analysis Mode

Run the complete analysis:

```bash
python3 load_xml.py
```

This will:
1. Download latest disclosure data
2. Filter to last 30 days of filings
3. Fetch PDFs in parallel
4. Analyze with AI
5. Display comprehensive summary

**First run takes 1-2 minutes** (downloads XML and PDFs)

## What You'll See

### Output Sections

1. **Filing Metadata Table**: Names, dates, document IDs
2. **PDF URLs List**: Links to original disclosure documents
3. **AI Analysis Summary**: Extracted stock transactions and patterns

### Example Summary

```
================================================================================
COMPREHENSIVE STOCK ANALYSIS SUMMARY
================================================================================
Analysis identified the following stock transactions across 15 filings:

Major Holdings:
- NVIDIA (NVDA): 5 purchases, 2 sales
- Apple (AAPL): 3 purchases
- Microsoft (MSFT): 4 purchases, 1 sale
...
```

## Troubleshooting

### "Command not found: python3"

Try `python` instead:
```bash
python load_xml.py --test
```

### "No module named 'pdf2image'"

Install dependencies:
```bash
pip install -r requirements.txt
```

### "OPENAI_API_KEY environment variable not set"

Either:
- **Run in test mode**: `python3 load_xml.py --test`
- **Set your API key**: `export OPENAI_API_KEY='sk-...'`

### "No filings found"

The default setting looks at last 30 days. Edit `load_xml.py`:
```python
DEFAULT_DAYS = 60  # Increase to 60 days
```

## Next Steps

### Customize Settings

Edit configuration in `load_xml.py`:

```python
# Look back period
DEFAULT_DAYS = 30  # Change to 7, 14, 60, 90, etc.

# Display limit
DEFAULT_TOP_N = None  # Change to 10, 20, etc. to limit results

# XML refresh
MAX_XML_AGE_DAYS = 2  # Change to refresh more/less often
```

### Understand Output

Read the [README.md](README.md) for:
- Detailed feature explanations
- Data source information
- Performance considerations
- Legal disclaimers

### Schedule Regular Runs

**macOS/Linux cron example** (daily at 9 AM):
```bash
# Edit crontab
crontab -e

# Add line:
0 9 * * * cd /path/to/2025FD && /usr/bin/python3 load_xml.py > output.log 2>&1
```

## Common Questions

**Q: How much does it cost to run?**  
A: Approximately $0.01-0.05 per filing analyzed (OpenAI API pricing)

**Q: Can I analyze older filings?**  
A: Yes, increase `DEFAULT_DAYS` constant in the script

**Q: Is this investment advice?**  
A: **NO.** This is informational only. See LICENSE for full disclaimer.

**Q: Where does the data come from?**  
A: Official House of Representatives disclosure server (public data)

**Q: Can I use this commercially?**  
A: Yes, under MIT license terms. See LICENSE file.

## Support

- **Documentation**: See README.md
- **Code Comments**: Check load_xml.py for detailed explanations
- **Issues**: Open an issue on the repository

## Legal Reminder

IMPORTANT: This tool is NOT investment advice. Always consult qualified professionals before making financial decisions. See LICENSE for full disclaimer.

---

**Ready to analyze?** Run `python3 load_xml.py --test` now!
