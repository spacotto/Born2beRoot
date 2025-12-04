# About WordPress
WordPress is a free, open-source **Content Management System (CMS)** that powers over 40% of all websites. It allows you to create and manage websites without writing code, though developers can extend it extensively.

## Getting Started
### Installation
WordPress requires a web host with PHP and MySQL. Most hosts offer one-click installation through their control panel.

### Manual installation
1. Download WordPress from wordpress.org
2. Create a MySQL database
3. Upload files via FTP
4. Run the installation script at yoursite.com/wp-admin/install.php
5. Enter database details and create an admin account

### Dashboard
Access the admin dashboard at `yoursite.com/wp-admin`. This is where you manage all content and settings.

## Core Concepts
### Posts vs Pages
**Posts** are timely content displayed in reverse chronological order (blog entries, news). They have categories and tags.

**Pages** are static content (About, Contact, Services). They exist outside the chronological flow and can be hierarchical.

### Themes
Themes control your site's **appearance**. You can install free themes from the WordPress repository or purchase premium themes. Change themes at Appearance → Themes without losing content.

### Plugins
Plugins add **functionality** to WordPress. Install from `Plugins → Add New`. Essential plugins often include SEO tools, security, backups, and contact forms.

## Content Management
### Creating Content
1. Navigate to Posts
2. Add New or Pages
3. Add New

The block editor (Gutenberg) lets you add content blocks like paragraphs, images, headings, and more.

Common blocks: Paragraph, Image, Heading, List, Quote, Button, Columns, Gallery.

### Media Library
Upload images, videos, and documents at `Media → Library`. WordPress automatically creates multiple image sizes for responsive design.

### Categories and Tags
**Categories** are hierarchical groupings for posts (like folders).

**Tags** are non-hierarchical keywords for specific topics.

## Essential Settings
### Permalinks
`Settings → Permalinks` controls URL structure. 
"Post name" structure (`yoursite.com/post-title`) is recommended for SEO.

### Reading Settings
`Settings → Reading` determines your homepage (latest posts or static page) and how many posts appear per page.

## User Roles
WordPress has five default roles with different permissions:
1. **Administrator**: Full access to everything
2. **Editor**: Manage and publish all posts/pages
3. **Author**: Write and publish own posts
4. **Contributor**: Write posts but can't publish
5. **Subscriber**: Only manage their profile

## Maintenance
### Updates
Regularly update WordPress core, themes, and plugins at Dashboard → Updates. Always backup before major updates.

### Backups
Use a backup plugin or your host's backup service. Back up both files and the database regularly.

### Security Tips
- Use strong passwords and two-factor authentication
- Keep everything updated
- Install a security plugin
- Use SSL/HTTPS
- Limit login attempts
- Remove unused themes and plugins

## Troubleshooting
### White Screen of Death
Usually caused by plugin/theme conflicts or memory limits. 
Disable plugins via FTP by renaming the plugins folder.

### 404 Errors
Go to `Settings → Permalinks` and click `Save Changes` to regenerate rewrite rules.

### Locked Out
Reset password via database or FTP by uploading a password reset script.

## File Structure
Key directories:
```
/wp-content/themes/     # Theme files
/wp-content/plugins/    # Plugin files
/wp-content/uploads/    # Media files
/wp-config.php          # Configuration file (database credentials)
```

## Development Basics
### Child Themes
Create a child theme to customize without losing changes during parent theme updates. Requires style.css with theme header and `functions.php`.

### Hooks
WordPress uses hooks for customisation:
- Actions: Execute code at specific points
- Filters: Modify data before display

### The Loop
The Loop displays posts. Most theme templates use it to iterate through and display content.

## Best Practices
- Keep login credentials secure
- Regular backups before changes
- Test plugins/themes on the staging site first
- Optimise images before uploading
- Use caching for performance
- Choose reputable theme/plugin sources
- Remove inactive plugins and themes
- Monitor site speed and uptime

## Resources
- Official Documentation: wordpress.org/documentation
- Support Forums: wordpress.org/support
- Developer Reference: developer.wordpress.org
- Theme Directory: wordpress.org/themes
- Plugin Directory: wordpress.org/plugins
