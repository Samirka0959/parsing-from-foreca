# parsing-from-foreca
//here there is the programm writing by me (p.s it's my first program)
<!DOCTYPE html>

<html>
<head>
    <meta charset="utf-8">
    <title>Прогноз Погоды</title>
</head>
<body>

    <p><strong>Temperature Conversion</strong></p>
    <label for="text">Degree = Celsius</label>


    <form  action="prob_parsing.php"  method="get">
        <p>
            <select name="menu" size="1" onchange="this.form.submit()">
                <option <?php if($_GET['menu'] == 'kelvin'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="kelvin">Kelvin</option>
                <option <?php if($_GET['menu'] == 'celsius'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="celsius">Celsius</option>
                <option <?php if($_GET['menu'] == 'fahrenheit'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="fahrenheit">Fahrenheit</option>
                <option <?php if($_GET['menu'] == 'newton'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="newton">Newton</option>
                <option <?php if($_GET['menu'] == 'rankine'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="rankine">Rankine</option>
                <option <?php if($_GET['menu'] == 'deliesle'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="delisle">Deliesle</option>
                <option <?php if($_GET['menu'] == 'reaumur'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="reaumur">Reaumur</option>
                <option <?php if($_GET['menu'] == 'romer'){$deyishen =$_GET['menu']; ?>selected="selected"<?php } ?> value="romer">Romer</option>
            </select>
        <h4><?php echo $deyishen  ; ?></h4>
    </form>

<?php

header('Content-Type: text/html; charset=utf-8');
$db = mysql_connect('localhost',"root",""); //соединяется с бд
mysql_set_charset('utf8',$db);
# {Парсинг Start}
mysql_select_db("test" ,$db); // Иыбирает текущую бд с именем hava
$ch = curl_init(); //инициализация
curl_setopt($ch, CURLOPT_URL, 'http://www.foreca.ru/Azerbaijan/Baku?tenday ');
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
$res = curl_exec($ch);
curl_close($ch);
preg_match_all('/class\=\"h5"\>([^\<]*).*?strong>\S(\d+).*?strong>\S(\d+)/usi', $res ,$Links);
echo "</pre>";


/** Samira re date start */
$startdate = strtotime("Tuesday");
$enddate = strtotime("+10 days",$startdate);
while ($startdate < $enddate) {
    // echo date("M d", $startdate),"<br>";
    $startdate = strtotime("+1 day", $startdate);
}
/** Samira re date end */


/** GET or POST
 */

foreach ($Links[1] as $key => $name) {

    $var1 = $Links[2][$key];
    $var2 = $Links[3][$key];
    $x = reDate($name);

    /**     на пока ставлю такое условие которое потом сменю на то что должно быть в html        */

    $scale1 = "C";
 $scale2 =$deyishen;
//    print_r($scale2);
    /**        end        */
if($_GET['menu']=='celsius'){
     $yoxla =0;
}
    else
    {
     $yoxla=5;
    }

    if ($yoxla ==5) {
                switch ($scale1) {
            case "C":
                switch ($deyishen) {
                    case "fahrenheit":
                        c_change_f($var1, $var2, $x);
                        break;
                    case "kelvin":
                        c_change_k($var1, $var2, $x);
                        break;
                    case "rankine":
                        c_change_r($var1, $var2, $x);
                        break;
                    case "delisle":
                        c_change_d($var1, $var2, $x);
                        break;
                    case "newton":
                        c_change_n($var1, $var2, $x);
                        break;
                    case "reaumur":
                        c_change_re($var1, $var2, $x);
                        break;
                    case "romer":
                        c_change_ro($var1, $var2, $x);
                        break;
                                 }

                break;

            case "F":
                switch ($scale2) {
                    case "celsius":
                        f_change_c($var1, $var2, $x);
                        break;
                    case "kelvin":
                        f_change_k($var1, $var2, $x);
                        break;
                    case "rankine":
                        f_change_r($var1, $var2, $x);
                        break;
                    case "delisle":
                        f_change_d($var1, $var2, $x);
                        break;
                    case "newton":
                        f_change_n($var1, $var2, $x);
                        break;
                    case "reaumur":
                        f_change_re($var1, $var2, $x);
                        break;
                    case "romer":
                        f_change_ro($var1, $var2, $x);
                        break;
                }

                break;

            case "K":
                switch ($scale2) {
                    case "celsius":
                        k_change_c($var1, $var2, $x);
                        break;
                    case "kelvin":
                        k_change_f($var1, $var2, $x);
                        break;
                    case "rankine":
                        k_change_r($var1, $var2, $x);
                        break;
                    case "delisle":
                        k_change_d($var1, $var2, $x);
                        break;
                    case "newton":
                        k_change_n($var1, $var2, $x);
                        break;
                    case "reaumur":
                        k_change_re($var1, $var2, $x);
                        break;
                    case "romer":
                        k_change_ro($var1, $var2, $x);
                        break;
                }

                break;
            case "D":
                switch ($scale2) {
                    case "celsius":
                        d_change_c($var1, $var2, $x);
                        break;
                    case "kelvin":
                        d_change_k($var1, $var2, $x);
                        break;
                    case "rankine":
                        d_change_r($var1, $var2, $x);
                        break;
                    case "fahrenheit":
                        d_change_f($var1, $var2, $x);
                        break;
                    case "newton":
                        d_change_n($var1, $var2, $x);
                        break;
                    case "reaumur":
                        d_change_re($var1, $var2, $x);
                        break;
                    case "romer":
                        d_change_ro($var1, $var2, $x);
                        break;
                }

                break;


        }
    }

    else
    {
        preg_match_all('/class\=\"h5"\>([^\<]*).*?strong>(\+?\-?\d+).*?strong>(\+?\-?\d+)/usi', $res ,$Links);
        echo "<br>  $x      :   Max" . $Links[2][$key] . " : Min" . $Links[3][$key];
    }
}
/** Функции для Цельсии  */

function c_change_f($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1*9/5+32) . " : Min    " . ($c_var2*9/5+32);
}
function c_change_k($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1+ 273.15) . " : Min    " . ($c_var2+ 273.15);
}
function c_change_r($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1 + 273.15) * 9/5). " : Min    " . ($c_var2 + 273.15) * 9 / 5;
}
function c_change_d($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ((100-$c_var1) * 3 / 2). " : Min    " . (100-$c_var2)*3/2;
}
function c_change_n($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1 * 33 / 100)) . " : Min    " . ($c_var2*33/100);
}
function c_change_re($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1) * 4 / 5). " : Min    " . ($c_var2)*4/5;
}
function c_change_ro($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1* 21 / 40 + 7.5). " : Min    " . ($c_var2* 21 / 40 + 7.5));
}
/** Функции для Фахранхейт  */

