# Scottish Breast Studies Group website

Source for [sbsg.scot](https://sbsg.scot), the website of the Scottish Breast Studies Group (SBSG). The site is built with [Jekyll](https://jekyllrb.com/) on the Minima theme and published by GitHub Pages from the `main` branch of this repository. Questions about the site go to [secretary@sbsg.scot](mailto:secretary@sbsg.scot).

## How publishing works

GitHub Pages rebuilds the site each time a change is merged into `main`, and the new version usually appears at sbsg.scot within a few minutes. The **Actions** tab shows each build; a red cross there means the build failed and the live site still shows the previous version. The custom domain is set in the `CNAME` file and registered with 20i, and GitHub Pages provides the HTTPS certificate.

Changes reach `main` through a pull request. A ruleset on `main` requires one approving review before a pull request can be merged, so every edit is seen by a second person before it goes live. Repository administrators can bypass the rule, but routine edits should still go through review.

## Making a change

Most edits are to text in a single Markdown file and can be made entirely in the browser.

1. Open the file on GitHub (for example `webinars.md`) and click the pencil icon.
2. Make the edit, then use the **Preview** tab to check the formatting.
3. Click **Commit changes**, choose **Create a new branch for this commit and start a pull request**, and give the branch a short descriptive name.
4. Open the pull request, describe the change in a sentence, and request a review from another editor.
5. Once the pull request is approved and merged, check the live page after a few minutes.

For larger changes, such as new images, several pages at once or layout changes, clone the repository with [GitHub Desktop](https://desktop.github.com/), work on a new branch, and open a pull request from there. Editors whose work computers do not allow software installation can fork the repository on GitHub, edit the fork in the browser and open a pull request from the fork.

## Where things are

| Path | Contents |
| --- | --- |
| `index.md` | Home page |
| `about.md`, `history.md`, `studies.md`, `webinars.md`, `centres.md`, `join.md`, `contact.md` | The pages in the top navigation |
| `privacy.md` | Privacy policy, covering the mailing list, analytics and embedded videos |
| `signup-QR.md` | Page reached from the sign-up QR code |
| `_posts/` | Blog posts |
| `_config.yml` | Site title, description, analytics ID, plugins and the order of the navigation tabs (`header_pages`) |
| `_layouts/default.html` | Page template, overriding the Minima default |
| `_includes/` | Shared fragments: `head.html` (metadata, icons, analytics), `footer.html`, `google-analytics.html`, `schema-org.html` (structured data for search engines) |
| `assets/main.scss`, `assets/css/style.scss` | Site styles and the SBSG colour palette |
| `assets/images/` | Images, logos and the sign-up QR code |
| `CNAME` | Custom domain; do not edit |

Each page starts with a front-matter block between two `---` lines that sets its layout, title and web address (`permalink`). Changing a permalink changes the page's address and breaks existing links to it, so leave permalinks as they are unless the change is intended.

## Common tasks

### Updating the webinar programme

All webinar information is in `webinars.md`, which has three parts. **Next Session** gives the speaker, chair, date, time and Teams registration link for the next webinar. **Programme** is a table of forthcoming sessions with one row per webinar. **Archive** lists past sessions by year.

After each webinar, replace the Next Session details with the following session, remove its row from the Programme table and add an entry under the correct year in the Archive. Teams registration links are long and contain characters that some editors alter, so paste them in full and test the link on the live page.

### Adding a webinar recording

Recordings are published on the [SBSG YouTube channel](https://www.youtube.com/@ScottishBreastStudiesGroup). Before a recording is published, confirm that every speaker has agreed to it and that no attendee who has not agreed can be seen, heard or named. Once the video is public, add a link and an embedded player to its Archive entry, replacing `VIDEO_ID` with the code after `youtu.be/` in the video's share link:

```html
<div style="position:relative;width:100%;max-width:720px;aspect-ratio:16/9;margin:0.5em 0 1.5em;">
  <iframe src="https://www.youtube-nocookie.com/embed/VIDEO_ID" title="Webinar title and speaker" style="position:absolute;inset:0;width:100%;height:100%;border:0;" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
```

The `youtube-nocookie.com` address loads YouTube's privacy-enhanced player, which sets no cookies until the visitor presses play, as the privacy policy states. Use this address for every embed so that the policy remains accurate.

### Adding a blog post

Create a file in `_posts/` named `YYYY-MM-DD-short-title.md` and copy the front matter from an existing post, changing the title, author, date, permalink and description. The description appears in search results and when the post is shared, so keep it to one or two sentences.

### Adding an image

Upload the image to `assets/images/`, keeping the file under about 500 KB, and reference it as `/assets/images/file-name.png`. Every image needs an `alt` description for screen readers.

### Updating the news section

The News section near the top of the home page is generated from `_data/news.yml`, so editors change that one file rather than the page itself. Each item has a label, title, date line, short summary and one or two links, and items appear in the order they are listed. An item stops appearing after its `show_until` date, and an optional `highlight` line (such as a registration deadline) stops appearing after its `highlight_until` date.

Dates are checked only when the site is rebuilt, which happens when a change is merged into `main`. An expired item therefore stays on the live site until the next change of any kind is published, so remove or update stale items when editing the site. When the next webinar changes, update both `webinars.md` and its item in `_data/news.yml`. Keep three or four items at most, and keep each summary to two or three sentences.

### Changing the navigation

The tabs and their order are set by the `header_pages` list in `_config.yml`. A new page appears in the navigation only once it is added to that list.

## Analytics and the mailing list

Google Analytics (property `G-M78TDHRYNC`) is loaded through `_includes/google-analytics.html`, and only in the production build on GitHub Pages, so local previews are not counted. The mailing-list sign-up form on `join.md` is an EmailOctopus form; subscriber data is held in EmailOctopus, not in this repository. Any change to what the site collects, or to the services it uses, needs a matching change to `privacy.md`.

## Previewing locally (optional)

Previewing on your own computer is useful for layout or style changes but is not needed for text edits. With Ruby installed, run the following in the repository folder and open http://localhost:4000:

```
gem install jekyll minima jekyll-feed jekyll-seo-tag jekyll-sitemap
jekyll serve
```

## Line endings on Windows

The repository stores files with Unix (LF) line endings. Git for Windows converts them to Windows (CRLF) endings on checkout and back again on commit, provided `core.autocrlf` is set to `true`, which is the installer's default. If `git status` reports almost every file as modified with no visible change, the line-ending setting is the cause; run `git config core.autocrlf true` in the repository rather than committing those files.
