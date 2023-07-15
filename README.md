
## Sending Form Data to a Database with PHP and MySQL

#  Prerequisites
-  Basic knowledge of HTML, PHP, and MySQL.
 - A web server with PHP and MySQL support set up.


## Step 1: Create the Database Table


 Start by creating a new table in your MySQL database to store the form data.
 For example, let's assume the table name is users, and it has the following columns:


- id (INT, AUTO_INCREMENT, PRIMARY KEY)
- name (VARCHAR)
- email (VARCHAR)
- message (TEXT)
```
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255),
  message TEXT
); 
```
## Step 2: Create the HTML Form
1-  Create an HTML form where users can input their information. Here's an example form with input fields for name, email, and message:

```
<form action="process_form.php" method="POST">
  <label for="name">Name:</label>
  <input type="text" name="name" id="name" required>

  <label for="email">Email:</label>
  <input type="email" name="email" id="email" required>

  <label for="message">Message:</label>
  <textarea name="message" id="message" required></textarea>

  <button type="submit">Submit</button>
</form>
```
##  Step 3: Create the PHP Script to Process Form Data
1- Create a new PHP file, process_form.php, to handle the form submission and store the data in the database.


2- In 
`process_form.php`  establish a database connection using the appropriate credentials:

  ```
<?php
$servername = "localhost";
$username = "your_username";
$password = "your_password";
$dbname = "your_database";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}
?>
 ```
3-  Retrieve the form data using PHP's $_POST superglobal:
 ```
<?php
$name = $_POST['name'];
$email = $_POST['email'];
$message = $_POST['message'];
?> 
```
4- Prepare an SQL statement to insert the form data into the users table:

 ```
 <?php
$stmt = $conn->prepare("INSERT INTO users (name, email, message) VALUES (?, ?, ?)");
$stmt->bind_param("sss", $name, $email, $message);
$stmt->execute();
if ($stmt->affected_rows > 0) {
  echo "Data inserted successfully!";
} else {
  echo "Error: " . $stmt->error;
}
$stmt->close();
?>
  ```

5- Close the database connection:
 ```
 <?php
$conn->close();
?>

  ```


  # Step 4: Test the Form Submission

  1- Start your web server and open the form page in a web browser.

  2- Fill out the form with some sample data and submit it.

  3- If everything is set up correctly, you should see the success message, indicating  that 
the data has been inserted into the database.
