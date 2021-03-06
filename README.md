# scripts

## 權限設定  
指令：chomd

使用者owner/group/other三種  

各自有權限read/write/execute
(4/2/1)

EX:
-rwxrwx---
表示owner = rwx, group = rwx, other = ---  
owner = 4+2+1 = 7  
group = 4+2+1 = 7  
other = 0+0+0 = 0  

指令`chomd 770 檔名`  

## 參數  
$0：shell script名稱  
$1, $2...$n：第n個參數  
$@：輸入的參數清單  
$#：參數的總數  
$?:上一個指令的回傳直, 判斷指令執行是否成功, 成功即回傳0, 錯誤則會回傳錯誤代碼, 可以依據代碼查詢原因   

## Sort  
參數:  
-n:依數字大小排列  
-u:過濾重複的  

  
    
    
若引數為a b c, "$*"表示"a b c", "$@"表示"a" "b" "c"

## 指令  
**grep**：將含有關鍵字的一整行資料印出  
**awk**：將指定的欄位印出  

awk -F  
EX:  
awk -F, {'print $1'}  
以逗號作為分隔.印出第一筆資料

EX:  
A001 腳踏車 AEADDDEE9931  
A002 機車 FDEAEDFJK3394  
A003 火車 FJDKE3AK34940  
A004 超機車 FFJJEEE99300  
A005 飛機 AIRP33333900  
A006 坦克 TANK00000001  

`grep 車 formname`執行結果：  
A001 腳踏車 AEADDDEE9931  
A002 機車 FDEAEDFJK3394  
A003 火車 FJDKE3AK34940  
A004 超機車 FFJJEEE99300  

`awk {'print $2 "-" $3 '}`執行結果：  
腳踏車-AEADDDEE9931  
機車-FDEAEDFJK3394  
火車-FJDKE3AK34940  
超機車-FFJJEEE99300  
飛機-AIRP33333900  
坦克-TANK00000001 

**|**：pipe，導管  
A|B：把A的output作為B的input  

EX:  
`grep 車 formname | awk {'print $2 "-" $3'}`執行結果：  
腳踏車-AEADDDEE9931  
機車-FDEAEDFJK3394  
火車-FJDKE3AK34940  
超機車-FFJJEEE99300  

**搜尋取代**  
Linux：`sed –i ‘s/尋找目標字串/修改後的目標字串/g’ 檔案名稱`  
macOS：`sed –i '' ‘s/尋找目標字串/修改後的目標字串/g’ 檔案名稱` 

EX:
把檔案today20中的Doraemon改成洨叮噹  
`ed -i '' 's/Doraemon/洨叮噹/g' today20`  

"", ''差異  
單引號和雙引號解決變數之間有空格的問題  
``表示命令替換, 先執行``中的command, 並將結果assign給某變數, 以便使用  

**USERS=`who | wc -l`  
echo "Logged in user are $USERS"**  


## Rule of thumb: Use -a and -o inside square brackets, && and || outside.  

## It's important to understand the difference between shell syntax and the syntax of the [ command.  

## && and || are shell operators. They are used to combine the results of two commands. Because they are shell syntax, they have special syntactical significance and cannot be used as arguments to commands.  
## [ is not special syntax. It's actually a command with the name [, also known as test. Since [ is just a regular command, it uses -a and -o for its and and or operators. It can't use && and || because those are shell syntax that commands don't get to see.  
## But wait! Bash has a fancier test syntax in the form of [[ ]]. If you use double square brackets, you get access to things like regexes and wildcards. You can also use shell operators like &&, ||,  <, and > freely inside the brackets because, unlike [, the double bracketed form is special shell syntax. Bash parses [[ itself so you can write things like [[ $foo == 5 && $bar == 6 ]].


