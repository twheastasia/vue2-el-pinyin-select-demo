# vue2-el-pinyin-select-demo

# 需求
> 要求打出拼音字母就能搜索到内容，而不是汉字

# 实现
- 启用远程搜索，将filterable和remote设置为true，同时传入一个remote-method
- 利用第三方插件 pinyin-match 实现拼音比较
- 可以自定义多个待比较的字段名称

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
