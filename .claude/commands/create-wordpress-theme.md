# Create WordPress Theme

Generate a complete, production-ready WordPress theme with modern design, customizer integration, WooCommerce support, and optimization ready for ThemeForest or client delivery.

## Instructions

You are tasked with creating a COMPLETE, production-ready WordPress theme. This is a one-shot command that must produce a fully functional, polished theme ready for immediate deployment or marketplace submission.

### Step 1: Gather Requirements

First, ask the user these essential questions:
1. **Theme Purpose**: Blog, business, eCommerce, portfolio, or multipurpose?
2. **Design Style**: Modern, minimalist, elegant, corporate, or creative?
3. **Key Features**: What features are essential? (slider, mega menu, custom widgets)
4. **WooCommerce**: Does it need full eCommerce support?
5. **Page Builder**: Elementor compatible, Gutenberg-first, or custom?
6. **Target Audience**: Who will use this theme?

### Step 2: Complete Theme Structure

Create the following COMPLETE structure:

```
mytheme/
├── style.css
├── functions.php
├── index.php
├── header.php
├── footer.php
├── sidebar.php
├── single.php
├── page.php
├── archive.php
├── search.php
├── 404.php
├── comments.php
├── searchform.php
├── template-parts/
│   ├── content.php
│   ├── content-single.php
│   ├── content-page.php
│   ├── content-none.php
│   └── hero-section.php
├── templates/
│   ├── template-fullwidth.php
│   ├── template-homepage.php
│   ├── template-blog.php
│   └── template-landing.php
├── inc/
│   ├── theme-setup.php
│   ├── customizer.php
│   ├── custom-post-types.php
│   ├── widgets.php
│   ├── template-tags.php
│   ├── enqueue-scripts.php
│   └── woocommerce.php
├── assets/
│   ├── css/
│   │   ├── main.css
│   │   ├── responsive.css
│   │   └── woocommerce.css
│   ├── js/
│   │   ├── main.js
│   │   ├── navigation.js
│   │   └── customizer.js
│   └── images/
│       ├── logo.png
│       └── default-thumbnail.jpg
├── woocommerce/
│   ├── single-product.php
│   ├── archive-product.php
│   └── cart.php
├── languages/
│   ├── mytheme.pot
│   └── readme.txt
├── screenshot.png
└── README.md
```

### Step 3: Theme Configuration

```css
/*!
Theme Name: MyTheme
Theme URI: https://example.com/mytheme
Author: Your Name
Author URI: https://example.com
Description: A modern, responsive WordPress theme with WooCommerce support, customizer options, and professional design. Perfect for businesses, blogs, and online stores.
Version: 1.0.0
Requires at least: 5.8
Tested up to: 6.4
Requires PHP: 7.4
License: GNU General Public License v2 or later
License URI: LICENSE
Text Domain: mytheme
Tags: blog, e-commerce, custom-header, custom-logo, custom-menu, featured-images, footer-widgets, full-width-template, rtl-language-support, sticky-post, theme-options, threaded-comments, translation-ready, two-columns, right-sidebar
*/
```