function f_change_c($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 32) * 5 / 9) . " : Min    " . (($c_var2- 32) * 5 / 9);
}
function f_change_k($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1+ 459.67) * 5 / 9) . " : Min    " . (($c_var2+ 459.67) * 5 / 9);
}
function f_change_r($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1 + 459.67). " : Min    " . ($c_var2 + 459.67));
}
function f_change_d($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ((212-$c_var1)*5/6). " : Min    " . (212-$c_var2)*5/6;
}
function f_change_n($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1 - 32) * 11 / 60) . " : Min    " . (($c_var2 - 32) * 11 / 60);
}
function f_change_re($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 32) * 4 / 9). " : Min    " .(($c_var2- 32) * 4 / 9);
}
function f_change_ro($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 32) * 7 / 24 + 7.5). " : Min    " . (($c_var2- 32) * 7 / 24 + 7.5);
}
/** Функции для Келвина  */

function k_change_c($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1- 273.15 ). " : Min    " . ($c_var2 - 273.15);
}
function k_change_f($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1 * 9 / 5 - 459.67)) . " : Min    " . (($c_var1 * 9 / 5 - 459.67));
}
function k_change_r($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1* 9 / 5). " : Min    " . ($c_var2 * 9 / 5);
}
function k_change_d($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ((373.15 - $c_var1) * 3 / 2). " : Min    " . ((373.15 - $c_var2) * 3 / 2);
}
function k_change_n($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1 - 273.15) * 33 / 100) . " : Min    " . (($c_var2 - 273.15) * 33 / 100);
}
function k_change_re($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 273.15) * 4 / 5). " : Min    " .(($c_var2- 273.15) * 4 / 5);
}
function k_change_ro($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 273.15) * 21 / 40 + 7.5). " : Min    " . (($c_var2- 273.15) * 21 / 40 + 7.5);
}
/** Функции для Ранкине  */

