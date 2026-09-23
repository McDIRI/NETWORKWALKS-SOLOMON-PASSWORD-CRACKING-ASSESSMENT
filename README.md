# # 🔐 PDF PASSWORD CRACKING LAB — USING JOHN THE RIPPER AND NETWORKWALKS WEB BASED PASSWORD CRACKER .

Dictionary-attack recovery of password-protected PDFs, comparing **John the Ripper** (Johnny GUI) against **NetworkWalks' browser-based cracker**.
<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-JohnTheRipper%20v1.9.0-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Skill-Weakness%20Pattern-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Report%20Writting-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Skill-Hash%20Extraction-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Risk%20Assessment-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Networkwalks%20Hash%20Calculator-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks%20Password%20Cracker-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Solomon%20Diri%20INTEN-C00000?style=flat-square" />
</p>
Training lab · NetworkWalks Cybersecurity Internship (Batch B083) · No production data involved.
Full write-up: [`Password_Security_Assessment_Report.docx`](./Password_Security_Assessment_Report.docx)

## Tools

- **John the Ripper** `1.9.0-jumbo-1` (Johnny GUI)
- **pdf2john.pl** / [Online HashCrack](https://hashcrack.online/) — `$pdf$` hash extraction
- **[NetworkWalks Password Cracker](https://networkwalks.com/password-cracker/)** — browser simulator
- Wordlists: `fasttrack.txt` (221 words) + a larger breach-derived dictionary

## Method

```bash
# Extract hash
perl pdf2john.pl "My Locked PDF2.pdf" > pdf_hash.txt

# Dictionary attack
john --format=PDF --wordlist=<wordlist.txt> pdf_hash.txt
john --show --format=PDF pdf_hash.txt
```

The simulator's first run (100-word list / fasttrack.txt) returned `ACCESS DENIED`; a larger wordlist against John the Ripper cracked all three targets.

## Table 1. Results — John the Ripper (Johnny GUI)

 | Target File |	Method	| Recovered Password |	Flag Captured |
 |---|---|---|---|
 | My locked pdf1.pdf	| John the Ripper (Johnny GUI),dictionary mode |	good-luck |	nw{cybersecurity_flag_captured_2608} |
 | My locked pdf2.pdf	| John the Ripper (Johnny GUI), dictionary mode |	password1 |	nw{networkwalks_persistence_jtr_270521} |
 | My locked pdf3.pdf	| John the Ripper (Johnny GUI), dictionary mode |	1qaz2wsx |	nw{networkwalks_flag_260821_1} |

## Table 2. Results — NetworkWalks Online Password Cracker 

| Target File |	Method |	Recovered Password |	Flag Captured |
|---|---|---|---|
| My locked pdf1.pdf |	NetworkWalks online cracker |	Password1 |	nw{networkwalks_flag1_jtr_270521_1} |
| My locked pdf2.pdf |	NetworkWalks online cracker |	Password1 |	nw{networkwalks_persistence_jtr_270521} |
| My locked pdf3.pdf |	NetworkWalks online cracker |	1qaz2wsx	| nw{networkwalks_flag_260821_1} |

## SCREENSHOT EVIDENCE



## Key Takeaways

- All recovered passwords were common, low-entropy strings — trivial once the right wordlist is used.
- **Wordlist coverage**, not tool sophistication, decides most dictionary attacks.
- `1qaz2wsx` looks complex but is a keyboard-walk pattern in every major breach wordlist.
- Extracting a `$pdf$` hash never modifies the original file — safe to repeat offline.

## Mitigations

- Use long, random passphrases — avoid dictionary words and keyboard-walk patterns.
- Prefer AES-256 (PDF 2.0 / ISO 32000-2) over legacy RC4/128-bit encryption.
- Don't rely on a document password alone — pair with access controls.
- Avoid uploading sensitive PDFs to third-party hash tools outside a lab context.
- Use a password manager for document passwords.

## Disclaimer

All files, passwords, and flags belong to a controlled NetworkWalks training lab — shared for educational purposes only.

---
**Author:** Solomon Isaiah Diri
