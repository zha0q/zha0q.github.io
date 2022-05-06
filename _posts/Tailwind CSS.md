### Tailwind CSS

**运行**

`npx tailwindcss-cli build css/tailwind.css -o build/tailwind.css`

**安装**

`npm install -D tailwindcss postcss autoprefixer vite`

**生成配置文件**

`npx tailwind init -p`

```css
@tailwind base;
/* 基础层 */
@tailwind components;
/* 组件层*/
@tailwind utilities;
```

1. #####  基础层

   这是一个CSS重置 使用现代规范化对边距字体大小进行重置

2. ##### 组件层



#### **基础**

> 自定义class

#### **响应式布局：**

```css
/* 媒体查询 */
{
    "sm": "640px",
    "md": "768px",
    "lg": "1024px",
    "xl": "1280px",
    "2xl": "1536px"
}
```

`  class="sm: bg-blue-300"` 会在sm以上背景颜色变成蓝色300

`sm: object-cover` 将对象设置为始终以适当的横纵比显示的方式裁剪，不会失真

`sm: object-center`将对象始终置为中间

`class="hidden lg: block"`

### 伪类

支持伪类的前缀标签，以及可以和响应式一起使用





#### **变体variants**

##### 覆盖默认变体

任何直接在 `variants` 键下配置的变体将**覆盖**该插件的默认变体。

```js
// tailwind.config.js
module.exports = {
  variants: {
    backgroundColor: ['hover', 'focus'],
    borderColor: ['focus', 'hover'],
  },
}
```

当覆盖变体时，**变体会按照您指定的顺序生成**，因此列表末尾的变体将优先于列表开头的变体。

例如，在这里，`focus` 变体对 `backgroundColor` 功能类具有最高优先级，但 `hover` 变体对 `borderColor` 功能类具有最高优先级。

##### 启用额外变体

```js
// tailwind.config.js
module.exports = {
  variants: {
    // The 'active' variant will be generated in addition to the defaults
    extend: {
      backgroundColor: ['active']
    }
  },
}
```



### @layer 抽象为类

```css
@layer components {
    .btn {
        @apply
        inline-block px-3 py-5 rounded-lg
        shadow-lg uppercase tracking-widest bg-indigo-500
        text-white hover:bg-indigo-400 hover:-translate-y-0.5
        transform transition focus:ring-2 focus:ring-offset-2
        active:bg-indigo-700
    }
}
```

示例：为component编写btn类



### 自定义样式

```js
theme: {
    extend: {
        color: {
            brand: {
                light: "#3fbaeb",	//brand-light
                DEFAULT: "#0fa9e6",  //brand
                dark: "#0c87b8",	//brand-dark
            }
        }
    }
}
```



示例：自定义颜色

### 



### 针对生产环境

style.css文件有19万行代码，对生产环境并不友好，我们没有用到的代码也会被打包进来，所以还要做生产环境配置

> package.json

`"build": "cross-env NODE_ENV=production postcss css/style.css -o dist/style.css"`

> tailwind.config.js

`purge: [ './dist/**/*.html' ]`

这样build出的代码会按需打包了



