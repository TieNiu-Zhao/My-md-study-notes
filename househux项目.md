# Nuxt3.js

nuxt 是一个提供前端（vue）与后端（nitro）的全栈 web 框架。

中文官网：https://nuxt.org.cn/

## Nuxt 的优势

- CSR / SPA 与 SSR / MPA

  单页面应用：SPA（Single Page Application），又称客户端渲染（CSR，Client Side Render）

  多页面应用：MPA（Multiple Page Application），又称服务端渲染（SSR，Server Side Render）

  单页面应用 - SPA 在查看源代码的时候看不到全部内容，而服务端渲染 - SSR 可以查看源代码，即**更好的 SEO**，针对异步 ajax 搜索引擎是抓不到的，因此 SSR 很重要，且**首屏加载速度更快**。

  SSR 的缺点是后续访问页面切换会增加服务器压力，高并发时更明显。

## Nuxt 项目结构

- 整体结构

  ```
  .nuxt
  node_modules
  assets					// 资源目录，放静态资源less、font等
  components			// 约定的组件位置
  composables			// 抽象出的组合式函数
  layouts					// 布局目录
  libs						// 通用库函数、工具函数
  pages						// 约定的路由文件位置
  plugins					// 全局使用的插件与自定义指令
  public					// 公共img资源等
  server					// 约定的服务端目录，用于后端开发
  services				// 接口
  stores					// 状态
  types						// 类型定义
  app.vue					// 核心页面 - 初始化挂载
  ```

- components / 组件

  在此文件夹下创建的组件**默认就是全局组件**，可以在其他地方直接调用，**无需导入**，在本项目中一般用于 pages 下。

- layouts / 布局目录

  例如主页的上半部分和底部，切换页面时还是会保留，这一部分就会被放在布局里。

- pages / 路由

  在此文件夹下创建的 vue 文件名，Nuxt 会自动生成 url 为此文件名的路由，一旦有 page 文件夹，app.vue 就不再是主页，主页会变成 pages 下的 index.vue。

- server / 服务端

  在此文件夹下可以有 api、router、middleware、plugin 等多个子文件夹。

---

# 项目

## 项目服务器

```bash
ssh root@8.217.83.40
cd /data
```

## 使用的 VScode 插件

- Code Spell Checker

  实时检查拼写错误。

- Eslint

  识别 Javascript 代码中的问题。

- Gitlens

  用于快速查看 git 注释与历史提交记录。

- I18n Ally

  用于增强国际化开发体验，可以通过鼠标悬停/右键菜单查看或编辑翻译。

- Prettier

  自动格式化代码，减少多人协作的代码风格的争论。保持整个项目中代码一致性。

- vue - Official

  vue 官方插件，提供 vue 语法高亮、代码补全等。

- WindiCSS

  内联 CSS 样式库，是 Tailwind CSS 的简易版本，编译更快。

---

## 项目结构

### 主页

1. 主页结构

   主页由大多数页面都有的顶部导航与底部广告，由布局完成

   Layouts/default.vue

   由 slot 替换中间内容。替换的部分在 pages 文件夹下。

   ```vue
   <template>
     <div class="relative min-h-100vh pb-56">
       <Header class="bg-white fixed"></Header>
       <div class="pt-24 pb-20 <md:pt-18 <xss:(pt-14)">
         <slot />
       </div>
       <Footer class="w-full absolute bottom-0 left-0" />
     </div>
   </template>
   ```

   pages/index.vue

   ```vue
   <HomeAdvantage/>       <!-- 您2024年最好的投资决策！ + 滚动展示区 -->
   <HomeSmallAdvantage/>	 <!-- 上个组件的移动端版本 -->
   <HomeNewProjectList/>  <!-- 所有楼盘 + 楼盘列表 -->
   <HomeRecommendList/>   <!-- 房源推荐 + 房源列表(PropertyPriceCard) -->
   <HomeMeetingIntro />   <!-- 黄金签证问询 - 一张城市图片 + 按钮与描述span -->
   <HomeIntro/>					 <!-- App 广告(左/右) + 为什么选择houselux + 经纪人团队 + 合作伙伴 -->
   <HomeIntroMobile/>     <!-- 上个组件的移动端版本 -->
   <HomeContact />				 <!-- 联系房产顾问 -->
   <Contact/>						 <!-- (浮层)您投资迪拜房产最关注的是什么？ -->
   ```


---

## 常见需求总结

### banner 图

以一个宽度为全屏的图为例，图片可能会非常大，如果只设置 w-full 会在缩放窗口时导致屏幕发生变形。

