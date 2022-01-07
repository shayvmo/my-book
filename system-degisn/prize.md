## 简单抽奖算法



https://wx.wei1.top/blog/index/detail/item/465.html



```php
function getRand($proArr)
{
    $result = '';
    //概率数组的总概率精度
    $proSum = array_sum($proArr);
    //概率数组循环
    foreach ($proArr as $key => $proCur) {
        $randNum = mt_rand(1, $proSum);
        if ($randNum <= $proCur) {
            $result = $key;
            break;
        } else {
            $proSum -= $proCur;
        }
    }
    unset ($proArr);
    return $result;
}



function getPrizes()
{
    return array(
        '0' => array('id' => 1, 'prize' => '免费服务器', 'v' => 1),
        '1' => array('id' => 2, 'prize' => '免费数据库', 'v' => 19),
        '2' => array('id' => 3, 'prize' => '免费公众号官网', 'v' => 100),
        '3' => array('id' => 4, 'prize' => '免费服装版小程序', 'v' => 100),
        '4' => array('id' => 5, 'prize' => '免费生鲜版小程序', 'v' => 150),
        '5' => array('id' => 6, 'prize' => '免费小商户版小程序', 'v' => 100),
        '6' => array('id' => 7, 'prize' => '1年免费物联网自动化系统', 'v' => 80),
        '7' => array('id' => 8, 'prize' => '免费物流发货系统', 'v' => 50),
        '8' => array('id' => 9, 'prize' => '哎呀，与奖品擦肩而过了，继续努力哦', 'v' => 400),
    );
}

function getResult($prize_arr,$retYesArr=false)
{
    $rid = getRand(array_column($prize_arr, 'v', 'id')); //根据概率获取奖项id

    //用ID作为数组key重组多维数组
    $temArr = array_column($prize_arr,null,'id');
    //只返回中奖的项目
    if ($retYesArr){
        return $temArr[$rid];
    }

    $res['yes'] = $temArr[$rid]['prize']; //中奖项
    unset($temArr[$rid]); //将中奖项从数组中剔除，剩下未中奖项
    shuffle($temArr); //打乱数组顺序
    $pr = [];
    $count = count($temArr);
    for ($i = 0; $i < $count; $i++) {
        $pr[] = $temArr[$i]['prize'];
    }
    $res['no'] = $pr;
    return $res;
}
```

