# Deploying casad.io to GitHub Pages

These instructions assume you have a GitHub account (thecdepot) and own casad.io through Namecheap.

## Step 1: Create the repository

1. Go to https://github.com/new
2. Repository name: `casad.io`
3. Set visibility to Public (GitHub Pages requires public repos on free accounts)
4. Leave all other options off (no README, no .gitignore, no license)
5. Click "Create repository"

## Step 2: Upload the site files

After creating the empty repository, GitHub shows a page with setup instructions. Ignore those.

1. On the repository page, click "uploading an existing file" (this link appears in the instructions GitHub shows for empty repos). If you do not see it, click "Add file" then "Upload files" from the repository's main page.
2. Drag the entire contents of the casad-io folder into the upload area. This includes:
   - `index.html`
   - `full-text.html`
   - `about.html`
   - `second-book.html`
   - `CNAME`
   - `css/` folder (containing `style.css`)
   - `chapters/` folder (containing 01.html through 24.html)
3. Scroll down. In the "Commit changes" section, leave the default message or type "Initial site upload."
4. Click "Commit changes."

Important: upload the *contents* of the casad-io folder, not the folder itself. The `index.html` file must be at the root level of the repository.

## Step 3: Enable GitHub Pages

1. In your repository, click "Settings" (the gear icon tab along the top).
2. In the left sidebar, click "Pages."
3. Under "Source," select "Deploy from a branch."
4. Under "Branch," select `main` and `/ (root)`. Click "Save."
5. GitHub will begin building the site. This takes about a minute.

After the build completes, the site will be live at `https://thecdepot.github.io/casad.io/` temporarily. The custom domain setup in the next step replaces this URL.

## Step 4: Configure the custom domain in GitHub

Still in Settings > Pages:

1. Under "Custom domain," type `casad.io` and click "Save."
2. GitHub will check the DNS. It will show an error until you complete Step 5. That is expected.
3. After DNS is configured (Step 5), return here and check "Enforce HTTPS." This may take up to 24 hours to become available after DNS propagation.

## Step 5: Configure DNS in Namecheap

1. Log in to Namecheap. Go to Domain List. Click "Manage" next to casad.io.
2. Click the "Advanced DNS" tab.
3. Delete any existing host records (parking page, email forwarding, etc.) that you do not need.
4. Add the following records:

**A Records (point the root domain to GitHub Pages):**

| Type | Host | Value |
|------|------|-------|
| A Record | @ | 185.199.108.153 |
| A Record | @ | 185.199.109.153 |
| A Record | @ | 185.199.110.153 |
| A Record | @ | 185.199.111.153 |

**CNAME Record (point www to GitHub):**

| Type | Host | Value |
|------|------|-------|
| CNAME | www | thecdepot.github.io. |

Note the trailing period after `thecdepot.github.io.` in the CNAME value. Some registrars add it automatically.

5. Save all records.

## Step 6: Wait for DNS propagation

DNS changes typically take 10 to 30 minutes but can take up to 48 hours. You can check propagation status at https://dnschecker.org by searching for `casad.io`.

Once propagation completes:
- `casad.io` will load the site
- `www.casad.io` will redirect to `casad.io`
- GitHub will issue a free SSL certificate, enabling HTTPS

## Step 7: Verify HTTPS

After DNS propagates (usually within an hour), go back to your repository Settings > Pages. The "Enforce HTTPS" checkbox should now be available. Check it if it is not already checked.

Visit `https://casad.io` to confirm the site loads with a valid certificate.

## Updating the site later

To update any file:
1. Go to the repository at https://github.com/thecdepot/casad.io
2. Navigate to the file you want to change
3. Click the pencil icon (edit) to edit directly in the browser, or use "Add file" > "Upload files" to replace files
4. Commit the change. The site rebuilds automatically within a minute.

To add chapter text: open the relevant file in `chapters/` (e.g., `01.html`), find the placeholder paragraph, and replace it with the chapter content formatted as HTML paragraphs.
