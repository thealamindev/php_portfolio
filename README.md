# php_portfolio



<?php
$portfolio_name = $_POST['portfolio_name'];
$portfolio_catagory = $_POST['portfolio_catagory'];
// $portfolio_photo = $_POST['portfolio_photo'];

$db_connect = mysqli_connect('localhost', 'root', '', 'farzi');

$portfolio_insert_quary = "INSERT INTO portfolios (portfolio_name, portfolio_catagory) VALUES ('$portfolio_name', '$portfolio_catagory')";

mysqli_query($db_connect, $portfolio_insert_quary);
$id= mysqli_insert_id($db_connect);

// Portfolio Image Upload 
$uploaded_file_name = $_FILES['portfolio_photo']['name'];
$after_ex_file = explode('.', $uploaded_file_name);
$extention = end($after_ex_file);

$new_name = $id . '.' . $extention;
$temp_loaaction = $_FILES['portfolio_photo']['tmp_name'];
$new_location = "uploads\portfolio_photo/" . $new_name;
move_uploaded_file($temp_loaaction, $new_location);

$portfolio_upadte_quary = "UPDATE portfolios SET portfolio_photo = '$new_name' WHERE id = '$id'";
mysqli_query($db_connect, $portfolio_upadte_quary);
header('location: add_portfolio.php');

// Portfolio Image Upload 

