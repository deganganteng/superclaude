# /browser — Browser Automation

Gunakan untuk automasi browser: scraping, form filling, testing UI, dll.

## Instruksi untuk Claude Code

Ketika user menjalankan `/browser <url atau task>`, setup dan jalankan browser automation.

---

## Setup (Pertama Kali)

```bash
# Check jika browser-use sudah terinstall
pip show browser-use 2>/dev/null || pip install browser-use playwright
playwright install chromium
```

## Cara Pakai

### Simple Browse & Extract
```python
# .claude/scripts/browser_task.py
import asyncio
from browser_use import Agent
from langchain_anthropic import ChatAnthropic

async def run(task: str):
    agent = Agent(
        task=task,
        llm=ChatAnthropic(model="claude-opus-4-5"),
    )
    result = await agent.run()
    return result

asyncio.run(run("[TASK_DARI_USER]"))
```

### Common Tasks

**Scrape data:**
```
Task: "Buka [URL], ambil semua [data yang diminta], simpan ke file JSON"
```

**Test UI flow:**
```
Task: "Buka localhost:3000, login dengan [credentials], test [user flow]"
```

**Fill form:**
```
Task: "Buka [URL], isi form dengan data: [data], submit, screenshot hasil"
```

---

## Output
Hasil browser task disimpan di `.claude/browser-output/` dengan timestamp.

```bash
mkdir -p .claude/browser-output
echo "[$(date -Iseconds)] BROWSER: Task executed — [deskripsi]" >> .claude/logs/action-log.md
```

---

## Tips
- Untuk login, pastikan credentials ada di `.env` (jangan hardcode)
- Untuk scraping, cek robots.txt dulu
- Screenshot otomatis tersimpan jika ada error
