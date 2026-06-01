# MP Design — Deploy uputstvo (GitHub Pages)

Korak-po-korak vodič za postavljanje sajta uživo. Pošto već imaš `.git` folder u Website direktorijumu, znači da je repo već inicijalizovan.

---

## 📋 Pre nego što kreneš — provera

Otvori PowerShell ili CMD u `C:\Users\LEGION PRO\Desktop\Website` (Shift + desni klik → "Open PowerShell window here") i pokreni:

```bash
git status
```

Treba da vidiš listu fajlova ("modified", "untracked"). Ako kaže "fatal: not a git repository", javi mi.

```bash
git remote -v
```

Ako vidiš `origin` URL koji vodi ka tvom GitHub-u — odlično, samo nastavi. Ako kaže prazno, treba da ga povežemo (vidi sekciju 4).

---

## 1️⃣ Pripremi commit

```bash
git add .
git commit -m "MP Design v1 — live ready"
```

Ako te git pita za ime/email pri prvom commit-u, ukucaj:
```bash
git config --global user.name "tvoje ime"
git config --global user.email "mpdsgnn@gmail.com"
```

---

## 2️⃣ Push na GitHub

```bash
git push origin main
```

Ako kaže "fatal: refusing to push" ili tako nešto, probaj:
```bash
git push -u origin main
```

Ako kaže da je grana `master` umesto `main`:
```bash
git push -u origin master
```

---

## 3️⃣ Uključi GitHub Pages

1. Otvori svoj repo na **github.com** (npr. `github.com/tvoje-ime/Website`)
2. Klik na **Settings** (gore desno, gear ikon)
3. U levom meniju klik na **Pages**
4. Pod "Build and deployment" → "Source": izaberi **Deploy from a branch**
5. "Branch": izaberi **main** (ili master) i **/(root)** → Klik **Save**
6. Sačekaj 1-3 minuta, pa osveži stranicu

Pojaviće se zelena traka sa linkom: `Your site is live at https://tvoje-ime.github.io/Website/`

---

## 4️⃣ Ako nemaš `origin` setup (prvi put)

```bash
# Idi na github.com → "New repository" → ime: "Website" (ili kako želiš) → Create
# Kopiraj URL koji ti GitHub pokaže (npr. https://github.com/USERNAME/Website.git)

git remote add origin https://github.com/USERNAME/Website.git
git branch -M main
git push -u origin main
```

---

## 🚨 Najčešći problemi

**Problem: "Slike ne učitavaju, prikazuje 404"**

Razlog: Linux (GitHub server) razlikuje velika i mala slova, Windows ne. Ako u HTML-u piše `Peugeot 508/index.html` ali folder se zove `peugeot 508/`, na GitHub-u neće raditi.

**Provera:** Ovaj sajt koristi sledeće tačne nazive — moraju biti identični u tvom folderu:
- `Peugeot 508/` (velikim P)
- `audi a6/` (malim slovima)
- `citroen c2/` (malim slovima)
- `vw 7 gti/` (malim slovima)
- `scan files/` (malim slovima)
- `3D printing projects/` (3D velikim, ostalo malim)
- `homepage/` (malim slovima)

Razmaci u imenima nisu problem na GitHub Pages — ali velika/mala slova jesu.

**Problem: "Videi se i dalje sporo učitavaju"**

To je rešeno u najnovijoj verziji `index.html` koju imaš sad (lazy load). Videi se ne učitavaju dok ne otvoriš tu kategoriju. Prvi load je sad ~5-15 MB umesto 17+ MB.

**Problem: "Push odbijen, kaže velik fajl"**

GitHub odbija fajlove preko 100 MB. Proveri:
```bash
# U PowerShell
Get-ChildItem -Recurse | Where-Object {$_.Length -gt 100MB} | Select-Object FullName, @{Name='SizeMB';Expression={[math]::Round($_.Length/1MB,2)}}
```

Ako se nešto pojavi, treba kompresovati.

---

## 📦 Šta se deploy-uje

Cela sadržina `Website/` foldera, osim:
- `.git/` (ne ide na deploy, samo lokalno)
- `mnt/` (verovatno mock folder, ne deploy-uje se sam po sebi)
- `Folder - telefon/` (slike za mobile, ostavi za sada — koristićemo ih kad pravimo mobile verziju)

---

## 🌐 Custom .com domain (kasnije)

Kad budeš spreman za pravi domen:
1. Kupi npr. `mpdesign.rs` ili `.com` (Hostinger, GoDaddy, Namecheap)
2. U domain DNS settings dodaj **CNAME** ka `tvoje-ime.github.io`
3. U repo Settings → Pages → "Custom domain" → ukucaj domen
4. GitHub će ti dati besplatni SSL (https://)

---

## ✅ Kad sve proradi, javi mi link sajta da proverimo zajedno.
