---

title: 利用Bash实现图片重命名以及上传git
tags: [git使用,gitcode,bash,图床]
categories: [412B-框架工具]
description: 进入文章

---

---

脚本:
```bash
#!/bin/bash  
# 字体样式
FONT_STYLE="\033[47;34m"
FONT_RES="\033[0m"
  
# 定义目标文件夹路径  
src_folder="V:\300_工作\310_待归档\image_handle"
target_folder="E:\Git仓库\GitCode\image"  
image_url_root="https://gitcode.net/qq_50848214/image/-/raw/master/"
# 切换到目标文件夹  
cd $src_folder  

# 提示用户输入前缀
echo  -e "${FONT_STYLE}[>_<]place input prefix :${FONT_RES}"
read pre
# 遍历文件夹中的所有文件
for file in *; do  
    # 筛选图片文件:只对图片文件进行操作
    if [[ "${file##*/}" =~ \.(jpg|jpeg|png|gif|JPG|JPEG|PNG|GIF)$ ]]; then    
        # 添加前缀
        mv "$file" "$pre-$file"
        # 移动文件到指定文件夹
        mv "$pre-$file" "$target_folder"
        # 输出图片url
        echo -e "\n$image_url_root$pre-$file\n"
    fi  
done

# 是否执行提交任务
echo -e "${FONT_STYLE}commit now?(y/n)${FONT_RES}"
read is_commit

if [ "$is_commit" == "y" ] ;then
    # 切换到指定目录
    cd $target_folder
    # 执行提交任务
    git add .
    git commit -m "$pre"
    git push origin master
    echo -e "${FONT_STYLE}[⚙️]commit end${FONT_RES}"
else
    
    echo -e "${FONT_STYLE}[>_<]if you want to commit again,place input 'y' >${FONT_RES}"
    read flag
    if [ "$flag" == "y" ] ;then
            # 切换到指定目录
            cd $target_folder
            # 执行提交任务
            git add .
            git commit -m "$pre"
            git push origin master
            echo -e "${FONT_STYLE}[⚙️]commit end${FONT_RES}"
    else
        echo -e "${FONT_STYLE}[╮(╯▽╰)╭]rename and move end,place commit yourself!${FONT_RES}"
    fi
fi

read end;
```



---

> Citation:
> - []()
> 
> References:
> - [简介 - Bash 脚本教程 - 网道 (wangdoc.com)](https://wangdoc.com/bash/intro)