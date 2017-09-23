# hello-world
just another respository
<?php
header("content-Type:text/html;charset=utf-8");
$r_id=$_POST['run_id'];
$r_title=$_POST['run_title'];
$dbms='mysql';
$dbName='db1';
$user='root';
$pwd='';
$host='localhost';
$dsn="$dbms:host=$host;dbname=$dbName";
try{
	$pdo=new PDO($dsn,$user,$pwd);
	echo "PDO连接成功";
	$pdo->query('set names utf-8;');
	$pdo->query('character_client_names:utf-8;');
	$query="insert into rundb1 values('$r_id','$r_title')";
	$rs=$pdo->exec($query);
	if($rs){
		echo "插入成功";
		}

	$query2="select * from rundb1";
    $result2=$pdo->prepare($query2);
	$result2->execute();
	
	
	while($res=$result2->fetch(PDO::FETCH_ASSOC)){
		echo"<br>";
		echo $res['run_id'];
		echo"<br>";
		echo $res['run_title'];
	}
}
catch(PDOException $e){
	die("erro!:".$e->getMessage()."<br>");
}

?>
