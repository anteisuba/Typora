cat /etc/shells

echo $HOME  系统的根目录

echo $PATH 存储系统的查找路径

echo $SHELL 环境变量

echo $0  执行的脚本的名称

chmod +x game.ch	添加权限

ls -ltr game.sh

<img src="/Users/fulina/Library/Application Support/typora-user-images/截屏2024-07-19 13.30.47.png" alt="截屏2024-07-19 13.30.47"  />

 .bashrc	存储环境变量

source .bashrc

系统变量



shuf -i 1-10 -n 1	生成随机数1～10

echo $RANDOM	生成随机数

echo  $((RANDOM % 10 + 1))

​		等于 大于 小于 不等于

If [[ $guess -eq/lt/gt/ne $number ]]; then

​	echo "猜对了"

elif [[ ]]

Else











