样式1
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

样式二

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