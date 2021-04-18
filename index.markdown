---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

#layout: home


layout: default
title: Home
---
body:
            theme-base: theme-base-07 # 可选的主题色包括08~0f，见 <https://github.com/poole/lanyon>
            layout-reverse: true # 开启后sidebar在右边，反之左边
            sidebar-overlay: true # 开启后正文不随sidebar移动而移动
          append_to_head: # 通过内嵌html的方式引入并定制插件，删改前确定知道自己在做什么。定制插件的方式可以参考这篇文章 <https://wu-kan.cn/_posts/2019-01-18-基于Jekyll搭建个人博客/>
            - | #一些页面优化标签，看不懂可跳过
              <meta
                name="viewport"
                content="width=device-width,minimum-scale=1,initial-scale=1"
              />
              <meta
                http-equiv="content-type"
                content="text/html; charset=utf-8"
              />
              <link
                rel="alternate"
                href="/feed.xml"
                title="RSS"
                type="application/rss+xml"
              />
            - | # 网站小图标，可换成你自己的图片，改href中的部分即可
              <link
                rel="apple-touch-icon-precomposed"
                href="https://gravatar.loli.net/avatar/289efba375d63424de3c49569c446744?s=320"
              />
              <link
                rel="shortcut
                icon"
                href="https://gravatar.loli.net/avatar/289efba375d63424de3c49569c446744?s=32"
              />
            - | # 来自lanyon的页面样式，不要改
              <link
                rel="stylesheet"
                href="https://cdn.jsdelivr.net/combine/gh/poole/lanyon@v1.1.0/public/css/poole.min.css,gh/poole/lanyon@v1.1.0/public/css/lanyon.min.css,gh/poole/lanyon@v1.1.0/public/css/syntax.min.css"
              />
            - | # 用js引入fontawesome图标样式，功能更丰富
              <script
                async="async"
                src="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5.15.3/js/all.min.js"
              ></script>
            - | # 引入live2d看板娘！不需要可以把这一项都删掉
              <link
                rel="stylesheet"
                href="https://cdn.jsdelivr.net/gh/Dreamer-Paul/Pio@2.4/static/pio.min.css"
              />
              <script
                async="async"
                src="https://cdn.jsdelivr.net/combine/gh/Dreamer-Paul/Pio@2.4/static/l2d.min.js,gh/Dreamer-Paul/Pio@2.4/static/pio.min.js"
                onload='
                  let pio_container = document.createElement("div");
                  pio_container.classList.add("pio-container");
                  pio_container.classList.add("right");
                  pio_container.style.bottom = "-2rem";
                  pio_container.style.zIndex = "1";
                  document.body.insertAdjacentElement("beforeend", pio_container);
                  let pio_action = document.createElement("div");
                  pio_action.classList.add("pio-action");
                  pio_container.insertAdjacentElement("beforeend", pio_action);
                  let pio_canvas = document.createElement("canvas");
                  pio_canvas.id = "pio";
                  pio_canvas.style.width = "14rem";
                  pio_canvas.width = "600";
                  pio_canvas.height = "800";
                  pio_container.insertAdjacentElement("beforeend", pio_canvas);
                  let pio = new Paul_Pio({
                    "mode": "fixed",
                    "hidden": true,
                    "night": "for(let i=7; i<16; ++i) if(document.body.classList.contains(`theme-base-0`+i.toString(16))) { document.body.classList.remove(`theme-base-0`+i.toString(16)); document.body.classList.add(`theme-base-0`+((i-6)%9+7).toString(16)); break; }",
                    "content": {
                      "link": ["https:\/\/jekyll-theme-WuK.wu-kan.cn"],
                      "skin": ["要换成我的朋友吗？", "让她放个假吧~"],
                      "hidden": true,
                      "custom": [{
                        "selector": "a",
                        "type": "link",
                      }, {
                        "selector": ".sidebar-toggle",
                        "text": "打开侧边栏叭~"
                      }, {
                        "selector": ".effect-info",
                        "text": "哇，你发现了什么！"
                      }, {
                        "selector": "#sidebar-search-input",
                        "text": "想搜索什么呢？很多干货哦！"
                      }, {
                        "selector": "#toc",
                        "text": "这是目录~"
                      }, {
                        "selector": ".page-title",
                        "text": "这是标题~"
                      }, {
                        "selector": ".v",
                        "text": "评论没有审核，要对自己的发言负责哦~"
                      }]
                    },
                    "model": [
                      "https:\/\/cdn.jsdelivr.net/gh/imuncle/live2d/model/33/model.2018.bls-winter.json",
                      "https:\/\/cdn.jsdelivr.net/gh/imuncle/live2d/model/platelet-2/model.json",
                      "https:\/\/cdn.jsdelivr.net/gh/imuncle/live2d/model/xiaomai/xiaomai.model.json",
                      "https:\/\/cdn.jsdelivr.net/gh/imuncle/live2d/model/mashiro/seifuku.model.json",
                      "https:\/\/cdn.jsdelivr.net/gh/imuncle/live2d/model/Violet/14.json",
                      "https:\/\/cdn.jsdelivr.net/gh/xiaoski/live2d_models_collection/Kobayaxi/Kobayaxi.model.json",
                      "https:\/\/cdn.jsdelivr.net/gh/xiaoski/live2d_models_collection/mikoto/mikoto.model.json",
                      "https:\/\/cdn.jsdelivr.net/gh/xiaoski/live2d_models_collection/uiharu/uiharu.model.json"]
                  });'
              ></script>
            - | # 百度爬虫推送，http站点使用 http://push.zhanzhang.baidu.com/push.js
              <script
                src='https://zz.bdstatic.com/linksubmit/push.js'
                async="async"
              ></script>
            - | # 网站背景图片，分竖屏、宽屏；改链接即可，不想用可以把这一项全删掉；要换壁纸图片的话可把url内的部分换成你自己的，比如你放在 /assets/image/background.jpg，那就改成 url(/assets/image/background.jpg)
              <style>
                .wrap {
                  transition-property: width,background-size,transform;
                  transition-duration: .3s;
                  transition-timing-function: ease-in-out;
                  min-height: 100%;
                  display: inline-block;
                  background-size: 100% auto;
                  background-position: 0% 0%;
                  background-repeat: no-repeat;
                  background-attachment: fixed;
                  background-image: url(https://Mizuno-Ai.wu-kan.cn/pixiv/74559485_p1.webp);
                }
                @media (min-aspect-ratio: 2400/1850) {
                  .wrap {
                    background-image: url(https://Mizuno-Ai.wu-kan.cn/pixiv/71932901_p0.webp);
                  }
                }
                .sidebar-overlay #sidebar-checkbox:checked ~ .wrap {
                  width: calc(100% - 14rem);
                  background-size: calc(100% - 14rem) auto;
                  transform: translateX(14rem);
                }
                .layout-reverse.sidebar-overlay #sidebar-checkbox:checked ~ .wrap {
                  transform: translateX(0);
                }
              </style>
            - | # 网站字体，要换字体建议架梯子上<https://fonts.google.com/>挑选，再通过fonts.loli.net 加速引入
              <style>
                .sidebar,
                html,
                h1,
                h2,
                h3,
                h4,
                h5,
                h6 {
                  font-family: "Courier New", "Courier", "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft JhengHei", "Microsoft YaHei", monospace;
                }
              </style>
            - | # 网页标题使用加粗字号
              <style>
                h1,
                h2,
                h3,
                h4,
                h5,
                h6 {
                  font-weight: bold;
                }
              </style>
            - | #修复行内图片默认样式
              <style>
                img {
                  display: inline-block;
                  margin: 0;
                }
              </style>
            - | # 彩虹滚动条，仅对Chrome系浏览器生效
              <style>
                ::-webkit-scrollbar {
                  width: 3px;
                  height: 3px;
                }
                ::-webkit-scrollbar-thumb {
                  background-image: linear-gradient(45deg, Cyan 0%, Magenta 50%, Yellow 100%);
                }
              </style>
            - | # 选中字体颜色
              <style>
                ::selection {
                  color: White;
                  background: Black;
                }
              </style>
