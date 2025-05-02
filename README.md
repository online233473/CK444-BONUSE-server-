# CK444-BONUSE-server-
payment-page
<?php
session_start();
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $username = $_POST['username'];

    // ডেমো ইউজারচেক (বাস্তবে ডাটাবেসে চেক করতে হবে)
    $allowed_users = ['user1', 'user2', 'admin'];

    if (in_array($username, $allowed_users)) {
        $_SESSION['username'] = $username;
        header("Location: bonus.php");
        exit();
    } else {
        $error = "ইউজারনেম ভুল!";
    }
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>CK444 লগইন</title>
</head>
<body>
    <h2>CK444 লগইন</h2>
    <?php if (isset($error)) echo "<p style='color:red;'>$error</p>"; ?>
    <form method="POST">
        ইউজারনেম: <input type="text" name="username" required>
        <input type="submit" value="লগইন">
    </form>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION['username'])) {
    header("Location: login.php");
    exit();
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>CK444 বোনাস অ্যাড</title>
</head>
<body>
    <h2>স্বাগতম, <?php echo htmlspecialchars($_SESSION['username']); ?>!</h2>
    <form method="POST" action="save_bonus.php">
        বোনাস নাম: <input type="text" name="bonus_name" required><br>
        বোনাস পরিমাণ: <input type="number" name="bonus_amount" required><br>
        <input type="submit" value="বোনাস অ্যাড করুন">
    </form>
    <a href="logout.php">লগআউট</a>
</body>
</html>
<?php
session_start();
if (!isset($_SESSION['username'])) {
    header("Location: login.php");
    exit();
}

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $bonus_name = $_POST['bonus_name'];
    $bonus_amount = $_POST['bonus_amount'];

    // বাস্তবে এখানে ডাটাবেসে সেভ করতে হবে
    echo "বোনাস সংরক্ষিত হয়েছে:<br>";
    echo "নাম: " . htmlspecialchars($bonus_name) . "<br>";
    echo "পরিমাণ: " . htmlspecialchars($bonus_amount);
}
?>
<?php
session_start();
session_destroy();
header("Location: login.php");
exit();

