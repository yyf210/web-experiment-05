# 实验5 Web前端技术推荐墙

## 作业内容
制作一个 Web 前端技术推荐墙页面，以卡片网格的形式展示 10 个前端相关技术，综合练习 HTML、CSS 与 JavaScript 的配合使用，重点掌握由数据驱动页面渲染、搜索过滤以及事件委托的写法。

## 功能说明
- 页面以卡片形式展示 10 个前端技术：HTML5、CSS3、JavaScript、Vue.js、React、Node.js、TypeScript、Webpack、Vite、Next.js
- 每张卡片包含技术图标、名称、一句话简介、难度等级（入门 / 进阶 / 高级）以及学习人数
- 顶部搜索框输入关键词时，根据技术名称或简介实时过滤并重新渲染卡片
- 点击任意卡片会弹出该技术的名称（使用事件委托实现，不需要给每张卡片单独绑定事件）
- 卡片悬停时有上浮和阴影加深的过渡动画效果

## 技术要点
1. HTML 结构：页面标题、搜索框 `<input>`、卡片容器 `<div id="techGrid">`
2. CSS 布局：
   - `display: grid` 配合 `auto-fill` 和 `minmax()` 实现响应式卡片网格
   - 卡片圆角、内边距、`:hover` 时 `transform: translateY()` 上浮与 `box-shadow`
3. JavaScript：
   - 用对象数组 `technologies` 统一存储 10 条技术数据
   - `map()` 遍历数组 + 模板字符串 `` ` `` 生成每张卡片的 HTML
   - `.join('')` 拼接字符串后通过 `innerHTML` 一次性渲染到页面
   - `filter()` + `includes()` 实现搜索关键词过滤
   - 监听搜索框 `input` 事件，输入时实时过滤并重新调用渲染函数
   - 事件委托：在父容器上监听 `click`，用 `e.target.closest('.tech-card')` 找到被点的卡片，再通过 `dataset.name` 取技术名

## 运行方式
直接用浏览器打开 `index.html` 即可，无需安装任何依赖。
在 VS Code 中推荐安装 **Live Server** 插件，右键 `index.html` → `Open with Live Server` 实时预览。

## 遇到的困难及解决方法
1. 卡片一开始排不成一行几个，查了 `grid` 的 `auto-fill` + `minmax()` 用法后实现了自适应列数。
2. 搜索时大小写不一致导致匹配不到，把关键词和技术名称都用 `toLowerCase()` 转小写后再比较解决。
3. 给每张卡片单独绑定点击事件太麻烦，后来改用事件委托，在父容器上监听一次点击，用 `closest()` 判断点的是不是卡片。
