title: <% tp.file.title %>
date: <% tp.date.now("YYYY-MM-DD") %>
tags: [""]  # 标签，多个用逗号分隔
categories: [""]  # 分类
series: ""  # 系列文章（可选）
share: false  # 是否允许分享
draft: false  # false 表示发布状态，true 为草稿
dir: posts/<% tp.file.title %>  # 资源存放目录（如图片）
lastmod: <% tp.date.now("YYYY-MM-DD HH:mm:ss ZZ") %>  # 最后修改时间