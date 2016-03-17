---
title: 测试demo
categories: git
date: 2016-03-17 13:40:55
timestamp:
catAlias:
tags: [测试]
keywords:
description: 测试使用
---

# Sublime Text 2 MarkDown preview #

A simple ST2 plugin to help you preview your markdown files.

Preview the current md file in your web browser.

### Installation :

 - you should use [sublime package manager][3]
 - use `cmd+shift+P` then `Package Control: Install Package`
 - look for `MarkdownPreview` and install it.

## Usage :
Pma
 - use `cmd+shift+P` then `MarkdownPreview` to launch a preview
 - or bind some key in your user key binding, using a line like this one:
   `{ "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser"} },`
 - once converted a first time, the output HTML will be updated on each file save

### Uses :

 - [python-markdown][0] for markdown parsing
 - [clownfart markown.css][1] for markdown styling

The code is available at github [https://github.com/revolunet/sublimetext-markdown-preview][2]

Licence MIT : [http://revolunet.mit-license.org][4]

 [0]: https://github.com/waylan/Python-Markdown
 [1]: https://github.com/clownfart/Markdown-CSS
 [2]: https://github.com/revolunet/sublimetext-markdown-preview
 [3]: http://wbond.net/sublime_packages/package_control
 [4]: http://revolunet.mit-license.org

![Alt text](http://lnmp.org/images/screenshots/lnmp-install-success.jpg)

![Alt text](http://www.iplaysoft.com/plus/hotimg/tap.jpg "Optional title")




	def isNavigationUrl(url) :
	    '''
	    如果连接（a标签）的名字含有 导航 或者 地图 或者 href中含 sitemap 的
	    '''
	    try :
	        print url
	        htmlFile = urllib.urlopen(url)
	        content = parseToUTF8(htmlFile)
	    except UnicodeDecodeError :
	        print "error: " + url
	        return NON
	    except IOError :
	        return FAIL
	            
	    # 正则判断
	    regExp = '''(?is)<A[^>]*href[\s]*?=([^>]*?)>((?!</a).)*?(地图|导航).*?</A>'''
	    regExp2 = '''(?i)<a[^>]*href[\s]*?=([^>]*?)sitemap([^>]*?)>'''
	    if re.search(regExp, content) or re.search(regExp2, content) :
	        return SUCCESS

	    return EMPTY