# ONE × STRAND ZipLine — regisztrációs űrlap

Statikus, framework-mentes űrlap fesztivál-netre optimalizálva
(~40 KB összesen, subsetelt Mont woff2 fontokkal).

## Hogyan működik

```
QR a sisakon → https://<DOMAIN>/6 → űrlap (SISAK #06)
             → POST a Google Apps Script API-ra
             → Google Sheet ÉLŐ lap frissül (teal AKTÍV sor)
```

A backend változatlan: a Google Sheet a dashboard, az ELKÜLDVE pipa
resetel, a NAPLÓ auditál.

## Deploy (Vercel)

1. Push ebbe a GitHub repóba
2. [vercel.com](https://vercel.com) → Add New → Project → importáld a repót
   - Framework preset: **Other** (nincs build, statikus)
   - Build command: üres · Output directory: üres
3. Deploy → kapsz egy `*.vercel.app` URL-t
4. Settings → Domains → add hozzá a saját domaint, állítsd be a DNS-t
   (CNAME → cname.vercel-dns.com)

## URL formátum

- `https://<DOMAIN>/6` → SISAK #06 (ez megy a QR-kódokba — rövid = ritkább QR = könnyebb szkennelés)
- `https://<DOMAIN>/?helmet=6` → ugyanaz, fallback

## Fontos

- Az Apps Script API URL az `index.html`-ben az `API` konstans.
  Ha a scriptet újradeployolod ÚJ deployment ID-vel, itt át kell írni!
  (Ugyanarra az ID-re deployolva — `clasp deploy --deploymentId ...` — nem kell.)
- QR-kódokat csak a domain élesítése UTÁN generáljuk/nyomtatjuk!
