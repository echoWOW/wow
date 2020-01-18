# wow
随心笔记
hello,this is my first day.I hope I will have a good process
php生成4位数字验证码的实现代码
session_start(); 
//srand((double)microtime()*1000000); 
$authnum=$_SESSION['authnum']; 
//验证用户输入是否和验证码一致 
if(isset($_POST['authinput'])){ 
      if(strcmp($_POST['authinput'],$_SESSION['authnum'])==0){ 
            echo"验证成功！"; 
      }else{ 
            echo"验证失败！"; 
      } 
 
//authimg.php

<?php 
//生成验证码图片 
Header("Content-type:image/PNG"); 
srand((double)microtime()*1000000);//播下一个生成随机数字的种子，以方便下面随机数生成的使用 
  
session_start();//将随机数存入session中 
$_SESSION['authnum']=""; 
$im=imagecreate(62,20);//制定图片背景大小 
  
$black=ImageColorAllocate($im,0,0,0);//设定三种颜色 
$white=ImageColorAllocate($im,255,255,255); 
$gray=ImageColorAllocate($im,200,200,200); 
  
imagefill($im,0,0,$gray);//采用区域填充法，设定（0,0） 
  
while(($authnum=rand()%100000)<10000); 
//将四位整数验证码绘入图片 
$_SESSION['authnum']=$authnum; 
imagestring($im,5,10,3,$authnum,$black); 
//用col颜色将字符串s画到image所代表的图像的x，y座标处（图像的左上角为0,0）。 
//如果font是1，2，3，4或5，则使用内置字体 
  
for($i=0;$i<200;$i++)//加入干扰象素 
{ 
$randcolor=ImageColorallocate($im,rand(0,255),rand(0,255),rand(0,255)); 
imagesetpixel($im,rand()%70,rand()%30,$randcolor); 
} 
ImagePNG($im); 
ImageDestroy($im); 
?>
