# Key Ring Inspector

**AppADay 173** | Utility | Claude API (optional key Test only)

Key Ring Inspector compares the Claude API keys in your encrypted AppADay backup file with the keys saved in this browser. For every AI app it shows whether the two copies match, differ, exist only in the file, exist only in the browser, or are missing. You can fix gaps in either direction, test a key against Anthropic, and download a fresh encrypted backup.

## How to use it

**Open your backup.** Choose appaday-keys.json, type its passphrase, and tap Open and compare. The page decrypts the file in your browser with Web Crypto, using the key ring format described in KEYS.md in the portal repo. A wrong passphrase and a file that is not an AppADay key file get different messages. No backup yet? Start from this browser's keys builds a new file copy from what this browser already holds.

**Read the rows.** The default key has its own row at the top. Every AI app then gets a row with its number, name, and a status chip: Match, Mismatch, Only in file, Only in browser, or Missing. A missing app notes whether the default key covers it. Each row shows the last four characters of the file value and the browser value side by side. Tap a row to open it, reveal the full values, or copy either one. Filter chips along the top narrow the list to one status. Any key found in this browser or the file for an app number that is not in the built in AI list gets an extra row.

**Fix gaps.** Each row offers Replace (or Add when nothing is stored), Copy file to browser, Copy browser to file, and delete from the file or the browser. Replace and Add let you choose File and browser, File only, or Browser only. Two bulk buttons copy every differing key in one direction. Deletes and bulk copies ask for a second tap. Edits to the file copy stay in memory until you download, and a badge reminds you they are unsaved. Edits to the browser copy are written to localStorage right away, under the exact names the key ring uses (appaday.key.NNN and appaday.key.default), and only keys that pass the key ring plausibility rule (20 to 400 characters, no spaces) are accepted.

**Test a key.** Test file key and Test browser key send one request with max_tokens set to 1 straight to api.anthropic.com and report OK for 200, Bad for 401 or 403, Rate limited for 429, or Unreachable for a network error. The result never shows the full key.

**Download.** Download updated backup re-encrypts the file copy with the passphrase you opened it with, or with a new one you type (at least 12 characters, typed twice), and saves appaday-keys.json. On iPhone and Android the share sheet opens after a second tap so the file can go to Files or Drive. Afterward the passphrase and the decrypted keys are cleared from the page. Replace your older copy with the new file.

## Privacy

No key leaves your device except an optional Test on a row, which sends one token request directly to api.anthropic.com. Loading the page only fetches the shared portal scripts and config.json, which carry no keys. The passphrase is never stored, and the decrypted keys live only in memory until you download, lock, or close the page. Saved to a phone home screen, the app has its own storage and sees only the keys saved there.

## Model

The model is not hardcoded. Test asks the portal's shared models.js for the haiku tier at the moment you tap it, which follows the AppADay central [config.json](https://augustineiacopelli.github.io/appaday/config.json).

## Links

Live app: https://augustineiacopelli.github.io/appaday-173-key-ring-inspector/

Portfolio: https://augustineiacopelli.github.io/appaday/
