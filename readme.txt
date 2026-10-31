=== Codeally Media Sanitizer ===
Contributors: oldrup
Tags: webp, filename, image-upload
Requires at least: 6.9
Tested up to: 7.1
Requires PHP: 8.2
Stable tag: 1.2.3
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Adds WebP upload handling and filename cleanup for WordPress's Modern Image Formats plugin.

== Description ==
This plugin requires the official [Modern Image Formats](https://wordpress.org/plugins/webp-uploads/) plugin. In **Settings > Media**, set its target image format to **WebP**. This plugin is configured for WebP; it does not support or optimize AVIF.

Codeally Media Sanitizer adjusts WordPress media uploads when Modern Image Formats is active and configured for WebP. It:

* Sets WordPress's WebP image-editor quality value to 70 when WebP images are generated.
* Cleans filenames on uploads and sideloads, including transliteration of Danish letters and many other characters. It preserves the original filename as the Media Library title.
* Deletes the unscaled original when WordPress generates a scaled image and records the original in attachment metadata. With WordPress's default big-image threshold, this generally applies when either image dimension exceeds 2560 pixels. The original file is deleted, so retain backups if you need it.
* Updates the attachment's MIME type to `image/webp` when its attached file has a `.webp` extension.

The plugin does not convert images by itself, scan or convert existing Media Library items, or perform bulk optimization. Its changes apply to uploads handled after activation. Existing images are unaffected unless you separately run a suitable image regeneration or migration workflow.

Developed by [Bjarne Oldrup](https://oldrup.dk/) and sponsored by [Codeally](https://codeally.dk/).
Filename sanitization character mapping adapted and expanded from [Clean Image Filenames](https://wordpress.org/plugins/clean-image-filenames/).

== Frequently Asked Questions ==

=== How do I set up and configure the plugin? ===
1. Install and activate the official [Modern Image Formats](https://wordpress.org/plugins/webp-uploads/) plugin.
2. Go to **Settings > Media** and select **WebP** as the target format. Modern Image Formats may default to AVIF, which this plugin does not support.
3. Install and activate Codeally Media Sanitizer.
4. Upload images through WordPress. The plugin applies its filename, WebP quality, original-file cleanup, and MIME-type behavior as described above.

=== Can I use this plugin to convert existing media to WebP? ===
No. The plugin does not process existing media or include a bulk converter. A separate regeneration or migration workflow may regenerate image sizes with Modern Image Formats active, but the result depends on that plugin's settings and does not automatically update image URLs embedded in post content. Back up the site and understand the fallback-image behavior before regenerating media.

=== How does this work together with thumbnail regeneration plugins? ===
Regeneration behavior depends on Modern Image Formats settings and the regeneration tool. If fallback images are disabled, regenerated JPEG sub-sizes may be removed and existing content that links directly to those files may break. Keeping fallback images can preserve those JPEG files. This plugin does not rewrite URLs in posts.

=== How does this plugin work with form plugins like WS Form? ===
Filename sanitization is applied through WordPress's upload and sideload filters. Form plugins may handle files differently, so behavior can depend on how a particular plugin passes files through WordPress. Compatibility with form plugins is not guaranteed.

=== Where can I find official documentation and references? ===
- [WordPress Performance Team: Modern Image Formats Plugin](https://wordpress.org/plugins/webp-uploads/)
- [WordPress Developer Reference: wp_handle_upload_prefilter](https://developer.wordpress.org/reference/hooks/wp_handle_upload_prefilter/)
- [WordPress Core Notes: Handling of Big Images in WP 5.3+](https://make.wordpress.org/core/2019/10/09/introducing-handling-of-big-images-in-wordpress-5-3/)

== Installation ==
1. Install and activate the [Modern Image Formats](https://wordpress.org/plugins/webp-uploads/) plugin.
2. In **Settings > Media**, select **WebP** as the target format.
3. Upload the Codeally Media Sanitizer plugin to your WordPress `/wp-content/plugins/` directory.
4. Activate it through the WordPress admin.

== Changelog ==
= 1.2.3 =
- First public release

== Screenshots ==
1. screenshot-1.png: Standard JPEG format, default quality 82, original file kept, total 4700 KB.
2. screenshot-2.png: Modern Image Formats enabled, WebP quality 82, original kept, total 4000 KB.
3. screenshot-3.png: Codeally Media Sanitizer enabled, WebP quality 70, original purged, total 300 KB.
4. screenshot-4.png: Applied settings under Settings > Media: WebP without fallback JPEG output.