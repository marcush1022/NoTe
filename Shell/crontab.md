#crontab 用于设置周期执行的命令, 并将其存放于crontab文件中;
#使用crontab可以在指定时间运行一个shell或几个linux指令;

`向crontab中添加命令:`
crontab -e
例: 0 5 * * * /root/bin/bkup.sh
每天早5点运行bkup.sh

`crontab -l`
显示所有cron命令;

`crontab文件格式:`
{minute}{hour}{day-of-month}{month}{day-of-week}{full-path-of-shell-script}
minute区间: 0~59
hour区间: 0~23
day-of-month: 0~31
month: 1~12
day-of-week: 1~7

`/dev/null 2>&1: 将标准输出和错误输出定向到/dev/null中, 即将产生的所有信息丢弃;`
例: 00 2 * * * cd /data/ubill/ubill-crontask-set0 && sh run_task.sh auto_pay/auto_delete_order_resource_value.sh > /dev/null 2>&1

`command > file 2>file 和 command > file 2>&1 的区别:`
1. command > file 2>file的含义是将所有的输出写到文件file中, `这样写stdout和stderr都直接送到file中, file会打开两次, stdout和stderr会相互覆盖, 相当于使用了两个使用file的管道FD1和FD2`;
2. command > file 2>&1将stdout直接写到file, stderr继承了FD1的管道后再写入file, file只打开了一次, 只用了一次管道FD1, 提高IO效率;
