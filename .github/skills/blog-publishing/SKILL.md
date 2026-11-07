---
name: blog-publishing
description: Publish source-folder blog articles to this Jekyll site as separate posts, preserving text and metadata while handling images, links, duplicates, and validation.
---

# Blog publishing

Use this skill when asked to create or update blog posts for this repository, including posts made from source folders, or to prepare post images and links. Work only with source material supplied or explicitly identified by the user. Do not copy private source articles or images into this skill.

## Workflow

1. **Inspect before editing.** Read the repository instructions, `_config.yml`, a few recent posts in `_posts/`, the relevant layout/includes, and `.github/workflows/ci.yml`. Check the working tree and do not overwrite unrelated changes.
2. **Inventory the complete source.** Recursively list every file in the supplied folders. Classify each as an article, supporting information, image/media, or unrelated. Map each article to its supporting information and images; do not silently omit files or combine distinct articles. If the intended article boundaries or use of supporting material are unclear, ask before publishing.
3. **Check for duplicates.** Compare titles, canonical/source URLs, and article content with existing posts before creating anything. Update an existing post only when that is what the user asked for; otherwise report likely duplicates and pause those items.
4. **Audit source quality.** Proofread each article for likely typos, grammar or punctuation problems, broken sentences, duplicated passages, placeholders, malformed text, and signs that content is truncated (for example, a heading with no section or a list that stops abruptly). Check for internal contradictions, suspicious numbers or names, and factual claims that need a reliable source; verify claims against appropriate authoritative sources when practical, especially clinical, legal, or other high-impact claims. Treat these as potential errors, not permission to rewrite: preserve the supplied text and report each concern with its file, a short excerpt, why it may be wrong, any evidence or verification, and a suggested correction if clear. Ask the user to confirm substantive or uncertain corrections before changing them. Do not present an unverified claim as fact.
5. **Reconcile dates and filenames.** Compare explicit publication dates in the article, source metadata, any source filename, and any existing post or canonical page. Filesystem timestamps alone are not evidence of publication date. If dates conflict, are incomplete, or cannot be verified, ask the user which date to use; never silently choose one. Before creating a post, ensure the date is a valid Jekyll date in `YYYY-MM-DD` form, the `_posts/YYYY-MM-DD-title-in-kebab-case.md` filename uses that same date, and its lowercase kebab-case title slug matches the post title. Check for filename collisions and for unintended future dates; retain a future date only when it is explicitly intended and verified. Report mismatches and proposed resolutions for user confirmation.
6. **Confirm publication details.** Preserve the source wording and structure unless editing is requested. Use the actual publication date and source title. Do not infer or fabricate dates, authors, descriptions, attribution, or factual claims; ask for missing required details. For imported LinkedIn articles, retain the canonical LinkedIn URL and identify the original publication in the post.
7. **Create or update one Jekyll post per article.** Apply the [post front matter standard](#post-front-matter-standard) to every new or updated post, whether or not it came from an imported source folder. Preserve verified existing metadata when updating; do not add, remove, or change values based on guesswork. Add `canonical_url` for republished material when available. Do not add unsupported front matter or change site-wide settings for an individual post.
8. **Handle images as local assets.** Reuse a supplied image when it is clearly associated with the article. If an external image must be obtained, use only a user-provided or otherwise authorized source; do not bypass access controls. Verify the downloaded file is a valid image and use its actual format and extension. Store it under the closest matching existing directory in `assets/img/` (for example, LinkedIn article assets under `assets/img/linkedin/<post-slug>/` and WIALT artwork under `assets/img/wialt/`). Before setting `cover-img`, inspect the current post layout, header include, and responsive/theme styles to confirm how that post type or tag uses it; for example, WIALT post headers currently suppress the cover background even though the image may still be used by the home-page feed. Do not assume a cover appears behind every post title. When it is used as a header, preview the rendered crop on desktop and mobile in both light and dark themes; select a title-safe image/crop with sufficient contrast, or omit the cover and place the image inline when composition or contrast is poor. Reference images with site-root paths in `cover-img` and/or Markdown. Write concise, accurate alt text based on the image; do not guess at unseen image content.
9. **Preserve and verify links.** Keep source URLs and useful links intact. Check that each destination resolves to the intended article, episode, or reference; follow redirects and use the canonical destination where clear. Do not replace an inaccessible or ambiguous link with a guess—report it for review. Ensure links in the post use valid Markdown and local asset paths exist.
10. **Review and validate.** Check every new or updated post against the front matter standard, confirm dates and filenames agree, images render from the correct paths, attribution/canonical URLs are retained, and no unrelated files changed. For imports, also check every source article has exactly one intended post. Build and preview a representative post (including any applicable special rendering path such as WIALT); verify title readability on desktop and mobile in both light and dark themes, and inspect the source image dimensions/aspect ratio together with its actual rendered crop. Run the Jekyll build used by `.github/workflows/ci.yml` when the required dependencies and CI configuration are available; otherwise perform the strongest available local checks and state what could not be run.
11. **Return a reviewable result.** Summarize the created or updated posts, assets, unresolved issues, and validation performed. Include a separate list of suspected source errors and date/filename discrepancies, with the evidence and what needs the user's decision; distinguish verified errors from possibilities. Leave the changes for review. Do not commit, open a pull request, merge, or deploy unless the user explicitly requests that action.

## Site conventions

- Posts live in `_posts/`; their dates are part of both the filename and front matter.
- Site post defaults and the post layout are defined in `_config.yml` and `_layouts/post.html`. The layout renders tags and the tag sidebar.
- Keep imported-source attribution in the post body as well as `canonical_url` when the source is LinkedIn, following existing posts.
- Use the smallest change that meets the request. Never add source-folder contents or personal material to this skill itself.

## Post front matter standard

Apply this standard to **every post creation and update**, including original writing, imported articles, and edits to existing posts.

Use this core field order and representation:

```yaml
---
layout: post
title: "Post title"
date: YYYY-MM-DD
tags: [existing-tag, another-tag]
author: Author name
---
```

The values above are format examples, not metadata to copy. Replace them only with verified or user-confirmed values.

- **Required for each post:** `layout: post`, `title`, `date`, `tags`, and `author`. This matches the post front matter in `_posts/`; although `_config.yml` defaults posts to the `post` layout, retain the explicit `layout` used throughout the posts. The header displays the title, author, and date; the post layout uses tags for links and the topic sidebar.
- **Optional when supported by the post:** `description` (present on some posts, absent on others), `excerpt` (a deliberate feed excerpt), `canonical_url` (when the post republishes or refers to an original canonical publication), `cover-img` (when an appropriate local image exists and its rendering has been checked), `display_date` (only when the intentionally displayed date differs from the normal formatted post date), and `last-updated` (only when recording a real update date). Keep optional metadata only when it is accurate and useful; do not add empty values. The configured layout already supplies `comments` and `social-share` defaults, so do not repeat them without a specific reason.
- **Date and filename:** Write `date` as an unquoted ISO calendar date, `YYYY-MM-DD`, and use the exact same date at the start of `_posts/YYYY-MM-DD-title-in-kebab-case.md`. Use a lowercase kebab-case slug based on the title. Check for collisions and unintended future dates. Resolve dates from publication evidence, not filesystem timestamps. If the date is missing or sources disagree, pause and get confirmation rather than choosing one.
- **Tags:** Always use a YAML list in the same inline form as existing posts, including for one tag: `tags: [pharmacy]`. Use individual tag strings, not a scalar, comma-separated string, or `categories` field. Reuse the site's established tag spelling and capitalization where relevant (for example, `WIALT`, `AI`, and `NHS` appear in existing tags); do not silently create near-duplicate variants or invent tags when the topic/taxonomy is unclear.
- **Updates and mismatches:** Preserve verified metadata when editing. If a required value is absent or ambiguous, do not infer it from surrounding content or site defaults; request the missing fact or retain the existing confirmed value. If an existing title/date and its filename disagree, report the mismatch and confirm the correction before changing it. The permalink is derived from the post date and title in `_config.yml`, so changing either can change a published URL; do not rename a published post or alter its permalink without confirmation.