```php
<?php
// functions.php

/**
 * Theme Setup
 */
function mytheme_setup() {
    // Make theme available for translation
    load_theme_textdomain('mytheme', get_template_directory() . '/languages');

    // Add default posts and comments RSS feed links to head
    add_theme_support('automatic-feed-links');

    // Let WordPress manage the document title
    add_theme_support('title-tag');

    // Enable support for Post Thumbnails
    add_theme_support('post-thumbnails');
    set_post_thumbnail_size(1200, 630, true);

    // Add custom image sizes
    add_image_size('mytheme-featured', 800, 450, true);
    add_image_size('mytheme-thumbnail', 400, 300, true);
    add_image_size('mytheme-hero', 1920, 800, true);

    // Register navigation menus
    register_nav_menus(array(
        'primary' => esc_html__('Primary Menu', 'mytheme'),
        'footer' => esc_html__('Footer Menu', 'mytheme'),
        'mobile' => esc_html__('Mobile Menu', 'mytheme'),
    ));

    // Switch default core markup to output valid HTML5
    add_theme_support('html5', array(
        'search-form',
        'comment-form',
        'comment-list',
        'gallery',
        'caption',
        'style',
        'script',
    ));

    // Add theme support for selective refresh for widgets
    add_theme_support('customize-selective-refresh-widgets');

    // Add support for custom logo
    add_theme_support('custom-logo', array(
        'height' => 100,
        'width' => 400,
        'flex-height' => true,
        'flex-width' => true,
    ));

    // Add support for custom header
    add_theme_support('custom-header', array(
        'default-image' => '',
        'width' => 1920,
        'height' => 500,
        'flex-height' => true,
        'flex-width' => true,
    ));

    // Add support for custom background
    add_theme_support('custom-background', array(
        'default-color' => 'ffffff',
    ));

    // Add support for Block Styles
    add_theme_support('wp-block-styles');

    // Add support for full and wide align images
    add_theme_support('align-wide');

    // Add support for editor styles
    add_theme_support('editor-styles');
    add_editor_style('assets/css/editor-style.css');

    // Add support for responsive embeds
    add_theme_support('responsive-embeds');

    // WooCommerce support
    add_theme_support('woocommerce');
    add_theme_support('wc-product-gallery-zoom');
    add_theme_support('wc-product-gallery-lightbox');
    add_theme_support('wc-product-gallery-slider');
}
add_action('after_setup_theme', 'mytheme_setup');

/**
 * Set the content width in pixels
 */
function mytheme_content_width() {
    $GLOBALS['content_width'] = apply_filters('mytheme_content_width', 1200);
}
add_action('after_setup_theme', 'mytheme_content_width', 0);

/**
 * Register widget areas
 */
function mytheme_widgets_init() {
    register_sidebar(array(
        'name' => esc_html__('Sidebar', 'mytheme'),
        'id' => 'sidebar-1',
        'description' => esc_html__('Add widgets here to appear in your sidebar.', 'mytheme'),
        'before_widget' => '<section id="%1$s" class="widget %2$s">',
        'after_widget' => '</section>',
        'before_title' => '<h2 class="widget-title">',
        'after_title' => '</h2>',
    ));

    register_sidebar(array(
        'name' => esc_html__('Footer 1', 'mytheme'),
        'id' => 'footer-1',
        'description' => esc_html__('Footer widget area 1', 'mytheme'),
        'before_widget' => '<div id="%1$s" class="widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>',
    ));

    register_sidebar(array(
        'name' => esc_html__('Footer 2', 'mytheme'),
        'id' => 'footer-2',
        'description' => esc_html__('Footer widget area 2', 'mytheme'),
        'before_widget' => '<div id="%1$s" class="widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>',
    ));

    register_sidebar(array(
        'name' => esc_html__('Footer 3', 'mytheme'),
        'id' => 'footer-3',
        'description' => esc_html__('Footer widget area 3', 'mytheme'),
        'before_widget' => '<div id="%1$s" class="widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>',
    ));

    register_sidebar(array(
        'name' => esc_html__('Footer 4', 'mytheme'),
        'id' => 'footer-4',
        'description' => esc_html__('Footer widget area 4', 'mytheme'),
        'before_widget' => '<div id="%1$s" class="widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>',
    ));
}
add_action('widgets_init', 'mytheme_widgets_init');

/**
 * Enqueue scripts and styles
 */
function mytheme_scripts() {
    // Stylesheet
    wp_enqueue_style('mytheme-style', get_stylesheet_uri(), array(), '1.0.0');
    wp_enqueue_style('mytheme-main', get_template_directory_uri() . '/assets/css/main.css', array(), '1.0.0');
    wp_enqueue_style('mytheme-responsive', get_template_directory_uri() . '/assets/css/responsive.css', array(), '1.0.0');

    // Google Fonts
    wp_enqueue_style('mytheme-fonts', 'https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap', array(), null);

    // JavaScript
    wp_enqueue_script('mytheme-navigation', get_template_directory_uri() . '/assets/js/navigation.js', array('jquery'), '1.0.0', true);
    wp_enqueue_script('mytheme-main', get_template_directory_uri() . '/assets/js/main.js', array('jquery'), '1.0.0', true);

    // Comment reply script
    if (is_singular() && comments_open() && get_option('thread_comments')) {
        wp_enqueue_script('comment-reply');
    }

    // Localize script
    wp_localize_script('mytheme-main', 'mythemeData', array(
        'ajax_url' => admin_url('admin-ajax.php'),
        'nonce' => wp_create_nonce('mytheme-nonce'),
    ));
}
add_action('wp_enqueue_scripts', 'mytheme_scripts');

// Include additional theme files
require get_template_directory() . '/inc/theme-setup.php';
require get_template_directory() . '/inc/customizer.php';
require get_template_directory() . '/inc/custom-post-types.php';
require get_template_directory() . '/inc/widgets.php';
require get_template_directory() . '/inc/template-tags.php';

// WooCommerce support
if (class_exists('WooCommerce')) {
    require get_template_directory() . '/inc/woocommerce.php';
}
```

