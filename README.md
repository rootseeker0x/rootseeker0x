## Hi there 👋

import os, zipfile

base='/mnt/data/pentest_journal'
os.makedirs(base, exist_ok=True)

# structure
dirs=[
    'machines',
    'cheatsheets',
    'tools/nmap-templates',
    'tools/exploitation',
    'tools/automation'
]
for d in dirs:
    os.makedirs(os.path.join(base,d), exist_ok=True)
    # add placeholder
    with open(os.path.join(base,d,'.gitkeep'),'w') as f: f.write('')

# README.md
readme = """# 🕵️‍♂️ Pentest Learning Journal
Dokumentacja moich postępów w TryHackMe, HackTheBox i treningach pentestowych.

## 🔥 Cele nauki
- Zrozumienie podstaw enumeracji i exploitation  
- Podnoszenie umiejętności privilege escalation  
- Automatyzacja powtarzalnych czynności  
- Rozwój jako przyszły pentester  

---

# 📅 Postępy (chronologicznie)

| Data | Maszyna / Kurs | Platforma | Poziom | Status | Notatki |
|------|----------------|-----------|--------|--------|---------|
| 2025- | ... | THM | Easy | ✔ | ... |

---

# 📁 Struktura repozytorium

/
├── machines/
│   ├── machine-name/
│   │   ├── README.md
│   │   ├── screenshots/
│   │   └── notes.txt
│
├── cheatsheets/
│   ├── linux-priv-esc.md
│   ├── windows-priv-esc.md
│   ├── enumeration.md
│
└── tools/
    ├── nmap-templates/
    ├── exploitation/
    └── automation/
"""
with open(os.path.join(base,'README.md'),'w') as f: f.write(readme)

# cheatsheet files
cheats = {
    'linux-priv-esc.md': "# Linux Privilege Escalation Cheatsheet\n",
    'windows-priv-esc.md': "# Windows Privilege Escalation Cheatsheet\n",
    'enumeration.md': "# Enumeration Cheatsheet\n"
}
for name,content in cheats.items():
    with open(os.path.join(base,'cheatsheets',name),'w') as f: f.write(content)

# zip
zip_path='/mnt/data/pentest_learning_journal.zip'
with zipfile.ZipFile(zip_path,'w') as z:
    for root,_,files in os.walk(base):
        for file in files:
            fp=os.path.join(root,file)
            z.write(fp, os.path.relpath(fp, base))

zip_path