function r_change_c($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 491.67) * 5 / 9 ). " : Min    " . (($c_var2- 491.67) * 5 / 9 );
}
function r_change_f($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1 - 459.67) . " : Min    " . ($c_var2 - 459.67);
}
function r_change_k($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1* 5 / 9). " : Min    " . ($c_var2 * 5 / 9);
}
function r_change_d($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ((671.67 - $c_var1) * 5 / 6). " : Min    " . ((671.67 - $c_var2) * 5 / 6);
}
function r_change_n($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1  - 491.67) * 11 / 60) . " : Min    " . (($c_var2  - 491.67) * 11 / 60);
}
function r_change_re($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 491.67) * 4 / 9). " : Min    " .(($c_var2- 491.67) * 4 / 9);
}
function r_change_ro($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (($c_var1- 491.67) * 7 / 24 + 7.5). " : Min    " . (($c_var2- 491.67) * 7 / 24 + 7.5);
}

/** Функции для Делисле  */

function d_change_c($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (100 - $c_var1 * 2 / 3 ). " : Min    " . (100 - $c_var2 * 2 / 3 );
}
function d_change_f($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1 - 459.67) . " : Min    " . ($c_var2 - 459.67);
}
function d_change_r($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (212 - $c_var1 * 6 / 5). " : Min    " . (212 - $c_var2 * 6 / 5);
}
function d_change_k($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (373.15 - $c_var1 * 2 / 3). " : Min    " . (373.15 - $c_var2 * 2 / 3);
}
function d_change_n($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (33 - $c_var1 * 11 / 50) . " : Min    " . (33 - $c_var2 * 11 / 50);
}
function d_change_re($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (80 - $c_var1 * 8 / 15). " : Min    " .(80 - $c_var2 * 8 / 15);
}
function d_change_ro($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (60 - $c_var1 * 7 / 20). " : Min    " . (60 - $c_var2 * 7 / 20);
}
/** Функции для Нютон  */

function n_change_c($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1* 100 / 32 ). " : Min    " . ($c_var2* 100 / 32 );
}
function n_change_f($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1  * 60 / 11 + 32) . " : Min    " . ($c_var2  * 60 / 11 + 32);
}
function n_change_r($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1 * 60 / 11 + 491.67). " : Min    " . ($c_var2 * 60 / 11 + 491.67);
}
function n_change_k($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1* 100 / 33 + 273.15). " : Min    " . ($c_var2* 100 / 33 + 273.15);
}
function n_change_d($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . (33 - $c_var1* 50 / 11) . " : Min    " . (33 - $c_var2* 50 / 11);
}
function n_change_re($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1* 80 / 33). " : Min    " .($c_var2* 80 / 33);
}
function n_change_ro($c_var1,$c_var2,$xx)
{
    echo "<br>  $xx      :   Max    " . ($c_var1* 35 / 22 + 7.5). " : Min    " . ($c_var2* 35 / 22 + 7.5);
}



function reDate($name)
{
    switch ($name) {
        case "Сегодня":
            return date('Y-m-d');
            break;
        case "Завтра":
            return date('Y-m-d', strtotime("+1 day"));
            break;
        default:
            preg_match('/\w+\s+(\d+)\.(\d+)/usi', $name, $results);
            return date('Y-m-d', strtotime(date('Y') . "-" . $results[2] . "-" . $results[1]));
            break;
    }
}

