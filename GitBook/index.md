# 常用命令

- 启动服务
  
  ```
  gitbook serve
  ```

- 停止服务
  
  ```
  control + c  //终端
  ```

- 编辑书籍
  
  ```
  gitbook build
  ```

# 插件

## 常用命令

启动服务

```
gitbook serve
```

安装插件

```
gitbook install
```

打包

```
gitbook build . docs
```

## 插件

1. [参考](https://segmentfault.com/a/1190000019806829)
2. [GitBook 悬浮目录](https://github.com/zq99299/gitbook-plugin-anchor-navigation-ex)
3. [GitBook 插件](https://www.jianshu.com/p/427b8bb066e6)
4. [GitBook 插件](http://gitbook.zhangjikai.com/plugins.html)

### 其他搭建方式

## docsify

与GitPage 搭配使用效果与GitBook类似

1. [github](https://github.com/docsifyjs/docsify)
2. [在线的示例](http://doc.zhangjikai.com/#/)

# 样式

## 样式1

```
{
    "title": "gitbook tutorial",
    "structure": {
        "readme": "README.md"
    },
    "plugins": [ 
        "-search",
        "github",
        "hide-element",
        "splitter", 
        "expandable-chapters",
        "tbfed-pagefooter",
        "back-to-top-button",
        "code",
        "page-toc-button" 
    ],
    "pluginsConfig": {
        "code": {
        "copyButtons": true
        },
          "hide-element": {
            "elements": [".gitbook-link"]
        },
        "github": {
            "url": "https://github.com/huangqiqiang/Book"
        },
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy huangqiqiang 2020",
            "modify_label": "该文件修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        },
        "theme-default": {
            "showLevel": true
        },
        "page-toc-button": {
            "maxTocDepth": 2,
            "minTocSize": 2
        }
    }
}
```

## 样式二

```
{
    "title": "gitbook tutorial",
    "structure": {
        "readme": "README.md"
    },
    "plugins": [ 
        "-search",
        "github",
        "hide-element",
        "splitter", 
        "expandable-chapters",
        "tbfed-pagefooter",
        "code",
        "anchor-navigation-ex" 
    ],
    "pluginsConfig": {
        "code": {
        "copyButtons": true
        },
          "hide-element": {
            "elements": [".gitbook-link"]
        },
        "github": {
            "url": "https://github.com/huangqiqiang/Book"
        },
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy huangqiqiang 2020",
            "modify_label": "该文件修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        },
          "anchor-navigation-ex": {
           "associatedWithSummary":true
        },
          "theme-default": {
          "showLevel": true,
           "mode": "float",
            "float": { 
            "floatIcon": "fa fa-navicon", 
            "showLevelIcon": false, 
            "level1Icon": "fa fa-hand-o-right", 
            "level2Icon": "fa fa-hand-o-right",
            "level3Icon": "fa fa-hand-o-right"
            }
        }
    }
}
```
