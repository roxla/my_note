# PR

1. fork GitHub上的目标仓库

2. https方式clone目标仓库

3. 与自己在GitHub上的Repository建立链接，*注意此处的SSH为自己的GitHub上的Repository的SSH*

   ```sh
   git remote add roxla git@github.com:roxla/vue3-baidu-map-gl.git
   ```

4. 从当前分支创建新的工作分支

   ```sh
   # 新建并切换到新建的分支 test
   git checkout -b test
   # 查看当前所在分支
   git branch
   ```

5. 修改clone下来的代码

6. 使用 git status 检查文件修改是否成功

7. 添加文件到缓存 

   ```sh
   git add 修改的文件
   ```

8. 提交文件

   ```sh
   # 单文件修改
   git commit -m "info"
   # 多个文件修改
   git commit -am "info"
   ```

9. 将提交的文件提交到远程的fork仓库

   git push roxla

10. ![](./assets/roxla_vue3-baidu-map-gl%20at%20test%20%E2%80%94%20Firefox%20Developer%20Edition%202024_2_6%2014_43_17.png)

    ![](./assets/roxla_vue3-baidu-map-gl%20at%20test%20%E2%80%94%20Firefox%20Developer%20Edition%202024_2_6%2014_46_11.png)