### Step 4: Header Template

```php
<?php
// header.php
?>
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo('charset'); ?>">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="profile" href="https://gmpg.org/xfn/11">
    <?php wp_head(); ?>
</head>

<body <?php body_class(); ?>>
<?php wp_body_open(); ?>

<div id="page" class="site">
    <a class="skip-link screen-reader-text" href="#primary">
        <?php esc_html_e('Skip to content', 'mytheme'); ?>
    </a>

    <!-- Header -->
    <header id="masthead" class="site-header">
        <!-- Top Bar -->
        <div class="header-top">
            <div class="container">
                <div class="header-top-content">
                    <div class="header-info">
                        <?php
                        $email = get_theme_mod('mytheme_contact_email');
                        $phone = get_theme_mod('mytheme_contact_phone');

                        if ($email) : ?>
                            <span class="header-email">
                                <i class="icon-envelope"></i>
                                <a href="mailto:<?php echo esc_attr($email); ?>">
                                    <?php echo esc_html($email); ?>
                                </a>
                            </span>
                        <?php endif;

                        if ($phone) : ?>
                            <span class="header-phone">
                                <i class="icon-phone"></i>
                                <a href="tel:<?php echo esc_attr($phone); ?>">
                                    <?php echo esc_html($phone); ?>
                                </a>
                            </span>
                        <?php endif; ?>
                    </div>

                    <div class="header-social">
                        <?php mytheme_social_links(); ?>
                    </div>
                </div>
            </div>
        </div>

        <!-- Main Header -->
        <div class="header-main">
            <div class="container">
                <div class="header-content">
                    <!-- Logo -->
                    <div class="site-branding">
                        <?php
                        if (has_custom_logo()) {
                            the_custom_logo();
                        } else { ?>
                            <h1 class="site-title">
                                <a href="<?php echo esc_url(home_url('/')); ?>">
                                    <?php bloginfo('name'); ?>
                                </a>
                            </h1>
                            <?php
                            $description = get_bloginfo('description', 'display');
                            if ($description || is_customize_preview()) : ?>
                                <p class="site-description">
                                    <?php echo $description; ?>
                                </p>
                            <?php endif;
                        } ?>
                    </div>

                    <!-- Navigation -->
                    <nav id="site-navigation" class="main-navigation">
                        <?php
                        wp_nav_menu(array(
                            'theme_location' => 'primary',
                            'menu_id' => 'primary-menu',
                            'container_class' => 'menu-container',
                            'fallback_cb' => 'mytheme_fallback_menu',
                        ));
                        ?>
                    </nav>

                    <!-- Header Actions -->
                    <div class="header-actions">
                        <!-- Search -->
                        <button class="search-toggle" aria-label="<?php esc_attr_e('Search', 'mytheme'); ?>">
                            <i class="icon-search"></i>
                        </button>

                        <?php if (class_exists('WooCommerce')) : ?>
                            <!-- Cart -->
                            <a class="cart-toggle" href="<?php echo esc_url(wc_get_cart_url()); ?>">
                                <i class="icon-cart"></i>
                                <span class="cart-count">
                                    <?php echo WC()->cart->get_cart_contents_count(); ?>
                                </span>
                            </a>
                        <?php endif; ?>

                        <!-- Mobile Toggle -->
                        <button class="mobile-toggle" aria-label="<?php esc_attr_e('Menu', 'mytheme'); ?>">
                            <span></span>
                            <span></span>
                            <span></span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Search Form -->
        <div class="header-search">
            <div class="container">
                <?php get_search_form(); ?>
                <button class="search-close">×</button>
            </div>
        </div>
    </header>

    <!-- Mobile Menu -->
    <div class="mobile-menu">
        <div class="mobile-menu-content">
            <?php
            wp_nav_menu(array(
                'theme_location' => 'mobile',
                'menu_id' => 'mobile-menu',
                'fallback_cb' => 'mytheme_fallback_menu',
            ));
            ?>
        </div>
    </div>

    <div id="content" class="site-content">
```

