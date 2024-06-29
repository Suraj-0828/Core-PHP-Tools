# index.htm -> file means ( under constraction ) project work on process...
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

# Backend PHP CODE FORM SUBMIT GET MESSAGE ON GMAIL

========================================================

<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Sanitize and retrieve form data
    $firstname = htmlspecialchars($_POST['firstname']);
    $lastname = htmlspecialchars($_POST['lastname']);
    $email = htmlspecialchars($_POST['email']);
    $phone = htmlspecialchars($_POST['phone']);

    // Prepare email content
    $to = "your-email@example.com"; // Replace with your email address
    $subject = "New Contact Form Submission";
    $message = "First Name: $firstname\n";
    $message .= "Last Name: $lastname\n";
    $message .= "Email: $email\n";
    $message .= "Phone: $phone\n";

    $headers = "From: $email";

    // File upload handling
    if ($_FILES['file']['error'] == 0) {
        $file_path = $_FILES['file']['tmp_name'];
        $file_name = $_FILES['file']['name'];
        $file_type = $_FILES['file']['type'];

        // Validate file type (optional)
        $allowed_types = array('application/pdf'); // Add more MIME types as needed
        if (in_array($file_type, $allowed_types)) {
            $file_content = chunk_split(base64_encode(file_get_contents($file_path)));

            // Append file to email message
            $boundary = md5(uniqid(time()));
            $headers .= "\r\nMIME-Version: 1.0\r\n";
            $headers .= "Content-Type: multipart/mixed; boundary=\"$boundary\"\r\n\r\n";
            $message = "--$boundary\r\n";
            $message .= "Content-Type: text/plain; charset=\"utf-8\"\r\n";
            $message .= "Content-Transfer-Encoding: 7bit\r\n\r\n";
            $message .= "First Name: $firstname\n";
            $message .= "Last Name: $lastname\n";
            $message .= "Email: $email\n";
            $message .= "Phone: $phone\n";
            $message .= "--$boundary\r\n";
            $message .= "Content-Type: application/pdf; name=\"$file_name\"\r\n";
            $message .= "Content-Transfer-Encoding: base64\r\n";
            $message .= "Content-Disposition: attachment; filename=\"$file_name\"\r\n\r\n";
            $message .= $file_content . "\r\n";
            $message .= "--$boundary--";
        } else {
            // Invalid file type, handle error as needed
            header("Location: failed.php?error=filetype");
            exit();
        }
    }

    // Send email
    if (mail($to, $subject, $message, $headers)) {
        header("Location: send.php"); // Redirect to send.php on success
        exit();
    } else {
        header("Location: failed.php"); // Redirect to failed.php on failure
        exit();
    }
} else {
    header("Location: index.php"); // Redirect back to index.php if accessed directly
    exit();
}
?>

