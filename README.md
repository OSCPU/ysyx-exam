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
特别地，上述过程会使用`exam_defconfig`的配置来编译NEMU，
你可以在自测时打开menuconfig查看并按需调整你的配置。

排查问题后，你需要更新上述仓库，然后重新进行自测。

自测成功后，可删除`~/exam-test`目录。

## 填写考核申请表

未发布

## 考核流程

未发布