### Step 5: Customizer Integration

```php
<?php
// inc/customizer.php

/**
 * Customizer Settings
 */
function mytheme_customize_register($wp_customize) {
    // Remove default sections (optional)
    // $wp_customize->remove_section('colors');

    /**
     * General Settings
     */
    $wp_customize->add_section('mytheme_general', array(
        'title' => __('General Settings', 'mytheme'),
        'priority' => 30,
    ));

    // Logo Width
    $wp_customize->add_setting('mytheme_logo_width', array(
        'default' => 200,
        'transport' => 'refresh',
        'sanitize_callback' => 'absint',
    ));

    $wp_customize->add_control('mytheme_logo_width', array(
        'label' => __('Logo Width (px)', 'mytheme'),
        'section' => 'mytheme_general',
        'type' => 'number',
        'input_attrs' => array(
            'min' => 50,
            'max' => 500,
            'step' => 10,
        ),
    ));

    /**
     * Header Settings
     */
    $wp_customize->add_section('mytheme_header', array(
        'title' => __('Header Settings', 'mytheme'),
        'priority' => 40,
    ));

    // Sticky Header
    $wp_customize->add_setting('mytheme_sticky_header', array(
        'default' => true,
        'transport' => 'refresh',
        'sanitize_callback' => 'mytheme_sanitize_checkbox',
    ));

    $wp_customize->add_control('mytheme_sticky_header', array(
        'label' => __('Enable Sticky Header', 'mytheme'),
        'section' => 'mytheme_header',
        'type' => 'checkbox',
    ));

    // Contact Email
    $wp_customize->add_setting('mytheme_contact_email', array(
        'default' => '',
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_email',
    ));

    $wp_customize->add_control('mytheme_contact_email', array(
        'label' => __('Contact Email', 'mytheme'),
        'section' => 'mytheme_header',
        'type' => 'email',
    ));

    // Contact Phone
    $wp_customize->add_setting('mytheme_contact_phone', array(
        'default' => '',
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_text_field',
    ));

    $wp_customize->add_control('mytheme_contact_phone', array(
        'label' => __('Contact Phone', 'mytheme'),
        'section' => 'mytheme_header',
        'type' => 'text',
    ));

    /**
     * Homepage Settings
     */
    $wp_customize->add_section('mytheme_homepage', array(
        'title' => __('Homepage Settings', 'mytheme'),
        'priority' => 50,
    ));

    // Hero Heading
    $wp_customize->add_setting('mytheme_hero_heading', array(
        'default' => __('Welcome to Our Website', 'mytheme'),
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_text_field',
    ));

    $wp_customize->add_control('mytheme_hero_heading', array(
        'label' => __('Hero Heading', 'mytheme'),
        'section' => 'mytheme_homepage',
        'type' => 'text',
    ));

    // Hero Subheading
    $wp_customize->add_setting('mytheme_hero_subheading', array(
        'default' => __('Build something amazing', 'mytheme'),
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_textarea_field',
    ));

    $wp_customize->add_control('mytheme_hero_subheading', array(
        'label' => __('Hero Subheading', 'mytheme'),
        'section' => 'mytheme_homepage',
        'type' => 'textarea',
    ));

    // Hero Button Text
    $wp_customize->add_setting('mytheme_hero_button_text', array(
        'default' => __('Get Started', 'mytheme'),
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_text_field',
    ));

    $wp_customize->add_control('mytheme_hero_button_text', array(
        'label' => __('Hero Button Text', 'mytheme'),
        'section' => 'mytheme_homepage',
        'type' => 'text',
    ));

    // Hero Button URL
    $wp_customize->add_setting('mytheme_hero_button_url', array(
        'default' => '#',
        'transport' => 'refresh',
        'sanitize_callback' => 'esc_url_raw',
    ));

    $wp_customize->add_control('mytheme_hero_button_url', array(
        'label' => __('Hero Button URL', 'mytheme'),
        'section' => 'mytheme_homepage',
        'type' => 'url',
    ));

    /**
     * Colors
     */
    $wp_customize->add_section('mytheme_colors', array(
        'title' => __('Theme Colors', 'mytheme'),
        'priority' => 60,
    ));

    // Primary Color
    $wp_customize->add_setting('mytheme_primary_color', array(
        'default' => '#007bff',
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_hex_color',
    ));

    $wp_customize->add_control(new WP_Customize_Color_Control($wp_customize, 'mytheme_primary_color', array(
        'label' => __('Primary Color', 'mytheme'),
        'section' => 'mytheme_colors',
    )));

    // Secondary Color
    $wp_customize->add_setting('mytheme_secondary_color', array(
        'default' => '#6c757d',
        'transport' => 'refresh',
        'sanitize_callback' => 'sanitize_hex_color',
    ));

    $wp_customize->add_control(new WP_Customize_Color_Control($wp_customize, 'mytheme_secondary_color', array(
        'label' => __('Secondary Color', 'mytheme'),
        'section' => 'mytheme_colors',
    )));

    /**
     * Social Links
     */
    $wp_customize->add_section('mytheme_social', array(
        'title' => __('Social Links', 'mytheme'),
        'priority' => 70,
    ));

    $social_networks = array(
        'facebook' => 'Facebook',
        'twitter' => 'Twitter',
        'instagram' => 'Instagram',
        'linkedin' => 'LinkedIn',
        'youtube' => 'YouTube',
    );

    foreach ($social_networks as $network => $label) {
        $wp_customize->add_setting('mytheme_social_' . $network, array(
            'default' => '',
            'transport' => 'refresh',
            'sanitize_callback' => 'esc_url_raw',
        ));

        $wp_customize->add_control('mytheme_social_' . $network, array(
            'label' => $label . ' ' . __('URL', 'mytheme'),
            'section' => 'mytheme_social',
            'type' => 'url',
        ));
    }

    /**
     * Footer Settings
     */
    $wp_customize->add_section('mytheme_footer', array(
        'title' => __('Footer Settings', 'mytheme'),
        'priority' => 80,
    ));

    // Copyright Text
    $wp_customize->add_setting('mytheme_copyright_text', array(
        'default' => sprintf(__('© %d %s. All rights reserved.', 'mytheme'), date('Y'), get_bloginfo('name')),
        'transport' => 'refresh',
        'sanitize_callback' => 'wp_kses_post',
    ));

    $wp_customize->add_control('mytheme_copyright_text', array(
        'label' => __('Copyright Text', 'mytheme'),
        'section' => 'mytheme_footer',
        'type' => 'textarea',
    ));
}
add_action('customize_register', 'mytheme_customize_register');

/**
 * Sanitization Functions
 */
function mytheme_sanitize_checkbox($checked) {
    return ((isset($checked) && true == $checked) ? true : false);
}

/**
 * Output custom CSS to live site
 */
function mytheme_customizer_css() {
    $primary_color = get_theme_mod('mytheme_primary_color', '#007bff');
    $secondary_color = get_theme_mod('mytheme_secondary_color', '#6c757d');
    $logo_width = get_theme_mod('mytheme_logo_width', 200);

    ?>
    <style type="text/css">
        :root {
            --primary-color: <?php echo esc_attr($primary_color); ?>;
            --secondary-color: <?php echo esc_attr($secondary_color); ?>;
        }

        .custom-logo {
            max-width: <?php echo esc_attr($logo_width); ?>px;
        }

        .btn-primary,
        .button,
        button[type="submit"] {
            background-color: var(--primary-color);
        }

        .btn-primary:hover,
        .button:hover,
        button[type="submit"]:hover {
            background-color: var(--secondary-color);
        }

        a {
            color: var(--primary-color);
        }

        a:hover {
            color: var(--secondary-color);
        }
    </style>
    <?php
}
add_action('wp_head', 'mytheme_customizer_css');
```

