---
name: blog-publishing
description: Publish source-folder blog articles to this Jekyll site as separate posts, preserving text and metadata while handling images, links, duplicates, and validation.
---

# Blog publishing

Use this skill when asked to turn one or more source folders into blog posts for this repository, or to prepare post images and links. Work only with source material supplied or explicitly identified by the user. Do not copy private source articles or images into this skill.

## Workflow

1. **Inspect before editing.** Read the repository instructions, `_config.yml`, a few recent posts in `_posts/`, the relevant layout/includes, and `.github/workflows/ci.yml`. Check the working tree and do not overwrite unrelated changes.
2. **Inventory the complete source.** Recursively list every file in the supplied folders. Classify each as an article, supporting information, image/media, or unrelated. Map each article to its supporting information and images; do not silently omit files or combine distinct articles. If the intended article boundaries or use of supporting material are unclear, ask before publishing.
3. **Check for duplicates.** Compare titles, canonical/source URLs, and article content with existing posts before creating anything. Update an existing post only when that is what the user asked for; otherwise report likely duplicates and pause those items.
4. **Confirm publication details.** Preserve the source wording and structure unless editing is requested. Use the actual publication date and source title. Do not infer or fabricate dates, authors, descriptions, attribution, or factual claims; ask for missing required details. For imported LinkedIn articles, retain the canonical LinkedIn URL and identify the original publication in the post.
5. **Create one Jekyll post per article.** Follow the filename convention `_posts/YYYY-MM-DD-title-in-kebab-case.md` and the metadata used by nearby posts, typically `layout: post`, `title`, `date`, `description`, `tags`, and `author`. Add `canonical_url` for republished material when available. Use the repository's existing tag and category conventions; do not add unsupported front matter or change site-wide settings for an individual post.
6. **Handle images as local assets.** Reuse a supplied image when it is clearly associated with the article. If an external image must be obtained, use only a user-provided or otherwise authorized source; do not bypass access controls. Verify the downloaded file is a valid image and use its actual format and extension. Store it under the closest matching existing directory in `assets/img/` (for example, LinkedIn article assets under `assets/img/linkedin/<post-slug>/` and WIALT artwork under `assets/img/wialt/`). Reference it with a site-root path in `cover-img` and/or Markdown. Write concise, accurate alt text based on the image; do not guess at unseen image content.
7. **Preserve and verify links.** Keep source URLs and useful links intact. Check that each destination resolves to the intended article, episode, or reference; follow redirects and use the canonical destination where clear. Do not replace an inaccessible or ambiguous link with a guess—report it for review. Ensure links in the post use valid Markdown and local asset paths exist.
8. **Review and validate.** Check every source article has exactly one intended post, required front matter is present, dates and filenames agree, images render from the correct paths, attribution/canonical URLs are retained, and no unrelated files changed. Run the Jekyll build used by `.github/workflows/ci.yml` when the required dependencies and CI configuration are available; otherwise perform the strongest available local checks and state what could not be run.
9. **Return a reviewable result.** Summarize the created or updated posts, assets, unresolved issues, and validation performed. Leave the changes for review. Do not commit, open a pull request, merge, or deploy unless the user explicitly requests that action.

## Site conventions

- Posts live in `_posts/`; their dates are part of both the filename and front matter.
- Site post defaults and the post layout are defined in `_config.yml` and `_layouts/post.html`. The layout renders tags and the tag sidebar.
- Keep imported-source attribution in the post body as well as `canonical_url` when the source is LinkedIn, following existing posts.
- Use the smallest change that meets the request. Never add source-folder contents or personal material to this skill itself.
