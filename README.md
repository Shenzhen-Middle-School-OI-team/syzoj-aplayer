# SYZOJ APlayer

## 介绍

使用 [MetingJS](https://github.com/metowolf/MetingJS)，在 [syzoj](https://github.com/syzoj/syzoj) 首页中显示 [APlayer](https://github.com/MoePlayer/APlayer)！

## 安装步骤

假设 [syzoj](https://github.com/syzoj/syzoj) 网页端安装在 `/opt/syzoj/web` 中，下面的所有操作都在这个目录中。

### 1. 引入 css 和 js

进入 `/views/header.ejs`，在 `<head>` 中添加以下代码：

```ejs
<!-- imports -->
<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>
<!-- end imports-->
```

可以参考仓库中的 `header.ejs` 文件。

### 2. 修改首页 html 代码

进入 `/views/index.ejs`，找到这段代码：

```ejs
<% if (typeof links !== 'undefined' && links && links.length) { %>
    <h4 class="ui top attached block header font-content"><i class="ui linkify icon"></i>友情链接</h4>
    <div class="ui bottom attached segment">
        <ul style="margin: 0; padding-left: 20px; ">
            <% for (let link of links) { %>
            <li><a href="<%= link.url %>"><%= link.title %></a></li>
            <% } %>
        </ul>
    </div>
<% } %>
```

在这段代码上面添加：

```ejs
<% if (typeof syzoj.config.aplayer !== 'undefined' && syzoj.config.aplayer && syzoj.config.aplayer.use == true) { %>
    <!-- add aplayer in the side column-->
    <h4 class="ui top attached block header font-content"><i class="ui music icon"></i>音乐播放</h4>
    <div class="ui bottom attached segment">
        <meting-js 
                   server="<%= syzoj.config.aplayer.server %>"
                   type="<%= syzoj.config.aplayer.type %>"
                   id="<%= syzoj.config.aplayer.id %>">
        </meting-js>
    </div>
    <!-- end additions-->
<% } %>
```

可以参考仓库中的 `index.ejs` 文件。

### 3. 配置 [APlayer](https://github.com/MoePlayer/APlayer)

进入 `后台管理 - 配置文件`，或者直接编辑 `config.json`，在大括号中插入以下配置文件：

```json
"aplayer": {
  "use": true,
  "type": "playlist",
  "server": "netease",
  "id": "4950785127"
}
```

其中 `use` 代表是否显示，下面三个参数请参考 [MetingJS 的说明文档](https://github.com/metowolf/MetingJS/blob/master/README.md)。

## 结果展示

![result.png](https://i.loli.net/2020/07/03/SaRYCMbvmBjKG7d.png)