- **解决办法：**

  为图片定死宽高，一个都不能少，假如大屏幕宽度为2130，超过这个宽度才开启 w-full，即自动缩放效果。

  **重点在为容器添加 overflow-hidden w-full（如果占满宽度）**

  **并为图片添加 absolute、 top-1/2、left-1/2、marginTop 与 marginLeft**

  **使用 JS 在小于图片的宽度下 定死宽高为图片的宽高，超出部分裁剪**，在超出这个宽高才设置为屏幕宽高。

  ```vue
  <div class="relative overflow-hidden w-full">
    <ImageWrapper
      image="/imgs/pc-bg.png"
      objectFit="cover"
      class="absolute top-1/2 left-1/2 max-w-none"
      :style="{
        height: bannerStyle.bannerHeight + 'px',
        width: bannerStyle.bannerWidth + 'px',
        marginTop: `-${bannerStyle.bannerHeight / 2}px`,
        marginLeft: `-${bannerStyle.bannerWidth / 2}px`
      }"
    />
  </div>
  <script>
  // 这张图片是 3024 * 1472 像素，基本是 2:1
  const { width: windowWidth } = useWindowSize()
  const bannerStyle = computed(() => {
    let bannerHeight, bannerWidth, maskHeight, maskWidth
    if (windowWidth.value > 2130) {
      bannerWidth = windowWidth.value
      bannerHeight = bannerWidth / 2
    } else {
      bannerWidth = 2130
      bannerHeight = 1040
    }
    return { bannerWidth, bannerHeight }
  })
  </script>
  ```

---

### 瀑布流

1. 使用 grid 加少量 js 实现瀑布流

   **使用 grid-auto-rows: 1px; 设置隐式行，每行1px**

   **使用 grid-row-start: auto;** 与**动态添加 grid-row-end** 来规定每个 item 跨越多少行，即多少 px

   就可以实现瀑布流

   **例子：**

   ```html
   <style>
       .container {
           display: grid;
           grid-template-columns: repeat(2, 1fr);  /* 两列，每列均分, 2 可以换成auto-fit */
           grid-gap: 10px;
       }
       .item {
       		grid-row-start: auto;
       }
   </style>
   <body>
       <div class="container">
         <div class="item"></div>
         <div class="item"></div>
         <div class="item"></div>
         <div class="item"></div>
       </div>
     	<script>
     			const items = document.querySelectorAll(".item")
       		items.forEach((item) => {
         			const height = Number.parseInt(
           				getComputedStyle(item).getPropertyValue("height")
         			)
         			item.style.height = height + "px"
         			item.style.gridRowEnd = "span " + height		// 动态计算高度加在 grid-row-end
       		})
     	</script>
   </body>
   ```

   [可能的问题：图片是异步、懒加载，无法获取高度的情况。]

2. 使用纯 gird 实现瀑布流

   此方法目前还不行，只有火狐支持，还需要开设置。

   ```html
   <style>
       .container {
           display: grid;
           grid-template-columns: repeat(2, 1fr);     /* 两列，每列均分 */
           grid-gap: 10px;
       }
       .img {
       		width: 100%;
   				grid-template-rows: masonry;								/* 重点在这 */
       }
   </style>
   <body>
       <div class="container">
           <img src="" alt="">
           <img src="" alt=""> 
           <img src="" alt=""> 
           <img src="" alt=""> 
       </div>
   </body>
   ```

---

  ## 做过的特殊需求

### 吸顶组件

首先写一个自定义指令：

plugins / location-directive.ts

思路，给模块绑定 v-location-id，绑定的模块进入视口监听滚动行为，离开视口解绑滚动行为。

并且记录当前 activeId，获取当前模块距离顶部的距离，当这个模块可视且有区域位于吸顶下面，他就是被选中的模块，当 activeId 发生变化时**发送事件**。

```ts
import { defineNuxtPlugin } from '#app'
import { eventHub } from '~/libs'

let activeId: null | string = null

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.directive('location-id', {
    mounted(el, binding) {
      const ceilingTab = document.querySelector('.ceiling-tab')
      if (ceilingTab) {
        el.id = binding.value
        const height = ceilingTab.clientHeight
        el.handleScroll = () => {
          const { top, bottom } = el.getBoundingClientRect()
          if (parseInt(top) <= height && bottom > height && el.id !== activeId) {
            activeId = el.id
            eventHub.emit('activeIdChange', el.id)
          }
        }

        el.observer = new IntersectionObserver(
          (entries) => {
            entries.forEach((entry) => {
              if (entry.isIntersecting) {
                window.addEventListener('scroll', el.handleScroll)
              } else {
                window.removeEventListener('scroll', el.handleScroll)
              }
            })
          },
          {
            rootMargin: `-${height}px 0px 0px 0px`,
          }
        )
        el.observer.observe(el)
      }
    },
    unmounted(el) {
      if (el.observer) {
        el.observer.unobserve(el)
      }
      if (el.handleScroll) {
        window.removeEventListener('scroll', el.handleScroll)
      }
    },
  })
})
```

