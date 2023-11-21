# lommeregnerdk
<!-- HTML Form for input -->
<form method="post" action="download_file.php">
    <label for="fileUrl">Enter URL of the file to download:</label>
    <input type="text" id="fileUrl" name="fileUrl">
    <input type="submit" value="Download">
</form>
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST" && !empty($_POST["fileUrl"])) {
    $url = $_POST["fileUrl"];

    // Use basename() to get the file name from the URL
    $fileName = basename($url);

    // Use file_get_contents() to download the file
    $fileContent = file_get_contents($url);
    if ($fileContent === false) {
        die("Error: Unable to download file.");
    }

    // Specify the path where the file will be saved
    $savePath = "downloads/" . $fileName; // Ensure this directory exists and is writable

    // Use file_put_contents() to save the file locally
    if (file_put_contents($savePath, $fileContent) === false) {
        die("Error: Unable to save the file.");
    }

    echo "File downloaded and saved successfully.";
} else {
    echo "No URL provided.";
}
?>
