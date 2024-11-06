1. 准备仓库和文件
在使用脚本之前，请确保你已经创建了一个 GitHub 仓库，并且已经把它克隆到本地。

假设你的 GitHub 仓库名称为 my-demo-repo，你已经在终端中运行以下命令来克隆仓库：

bash
复制代码
git clone https://github.com/<your-username>/my-demo-repo.git
cd my-demo-repo
这样你现在就在仓库目录下，并可以开始编辑文件。

2. 创建自动提交脚本 auto_commit.sh
在仓库目录中，创建一个文件 auto_commit.sh。可以用以下命令：

bash
复制代码
touch auto_commit.sh
然后用编辑器打开 auto_commit.sh（可以用 nano, vim 或其他编辑器）并粘贴以下代码：

bash
复制代码
#!/bin/bash

# 设置你要操作的文件名
FILENAME="demo-file.txt"

# 设置提交的次数
NUM_COMMITS=10

# 循环执行提交
for ((i=1; i<=NUM_COMMITS; i++))
do
    # 生成随机内容并添加到文件
    echo "Random change $RANDOM" >> $FILENAME
    
    # 添加更改到暂存区
    git add $FILENAME
    
    # 提交更改并生成提交消息
    git commit -m "Automated commit $i"
    
    # 推送更改到远程仓库
    git push origin main
    
    # 设置延迟时间（可选），避免提交过快
    sleep 1
done

echo "完成 $NUM_COMMITS 次自动提交"
3. 脚本的各部分详解
以下是脚本中各行代码的含义：

#!/bin/bash：这是脚本的声明，用来告诉系统该脚本使用 bash 解释器执行。
变量设置
FILENAME="demo-file.txt"：指定要修改的文件名（demo-file.txt）。如果文件不存在，可以提前创建：echo "Initial content" > demo-file.txt。
NUM_COMMITS=10：指定要自动提交的次数。这里设置为 10，你可以根据需要调整。
循环操作
for ((i=1; i<=NUM_COMMITS; i++))：定义一个循环，从 1 开始，到 NUM_COMMITS 的值为止。在这个例子中，NUM_COMMITS=10，所以循环会执行 10 次。
在循环内，每次都会执行以下操作：

生成随机内容并添加到文件

bash
复制代码
echo "Random change $RANDOM" >> $FILENAME
这里 $RANDOM 是一个系统变量，每次调用都会生成一个随机数，把它写入文件 demo-file.txt 中，这样文件内容会不断变化，便于提交。

添加更改到暂存区

bash
复制代码
git add $FILENAME
将文件更改添加到 Git 的暂存区，准备提交。

提交更改并生成提交消息

bash
复制代码
git commit -m "Automated commit $i"
使用 git commit 创建一个新提交，并指定提交信息为 Automated commit $i，其中 $i 表示当前循环的次数，确保每次提交的信息唯一。

推送更改到远程仓库

bash
复制代码
git push origin main
将提交推送到 GitHub 的 main 分支。如果你的分支名称不同（如 master），需要相应地修改这里。

延迟一秒（可选）

bash
复制代码
sleep 1
设置 1 秒延迟，防止提交太快导致网络问题。可以根据情况调整或删除这一行。

4. 赋予脚本执行权限
在终端中执行以下命令，赋予脚本执行权限：

bash
复制代码
chmod +x auto_commit.sh
5. 运行脚本
执行以下命令启动自动提交：

bash
复制代码
./auto_commit.sh
6. 运行结果
脚本运行后，终端会逐行显示每次提交的信息。脚本结束后，你的 GitHub 仓库中将多出 NUM_COMMITS 次提交记录，每次提交的信息会按照顺序编号。
# 可能用到的代码

textgit config user.name "username"
git config user.email "邮箱.com"
git config --global core.autocrlf true
chmod +x auto_commit.sh
./auto_commit.sh
