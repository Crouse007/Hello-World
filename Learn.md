# Shell
##### 从文件中读取数据
    #!/bin/bash
    # reading data from a file

    count=1
    cat test | while read line
    do
        echo "Line $count: $line"
        count=$[ $count + 1 ]
    done
    echo "Finished processing the file"
****
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
****
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
****
##### 捕捉脚本的退出
    #!/bin/bash

    # trapping the script exit

    trap "echo byebye" EXIT

    count=1
    while [ $count -le 5 ]
    do
        echo "Loop #$count"
        sleep 3
        count=$[ $count + 1 ]
    done
 *****
##### 移除捕捉
    #!/bin/bash

    # removeing a set trap

    trap "echo byebye" EXIT

    count=1
    while [ $count -le 5 ]
    do
        echo "Loop #$count"
        sleep 3
        count=$[ $count + 1 ]
    done
    #移除捕捉
    trap - EXIT
    echo "I just removed the trap"
    
****
