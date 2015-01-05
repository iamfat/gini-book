# 书写你的第一个应用

**Gini** 是一个 __基于模块组织的框架__. 每一个Gini App实际上只是一个最顶层的模块. 

### 建立一个应用
```bash
$ mkdir sample
$ cd sample
$ gini init
Shortname [sample]:
Name [Sample]:
Description [App description...]:
Version [0.1]:
Dependencies [N/A]:
$ _
```
这个操作会在这个`sample`的根目录生成一个 `gini.json`. 这个文件里面包括了你需要的所有模块信息
```json
{
    "id": "sample",
    "name": "Sample",
    "description": "App description...",
    "version": "0.1",
    "dependencies": ""
}
```
