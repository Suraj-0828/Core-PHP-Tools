# Core-PHP-Tools
Start to End Website Design
First Create ->
important file
1. index.php    
2. header.php
3. footer.php
4. succes.php
5. failed.php
6. send message.php
7. .htaccess
8. assets
9. assets/images/......
10. assets/css......
11. assets/javascript.....

 ==========================================================
``` <!-- index.php -->
<?php include 'header.php'; ?>

<main>
    <p>This is the main content of the page.</p>
</main>

<?php include 'footer.php'; ?>
===========================================================
 # Project Root #
===========================================================
# /project-root
    /assets
        /images
        /fonts
        /videos
    /css
        styles.css
    /js
        main.js
    /components
        header.php
        footer.php
        nav.php
    /pages
        index.php
        about.php
        contact.php
    /includes
        database.php
        config.php
    /node_modules (if using npm)
    .gitignore
    package.json (if using npm)
    README.md

    #after this 
===========================================
    <?php include 'components/header.php'; ?>
<?php include 'components/nav.php'; ?>

<main>
    <section>
        <h2>Welcome to My Website</h2>
        <p>This is the main content of the page.</p>
    </section>
</main>

<?php include 'components/footer.php'; ?>
========================================================
