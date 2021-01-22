使用PyTorch设置多线程（threads）进行数据读取（DataLoader），其实是假的多线程，他是开了N个子进程（PID都连着）进行模拟多线程工作，所以你的程序跑完或者中途kill掉主进程的话，子进程的GPU显存并不会被释放，需要手动一个一个kill才行，具体方法描述如下：

1.先关闭ssh（或者shell）窗口，退出重新登录

2.查看运行在gpu上的所有程序：
```
fuser -v /dev/nvidia*
```

3.kill掉所有（连号的）僵尸进程