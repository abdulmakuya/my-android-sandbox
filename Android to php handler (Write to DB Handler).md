# Android to php handler (Write to DB Handler)
```php
<?php
// Create connection
$servername = "localhost";
$username = "hopeofto_samid";
$password = "ArB2DjcABQVt";
$dbname = "hopeofto_bizdirectory";
// Create connection
$conn = mysqli_connect($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} 
//capture data from front end
//$VARIABLENAME = $_REQUEST['KEY'];
$received_name = $_REQUEST['c_name'];


//INSERT INTO tablename (col1,col2,col3.....)
//VALUES (val1,val)

$sql = "INSERT INTO company_registration (col_name,col_phone,col_email,col_adress,col_bio,col_category,col_region )

VALUES ('$received_name','$received_phone','$received_email','$received_adress','$received_bio','$received_category','$received_region')";

if ($conn->query($sql) === TRUE) {
    echo "1";
} else {
    echo "Error: " . $sql . "<br>" . mysqli_error($conn);
}
$conn->close();

?>
```
