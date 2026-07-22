# Publishing tdogtaekwondo.com on GitHub Pages

Step by step, from nothing to live on your domain, and moving the domain across
from Wix. No coding required.

Placeholders used below:
- `YOURNAME` = your GitHub username
- `REPO` = whatever you name the repository (suggested: `tdog-website`)

---

## Before you start: what has already been checked

These were verified against the actual files, so you do not need to worry about them:

- `index.html` sits at the top level, where GitHub Pages needs it.
- All 1,300 image, video, PDF and page links resolve with exact capitalisation.
  GitHub servers are case sensitive, Windows is not, so this is the most common
  cause of images silently breaking after a move. Yours are clean.
- No file exceeds 25 MB, so nothing will be rejected on upload.
- 961 files, 118 MB total. Well inside the 1 GB GitHub Pages limit.
- `.nojekyll` has been added, so GitHub serves the files exactly as they are.
- There are no absolute links back to tdogtaekwondo.com and no leftover Wix
  references, so the site will work correctly on the temporary test address.

---

## Two things to know up front

**1. The repository must be Public.**
On the free GitHub plan, Pages only works from public repositories. Private
repository Pages requires a paid plan. Your site is public anyway once it is
live, so this only means the source files are visible too.

**2. You cannot drag 961 files into the GitHub website.**
The browser uploader accepts a maximum of 100 files per commit. You have 961,
mostly gallery photos. Use GitHub Desktop instead (Part 1 below). It is a normal
desktop app with no command line, and it has no practical file count limit. The
website uploader is still fine later for small text edits.

---

## Part 1 | Put the site on GitHub

### 1.1 Create a GitHub account
Go to github.com and sign up. Free plan is fine. Skip if you already have one.

### 1.2 Create the repository
1. Click the **+** at the top right, then **New repository**.
2. Repository name: `tdog-website`.
3. Set it to **Public**.
4. Do **not** tick "Add a README file". The folder already has one.
5. Click **Create repository**.

### 1.3 Install GitHub Desktop
Download from desktop.github.com, install it, and sign in with your GitHub account.

### 1.4 Clone the empty repository to your computer
1. In GitHub Desktop: **File** then **Clone repository**.
2. Pick `YOURNAME/tdog-website` from the list.
3. Choose where to put it on your computer, for example your Documents folder.
4. Click **Clone**. You now have an empty folder with that name.

### 1.5 Copy the site files in
1. Unzip the deployment package.
2. Open it and select **everything inside** it: all the `.html` files, the
   `assets` folder, the two school PDFs, `README.md`, `PUBLISHING.md`, and the
   hidden `.nojekyll` file.
3. Copy those **contents** into the cloned folder from step 1.4.

   Critical: copy the contents, not the containing folder. When you are done,
   `index.html` must sit directly inside `tdog-website`, not inside
   `tdog-website/something-else/`.

   On Windows, tick **View** then **Hidden items** so `.nojekyll` is visible and
   gets copied. On Mac, press **Cmd + Shift + .** to show hidden files.

### 1.6 Commit and push
1. Switch back to GitHub Desktop. It will list roughly 961 changed files.
2. In the **Summary** box at the bottom left, type `Initial site upload`.
3. Click **Commit to main**.
4. Click **Push origin** at the top.

Uploading 118 MB takes a few minutes. When the push finishes, refresh your
repository page on github.com and you should see all the files.

---

## Part 2 | Turn on GitHub Pages and test

1. In your repository, click **Settings**.
2. In the left sidebar, click **Pages**.
3. Under "Build and deployment", set **Source** to **Deploy from a branch**.
4. Set **Branch** to `main` and the folder to `/ (root)`. Click **Save**.
5. Wait one to two minutes, then refresh. GitHub shows your live address:

   `https://YOURNAME.github.io/tdog-website/`

**Test this properly before touching DNS.** Open every page, click through the
program tabs, the competition level tabs, the gallery filters and lightbox, and
open both school PDFs. Everything should work exactly as it does locally.

If a page looks unstyled or an image is missing, tell me the page and I will fix
it. Do not proceed to the domain step until the test address is correct.

---

## Part 3 | Point tdogtaekwondo.com at GitHub

Do this only once Part 2 looks right.

Your domain is registered with Wix. Wix does not allow changing nameservers on a
Wix domain, but it does let you edit the DNS records directly, which is all that
is needed. The domain stays registered with Wix and keeps renewing there.

### 3.1 Open your Wix DNS records
1. Go to **Domains** in your Wix account (manage.wix.com/account/domains).
2. Click the **Domain Actions** icon next to tdogtaekwondo.com.
3. Select **Manage DNS Records**.

### 3.2 Replace the A records
In the **A (Host)** section:

