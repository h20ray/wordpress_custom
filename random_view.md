# WordPress Custom Initial Post Views

This WordPress custom code automatically sets a random initial post view count for new posts using the **Post Views Counter** plugin. It ensures that every newly created post starts with a random number of views between 512 and 768 to simulate some activity before the post is officially live.

## How It Works

- Hooks into the `save_post` action to trigger the function when a new post is saved.
- Applies only to posts that are new (in `auto-draft` or `draft` status) and does not modify existing posts.
- Sets a random number of views between 512 and 768 on each new post using the **Post Views Counter** plugin's `pvc_update_post_views` function.

## Code

Paste the code for the custom post views function inside your theme's `functions.php` file.

```php
/**
 * ANDORU CUSTOM VIEW: Set random initial post views for new posts
 */

function set_initial_random_post_views_on_new_post($post_id, $post) {
    // Skip if this is an auto-save or a revision
    if (defined('DOING_AUTOSAVE') && DOING_AUTOSAVE) {
        return;
    }

    // Skip if it's an edit or a non-new post
    if ($post->post_status !== 'auto-draft' && $post->post_status !== 'draft') {
        return;
    }

    // Only apply to posts
    if ($post->post_type !== 'post') {
        return;
    }

    // Generate random views between 512 and 768
    $random_views = rand(512, 768);

    // Set the random views using the Post Views Counter function
    pvc_update_post_views($post_id, $random_views);
}

// Hook into 'save_post' action
add_action('save_post', 'set_initial_random_post_views_on_new_post', 10, 2);

```

## Installation

### Prerequisites

1. **WordPress Version**: Ensure you are using WordPress and have administrative access to your site.
2. **Post Views Counter Plugin**: Install and activate the [Post Views Counter](https://wordpress.org/plugins/post-views-counter/) plugin by dFactory.

### Step-by-Step Installation

1. **Log in to WordPress Admin**:
   - Go to your WordPress dashboard by logging in with an administrator account.

2. **Navigate to Your Theme's `functions.php`**:
   - In the WordPress dashboard, go to **Appearance > Theme File Editor**.
   - In the right sidebar, find and click on the `functions.php` file under your active theme.

3. **Add the Custom Code**:
   - Scroll down to the bottom of the `functions.php` file and paste the code from the **Code** section.

4. **Save the Changes**:
   - Once you’ve added the code, click the **Update File** button to save your changes.

5. **Test the Functionality**:
   - Create a new post from the WordPress dashboard. After saving the post, it should automatically have a random number of views between 512 and 768.
   - You can check the post views by viewing the post and checking the post views counter (depending on how the Post Views Counter plugin is set up to display).

## Additional Tips

- If you want to display post views on your site, ensure that the **Post Views Counter** plugin is properly configured to show the views for each post.
- You can adjust the random range by changing the numbers in the `rand()` function, e.g., `rand(512, 1920)`.

---

This solution helps give the appearance of early engagement on newly published content, ideal for blogs and websites looking to simulate initial activity.