### Step 6: WooCommerce Integration

```php
<?php
// inc/woocommerce.php

/**
 * WooCommerce Customization
 */

// Remove default WooCommerce wrappers
remove_action('woocommerce_before_main_content', 'woocommerce_output_content_wrapper', 10);
remove_action('woocommerce_after_main_content', 'woocommerce_output_content_wrapper_end', 10);

// Add custom wrappers
add_action('woocommerce_before_main_content', 'mytheme_wrapper_start', 10);
add_action('woocommerce_after_main_content', 'mytheme_wrapper_end', 10);

function mytheme_wrapper_start() {
    echo '<div id="primary" class="content-area woocommerce-page">';
    echo '<main id="main" class="site-main">';
}

function mytheme_wrapper_end() {
    echo '</main>';
    echo '</div>';
}

// Change number of products per row
add_filter('loop_shop_columns', 'mytheme_loop_columns');
function mytheme_loop_columns() {
    return 3; // 3 products per row
}

// Change number of products per page
add_filter('loop_shop_per_page', 'mytheme_products_per_page');
function mytheme_products_per_page() {
    return 12;
}

// Add cart icon to header
add_filter('woocommerce_add_to_cart_fragments', 'mytheme_cart_count_fragments', 10, 1);
function mytheme_cart_count_fragments($fragments) {
    ob_start();
    ?>
    <span class="cart-count"><?php echo WC()->cart->get_cart_contents_count(); ?></span>
    <?php
    $fragments['.cart-count'] = ob_get_clean();
    return $fragments;
}

// Customize Add to Cart button text
add_filter('woocommerce_product_single_add_to_cart_text', 'mytheme_custom_add_to_cart_text');
add_filter('woocommerce_product_add_to_cart_text', 'mytheme_custom_add_to_cart_text');
function mytheme_custom_add_to_cart_text() {
    return __('Add to Bag', 'mytheme');
}

// Remove breadcrumbs
remove_action('woocommerce_before_main_content', 'woocommerce_breadcrumb', 20);

// Add breadcrumbs in custom location
add_action('woocommerce_before_shop_loop', 'woocommerce_breadcrumb', 10);

// Declare WooCommerce support
function mytheme_woocommerce_setup() {
    add_theme_support('woocommerce', array(
        'thumbnail_image_width' => 300,
        'single_image_width' => 600,
        'product_grid' => array(
            'default_rows' => 4,
            'min_rows' => 2,
            'max_rows' => 8,
            'default_columns' => 3,
            'min_columns' => 2,
            'max_columns' => 5,
        ),
    ));
}
add_action('after_setup_theme', 'mytheme_woocommerce_setup');
```