1. Add four new records, each with **Host Name** left blank (or `@` if Wix
   requires a value), pointing to these four GitHub Pages IP addresses:

   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

2. Click **Save**, then **Save Changes** in the pop-up.
3. **Now delete the old Wix A records.** Click the Domain Actions icon next to
   each old record and select Delete. Leaving them in place will cause visitors
   to randomly land on the old Wix site.

### 3.3 Replace the www CNAME record
In the **CNAME (Aliases)** section:

1. Add a record with **Host Name** `www` and **Value** `YOURNAME.github.io`
   (your GitHub username, then `.github.io`, with no repository name and no
   `https://`).
2. Save.
3. Delete the old Wix `www` CNAME record.

### 3.4 Leave everything else alone
Do not touch MX or TXT records. MX records carry email for the domain. Your
contact address is a Gmail address, so there may be nothing to preserve, but if
any MX or TXT records exist, leave them exactly as they are.

---

## Part 4 | Tell GitHub about the domain and turn on HTTPS

1. Back in your repository: **Settings** then **Pages**.
2. Under **Custom domain**, enter `tdogtaekwondo.com` and click **Save**.

   This automatically creates a `CNAME` file in your repository. That is
   expected and correct. It was deliberately left out of the upload package so
   that the test address in Part 2 would work rather than redirecting you to the
   old Wix site.

3. GitHub runs a DNS check. It may report an error for the first while, which is
   normal, DNS changes take time to spread. Wix advises up to 48 hours, though
   it is often much faster.
4. Once the check passes, GitHub issues a free SSL certificate. When the
   **Enforce HTTPS** tick box becomes available, tick it.

Ticking Enforce HTTPS is what makes the padlock appear and stops the browser
warning about an insecure site. If the box stays greyed out for more than a day
after DNS resolves, remove the custom domain, save, re-enter it and save again.
That forces the certificate to be reissued.

---

## Part 5 | Verify it worked

Check all four of these in a browser:

- `http://tdogtaekwondo.com`
- `http://www.tdogtaekwondo.com`
- `https://tdogtaekwondo.com`
- `https://www.tdogtaekwondo.com`

All four should end up on your new site with a padlock showing. GitHub
automatically redirects between the apex and www versions.

Use a private or incognito window, and ideally your phone on mobile data rather
than wifi. Your normal browser will have the old Wix site cached and can show it
for hours after the change is actually complete.

---

## Part 6 | After it is live

**Do not cancel anything at Wix until the new site has been confirmed working
for a few days.** If something goes wrong you can put the old A and CNAME
records back and the Wix site returns.

**Before cancelling any Wix plan, confirm with Wix what happens to the domain
registration.** The domain registration and the site plan are billed separately,
but if the domain came bundled as part of a Premium plan, cancelling can affect
it. Ask Wix directly and get the answer in writing before you cancel. Losing the
registration would mean losing the domain.

**Making changes from now on.** For small text edits, open the `.html` file on
github.com, click the pencil icon, edit, and click Commit changes. The live site
updates in about a minute. For anything larger, edit in the local folder and use
GitHub Desktop to commit and push.

**Optional tidy up.** These four files are internal working references and are
publicly downloadable once the site is live. You can delete them from the
repository with no effect on the site:
`gallery-asset-key.pdf` (13 MB), `gallery-asset-key.csv`,
`site-images-key.pdf`, `site-images-key.csv`.

**Optional security step.** GitHub recommends verifying your custom domain
(Settings, then Pages, under custom domain) to prevent anyone else claiming a
subdomain of it later.

---

## If something goes wrong

| Symptom | Most likely cause |
|---|---|
| Test address redirects to the old Wix site | A `CNAME` file is in the repository before DNS was switched. Delete it, test, then re-add the domain in Settings. |
| Site loads but has no styling or images | Files were uploaded one level too deep. `index.html` must be at the repository root. |
| Some images missing, others fine | A filename capitalisation mismatch. Send me the page and I will correct it. |
| Domain still shows Wix after a day | Old Wix A or CNAME records were not deleted, or browser cache. Test in incognito on mobile data. |
| Enforce HTTPS greyed out | Certificate not issued yet. Wait, then remove and re-add the custom domain. |

---

## Reference

- GitHub Pages custom domains, including the four IP addresses:
  https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- GitHub file and upload limits (100 files per web upload, 25 MB per file):
  https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository
- Wix, connecting a Wix domain to an external site:
  https://support.wix.com/en/article/connecting-a-wix-domain-to-an-external-site
- Wix, transferring a domain away from Wix (only if you ever want to leave Wix
  entirely, not required for this):
  https://support.wix.com/en/article/transferring-your-wix-domain-away-from-wix-2477749
