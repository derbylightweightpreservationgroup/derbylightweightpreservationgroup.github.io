# Derby Lightweight Preservation Group website

This repository contains the Jekyll source for the Derby Lightweight Preservation Group organisation website. It uses the [Alembic](https://github.com/daviddarnes/alembic) remote theme and is intended to be published at <https://derbylightweightpreservationgroup.github.io> using GitHub Pages.

## Prerequisites

Local development requires:

- Git
- Ruby
- Bundler

### Installing Ruby and Bundler on Windows

1. Confirm that Git is installed:

   ```powershell
   git --version
   ```

2. Download the latest 64-bit **Ruby+Devkit 3.3.x** installer from [RubyInstaller for Windows](https://rubyinstaller.org/downloads/). As of August 2026, the current 3.3 release is `Ruby+Devkit 3.3.12-1 (x64)`. The 3.3 release line is recommended because [GitHub Pages currently builds with Ruby 3.3](https://pages.github.com/versions.json), reducing differences between local and hosted builds.

3. Run the installer with its default options, including the option to add the Ruby executables to `PATH`.

4. Leave the final `ridk install` step enabled. When its terminal menu appears, select the entry labelled **MSYS2 and MINGW development toolchain** and allow it to finish.

5. Close the installer and open a new PowerShell window so the updated `PATH` is loaded.

6. Verify Ruby and RubyGems:

   ```powershell
   ruby --version
   gem --version
   ```

7. Check whether Bundler was installed with Ruby:

   ```powershell
   bundle --version
   ```

   If that command is unavailable, install and verify Bundler:

   ```powershell
   gem install bundler
   bundle --version
   ```

A separate global Jekyll installation is not needed. The repository's `Gemfile` installs the GitHub Pages-compatible Jekyll version through Bundler. See the [official Jekyll Windows installation guide](https://jekyllrb.com/docs/installation/windows/) for additional troubleshooting.

## Local installation

From the repository directory, install the dependencies:

```powershell
bundle install
```

`Gemfile.lock` should be committed after `bundle install` generates it. Keeping the lockfile makes local dependency installation reproducible. Do not create or edit the lockfile by hand.

The `jekyll-remote-theme` dependency is fixed to version `0.4.3`, which is the version used by GitHub Pages. This prevents Bundler from selecting a newer remote-theme release that is incompatible with the GitHub Pages dependency set.

The site pins Alembic to the published `4.1.0` tag (`afbd0c1f0988dd35ef7017f8c73faf5e3b376f89`) instead of following its changing `main` branch. Alembic's gem package declares Jekyll 4.x, but this repository consumes the theme through `jekyll-remote-theme`; the pinned layouts and assets have been tested with the GitHub Pages 232 dependency set and Jekyll 3.10.0 used here.

The `Gemfile` includes `tzinfo-data` on Windows because Windows does not provide the IANA timezone database needed for the site's `Europe/London` setting.

## Local preview

Start the local development server:

```powershell
bundle exec jekyll serve
```

Open <http://localhost:4000> in a browser. Stop the server with <kbd>Ctrl</kbd>+<kbd>C</kbd>.

To build the site without starting the server, run:

```powershell
bundle exec jekyll build
```

The generated site is written to `_site/`, which is ignored by Git.

## DLPG Committee preview

The published GitHub Pages site is currently configured as a preview solely for the DLPG Committee.

With `preview_mode: true` in `_config.yml`, every HTML page includes a search-engine `noindex` instruction and a visible draft notice. The sitemap and feed plugins are also disabled during the preview. These measures discourage indexing but do not make the site private: anyone with the URL can view and forward it, and the public repository can still be discovered.

Do not publish personal contact details, unapproved photographs, private working arrangements, credentials or other confidential material. Only add content that is safe to expose publicly even while it is awaiting final approval.

After building, verify the preview controls in PowerShell:

```powershell
Get-ChildItem _site -Recurse -Filter *.html | Select-String 'name="robots" content="noindex"'
Get-ChildItem _site -Recurse -Filter *.html | Select-String 'Draft preview.'
Test-Path _site/sitemap.xml
Test-Path _site/feed.xml
```

The HTML searches should find the metadata and notice on every generated page. Both `Test-Path` commands should return `False`. Do not add `Disallow: /` to `robots.txt`, because search crawlers need to read each page to observe its `noindex` instruction.

For the public launch:

1. Set `preview_mode: false` in `_config.yml`.
2. Restore `jekyll-sitemap` and `jekyll-feed` under `plugins`.
3. Complete the content checks in [Updating the site details](#updating-the-site-details).
4. Rebuild and confirm that neither `noindex` nor the draft notice appears in generated HTML.
5. Confirm that `_site/sitemap.xml` and `_site/feed.xml` are generated before deploying.

## Site structure

The public navigation is deliberately small:

- Home
- The Train
- Restoration
- Updates
- Support Us
- About
- Contact

Updates are standard Jekyll posts in `_posts/`. The Updates archive displays ten posts per page at `/updates/`, with further pages generated at `/updates/page2/`, `/updates/page3/` and so on. The changing restoration summary and task lists are stored in `_data/restoration.yml` and appear on the Home and Restoration pages. Two local layouts display restoration data and update featured images without exposing template code to routine CMS editors.

When upgrading Alembic, compare the upstream `post.html` and `page.html` structure with `_layouts/post.html` and `_layouts/restoration.html` before changing the pinned theme version.

## Editing with Pages CMS

Pages CMS reads `.pages.yml` from the repository root. It exposes only Updates, The Train, Restoration, Support Us, About, Contact and Restoration Status. Uploaded images are stored in `assets/uploads/` with safe filenames.

Fixed pages and restoration data cannot be created, renamed or deleted through the CMS. Update posts can be created and deleted, while their filenames cannot be renamed after creation. Technical files are not listed in the CMS, although normal GitHub repository permissions still apply outside it.

See `CONTRIBUTING.md` for writing, image preparation, alternative text, credits and copyright guidance.

## Updating the site details

Before publishing, replace the contact email placeholder everywhere it occurs. The following commands locate the values that may need updating:

```powershell
git grep -n -F "Derby Lightweight Preservation Group"
git grep -n -F "derbylightweightpreservationgroup"
git grep -n -F "[CONTACT EMAIL]"
git grep -n -F "TO BE CONFIRMED"
git grep -n -F "SAMPLE"
```

- Update the club name in `_config.yml`, `index.md`, and this README if the display name changes.
- Update the organisation slug in `_config.yml` and this README if the GitHub organisation changes.
- Replace every `[CONTACT EMAIL]` occurrence with the public club contact address.
- Replace each `[TO BE CONFIRMED: ...]` marker only with approved factual content.
- Delete the sample post and `assets/uploads/example-update.png` before launch.

Rebuild the site after making changes.

## Publishing with GitHub Pages

1. Commit the site files and push them to the `main` branch.
2. On GitHub, open the repository's **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select the `main` branch.
5. Select the `/ (root)` folder.
6. Save the setting.
7. Visit <https://derbylightweightpreservationgroup.github.io> after GitHub reports that deployment has completed.

GitHub Pages configuration is a manual repository setting. A successful local build does not confirm that the GitHub Pages deployment has completed.

## Deferred work

Custom DNS, GoDaddy DNS records and a `CNAME` file remain deferred. No custom GitHub Actions publishing workflow is required for this branch-publishing setup. Pages CMS must be connected to the repository separately; adding `.pages.yml` configures its editing interface but does not install the GitHub App or invite editors.