### Step 7: Template Tags

```php
<?php
// inc/template-tags.php

/**
 * Custom template tags for this theme
 */

/**
 * Display social media links
 */
function mytheme_social_links() {
    $social_networks = array(
        'facebook' => array('label' => 'Facebook', 'icon' => 'icon-facebook'),
        'twitter' => array('label' => 'Twitter', 'icon' => 'icon-twitter'),
        'instagram' => array('label' => 'Instagram', 'icon' => 'icon-instagram'),
        'linkedin' => array('label' => 'LinkedIn', 'icon' => 'icon-linkedin'),
        'youtube' => array('label' => 'YouTube', 'icon' => 'icon-youtube'),
    );

    echo '<div class="social-links">';
    foreach ($social_networks as $network => $data) {
        $url = get_theme_mod('mytheme_social_' . $network);
        if ($url) {
            printf(
                '<a href="%s" class="social-link social-%s" target="_blank" rel="noopener" aria-label="%s">
                    <i class="%s"></i>
                </a>',
                esc_url($url),
                esc_attr($network),
                esc_attr($data['label']),
                esc_attr($data['icon'])
            );
        }
    }
    echo '</div>';
}

/**
 * Display post meta information
 */
function mytheme_post_meta() {
    $time_string = '<time class="entry-date published updated" datetime="%1$s">%2$s</time>';
    if (get_the_time('U') !== get_the_modified_time('U')) {
        $time_string = '<time class="entry-date published" datetime="%1$s">%2$s</time><time class="updated" datetime="%3$s">%4$s</time>';
    }

    $time_string = sprintf(
        $time_string,
        esc_attr(get_the_date(DATE_W3C)),
        esc_html(get_the_date()),
        esc_attr(get_the_modified_date(DATE_W3C)),
        esc_html(get_the_modified_date())
    );

    echo '<div class="entry-meta">';

    // Posted by
    printf(
        '<span class="byline">%s <a href="%s" class="url fn n">%s</a></span>',
        esc_html__('by', 'mytheme'),
        esc_url(get_author_posts_url(get_the_author_meta('ID'))),
        esc_html(get_the_author())
    );

    // Posted on
    printf(
        '<span class="posted-on">%s %s</span>',
        esc_html__('on', 'mytheme'),
        '<a href="' . esc_url(get_permalink()) . '" rel="bookmark">' . $time_string . '</a>'
    );

    // Categories
    $categories_list = get_the_category_list(esc_html__(', ', 'mytheme'));
    if ($categories_list) {
        printf(
            '<span class="cat-links">%s %s</span>',
            esc_html__('in', 'mytheme'),
            $categories_list
        );
    }

    // Comments
    if (! is_single() && ! post_password_required() && (comments_open() || get_comments_number())) {
        echo '<span class="comments-link">';
        comments_popup_link(
            sprintf(
                wp_kses(
                    __('Leave a Comment<span class="screen-reader-text"> on %s</span>', 'mytheme'),
                    array('span' => array('class' => array()))
                ),
                wp_kses_post(get_the_title())
            )
        );
        echo '</span>';
    }

    echo '</div>';
}

/**
 * Display breadcrumbs
 */
function mytheme_breadcrumbs() {
    if (is_front_page()) return;

    echo '<nav class="breadcrumbs">';
    echo '<a href="' . esc_url(home_url('/')) . '">' . esc_html__('Home', 'mytheme') . '</a>';

    if (is_category() || is_single()) {
        echo ' / ';
        the_category(' / ');
        if (is_single()) {
            echo ' / ' . get_the_title();
        }
    } elseif (is_page()) {
        echo ' / ' . get_the_title();
    } elseif (is_search()) {
        echo ' / ' . esc_html__('Search Results', 'mytheme');
    } elseif (is_404()) {
        echo ' / ' . esc_html__('404 Not Found', 'mytheme');
    }

    echo '</nav>';
}

/**
 * Display reading time
 */
function mytheme_reading_time() {
    $content = get_post_field('post_content', get_the_ID());
    $word_count = str_word_count(strip_tags($content));
    $reading_time = ceil($word_count / 200);

    printf(
        '<span class="reading-time">%d %s</span>',
        $reading_time,
        esc_html__('min read', 'mytheme')
    );
}
```

