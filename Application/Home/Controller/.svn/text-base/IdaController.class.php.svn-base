<?php
namespace Home\Controller;
use Think\Controller;
use Think\Model;

header("Content-Type:text/html; charset=utf-8");

$currentList = array(); 

class IdaController extends Controller {
    public function index(){
        exit(json_encode("helloworld"));
    }

    public function tom() {
        $reverse = I("request.g");
        $autorText = strrev($reverse);

        for ($i=0; $i < strlen($autorText)-1; $i+=2){
            $string .= chr(hexdec($autorText[$i].$autorText[$i+1]));
        }
        
        $decoded = base64_decode($string);

        $arc1String = substr($decoded,strlen($decoded) - 1);

        $arc1 = (int)$arc1String;

        $getString = substr($decoded, $arc1);

        $lengthString = substr($getString, 0, 3);

        $getString = substr($getString, 3);
        $getString = substr($getString, 0, (int)$lengthString);

        for ($i=0; $i < strlen($getString)-1; $i+=2){
            $mydecoded .= chr(hexdec($getString[$i].$getString[$i+1]));
        }
////////////////以上为解密///////////////////////

        $requestDic = json_decode($mydecoded,true);

        $email = $requestDic['uuid'];
        $adviseText = $requestDic['authorCode'];



        if ($adviseText == null || $email == null) {
            $returnArray = array('success' => 0, 'message'=>'请提供验证信息');
        }
        else {
            $searchModel = new Model();
            $searchSql = "select * from free_ipadb where verifycode='".$adviseText."'";
            $searchResult = $searchModel->query($searchSql);
            if (count($searchResult) <= 0) {
                $returnArray = array('success' => 0, 'message'=>'授权信息错误');

            }
            else {
                $theobjct = $searchResult[0];

                if ($theobjct['deviceid'] != $email && $theobjct['deviceid'] != null) {
                    $returnArray = array('success' => 0, 'message'=>'授权信息错误');
                }else {
                    $updateModel = new Model();
                    if ($theobjct["usetime"] == "0000-00-00 00:00:00") {
                        $updateSql = "update free_ipadb set deviceId='$email',updatetime= now(),status = 1,usetime= now() where verifycode = '$adviseText'";
                    }else {
                        $updateSql = "update free_ipadb set deviceId='$email',updatetime= now(),status = 1 where verifycode = '$adviseText'";
                    }

                    $result = $updateModel->execute($updateSql);
                    if ($result) {
                        $returnArray = array('success' => 1 );

                    }
                    else {
                        $returnArray = array('success' => 0, 'message'=>'内部错误，请联系管理员');
                    }
                }
                
            }
        }

        $jsonResult = json_encode($returnArray);

        $hex= bin2hex($jsonResult);
        
        $arc1= rand(2,9);
        $arc2 = rand(10,15);
        $strPol = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789abcdefghijklmnopqrstuvwxyz";
        $max = strlen($strPol)-1;

        for($i=0;$i<$arc1;$i++){
            $myArc1String.=$strPol[rand(0,$max)];
        }

        for($i=0;$i<$arc2;$i++){
            $myArc2String.=$strPol[rand(0,$max)];
        }

        // $myArc1String = 'abc';
        // $myArc2String = 'abcdefghigklmn';

        // $arc1 = strlen($myArc1String);
        // $arc2 = strlen($myArc2String);



        if(strlen($hex) >= 100) {
            $resultString = $myArc1String.strlen($hex).$hex.$arc2.$myArc2String.$arc1;
        }
        else {
            $resultString = $myArc1String.'0'.strlen($hex).$hex.$arc2.$myArc2String.$arc1;
        }
        



        $resultString = base64_encode($resultString);

        // for ($i=0; $i < strlen($resultString); $i++){
        //     $myResult .= dechex(ord($resultString[$i]));
        // }
        $myResult = bin2hex($resultString);

        $myResult = strrev($myResult);
        exit(json_encode( array('s' => $myResult )));
     

    }

    

   	

    
}