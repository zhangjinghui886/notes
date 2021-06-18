#### files

哪些文件需要在npm push的时候进行提交的文件

```json
{
  "files": [
    "lib",
    "src",
    "packages",
    "types"
  ]
}
```

#### main

入口文件

```json
{
  "main":"./src/index.js"
}
```

如果没有提供这个字段, 默认是项目根目录下的`index.js`

#### config

与script有关的命令的配置

#### script

一些可执行的命令

#### dependencies, devDependencies, peerDependencies

peerDependencies不依赖哪个包，但是前提是这个包安装了，比如element-ui 需要安装vue，但是vue并不是element-ui的代码依赖

