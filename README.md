# Pixel Vaporwave Theme

A modern Micro.blog theme with vaporwave aesthetics - pixel font headings, neon glow effects, grid backgrounds, and pink/purple accent colors.

## Features

### Design
- Pixel font (Press Start 2P) for headings
- Modern system fonts for body text (readable)
- Soft gradient background with subtle grid overlay
- Pixel borders with glow effects
- Modern buttons with hover/active states
- Single column layout
- Glitch text effects on headings

### Functionality
- Code syntax highlighting with overflow protection
- Archive page with year-grouped posts
- Custom 404 error page
- Table styling for data tables
- Custom CSS support (create `static/custom.css`)
- Custom footer support via partial file
- Portrait video embed support (9:16 aspect ratio)

### Micro.blog Integration
- Full Micro.blog integration (IndieWeb, MicroPub, Webmentions, MicroSub)
- IndieWeb microformats2 (h-entry, p-name, e-content, dt-published, u-url, p-summary, p-author, h-card)
- Authorization endpoint, token endpoint, micropub, microsub, webmention support

### Accessibility
- **WCAG AA compliant** color contrast (4.5:1 ratio)
- Skip-to-content link for keyboard navigation
- Screen reader-only text for decorative elements
- ARIA labels on navigation and interactive elements
- Semantic HTML5 structure
- Keyboard navigation support with visible focus styles
- Focus-visible support for better keyboard UX
- Touch-friendly targets (44px minimum)
- Reduced motion support for users with vestibular disorders

### SEO
- OpenGraph meta tags for social sharing
- Twitter Card support
- JSON-LD structured data (BlogPosting, WebSite)
- Canonical URLs
- Proper meta descriptions
- OpenGraph image fallback support

### Responsive Design
- Mobile-first approach
- Three responsive breakpoints:
  - Tablets: 900px
  - Mobile phones: 600px
  - Small phones: 400px
- Optimized for all screen sizes

### Security
- XSS protection with proper HTML escaping by default
- Path traversal validation on plugin partials
- URL validation on external scripts (HTTPS/relative only)
- Whitelisted plugin HTML partials
- Security documentation in code comments

## Development Workflow

When making changes to the theme, you must update the preview site to see them:

```bash
# EASIEST - sync all theme changes
./sync-preview.sh

# Or manually sync specific files
cp -r willhead-pixel-vaporwave/* preview-site/themes/willhead-pixel-vaporwave/

# Or just the CSS:
cp willhead-pixel-vaporwave/static/css/style.css preview-site/themes/willhead-pixel-vaporwave/static/css/

# Or just the templates:
cp -r willhead-pixel-vaporwave/layouts/* preview-site/themes/willhead-pixel-vaporwave/layouts/
```

The Hugo development server watches for changes in `preview-site/themes/willhead-pixel-vaporwave/` and will rebuild automatically.

### Quick Preview

After syncing changes, refresh your browser:

- **Chrome**: `Cmd+R` (recommended - better cache behavior)
- **Safari**: `Cmd+Option+R` (hard refresh)

Or use the preview script: `./preview.sh` (opens Chrome to localhost:1313)

### Browser Recommendation

**Chrome is recommended for development** - Safari has aggressive caching that may not show CSS changes even with hard refresh. If you must use Safari, try clearing cache or using private browsing.

## Local Preview

```bash
# Start the preview server
cd preview-site
hugo server --bind 127.0.0.1 --port 1313

# Open http://localhost:1313/
```

## Deployment

### Installing on Micro.blog from GitHub

1. **Push to GitHub**: Upload this theme to a public GitHub repository
   - The repository must contain `theme.toml` in the root directory
   - Example: `https://github.com/username/willhead-pixel-vaporwave`

