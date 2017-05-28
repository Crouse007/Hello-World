# Shell
##### 反引号的使用
    #!/bin/bash
    #using the backtick character

    testing=`date`
    echo "The date and time are:$testing"
    
****

##### 通过反引号获得当前日期并生成唯一文件名.sh
    #!/bin/bash
    #copy the /usr/bin directory listing to a log file

    today=`date +%y%m%d`
    ls /usr/bin -al > log.$today
****
