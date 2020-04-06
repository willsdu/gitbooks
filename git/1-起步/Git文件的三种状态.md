## Git文件的三种状态

对于任何一种文件,在Git中都只有三种状态. 已提交(commited)，已暂存(staged)，已修改(modified). 已提交是安全的保存到Git库中了。已修改表示修改了Git中的某些文件，已暂存表示更新已经将更新放到下次要提交的清单中了。由此我们看到Git文件流转过程中的三个工作区域，Git的工作目录（working dir）, 暂存区域（stage area），本地仓库（git repo）
![Git文件的三种状态](../image/git/gitbasic_file_status.png)

一般的Git工作流程是
1. 在工作目录中修改某些文件
2. 将修改保存到暂存区域
3. 将暂存区域中的文件提交到本地仓库