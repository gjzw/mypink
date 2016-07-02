<?php
namespace Home\Controller;
use Think\Controller;
use Think\Model;

header("Content-Type:text/html; charset=utf-8");

$currentList = array(); 

class IndexController extends Controller {
    public function index(){
        $this->display();
    }


    public function loginaction() {

        $password = I("request.pass");
        $username = I("request.user");

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              setcookie("user", $username, time()+3600);
              setcookie("pass", $password, time()+3600);
              $this->display();
            }
            else {
              $this->error('用户名或密码错误');
            }
        }
        else {
          $this->error('用户名或密码错误');
        }
    }


    public function getVerify() {
        $username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }


    	$number = I("request.number");
        $seller = I("request.seller");
    	global $currentList;
    	$currentList = array();

    	$count = 0;
    	while (1) {
    		if ($count >= $number) {
    			break;
    		}
    		$str = null;
		   	$strPol = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789abcdefghijklmnopqrstuvwxyz";
		   	$max = strlen($strPol)-1;

		   	for($j=0;$j<8;$j++){
		    	$str.=$strPol[rand(0,$max)];
		   	}

		   	$isin = in_array($str,$currentList);
		   	if ($isin) {
		   		continue;
		   	}
		   	else {
		   		$theModel = new Model();
		   		$sql = "select * from free_ipadb where verifycode='".$str."'";

		   		$booksArray = $theModel->query($sql);
		   		if (count($booksArray) > 0) {
		   			continue;
		   		}

		   		

		   		$saveModel = new Model();
		   		$saveSql = "INSERT INTO free_ipadb (verifycode,status,createtime,channelname) VALUES('".$str."',0,now(),'$seller'); ";
		   		$result = $saveModel->execute($saveSql);
		   		if ($result) {
		   			$count ++;
		   			Array_push($currentList,$str);
		   		}
		   	}
    	}

    	

        print("<p style='color:#F00'>*已存入数据库，可以直接使用*</p>");

    	// print("<textarea rows='".$number."' cols='8']>");
        print("<table width = '500'>");
        $i = 0;
    	foreach($currentList as $gggg) {
            $i = $i+1;
            print("<tr>");
            print("<td>");
            print $i;
            print("</td>");
            print("<td>");
			print $gggg;
            print("</td>");
			// print("<br>");

            print("</tr>");
    	}
        print("</table>");
    	// print("</textarea>");

   	 }

     public function search() {
        $username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }
          $number = I("request.number");

      $theModel = new Model();
    $sql = "select id,verifycode,createtime,channelname,isdistribution,deviceId,usetime,updatetime from free_ipadb where verifycode='".$number."' order by id desc ";
    $booksArray = $theModel->query($sql);
    print("<table>");
    for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                      print($key);
                    }
                    else if($key == "verifycode") {
                      print("激活码");
                    }
                    else if($key == "createtime") {

                      print("创建时间");
                    }
                    else if($key == "channelname") {
                      print("渠道名");
                    }
                    else if($key == "isdistribution") {
                      print("已卖出");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                      print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');
        }
        print("</table>");

     }

   	 public function unverifyList() {
      $username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }


   	 	$number = I("request.number");

   	 	$theModel = new Model();
		$sql = "select id,verifycode,createtime,channelname,isdistribution from free_ipadb where status = 0 order by id desc limit $number";
		$booksArray = $theModel->query($sql);
		print("<table>");
		for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                    	print($key);
                    }
                    else if($key == "verifycode") {
                    	print("激活码");
                    }
                    else if($key == "createtime") {

                    	print("创建时间");
                    }
                    else if($key == "channelname") {
                    	print("渠道名");
                    }
                    else if($key == "isdistribution") {
                    	print("已卖出");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                    	print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');
        }
        print("</table>");

   	 }

   	 public function verifyedList() {
   	 	$username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }
   	 	$number = I("request.number");

   	 	$theModel = new Model();
		$sql = "select id,verifycode,createtime,channelname,isdistribution,deviceId,usetime,updatetime from free_ipadb where status = 1  order by id desc limit $number";
		$booksArray = $theModel->query($sql);

		print("<table>");
		for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                    	print($key);
                    }
                    else if($key == "verifycode") {
                    	print("激活码");
                    }
                    else if($key == "createtime") {

                    	print("创建时间");
                    }
                    else if($key == "channelname") {
                    	print("渠道名");
                    }
                    else if($key == "isdistribution") {
                    	print("已卖出");
                    }
                    else if($key == 'deviceId') {
                    	print("用户唯一标示");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                    	print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');

		}
   	 }

   	 public function allVerfiy() {
   	 	  $username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];



        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }
   	 	$number = I("request.number");

   	 	$theModel = new Model();
		$sql = "select id,verifycode,createtime,channelname,isdistribution,deviceId,usetime,updatetime from free_ipadb order by id desc limit $number";
		$booksArray = $theModel->query($sql);
		print("<table>");
		for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                    	print($key);
                    }
                    else if($key == "verifycode") {
                    	print("激活码");
                    }
                    else if($key == "createtime") {

                    	print("创建时间");
                    }
                    else if($key == "channelname") {
                    	print("渠道名");
                    }
                    else if($key == "isdistribution") {
                    	print("已卖出");
                    }
                    else if($key == 'deviceId') {
                    	print("用户唯一标示");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                    	print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');

		}
   	 }

   	 public function undistribute() {
      $username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }
   	 	$number = I("request.number");

   	 	$theModel = new Model();
		$sql = "select id,verifycode,createtime,channelname,isdistribution,deviceId,usetime,updatetime from free_ipadb where ISNULL(channelname) or channelname = '' order by id desc limit $number";
		$booksArray = $theModel->query($sql);
		print("<table>");
		for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                    	print($key);
                    }
                    else if($key == "verifycode") {
                    	print("激活码");
                    }
                    else if($key == "createtime") {

                    	print("创建时间");
                    }
                    else if($key == "channelname") {
                    	print("渠道名");
                    }
                    else if($key == "isdistribution") {
                    	print("已卖出");
                    }
                    else if($key == 'deviceId') {
                    	print("用户唯一标示");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                    	print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');

		}
   	 }

   	 public function distribute() {
   	 	$username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }


   	 	$number = I("request.number");

   	 	$theModel = new Model();
		$sql = "select id,verifycode,createtime,channelname,isdistribution,deviceId,usetime,updatetime from free_ipadb where channelname != 'null' and channelname != '' order by id desc limit $number";
		$booksArray = $theModel->query($sql);
		print("<table>");
		for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                    	print($key);
                    }
                    else if($key == "verifycode") {
                    	print("激活码");
                    }
                    else if($key == "createtime") {

                    	print("创建时间");
                    }
                    else if($key == "channelname") {
                    	print("渠道名");
                    }
                    else if($key == "isdistribution") {
                    	print("已卖出");
                    }
                    else if($key == 'deviceId') {
                    	print("用户唯一标示");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                    	print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');

		}
   	 }

   	 public function removeCode() {
   	 	$username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }


   	 	$startId = I("request.startId");
   	 	$endId = I("request.endId");

   	 	$model = new Model();
   	 	$sql ;
   	 	if ($startId < 0 && $endId < 0) {
   	 		$this->error('请提供要删除的ID');
   	 	}
   	 	else if($startId > 0 && $endId > 0) {
   	 		$sql = "delete from free_ipadb where id >= $startId && id <= $endId";
   	 		$result = $model->execute($sql);
   	 		if ($result) {
   	 			$this->success("删除成功");
   	 		}
   	 		else {
   	 			$this->error('删除失败');
   	 		}
   	 	}
   	 	else if($startId < 0 && $endId > 0) {
   	 		$sql = "delete from free_ipadb where id = $endId";
   	 		$result = $model->execute($sql);
   	 		if ($result) {
   	 			$this->success("删除成功");
   	 		}
   	 		else {
   	 			$this->error('删除失败');
   	 		}
   	 	}
   	 	else {
   	 		$this->error('删除单个激活码，请把激活码ID放到\'终止ID\'中');
   	 	}

   	 }

   	 public function sellCode() { 
   	 	$username = $_COOKIE["user"];
        $password = $_COOKIE["pass"];

        $realUser = C('username');
        $realPass = C('password');


        if ($username == $realUser) {
            if ($password == $realPass) {
              $this->display();
            }
            else {
              $this->display('index');
              return;
              }
        }
        else {
          $this->display('index');
          return;
        }
   	 	$startId = I("request.startId");
   	 	$endId = I("request.endId");
   	 	$sellName = I("request.seller");

   	 	if ($sellName == null || $sellName == '') {
   	 		$this->error('请填写渠道商');
   	 		return;
   	 	}
   	 	
   	 	$model = new Model();
   	 	$sql ;
   	 	if ($startId < 0 && $endId < 0) {
   	 		$this->error('请提供销售的ID');
   	 	}
   	 	else if($startId > 0 && $endId > 0) {
   	 		$sql = "update free_ipadb set channelname = '$sellName' ,isdistribution = 1  where id >= $startId && id <= $endId";
   	 		$result = $model->execute($sql);
   	 		if ($result) {
   	 			$this->success("销售成功");
   	 		}
   	 		else {
   	 			$this->error('销售失败');
   	 		}
   	 	}
   	 	else if($startId < 0 && $endId > 0) {
   	 		$sql = "update free_ipadb set channelname = '$sellName', isdistribution = 1  where id = $endId";
   	 		$result = $model->execute($sql);
   	 		if ($result) {
   	 			$this->success("销售成功");
   	 		}
   	 		else {
   	 			$this->error('销售失败');
   	 		}
   	 	}
   	 	else {
   	 		$this->error('销售单个激活码，请把激活码ID放到\'终止ID\'中');
   	 	}
   	 }
    

    public function searchj() {

        $this->display();

        $number = I("request.number");
        if ($number == null) {
            return;
        }

      $theModel = new Model();
    $sql = "select id,verifycode,createtime,channelname,isdistribution,deviceId,usetime,updatetime from free_ipadb where verifycode='".$number."' order by id desc ";
    $booksArray = $theModel->query($sql);
    print("<table>");
    for ($i=0; $i < count($booksArray); $i++) { 
            $book1 = $booksArray[$i];
            if ($i == 0) {
                print("<tr>");
                foreach($book1 as $key => $value)   {

                    print("<th>");
                    if ($key == "id") {
                      print($key);
                    }
                    else if($key == "verifycode") {
                      print("激活码");
                    }
                    else if($key == "createtime") {

                      print("创建时间");
                    }
                    else if($key == "channelname") {
                      print("渠道名");
                    }
                    else if($key == "isdistribution") {
                      print("已卖出");
                    }
                    else if($key == "usetime") {
                        
                        print("激活时间");
                    }
                    else if($key == "updatetime") {
                        print("上次使用时间");
                    }
                    else  {
                      print($key);
                    }
       
                    print("</th>");
                }

                print("</tr>");
            }

            print("<tr>");

            foreach($book1 as $key => $value)  {
                print("<td align=center>");
                print("$value");
                print("</td>");
            }
            print('</tr>');
        }
        print("</table>");
    }
}