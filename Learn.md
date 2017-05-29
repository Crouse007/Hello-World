# Shell
##### 结构化命令\错误的使用大于小于号
> 大于小于号必须转义，否则shell会将它们当做重定向符号而把字符串值当做文件名处理
> 大于小于号顺序和sort命令所采用的有所不同

		#!/bin/bash
		val1=baseball
		val2=hockey

		if [ $val1 > $val2 ]
		then
			echo "$val1 is greater than $val2"
		else
			echo "$val1 is less than $val2"
		fi
****

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
##### 使用getopts
> ：表示选项后面必须带有参数
> 例如：getopts ahfvc: option表明选项a、h、f、v可以不加实际值进行传递，而选项c必须取值。
> 使用选项取值时，必须使用变量OPTARG保存该值。
> OPTIND，反映下一个要处理的参数索引，初值是 1，每次执行 getopts 时都会更新。

		#!/bin/bash
		while getopts h:ms option
		do 
		    case "$option" in
		        h)
		            echo "option:h, value $OPTARG"
		            echo "next arg index:$OPTIND";;
		        m)
		            echo "option:m"
		            echo "next arg index:$OPTIND";;
		        s)
		            echo "option:s"
		            echo "next arg index:$OPTIND";;
		        \?)
		            echo "Usage: args [-h n] [-m] [-s]"
		            echo "-h means hours"
		            echo "-m means minutes"
		            echo "-s means seconds"
		            exit 1;;
		    esac
		done

		echo "*** do something now ***"
		
****

##### 使用getopts处理选项和参数
> ./a.sh -a -b 100 -c -d 100 200 300
> shift 3 前3个参数被销毁

	#!/bin/bash
	# processing options and parameters with getopts

	while getopts :ab:cd opt
	do
		case "$opt" in
		a) echo "Found the -a option";;
		b) echo "Found the -b option,with value $OPTARG";;
		c) echo "Found the -c option";;
		d) echo "Found the -d option";;
		*) echo "Unknown option: $opt";;
		esac
	done
	shift $[ $OPTIND - 1 ]
	count=1
	for param in "$@"
	do
		echo "Parameter $count: $param"
		count=$[ $count + 1 ]
	done
	
****

##### 反引号的使用
    #!/bin/bash
    #using the backtick character

    testing=`date`
    echo "The date and time are:$testing"
    
****

##### 通过反引号获得当前日期并生成唯一文件名
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
