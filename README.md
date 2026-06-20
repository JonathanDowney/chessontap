# Chess on Tap Website: Collaborator Editing Guide

This repository contains the files for the Chess on Tap website. Changes merged into the `main` branch are automatically published to the live website.

## What you can update

You can safely make routine updates such as:

- Website text, headings, dates, and event information
- Photos and other images in `img/`
- Links, captions, and basic HTML/CSS presentation changes

For changes that affect deployment or server configuration, contact the site owner first. These protected files require owner approval:

- `.github/workflows/`
- `deploy/`
- `Dockerfile`
- `docker-compose*.yml`
- `nginx/`

## Branch and pull request workflow

`main` is the production branch. It should always contain a working, publishable version of the site.

Do **not** edit or push directly to `main`. For every task, create a short-lived branch, open a pull request (PR), merge it, and then delete the branch.

### Start a new task

Before creating a new branch, update your local `main`:

```bash
git switch main
git pull
```

Create one branch for one focused task:

```bash
git switch -c update-july-events
```

Use clear branch names such as:

```text
update-july-events
add-tournament-photos
fix-homepage-link
refresh-about-copy
```

Avoid vague names such as `changes`, `edits`, `test`, or `new-stuff`.

### Make changes and open a PR

After making your edits:

```bash
git add .
git commit -m "Update July event details"
git push -u origin update-july-events
```

Then open a pull request on GitHub:

```text
update-july-events → main
```

Review the changed files and merge the PR when it is ready. Merging a normal content PR automatically deploys the change to the live website.

### After the PR is merged

Delete the branch on GitHub using the **Delete branch** button shown on the merged PR page. The repository may also be configured to delete merged branches automatically.

Then clean up your local copy:

```bash
git switch main
git pull
git fetch --prune
git branch -d update-july-events
```

`git fetch --prune` updates your local record of the repository and removes stale references to remote branches that have already been deleted on GitHub. It does **not** delete your local files or local branches.

Use `git branch -d` in normal circumstances. It refuses to delete a branch that has not been merged, which helps prevent accidental loss of unfinished work. Avoid `git branch -D` unless you are certain the branch is no longer needed.

Never reuse an old branch for a new, unrelated update. Start from an updated `main` branch each time.

## Editing text

Most visible website content is in:

```text
index.html
```

On GitHub:

1. Open `index.html`.
2. Click the pencil icon (**Edit this file**).
3. Make the needed text change.
4. At the bottom of the page, choose **Create a new branch for this commit and start a pull request**.
5. Give the branch and commit a clear name.
6. Click **Propose changes**.
7. Review and create the pull request.

Keep existing HTML tags and quote marks intact. Edit the text between the tags unless you intentionally need to change the page structure.

Example:

```html
<h2>Chess Night</h2>
<p>Join us every Tuesday at 6:00 p.m.</p>
```

Here, you can safely change the words `Chess Night` or the sentence inside the `<p>` tags.

## Uploading and using photos

Website images are stored in:

```text
img/
```

### Add an image

1. Open the `img/` folder on GitHub.
2. Click **Add file** → **Upload files**.
3. Upload the image.
4. Use a clear, lowercase filename with hyphens, for example:

```text
july-2026-chess-night.jpg
```

Avoid spaces, parentheses, and vague names such as `IMG_1234.jpg`.

5. Commit the upload to a new branch and open a PR.

### Add the image to the page

After uploading an image, reference it from `index.html` with a relative path:

```html
<img src="img/july-2026-chess-night.jpg" alt="Players at Chess on Tap in July 2026">
```

Always include useful `alt` text that describes the image for visitors using screen readers.

### Image guidelines

- Use JPG for photos and PNG for graphics that need transparency.
- Resize very large photos before uploading when practical.
- Prefer images that are reasonably compressed for the web.
- Do not upload private, copyrighted, or unapproved photos.
- Avoid replacing an existing file unless you are sure it is no longer used elsewhere on the site.

## Editing other page elements

You may make modest changes to layout, links, or styles when needed. Before changing HTML structure or CSS:

- Review the existing code around the change.
- Make one focused change per pull request when possible.
- Use the PR preview/diff to confirm you did not unintentionally remove other content.
- Check the live website after the PR is merged.

For substantial redesigns, navigation changes, JavaScript changes, or anything involving deployment/configuration files, open a PR and request the site owner's review before merging.

## Pull request checklist

Before merging, confirm:

- [ ] The content is accurate and proofread.
- [ ] Links work and point to the intended destination.
- [ ] New images display correctly and have descriptive `alt` text.
- [ ] Only intended files are included in the PR.
- [ ] The website still looks correct on desktop and mobile.
- [ ] No protected deployment or infrastructure files were changed unintentionally.

## What happens after merge

When a PR is merged into `main`:

1. GitHub Actions automatically deploys the repository to the production website.
2. The deployment normally completes within a few minutes.
3. Refresh the live site to confirm the update appears. A hard refresh may help if your browser has cached an older version.

## Need help?

When opening a PR, describe what you changed and add any questions or concerns in the PR description. For changes that might affect layout broadly, site behavior, or deployment, request review before merging.
