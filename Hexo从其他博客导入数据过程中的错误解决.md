

title: title
title: Hexo从其他博客导入数据过程中的错误解决
date: 2013-10-07 07:23:40
categories:
- 技术点滴
tags:
- hexo

---

导入了RSS之后，使用generate报错

\`\`\`
/usr/local/lib/node\_modules/hexo/node\_modules/yamljs/bin/yaml.js:1298
tinuationIndent = 1 + /^-((s+)(.+?))?s\*$/.exec(this.currentLine)[2].length;
	                                                                  ^
TypeError: Cannot read property 'length' of undefined
	at Object.YamlParser.getNextEmbedBlock (/usr/local/lib/node_modules/hexo/node_modules/yamljs/bin/yaml.js:1298:77)
	at Object.YamlParser.parse (/usr/local/lib/node_modules/hexo/node_modules/yamljs/bin/yaml.js:1170:37)
	at Object.Yaml.parse (/usr/local/lib/node_modules/hexo/node_modules/yamljs/bin/yaml.js:240:15)
	at Object.YAML.parse (/usr/local/lib/node_modules/hexo/node_modules/yamljs/bin/yaml.js:357:21)
	at module.exports (/usr/local/lib/node_modules/hexo/lib/util/yfm.js:23:23)
	at /usr/local/lib/node_modules/hexo/lib/plugins/processor/post.js:85:14
	at /usr/local/lib/node_modules/hexo/node_modules/async/lib/async.js:422:17
	at /usr/local/lib/node_modules/hexo/node_modules/async/lib/async.js:416:17
	at Array.forEach (native)
	at _each (/usr/local/lib/node_modules/hexo/node_modules/async/lib/async.js:32:24)
\`\`\`

根据[这篇文章](https://github.com/tommy351/hexo/issues/118)的描述，出现这种情况的原因在于某些导入的rss里面出现了空tag，就是一个横线+空格后面啥都没有。应对的办法是将`/usr/local/lib/node_modules/hexo/node_modules/yamljs/bin/yaml.js`其中1298行那一句

\`\`\`
continuationIndent = 1 + /^-((s+)(.+?))?s\*$/.exec(this.currentLine)[2].length;
\`\`\`

修改成为

\`\`\`
var obj = /^-((s+)(.+?))?s\*$/.exec(this.currentLine)[2];
if (obj != undefined) 
	 continuationIndent = 1 + obj.length;
}
\`\`\`

就可以了。