# “一生一芯”线上调试考核流程(测试版本)

本仓库用于“一生一芯”线上调试的考核。
你需要进行如下准备工作。

## 准备考核脚本（本仓库）

在上传你的仓库进行考核之前，请进行如下操作：
```bash
cd ysyx-workbench
git clone git@github.com:oscpu/ysyx-exam.git
rm -r ysyx-exam/.git
git add ysyx-exam
git commit -m "add exam file"
```

**注意：请遵从指示执行考核脚本，不要在ysyx-workbench中随意执行该脚本，
否则可能会对项目造成非预期的修改。**

## 上传你的仓库

请你将ysyx-workbench上传到一个公开的仓库。

## 考核环境自测

通过以下操作进行考核环境的自测，避免在考核时遇到环境配置相关的问题而花费额外的时间：
```bash
mkdir ~/exam-test
cd ~/exam-test
git clone 上一步上传仓库的URL ysyx-exam
cd ysyx-exam/ysyx-exam
source exam-init.sh # 此操作将会在当前shell中临时更新NEMU_HOME, AM_HOME, NAVY_HOME三个环境变量
cd nanos-lite
make ARCH=riscv64-nemu update
make ARCH=riscv64-nemu run
make ARCH=riscv64-npc run
exit # 退出当前shell, 避免继续使用考核环境中的环境变量
```

请检查上述过程是否能编译并在NEMU和NPC中运行仙剑，若否，请自行排查问题。
请注意，**使用绝对路径会导致你的项目无法在助教的环境中正确运行**,
请先自行修改，否则助教不会开展后续考核流程。
此外，上述过程会使用`exam_defconfig`的配置来编译NEMU，
你可以在自测时打开menuconfig查看并按需调整你的配置。

排查问题后，你需要更新上述仓库，然后重新进行自测。

自测成功后，可删除`~/exam-test`目录。

## 填写考核申请表

未发布

## 考核流程

1. 学生完成上述流程后，等待助教安排考核时间
1. 助教在代码仓库中注入3个错误，涵盖软件、硬件和环境（包括构建脚本和仿真环境等），
但不会在仙剑、libc、spike等学生没有进行直接开发的代码中注入错误，
也不会在Chisel代码中注入花哨的Scala语法糖
1. 助教通过`git init`重新创建工程，从而去掉`git diff`的记录
1. 助教每周安排线上调试的答辩（每人30分钟）
1. 每两名助教监考一位学生（负责注入错误的助教必须参加），强调答辩纪律，提醒答辩时间等
1. 学生答辩开始时，要求共享屏幕（整个桌面）并打开摄像头，助教录屏
1. 助教将注入错误的工程push到ysyx-exam仓库（即本仓库）的新分支（分支名称可随机命名），并把分支名称告知学生
1. 学生通过以下操作拉取考核代码：
  ```bash
  mkdir ~/exam-test
  cd ~/exam-test
  git clone -b 分支名称 git@github.com:OSCPU/ysyx-exam.git
  cd ysyx-exam/ysyx-exam
  source exam-init.sh # 此操作将会在当前shell中临时更新NEMU_HOME, AM_HOME, NAVY_HOME三个环境变量
  ```
1. 学生开始调试，助教开始计时
1. 考核结束时，助教停止录屏，学生退出腾讯会议
1. 答辩后，助教删除相应分支，并对学生进行评价，评价内容包括学生对项目细节的理解是否深入，对工具的掌握是否熟悉，调试方法是否清晰科学
