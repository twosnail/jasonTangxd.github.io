![Yelee](
http://i13.tietuku.com/404b8c63eb155793.jpg)

### Installation 安装主题

```
git clone https://github.com/MOxFIVE/hexo-theme-yelee.git themes/yelee
```

Change theme field in Hexo root's _config.yml file. 修改 Hexo 根目录对应配置文件。

```
theme: yelee
```

### Update 更新

```
cd themes/yelee
git pull
```

### git备份

```
次执行（此时当前分支应为hexo）
git add .;
git commit -m "...";
git push origin hexo；
```

### 发布网站
```
hexo g -d 发布网站到master分支上
```