### Step 8: Performance Optimization

```php
<?php
// Add to functions.php

/**
 * Performance Optimizations
 */

// Remove WordPress version from head
remove_action('wp_head', 'wp_generator');

// Remove WP emoji
remove_action('wp_head', 'print_emoji_detection_script', 7);
remove_action('wp_print_styles', 'print_emoji_styles');

// Disable embeds
function mytheme_disable_embeds() {
    wp_dequeue_script('wp-embed');
}
add_action('wp_footer', 'mytheme_disable_embeds');

// Lazy load images
function mytheme_add_lazy_load($content) {
    $content = str_replace('<img', '<img loading="lazy"', $content);
    return $content;
}
add_filter('the_content', 'mytheme_add_lazy_load');

// Optimize query
function mytheme_optimize_query($query) {
    if (!is_admin() && $query->is_main_query()) {
        if (is_home() || is_archive()) {
            $query->set('posts_per_page', 12);
        }
    }
}
add_action('pre_get_posts', 'mytheme_optimize_query');

// Enable Gzip compression
add_filter('mod_rewrite_rules', 'mytheme_add_gzip');
function mytheme_add_gzip($rules) {
    $gzip = <<<EOT
# Gzip compression
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript
</IfModule>
EOT;
    return $gzip . $rules;
}

// Defer JavaScript
function mytheme_defer_scripts($tag, $handle, $src) {
    if (is_admin()) return $tag;

    $defer_scripts = array('mytheme-main', 'mytheme-navigation');

    if (in_array($handle, $defer_scripts)) {
        return str_replace(' src', ' defer src', $tag);
    }

    return $tag;
}
add_filter('script_loader_tag', 'mytheme_defer_scripts', 10, 3);

// Preload critical assets
function mytheme_preload_assets() {
    echo '<link rel="preconnect" href="https://fonts.googleapis.com">';
    echo '<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>';
}
add_action('wp_head', 'mytheme_preload_assets', 1);
```