Components / CeilingTab.vue

思路：监听事件，改变当前选中的 activeID，点击 tab 的 item 触发屏幕滚动，屏幕滚动又会触发事件，事件又会触发修改 activeId，

监听 activeId 的变化，触发 tab 滚动，让活跃的 tab 总是能在中间区域。

```vue
<template>
  <ul
    ref="ceilingTab"
    class="ceiling-tab bg-white w-full overflow-x-auto sticky gap-2 top-0 z-3 flex justify-around items-center md:h-18 <md:h-15"
  >
    <li
      v-for="(item, index) in props.arr"
      :href="'#' + item.to"
      class="ceiling-tab-item px-2 py-2 h-full text-[#787878] whitespace-nowrap flex items-center gap-1 cursor-pointer <md:text-sm"
      :class="{ 'ceiling-tab-active': index === activeIndex }"
      @click="handleScroll(index)"
    >
      <component :is="item.icon" />
      {{ item.name }}
    </li>
  </ul>
</template>

<script setup lang="ts">
import { eventHub } from '@/libs'
const props = defineProps<{
  arr: Array<{
    to: string
    name: string
    icon: Component
  }>
}>()

const activeIndex = ref(0)
const ceilingTab = ref<null | HTMLElement>(null)
const { top } = useElementBounding(ceilingTab)
const isTabTop = computed(() => top.value < 1)

eventHub.on('activeIdChange', (id: string) => {
  activeIndex.value = props.arr.findIndex((item) => item.to === id)
})

const handleScroll = (id: number) => {
  windowScroll(id)
  // activeIndex.value = id
}

const tabScroll = (id: number) => {
  const tabContainer = ceilingTab.value
  const tabElement = ceilingTab.value?.children[id]
  if (tabElement && tabContainer) {
    const tabElementRect = tabElement.getBoundingClientRect()
    const tabContainerRect = tabContainer.getBoundingClientRect()
    const offsetLeft = tabElementRect.left - tabContainerRect.left
    const extraOffset = (tabContainerRect.width - tabElementRect.width) / 2
    tabContainer.scrollTo({
      left: tabContainer.scrollLeft + offsetLeft - extraOffset,
      behavior: 'smooth',
    })
  }
}
const windowScroll = (id: number) => {
  const element = document.getElementById(props.arr[id].to)
  if (element && ceilingTab.value) {
    const top = element.offsetTop - ceilingTab.value.clientHeight
    window.scrollTo({
      top: top,
      behavior: 'smooth',
    })
  }
}

watch(activeIndex, () => {
  tabScroll(activeIndex.value)
})

watch(isTabTop, () => {
  if (!isTabTop.value) {
    activeIndex.value = 0
  }
})

onMounted(() => {
  tabScroll(activeIndex.value)
})
</script>

<style scoped lang="less">
.ceiling-tab {
  -webkit-overflow-scrolling: touch;
  &::-webkit-scrollbar {
    display: none;
  }
  .ceiling-tab-item {
    position: relative;

    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      height: 2px;
      width: 0;
      background-color: black;
      transition: width 0.3s ease-in-out;
    }

    &.ceiling-tab-active::after {
      width: 100%;
    }
  }
}
</style>
```

坑1：

首先是自定义指令里的 `parseInt(top) <= height` ，这里如果不做 parseint，点击tab触发滚动触发 activeId 的改变可能 top 值有小数点，导致点击后明明滚动到对应模块了，但是最后一个事件没触发，指向选中模块的前一个模块。

坑2：

吸顶组件里的 `const isTabTop = computed(() => top.value < 1)`，这里因为有一个bug：当滑动过快时，滑倒最顶部，也就时未吸顶时，吸顶里的 activeID 本应该是0，但是选中1或者别的。所以想做一个是否吸顶的计算属性。

但是，如果是 top.value <= 0 的话，电脑端包括电脑上看移动端都是正常的，但是在 iphone 的 safari 上，这个 top 值一直在 0.34656 和 -0.36456 这样的小数波动，原因不明，猜测和手机刘海屏有关。