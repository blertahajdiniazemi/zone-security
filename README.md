# Zone Security website

Static website prepared for **GitHub Pages** with a working Formspree integration once a Formspree Form ID is added.

## Files

- `index.html` — the complete website.
- `assets/favicon.svg` — browser/site icon.
- `404.html` — custom not-found page.
- `.nojekyll` — tells GitHub Pages to publish the static files as-is.
- `robots.txt` — allows search-engine crawling.
- `site.webmanifest` — basic install/browser metadata.
- `sitemap.xml.example` — sitemap template; rename to `sitemap.xml` after confirming the final domain.
- `CNAME.example` — domain example. Rename to `CNAME` only when you are ready to use that domain.

## 1. Make the contact form send email

The form is already coded to submit to Formspree and display real loading, success, and error states.

1. Create/sign in to Formspree.
2. Create a new form and set its target email to `info@zonesecurity-ks.com` (or another verified email you prefer).
3. Copy the Form ID from the endpoint. It looks like:

   `https://formspree.io/f/abcdwxyz`

4. Open `index.html` and replace:

   `REPLACE_WITH_FORM_ID`

   with only the ID, for example `abcdwxyz`.

The final form action should look like:

```html
<form class="form" id="offerForm" action="https://formspree.io/f/abcdwxyz" method="POST" novalidate>
```

The site sends every form field with a `name` attribute. The visitor's `email` field is also usable by Formspree as the Reply-To address. A hidden `subject` field and `_gotcha` spam honeypot are included.

## 2. Upload to GitHub

Create a new repository, for example `zone-security`, and place **all files in this folder at the repository root**.

Using Git locally:

```bash
git init
git add .
git commit -m "Launch Zone Security website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/zone-security.git
git push -u origin main
```

Or upload the files through the GitHub website.

## 3. Turn on GitHub Pages

In the repository:

1. Open **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Choose branch **main** and folder **/(root)**.
4. Save.

The site will first be available at a GitHub Pages URL such as:

`https://YOUR-USERNAME.github.io/zone-security/`

## 4. Connect the custom domain

The contact email on the site uses `zonesecurity-ks.com`, so `CNAME.example` is prepared with that domain as the likely website domain. If your actual domain is different, edit the file before using it.

### In GitHub

Go to **Settings → Pages → Custom domain**, enter your domain, and save it.

If you publish from a branch, GitHub can create/update the `CNAME` file for you. Alternatively, rename `CNAME.example` to `CNAME` and make sure its only line is your exact domain.

### At your DNS provider — apex/root domain

For a root domain such as `zonesecurity-ks.com`, GitHub Pages currently documents these `A` records:

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Optional IPv6 `AAAA` records:

| Type | Name | Value |
|---|---|---|
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

### `www` subdomain

Create a CNAME record:

| Type | Name | Value |
|---|---|---|
| CNAME | www | YOUR-USERNAME.github.io |

Do **not** put the repository name in the CNAME target.

After DNS is correct, return to **Settings → Pages** and enable **Enforce HTTPS** when GitHub makes the option available.

## 5. Before launch

Check these items:

- Replace `REPLACE_WITH_FORM_ID` in `index.html`.
- Confirm the target email in Formspree.
- Test the form from the deployed website and confirm the message arrives.
- Confirm the phone link calls `+383 49 588 211`.
- Confirm `info@zonesecurity-ks.com` is the intended public email.
- Set the correct custom domain in GitHub Pages.
- If the final domain is `zonesecurity-ks.com`, rename `sitemap.xml.example` to `sitemap.xml`; otherwise edit its URL first.
- Add the DNS records at your domain provider.
- Enable HTTPS.
- Test desktop and mobile after deployment.

## Important security note

Do not put email passwords, SMTP passwords, API secret keys, or other private credentials in this repository. A GitHub Pages site is client-side/static and anything placed in its HTML or JavaScript can be viewed by visitors.
