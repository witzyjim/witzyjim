# Installation, editing and migration

## Install on staging first

1. Back up the existing database and wp-content files. Create a staging clone and record currently active plugins, menus, page templates and important URLs.
2. In **Plugins → Add New → Upload Plugin**, upload `invictus-core-1.0.0.zip` and activate **Invictus Core**.
3. In **Appearance → Themes → Add New → Upload Theme**, upload `invictus-editorial-1.0.0.zip` and activate **Invictus Editorial** on staging.
4. Visit **Settings → Permalinks** and save once if the resource archive does not resolve. The new resource library uses `/resource-library/`; existing `/publications/` content is not replaced or redirected automatically.
5. Under **Appearance → Customize → Invictus homepage**, edit the hero headline, introductory text, photo and alt text. Use **Site Identity** for a replacement logo/site icon. Review and approve the default editorial wording.
6. Assign a primary WordPress menu in the menu location. The fallback menu intentionally links to existing public organizational pages and to the new library; replace those with your staging/production pages as appropriate.
7. Add **Resources**, select formats/topics, add featured images, write accessible resource descriptions and set the public original-source URL. Only published resources appear publicly. Add **Programmes** for substantive programme pages. No sample research or content is inserted on activation.
8. Under **Settings → Invictus integrations**, configure a real HTTPS newsletter signup page, if available. Until configured, the footer offers a mailing-list enquiry email instead of pretending to subscribe visitors.
9. Configure the optional HTTPS Ask Invictus interface only after its backend is deployed and approved. It is loaded on visitor interaction, not automatically. Keep AI keys, SharePoint credentials and WhatsApp secrets on the chatbot server, never in WordPress settings or front-end JavaScript. Prefer a separate origin for the iframe; configure that server's CSP/frame-ancestors to permit only approved embedding origins. It needs its own operational/privacy review.

The theme is a classic/hybrid PHP theme with theme.json, block-editor styles, wide alignment, native custom-logo support and one reusable editorial statement pattern. General pages/posts and programme/resource pages use the native block editor. The default homepage is a composed PHP template with Customizer hero controls; its entire section layout is not a drag-and-drop full-site-editing canvas. A developer can extend the section templates; use normal WordPress pages for additional editorial layouts.

## Plugins

**Required for the resource-library functionality:** the supplied Invictus Core plugin. It keeps content types and taxonomies independent of presentation, including if the theme changes. Deactivation does not delete resource content. Theme-only activation still renders the homepage and normal WordPress content, with public-resource fallback links.

No premium plugin, ACF, slider library or page builder is required. Keep whichever existing SEO, backup, mail-delivery, security or caching tools are already appropriate for the site. Test current forms/embeds before changing their plugins. Configure a real newsletter provider rather than building another local database of subscriber email addresses. The chatbot itself and its WhatsApp connection are separate services, not bundled as a pretend working AI engine.

## Before production

- Review actual desktop, mobile and keyboard flows, approved copy, image rights, navigation and resource metadata.
- Audit existing WordPress post types and Elementor layouts; preserve shortcodes, contact forms, protected/member content and data-protection pages. This theme does not migrate Elementor's proprietary layout data automatically.
- Create an explicit old/new URL map and redirects where needed. Preserve analytics/SEO configuration, canonical URLs, titles, structured-data ownership and sitemap coverage through the site's existing SEO tooling. Do not install overlapping SEO plugins.
- Check production PHP/WordPress/plugin versions, multisite if applicable, actual CDN/cache configuration, image cropping, font rendering and accessibility with real content. Test resource PDFs, newsletter signup, analytics consent and chatbot embedding if enabled.
- Approve on staging, take a fresh backup, then deploy in a maintenance window. Keep the previous theme and database backup for rollback. No live deployment has been performed in this task.

## Local development review

A disposable local installation was validated using official WordPress PHP 8.3/Apache and MariaDB 11.4 containers. The isolated site used WordPress 7.1.3. Minimum declared versions are WordPress 6.6/PHP 8.1 but that entire version matrix has not been tested. Docker image digests are recorded in VALIDATION.md.

Current review container names are `ia-review-db` and `ia-review-wp`, connected by `ia-review`, bound only to loopback port 8088. Theme/plugin paths are read-only mounts from this project. Start existing review containers with `docker start ia-review-db ia-review-wp`. Docker processes and storage are not guaranteed to persist between cloud environments. A retained source ZIP is not a live staging deployment.

PHP integration fixtures in `tests/integration.php` and cleanup in `tests/cleanup.php` guard against execution outside the known local review URL. Never point them at a real site. The browser checks use Chromium/Playwright provided by this cloud image. Review data stays in `.runtime/` and Docker storage, and is excluded from every delivery ZIP. Do not publish local environment files or database backups.
