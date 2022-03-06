---
title: 告别阿里云
author: 黄俭
date: '2022-03-06'
slug: say-bye-to-AliCloud
categories:
  - Work
tags:
  - Linux
---

2020年初，Covid-19疫情刚起，全校学生都是在线上课，这时我申请了阿里云的一个服务器，ip地址是123.56.98.124。这也是我的第一个云服务器，系统是Ubuntu 18.04 bionic LTS，内核版本4.15.0-122-Generic, CPU:Intel Xeon E5-2682, RAM:2G。

在这个服务器上，我配置了一个nextcloud，还自己用PHP做了一个相册，后台数据库是mysql，数据库管理用phpMyAdmin。还用服务器收集学生的作业，其实就是一个PHP的脚本。代码如下所示：

 ```php
 <?php
    /*
        This code is loosely based
        on john@php-dude.com,
        the post 27-Jul-2001 12:00
        at http://www.php.net/manual/en/features.file-upload.php.
    */
	$HTML = NULL;


	if(count($_FILES) > 0){
		$allowed_types = array("application/zip", "application/x-zip-compressed","image/jpeg","image/jpg","image/png","image/gif");
		$size_limit = "3145728"; //3MiB

		$file = $_FILES["file"]["name"];
		$type = $_FILES["file"]["type"];
		$size = $_FILES["file"]["size"];
		$temp = $_FILES["file"]["tmp_name"];

    
		/*$path_info = pathinfo($PATH_TRANSLATED);*/
		


		//Web server anonymous user must have
		//write permissions to this path:
		$write_path = "/home/huang/20201451_Linux_04/" . $file;


		if ($file){
			if ($size < $size_limit){
				
				
      if (in_array($type, $allowed_types) ){
					if(move_uploaded_file($temp, $write_path)){
					//	$HTML = "<div>The file <tt>$file</tt> was sucessfully uploaded.</div>";
					} else {
					$HTML = "<div>The file <tt>$file</tt> upload failed.</div>";
				}
			} else {
				$HTML = "<div>Files of type <tt>$type</tt> are not permitted.</div>";
			}
		} else {
			$HTML = "<div>File exceeds the size limit of $size_limit bytes.</div>";
		}
	}

	$HTML .= "\n";
    }
?>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"
"http://www.w3.org/TR/REC-html40/loose.dtd">
<html>
<head>
    <meta name=VS_TARGETSCHEMA content="HTML 4.0">
    <meta name="editor" content="Huang Jian">
    <meta name="reply-to" content="57820048@qq.com">
    <meta name="keywords" content="">
    <meta name="description" content="">
    <title>Submit</title>
</head>
<body>
<?php echo $HTML ?>
<ol>
<h2>20201451班Linux第四次作业内容：</h2>
<li>截图表明自己完成了Linux下网页服务器httpd的配置；<br></li>
</ol>
<ol>
<h2>Linux第一次作业说明：</h2>
<li>作业必须打包成Zip文件上传或直接传一张图；<br></li>
<li>图中应有相册页面和非本机访问的页面 <br></li>
<li>文件名应包含姓名，学号和作业编号, 如"张三2020145112第4次.zip"。<br></li>
<li>作业必须在2020年12月25日15:00前提交。<br></li>
</ol>

<br>

<img src="sample/Linux-homework-sample-04.jpg" />

<br>
<hr>
<div align="center">
<form enctype="multipart/form-data" action="<?php echo htmlspecialchars($_SERVER['PHP_SELF']); ?>"
method="POST">
    Homework:
    <input name="file" type="file">
    <input type="submit" value="Submit">
</form>
</div>
<hr>

<table border="1" align="CENTER">
<caption>已经提交的作业</caption>
<th>作业</th><th>提交时间</th>
<?php
	if ($handle = opendir('/home/huang/20201451_Linux_04/')) {
		while (false !== ($file = readdir($handle))) {
			if ($file != "." && $file != "..") {
				echo "<tr><td>" . $file . "</td><td>" . date("D d M Y g:i A", filemtime("/home/huang/20201451_Linux_04/" . $file)) . "</td></tr>";
			}
		}
		closedir($handle);
	}
?>
</table>
<hr>
</body>
</html>

 ```

这个服务器服役了两年，现在愈发用得少了，下行带宽也是非常窄，1M。还有就是贵，刚申请的时候几百块，第二年续费突然就要1000多，阿里真是鸡贼，用户有了依赖，有了粘性之后就涨价，所以决定放弃了，今天把所有该备份的都备份了。以后我可能还会申请云服务器，但阿里云肯定不再是我的第一选择，目标应该是放在国外其他的品牌。

改nextcloud配置文件的路径也记一下：

 ```shell
  # cd /var/snap/nextcloud/current/nextcloud/config
 ```

