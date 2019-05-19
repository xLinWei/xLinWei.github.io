# Simple Minimal Theme

<div align=center><img src=assets/img/web1.jpg width=60%></div>
<div align=center><img src=assets/img/web2.jpg width=60%></div>

This is an simple jekyll theme, you can quickly build your own page web. This Jekyll Theme refer to [Github Pages Themes:Minimal](https://github.com/pages-themes/minimal).  
If you like this theme, you can **Fork & Star**.

## Installation
To get this theme, follow those simple steps:
1. Fork this repository ;
2. Change the name of forked repository to \<_your github name_>.github.io ;
3. Configure:read the [Configuration Guild](./docs/Configuration.md).

## Previewing Locally
If you want to preview the theme locally, you can do this:
1. Clone down the theme's repository
2. cd into the theme's directory
3. Run script/bootstrap to install the necessary dependencies
4. Run bundle exec jekyll serve to start the preview server
5. Visit localhost:4000 in your browser to preview the theme

Note:The above steps should be executed in Git. If step5 reports error"Permission denied - bind for 127.0.0.1:4000", the reason is the port:4000 is occupied. you can input command: `netstat -aon | findstr "4000"` in _cmd_ window， and find which PID occupy the port:4000. And then disable it.

## Usage
If you want to add your blog, you just add your _.md_ file to _"docs/"_ . In addition, you should modify you content in index.md file.