### Step 9: Documentation

```markdown
# Theme Documentation

## Installation

1. Download the theme ZIP file
2. Go to WordPress Admin → Appearance → Themes
3. Click "Add New" → "Upload Theme"
4. Choose the ZIP file and click "Install Now"
5. Click "Activate" to activate the theme

## Customization

### Via Customizer
Go to Appearance → Customize to access:
- Site Identity (logo, site icon)
- Colors
- Menus
- Widgets
- Homepage Settings
- Additional Settings

### Menus
1. Go to Appearance → Menus
2. Create a new menu
3. Assign it to "Primary Menu" location
4. Add pages, posts, custom links

### Widgets
1. Go to Appearance → Widgets
2. Drag widgets to:
   - Sidebar
   - Footer 1-4

## Page Templates

### Homepage Template
Select "Template: Homepage" when editing a page.

### Full Width Template
Select "Template: Full Width" for pages without sidebar.

### Blog Template
Select "Template: Blog" for custom blog page.

## WooCommerce

Theme includes full WooCommerce support:
- Custom product layouts
- Cart icon in header
- Optimized checkout
- Mobile-responsive design

## Child Theme

To create a child theme:
```php
// In child theme style.css
/*
Template: mytheme
*/

// In child theme functions.php
<?php
add_action('wp_enqueue_scripts', 'child_enqueue_styles');
function child_enqueue_styles() {
    wp_enqueue_style('parent-style', get_template_directory_uri() . '/style.css');
}
```

## Support

For support, please contact: support@yourtheme.com

## Changelog

### Version 1.0.0
- Initial release
```

### Success Criteria

The command is successful when you deliver:
✅ Complete WordPress theme
✅ Customizer integration with 20+ options
✅ WooCommerce full support
✅ Multiple page templates
✅ Widget areas
✅ Custom menus
✅ Responsive design
✅ SEO optimized
✅ Performance optimized
✅ Translation ready
✅ Complete documentation

This should be a COMPLETE, PRODUCTION-READY WordPress theme ready for client delivery or ThemeForest submission.
