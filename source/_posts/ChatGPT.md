---
title: 用ChatGPT优化wordpress：他真的，我哭死
---
<!-- wp:heading {"level":1} -->
<h1 class="wp-block-heading"><strong>问题啊啊啊啊啊啊</strong></h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>请给我写一个wordpress插件，它可以为我的网站生成静态html进行访问，同时登录用户不会通过缓存访问，每隔一段时间删除旧的缓存</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1 class="wp-block-heading"><strong>Chat GPT的回答</strong></h1>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;?php
/*
Plugin Name: Static HTML Generator
Description: Generates static HTML for your website and deletes old cache periodically
Version: 1.0
Author: Your Name
*/

// Define constants for the plugin
define( 'STATIC_HTML_GENERATOR_CACHE_DIR', WP_CONTENT_DIR . '/cache/static-html-generator/' ); // Directory to store cache files
define( 'STATIC_HTML_GENERATOR_CACHE_TIME', 3600 ); // Cache time in seconds, default is 1 hour

// Register activation and deactivation hooks
register_activation_hook( __FILE__, 'static_html_generator_activate' );
register_deactivation_hook( __FILE__, 'static_html_generator_deactivate' );

// Activate the plugin
function static_html_generator_activate() {
// Create cache directory
if ( ! file_exists( STATIC_HTML_GENERATOR_CACHE_DIR ) ) {
wp_mkdir_p( STATIC_HTML_GENERATOR_CACHE_DIR );
}
}

// Deactivate the plugin
function static_html_generator_deactivate() {
// Remove cache directory and all its contents
static_html_generator_rrmdir( STATIC_HTML_GENERATOR_CACHE_DIR );
}

// Remove directory and all its contents recursively
function static_html_generator_rrmdir( $dir ) {
if ( is_dir( $dir ) ) {
$objects = scandir( $dir );
foreach ( $objects as $object ) {
if ( $object != '.' &amp;&amp; $object != '..' ) {
if ( is_dir( $dir . '/' . $object ) ) {
static_html_generator_rrmdir( $dir . '/' . $object );
} else {
unlink( $dir . '/' . $object );
}
}
}
rmdir( $dir );
}
}

// Generate static HTML for the current page
function static_html_generator_generate() {
// Check if user is logged in
if ( is_user_logged_in() ) {
return; // Do not generate static HTML for logged in users
}

// Generate cache file name
$cache_file = STATIC_HTML_GENERATOR_CACHE_DIR . md5( get_permalink() ) . '.html';

// Check if cache file exists and is not expired
if ( file_exists( $cache_file ) &amp;&amp; ( time() - filemtime( $cache_file ) ) &lt; STATIC_HTML_GENERATOR_CACHE_TIME ) {
// Serve cache file and exit
readfile( $cache_file );
exit();
}

// Start output buffering
ob_start();

// Generate HTML for the current page
get_header();
if ( have_posts() ) {
while ( have_posts() ) {
the_post();
the_content();
}
}
get_footer();

// Write output buffer to cache file
file_put_contents( $cache_file, ob_get_contents() );

// End output buffering
ob_end_flush();
}

// Hook into WordPress to generate static HTML
add_action( 'wp', 'static_html_generator_generate' );

// Schedule a daily event to delete old cache files
add_action( 'static_html_generator_delete_cache', 'static_html_generator_delete_cache' );
if ( ! wp_next_scheduled( 'static_html_generator_delete_cache' ) ) {
wp_schedule_event( time(), 'daily', 'static_html_generator_delete_cache' );
}

// Delete old cache files
function static_html_generator_delete_cache() {
$cache_files = glob( STATIC_HTML_GENERATOR_CACHE_DIR . '*.html' );
foreach ( $cache_files as $cache_file ) {
if ( filemtime( $cache_file ) &lt; ( time() - STATIC_HTML_GENERATOR_CACHE_TIME ) ) {
unlink( $cache_file );
}
}
}</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":1} -->
<h1 class="wp-block-heading">附语：</h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>这个插件的功能很简单，它会在用户访问您的网站时生成静态HTML，并将其缓存到本地文件中。如果用户已登录，则会跳过静态HTML生成，并直接访问动态页面。每隔一段时间，该插件会删除旧的缓存文件，以确保您的网站保持最新状态。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>比我自己写得好多了，不过需要根据主题调整。它真的，我哭死。</p>
<!-- /wp:paragraph -->