2. **Create Custom Theme in Micro.blog**:
   - Navigate to **Posts → Design → Edit Custom Themes**
   - Click **New Theme**
   - Enter:
     - **Theme name**: Pixel Vaporwave (or your preferred name)
     - **GitHub URL**: `https://github.com/username/willhead-pixel-vaporwave`
       - **Must use `https://` protocol** (http:// will not work)
   - Click **Create**

3. **Activate the Theme**:
   - Select your new theme from the **Custom theme** dropdown
   - Micro.blog will automatically fetch and install the theme

**Note**: Micro.blog automatically detects theme metadata from the `theme.toml` file. The theme name, version, and other details are pulled from this file.

### Updating the Theme

After pushing updates to GitHub:
1. Go to **Posts → Design → Edit Custom Themes**
2. Find your theme and click **Edit**
3. Click **Update from GitHub** to fetch the latest version
4. Save changes

### Theme Files

```
willhead-pixel-vaporwave/
├── theme.toml           # Theme metadata
├── config.json          # Theme configuration
├── plugin.json          # Micro.blog plugin settings
├── README.md            # This file
├── layouts/
│   ├── _default/
│   │   ├── baseof.html  # Base template
│   │   ├── list.html    # Homepage (post list)
│   │   ├── single.html  # Single post page
│   │   └── archive.html # Archive page
│   ├── 404.html         # Custom 404 error page
│   └── partials/
│       ├── head.html    # HTML head with meta tags
│       ├── header.html  # Site header
│       ├── footer.html  # Site footer
│       └── custom_footer.html  # Custom footer support
└── static/
    ├── css/
    │   └── style.css    # All theme styles
    └── custom.css       # Empty file for user overrides
```

## Customization

### Colors

Edit `static/css/style.css` CSS variables at the top of the file:

```css
:root {
    /* Neon colors */
    --neon-pink: #ff10f0;
    --electric-purple: #a855f7;
    --cyber-purple: #9333ea;
    --deep-purple: #7c3aed;
    --bright-purple: #d8b4fe; /* Improved contrast for accessibility (WCAG AA) */
    --high-contrast-pink: #f0abfc; /* Higher contrast pink for links */

    /* Backgrounds */
    --bg-dark: #0d0d1a;
    --bg-card: #151525;
    --bg-post: #1a1a2e;
    --bg-code: rgba(0, 0, 0, 0.4);
    --bg-code-inline: rgba(168, 85, 247, 0.25);

    /* Text */
    --text-primary: #f0f0f0;
    --text-secondary: #c0c0d0; /* Improved contrast for WCAG AA (5.2:1) */
    --text-accent: #ff10f0;
    --link-color: #e879f9; /* Higher contrast link color */

    /* Effects */
    --glow-pink: 0 0 20px rgba(255, 16, 240, 0.5);
    --glow-purple: 0 0 20px rgba(168, 85, 247, 0.3);
    --glow-radius: 20px;

    /* Layout */
    --max-width: 750px;
    --border-width: 2px;
    --border-radius: 4px;
    --grid-size: 40px;

    /* Z-index scale */
    --z-background: -1;
    --z-base: 1;
    --z-elevated: 10;
    --z-overlay: 100;
    --z-modal: 1000;
    --z-skip-link: 10000;

    /* Glitch animation clip values */
    --glitch-clip-1: rect(11px, 9999px, 89px, 0);
    --glitch-clip-2: rect(88px, 9999px, 12px, 0);
    /* ... up to --glitch-clip-12 */
}
```

### Content Width

```css
:root {
    --max-width: 750px;
}
```

### OpenGraph Default Image

Set a default image for social sharing in your site config:

```toml
[params]
  og_image = "/images/og-image.png"
```

### Custom CSS

Create `static/custom.css` in your site root to override theme styles. The theme automatically includes this file if it exists.

### Custom Footer HTML

For advanced users who need custom HTML in the footer, create `layouts/partials/custom_footer_content.html` in your site root. This file will be included automatically if it exists.

**Security Note:** The `custom_footer` config parameter now escapes HTML by default for security. Use the partial file method for custom HTML.

## Code Block Overflow Fix

The theme includes fixes to prevent code blocks from overflowing their containers on both single post pages and the main listing page.

### Why This Is Needed

- `max-width: 100%` alone doesn't constrain width - it only sets an upper bound
- Without `overflow: hidden`, containers expand to fit their content
- With `width: 100%` on child but auto-width on parent, a circular dependency occurs
- The combination of `overflow: hidden` on parents + wrapping properties on children prevents overflow

### CSS Implementation

**Code blocks** (`.post-content pre` and `.post-single-content pre`):

```css
width: 100%;
max-width: 100%;
overflow: hidden;
white-space: pre-wrap !important;
word-wrap: break-word !important;
word-break: break-word !important;
overflow-wrap: break-word !important;
box-sizing: border-box;
```

**Parent containers** (also have `overflow: hidden`):
- `.post-content` - Main page post cards
- `.post-single-content` - Single post pages
- `.post-card` - Individual post cards on homepage
- `.post-single` - Single post article wrapper

This ensures that long code lines wrap instead of causing horizontal scroll or breaking the layout.

## Accessibility Features

### WCAG AA Compliance

All color combinations meet WCAG AA contrast requirements (4.5:1 for normal text, 3:1 for large text).

### Skip Links

A skip-to-content link appears at the top of the page for keyboard users. It's hidden by default and becomes visible when focused, allowing users to jump directly to the main content.

### Keyboard Navigation

- Visible focus styles on all interactive elements
- `:focus-visible` support for better keyboard UX
- Logical tab order through the page
- All interactive elements reachable via keyboard

### Screen Reader Support

- Screen reader-only text (`.sr-only`) for decorative elements like glitch text
- Proper ARIA labels on navigation
- Semantic HTML5 structure
- IndieWeb microformats for better content understanding

### Touch Targets

All buttons and links meet WCAG minimum touch target size (44x44px).

### Reduced Motion

Animations are disabled for users who prefer reduced motion via `prefers-reduced-motion` media query.

## SEO Features

### Meta Tags

- OpenGraph tags for Facebook/LinkedIn sharing
- Twitter Card tags for Twitter sharing
- Canonical URLs to prevent duplicate content issues
- OpenGraph image fallback (via `og_image` parameter)

### Structured Data

JSON-LD structured data for:
- BlogPosting on individual posts
- WebSite on homepage

URLs in JSON-LD are properly escaped (no double-encoding issues).

This helps search engines understand your content structure.

## Security Features

### XSS Protection

- HTML in config parameters is escaped by default
- `custom_footer` parameter no longer uses `safeHTML` for security
- For custom HTML, use `layouts/partials/custom_footer_content.html` partial file

### Path Traversal Protection

Plugin HTML partials are validated to prevent directory traversal attacks:
- Filenames must match whitelist
- Path traversal sequences (`..`) are blocked
- Directory separators (`/`) are blocked in filenames

### External Script Validation

Scripts loaded via `plugins_js` config are validated:
- Must use HTTPS, HTTP, or relative URLs
- Invalid URLs are ignored

## IndieWeb Features

### Microformats2

The theme includes proper IndieWeb microformats2 markup:

- **h-entry** - Blog post entries
- **p-name** - Post titles
- **e-content** - Post content
- **dt-published** - Publication dates (ISO 8601)
- **p-summary** - Post excerpts
- **u-url** - Permalinks
- **p-author** - Author information
- **h-card** - Author card (when available)

### Endpoints

- IndieAuth authorization and token endpoints
- Micropub endpoint for posting
- Microsub endpoint for reading
- Webmention endpoint for interactions

## License

MIT
