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

## Updating the site details

Before publishing, replace the contact email placeholder everywhere it occurs. The following commands locate the values that may need updating:

```powershell
git grep -n -F "Derby Lightweight Preservation Group"
git grep -n -F "derbylightweightpreservationgroup"
git grep -n -F "[CONTACT EMAIL]"
```

- Update the club name in `_config.yml`, `index.md`, and this README if the display name changes.
- Update the organisation slug in `_config.yml` and this README if the GitHub organisation changes.
- Replace every `[CONTACT EMAIL]` occurrence with the public club contact address.

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

Custom DNS, GoDaddy DNS records, a `CNAME` file, and Pages CMS are intentionally deferred to later phases. No custom GitHub Actions publishing workflow is required for this branch-publishing setup.
