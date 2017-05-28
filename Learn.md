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

##### 定时执行脚本
> 只执行一次，一次后失效
    #!/bin/bash

    # testing the at command

    at -f 4.sh 22:10
 
##### 捕捉信号
|信号值|符号|行为|    |
|-----|----|----|----|
|2|SIGINT|进程终端|CTRL+C|
|9|SIGKILL|强制终端|
|15|SIGTEM|请求中断|
|20|SIGTOP|停止（挂起）进程|CRTL+D|

    #!/bin/bash

    # testing signal trapping

    trap "echo 'Sorry! I have trapped Ctrl-C'" SIGINT SIGTERM

    echo this is a test program

    count=1

    while [ $count -le 10 ]
    do
        echo "Loop #$count"
        sleep 5
        count=$[ $count+1 ]
    done
