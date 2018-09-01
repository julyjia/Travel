Travel

> Vue2.5开发去哪儿网App

## 效果截图

<figure class="half">
    <img src="http://ww1.sinaimg.cn/large/e45e4a9ely1fuu2bpalzfj208j0fa77n.jpg">
    <img src="http://ww1.sinaimg.cn/large/e45e4a9ely1fuu2cx41jfj208m0ffwet.jpg">
</figure>

<figure class="half">
    <img src="http://ww1.sinaimg.cn/large/e45e4a9ely1fuu2bzlp6rj208r0dngsj.jpg">
    <img src="http://ww1.sinaimg.cn/large/e45e4a9ely1fuu2fizxhmj208p0bywhk.jpg">
</figure>

## 技术选型

【前台数据处理/交互/组件化】

- `Vue`：用于构建用户界面的 MVVM 框架。它的核心是**响应的数据绑定**和**组系统件**
- `vue-router`：为单页面应用提供的路由系统。
- `vuex`：Vue 集中状态管理，在多个组件共享某些状态时非常便捷
- `better-scroll`：iscroll 的优化版，使移动端滑动体验更加流畅
- `vue-awesome-swiper`：实现首页轮播图

【前后台交互】

- `mock`数据：index.json，city.json，detail.json
- `ajax请求`：axios

【模块化】

- `ES6`：使用`import`和`export`在浏览器中导入和导出各个模块， 一个js文件代表一个js模块
- `babel`：JS转译的整合工具，支持模块化。

【自动化构建及其他工具】

- `webpack`：项目的编译打包
- `vue-cli`：Vue 脚手架工具，快速搭建项目
- `eslint`：代码风格检查工具，规范代码格式

【css预编译器】

- `stylus`：可以创建健壮的、动态的、富有表现力的CSS。

## 前端路由

![路由](http://ww1.sinaimg.cn/large/e45e4a9ely1fuu2aw2v2ij20d8083mx4.jpg)

## 项目vue组件



![vue组件](http://ww1.sinaimg.cn/large/e45e4a9ely1fuu2bczmukj20f50flq34.jpg)

## 收获

【流程及开发方法】

1. 熟悉一个项目的开发流程  
2. 学会组件化、 模块化、 工程化的开发模式  
3. 掌握使用 vue-cli 脚手架初始化 Vue.js 项目  
4. 学会模拟 json 后端数据， 实现前后端分离开发  
5. 学会 ES6+eslint 的开发方式  
6. 掌握一些项目优化技巧  
7. 掌握git的基本使用

【vue插件或第三方库】

1. 学会使用 vue-router 开发单页应用  
2. 学会使用 axios与后端进行数据交互  
3. 学会使用 vuex 管理应用组件状态  
4. 学会使用 better-scroll实现页面滑动效果  

【样式/布局/效果相关】

1. 学会使用 stylus 编写模块化的 CSS  
2. 学会使用 Vue.js 的过渡编写酷炫的交互动画  
3. 学会制作并使用图标字体  
4. 学会解决移动端 1px 边框问题  
5. 学会 flex 弹性布局  

## 项目代码初始化

1. 在index.html中

   ```html
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
   ```

2. 引入reset.css

   在main.js中引入

   ```javascript
   import 'styles/reset.css'
   ```

3. 为了解决移动端的1像素边框问题，引入border.css，使用的是css中的scale做到的

   ```javascript
   import 'styles/border.css'
   ```

4. 在移动端有300ms点击延迟问题，在某些机型浏览器上，当你使用click事件时，会延迟300ms，然后再执行，这时使用click事件体验不是很好，需要安装一个fastclick库,安装完后重启服务，npm run start

   然后在main.js中引入，`import fastClick from 'fastclick'`，然后在下面写`fastClick.attach(document.body)`，这样移动端300ms延迟问题就解决了

   ```javascript
   cnpm install fastclick --save
   ```

   ```javascript
   import fastClick from 'fastclick'
   ```

   ```javascript
   fastClick.attach(document.body)
   ```

5. iconfont

6. git add.

7. git commit -m 'project init'

8. git push

克隆项目是git clone 项目地址

推送项目

先是 `git add .`，然后`git commit -m 'project init'`,提交到本地仓库。

然后`git push`,就把本地代码推送到了线上。

## 实现页面

主要页面：首页、城市列表页、详情页。下面主要介绍各个页面开发的一些细节和开发过程中遇到的问题及解决方案。

### **首页**

主要包括header区域、iconfont引入、多区块轮播、热销推荐组件和周末游组件的开发。

#### header区域开发

安装stylus `npm install stylus --save`, 然后安装stylus-loader，`npm install stylus-loader --save`,安装好后重新启动项目，`npm run start`

新建一个componts文件夹放置小组件

```javascript
import HomeHeader from './components/Header'

export default {
  name: 'Home',
  components: {
    HomeHeader,
  }
}
```

```CSS
<style lang="stylus" scoped>
```

在苹果上是2倍像素

1rem = html font-size = 50px   43px就是86px 就是.86rem   就是86/100

#### iconfont 的使用和代码优化

在assets的styles中建立一个varibles.styl文件写css变量

```css
$bgColor = #00bcd4
$darkTextColor = #333
$headerHeight = .86rem
```

@代表src目录，如果在css中要用@找src，前面要加一个~

可在webpack.base.config.js中修改默认路径，改完后要npm run start 重启后生效

```
resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      'styles': resolve('src/assets/styles'),
    }
  },
```

#### 要使用变量可以

```css
@import '~styles/varibles.styl'
```

#### 轮播图组件

用vue-awesome-swiper做轮播图。

```
cnpm install vue-awesome-swiper@2.6.7 --save
```

在main.js中引入`import VueAwesomeSwiper from 'vue-awesome-swiper'`

```javascript
Vue.use(VueAwesomeSwiper)
```

**遇到的问题：**

使用浏览器调试工具中的3g网络浏览时，刷新页面时，轮播图下数字会挪动。

**解决方法：**

在swiper最外层加一个div（.wrapper）标签，实现宽高比设置padding-bottom，写在height里面是相对于父容器的高度，写在padding-bottom是相对于

```css
  .wrapper
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 31.25% //图片宽高比，宽度会相对高度自动撑开31.25
    .swiper-img
      width: 100%
```

或者可直接写为

```css
.wrapper
    width: 100%
    height: 31.25vw
    .swiper-img
      width: 100%
```

但存在浏览器兼容性问题。

也可以写成，但是存在兼容性问题

```
.wrapper
    overflow: hidden
    width: 100%
    height: 21.26vw
      .swiper-img
        width: 100%
```

样式的穿透，不受scoped限制，可进行如下书写：

```
.wrapper >>> .swiper-pagination-bullet-active
      background: #fff !important
```

#### 开发周末游组件

超出内容写省略号：

```
ellipsis()
  overflow: hidden
  white-space: nowrap
  text-overflow: ellipsis
```

```
@import '~styles/mixins.styl'
```

#### 使用axios发送ajax请求

发送ajax可以使用浏览器自带的fetch，或者vue-resource，或者现在vue官方推荐我们使用axios，可以实现跨平台的vue请求。如果在浏览器上，他可以帮助你发送xhr的请求，在node服务器上，他可以帮你发送http请求。

希望整个首页只发送一个ajax请求，就放在home.vue首页组件中发送比较好。把ajax写在mouted中。

首先加入

```
import axios from 'axios'
```

然后测试

```javascript
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  methods: {
    getHomeInfo () {
      axios.get('/api/index.json')
        .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc (res) {
      console.log(res)
    }
  },
  mounted () {
    this.getHomeInfo()
  }
}
```

在static文件夹中创建一个mock文件夹模拟接口数据。在static文件夹中创建mock文件夹，里面创建index.json文件。模拟后端接口。之所以把数据放在这个目录下是因为在整个工程中，只有static中的数据可以被外部访问到，所以只有把数据放到static目录下才能访问数据。如果并不想把这个文件提交到线上，可以在.gitignore中添加static/mock语句。那么在git提交的时候此文件夹就不会被提交到线上仓库和本地仓库。

在.gitignore中添加一项static/mock，那么此mock文件夹就不会被提交到线上仓库和本地仓库。

此时本地模拟地址写成

```javascript
getHomeInfo () {
      axios.get('/static/mock/index.json')
        .then(this.getHomeInfoSucc)
    },
```

使用proxy代理功能。是此处仍然用api路径。

要想get地址中写'/api/index.json'，就需要打开config文件夹，写如下配置。

```
module.exports = {
  dev: {

    // Paths fiddler charles
    assetsSubDirectory: 'static',
    assetsPublicPath: '/project',
    proxyTable: {
      '/api': { //在此配置
        target: 'http://localhost:8080'
        pathRewrite: { //加一个配置项，希望把路径做一个替换，就是一旦请求的地址是以api开头的，那么
            '^/api': 'static/mock' //就把他替换到本地的static/mock文件夹下，这个功能是Paths webpack-dev-server提供的
        }
      }
    },


```

将实现准备好的index.json文件放在在mock文件夹下。有个ret为true代表服务器正确的响应了请求。

注意在写json文件中，最后不能多逗号。

### 城市列表详情页

城市列表详情页面的开发，主要包含路由的配置，BetterScroll的使用，vuex实现数据共享，localStorage的使用等内容。

#### 路由配置

打开router中的index.js

```
import City from '@/pages/city/City'

Vue.use(Router)

export default new Router({
  routes: [{
    path: '/',
    name: 'Home',
    component: Home
  }, {
    path: '/city',
    name: 'City',
    component: City
  }]
})


```

创建city文件夹和组件

我们希望首页点击城市跳转到city页面，则在header.vue中在header-right外包裹一层`<router-link>`标签，加一个to，意思是点击这个跳转到city路径。

```
<router-link to="/city">
    <div class="header-right">
      {{this.city}}
      <span class="iconfont arrow-icon icon-xiala"></span>
    </div>
  </router-link>

```

这是发现城市和下拉变成了绿色，原因是`<router-link>`是加a标签，其默认是绿色。可设置颜色#fff。

点击箭头，回到首页

```
<router-link to="/">
      <div class="iconfont header-back icon-fanhui"></div>
</router-link>

```

#### BetterScroll 的使用

https://github.com/ustbhuangyi/better-scroll

第三方包better-scroll，他是iscoll的封装，但是使用起来比iscoll更友好。

首先安装此包cnpm install better-scroll --save。在官网上看他的使用结构。

```
<div class="list" ref="wrapper">

import BScroll from 'better-scroll'

mounted () {
    this.scroll = new BScroll(this.$refs.wrapper)
  }

```

#### 页面的动态数据渲染

创建分支city-ajax

ajax请求一般放在页面最外面一个组件，这样发送一次请求就可获取页面上所有内容了。

先在组件中引入axios，然后在mouted中调用方法，方法定义在methods中。

```
import axios from 'axios'

methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      console.log(res)
    }
  },
  mounted () {
    this.getCityInfo()
  }
```

父组件

```
<city-list :cities="cities" :hot="hotCities"></city-list>

data () {
    return {
      cities: {},
      hotCities: []
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    }
  },
  mounted () {
    this.getCityInfo()
  }
}

```

子组件

```
props: {
    cities: Object,
    hot: Array
  },

```



```
<div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div
            class="button-wrapper"
            v-for="item of hot"
            :key="item.id"
          >
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>

```



v-for双重循环内部可以用innerItem of item，这时这里的父级key设置等于key可以，父级key值和子级key值一样也没有关系。只要这级key值不重复就行，和下一级重复不要紧。

双重循环写法

```
<div
        class="area"
        v-for="(item, key) of cities"
        :key="key"
      >
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div
            class="item border-bottom"
            v-for="innerItem of item"
            :key="innerItem.id"
          >
            {{innerItem.name}}
          </div>
        </div>
      </div>

```



字母表ajax获取修改

父组件

```
<city-alphabet :cities="cities"></city-alphabet>

```

子组件

```
<li class="item" v-for="(item, key) of cities" :key="key">{{key}}</li>

 props: {
    cities: Object
  }
```



```
<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list
      :cities="cities"
      :hot="hotCities"
      :letter="letter"
    ></city-list>
    <city-alphabet
      :cities="cities"
      @change="handleLetterChange"
    ></city-alphabet>
  </div>
</template>

<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>

```

#### 兄弟组件数据传递

创建分支city-components

要实现点击哪个字母就显示相关城市

首先初始代码

```
<template>
  <ul class="list">
    <li
      class="item"
      v-for="(item, key) of cities"
      :key="key"
      @click="handleLetterClick"
    >
    {{key}}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  methods: {
    handleLetterClick (e) {
      console.log(e.target.innerText)
    }
  }
}
</script>

```

希望把这个传递给list组件，要做一个兄弟组件的传值，兄弟组件的传值，之前讲过bus总线传值的方法，除此之外，如果比较简单，可以通过子传父，父在传另一个子的方式传值。

```
alphabet.vue（子） --> city.vue（父） --> list.vue（另一子）

```

alphabet.vue（子）

```
<li
      class="item"
      v-for="(item, key) of cities"
      :key="key"
      @click="handleLetterClick"
    >
    {{key}}
    </li>

methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)//通过this.$emit向外触发事件，事件名为change，事件携带的内容为e.target.innerText
    }
  }

```

 city.vue（父）

```
<city-alphabet
      :cities="cities"
      @change="handleLetterChange"
    >
    </city-alphabet>
    

methods: {
    handleLetterChange (letter) {
      console.log(letter)
    }
  },
    

```

完成子传父

再进行父传子

父组件

```
<city-list
      :cities="cities"
      :hot="hotCities"
      :letter="letter"
    >
    </city-list>

data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    handleLetterChange (letter) {
      this.letter = letter
    }
  }

```



list.vue（另一子）

```
 props: {
    cities: Object,
    hot: Array,
    letter: String
  },
  watch: { //利用监听器监听letter变化
    letter () {
      console.log(this.letter) //一旦letter变化就会执行这段代码
    }
  }

```

让其自动滚动到某个元素上

```
<div
        class="area"
        v-for="(item, key) of cities"
        :key="key"
        :ref="key"
      >
      
 watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
    }     
```

做在右侧字母表拖拽时，左侧城市列表也会滚动的效果.

构建一个名字为letters 的计算属性，数组里面大概是['A', 'B', 'C']的一个数组

根据当前手指触碰字母位置与A字母高度的差值，除以每个字母的高度，就可以知道当前是第几个字母了，然后去取这个字母触发change事件就可以

alphabet.vue（子）

```
<template>
  <ul class="list">
    <li
      class="item"
      v-for="item of letters"
      :key="item"
      :ref="item"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
      @click="handleLetterClick"
    >
    {{item}}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false
    }
  },
  methods: {
    handleLetterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        const startY = this.$refs['A'][0].offsetTop  //获取元素顶部高度
        const touchY = e.touches[0].clientY - 79
        const index = Math.floor((touchY - startY) / 20)
        if (index >= 0 && index < this.letters.length) {
          this.$emit('change', this.letters[index])
        }
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

```

#### 列表性能优化

当我们手指在字母表上面上下滑动的时候，下面代码就会执行，但是如果代码这么写，性能是比较低的。

```
handleTouchMove (e) {
      if (this.touchStatus) {
        const startY = this.$refs['A'][0].offsetTop
        const touchY = e.touches[0].clientY - 79
        const index = Math.floor((touchY - startY) / 20)
        if (index >= 0 && index < this.letters.length) {
          this.$emit('change', this.letters[index])
        }
      }

```

首先`this.$refs['A'][0].offsetTop`值是固定的，而我们每次执行这个方法时，都会执行一次此计算，可以在data中再定义一个变量startY初始值为0，再写一个updated的钩子。

```
data () {
    return {
      touchStatus: false,
      startY: 0
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop 
  },

```

当你初次渲染alphabet.vue的时候，当alphabet.vue重新渲染的时候， updated生命钩子就会被执行，页面已经展示了城市列表的内容，这个时候获取`this.$refs['A'][0].offsetTop`值就没有任何问题了。

第二步性能优化是做一个函数节流，当鼠标在字母上来回移动的时候，move执行频率是非常高的，可以做一个节流限制一下函数执行的频率。先定义一个timer为null

```
data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  
   methods: {
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 79
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    }
  }

```

#### 搜索逻辑实现

创建分支city-search-logic

此处也用到了节流函数

```
<template>
  <div>
    <div class="search">
      <input
        v-model="keyword"
        class="search-input"
        type="text"
        placeholder="输入城市名或拼音"
      >
    </div>
    <div class="search-content">
      <ul>
        <li class="search-item border-bottom" v-for="item of list">{{item.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
  .search
    height: .72rem
    padding: 0 .1rem
    background: $bgColor
    .search-input
      box-sizing: border-box
      width: 100%
      height: .62rem
      padding: 0 .1rem
      line-height: .62rem
      text-align: center
      border-radius: .06rem
      color: #666
  .search-content
    z-index: 1
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    background: #eee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      background: #fff
      color: #666
</style>

```

搜索出来的页面无法滚动，借助betterscroll解决，借助两个生命周期钩子，

```
 <div class="search-content" ref="search">

import Bscroll from 'better-scroll'

mounted () {
    this.scroll = new Bscroll(this.$refs.search)
  }

```

这时候输入a，可以看到页面可以正常滚动了，这时候处理一些细节。这时如果把a取消掉，可以看到列表依然还在。这时可以额外加一个判断

```
watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) { //额外加一个判断
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },

```

当我们输入一段长字符串，底下没有匹配的就什么都不显示，这时可以增加一个li标签如下

```
<li class="search-item border-bottom" v-show="!list.length">
          没有找到匹配数据
        </li>

```

但是这时一开始没搜索时会显示 没有找到匹配数据，可以加一个`  v-show="keyword"`，这时候没值的时候就会隐藏，有值的时候才会显示

```
div
      class="search-content"
      ref="search"
      v-show="keyword"
    >

```

要尽可能避免在模板中写逻辑，加一个计算属性

```
<li class="search-item border-bottom" v-show="hasNoData">
          没有找到匹配数据
        </li>
      </ul>
      
      
 computed: {
    hasNoData () {
      return !this.list.length
    }
  },

```

#### Vuex实现数据共享

创建分支city-vuex

想实现点击城市列表城市时，首页显示的城市跟着变，这就要求首页和城市选择页面有一些共用的数据要共享。或者说城市选择页面的数据要传递给首页。那么如何传递？因为两个组件之间没有一个共用的父级组件，就没办法通过父级组件进行传递。之前讲过bus总线的概念，这里可以使用，但是使用起来比较麻烦。官方提供给我们一个工具vuex，是官方推荐的数据框架，vue只能承担视图层的内容，但我们有大量数据需要传递的时候，往往需要一个数据框架进行辅助，vuex就是这样一个数据框架。

安装

```
npm install vuex --save
```

在src下面创建一个store的文件夹，里面创建一个index.js的文件。

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    city: '北京'
  }
})


```

在main.js中引入store

```
import store from './store'
```

```
new Vue({
  el: '#app',
  router,
  store,
  components: { App },
  template: '<App/>'
})
```

首页的city数据是共享的，以前city数据是ajax从后台获取，现在我们需要把此数据在前端共享，去掉home.vue中的city相关数据。不需要外部传递进去，把city.json中city的数据去掉。我们想把公共数据北京显示出来办法。点击Header.vue，去掉props中的city，把` {{this.city}} `改为` {{this.$store.state.city}} `每个组件都可以使用这个`$store`是因为在创建根组件时把store传进去了。紧接着vuex创建才store会被派发到每一个子组件中。在每个组件中就可以用`this.$store`获取到store，state是我们的公用数据，他里面的city就是要获取的数据。这个时候公用数据里面的北京就会显示在页面上。

进入城市列表，这时候当前城市里面显示的值也应该是首页显示的城市。进入list.vue中，把当前城市的北京缓存

`{{this.$store.state.city}} `

紧接着要实现逻辑功能，希望点击热门城市的时候，公用城市也跟着发生变化，就是希望改变state，需要先调用action，然后调用mutations，进入list.vue给每个热门城市都绑定一个click事件，生命周期函数尽量写在最下面。

组件通过dispatch方法触发actions

```
handleCityClick (city) {
      this.$store.dispatch('changeCity', city)
    }

```

但是你创建store的时候并没有actions，这时候需要创建actions，里面要有一个一样的actions  changeCity，他是一个方法。

```
export default new Vuex.Store({
  state: {
    city: '北京'
  },
  actions: {
    changeCity (ctx, city) {
      console.log(city)
    }
  }
})

```

actions中接收到了传递过来的城市，他需要调用mutations来改变公用的数据，所以接下来要创建一个mutations，之所以actions里面接收一个上下文ctx，是因为他可以帮忙拿到commit方法，然后执行changCity这个mutations，传过去的内容是city，mutations接收的state是所有参数的公用数据

```
export default new Vuex.Store({
  state: {
    city: '北京'
  },
  actions: {
    changeCity (ctx, city) {
      ctx.commit('changeCity', city)
    }
  },
  mutations: {
    changeCity (state, city) {
		state.city = city
    }
  }
})

```

通过vuex我们非常方便的实现了首页和列表页的数据共享。

可以看到我们改变state过程中并没有任何的异步操作，而且这个操作非常简单，不是批量的数据操作，这时其实组件没必要去调用actions做一个转换，可以直接调用mutations就可以，所以可以删掉actions，在组件中不用dispatch，而是直接使用commit方法直接调用mutations.

同时在search.vue中加入handleCityClick 方法和事件，使得搜索时点击城市也是共享的。

编程式导航。在网页跳转有两种方式，一种是通过a标签的方式，另一种是通过js的window.location.href的方式。在vue中也一样，我们可以通过 `<router-link>` 标签形式做跳转，可可以通过js做js形式的页面跳转，在vue中用的是编程式导航的形式。他提供的`router.push(location, onComplete?, onAbort?)`就是帮我们做页面跳转的。

当我们城市被点击的时候，首先改变城市的内容，接着进行页面跳转，项目中使用vue-router，那么每一个组件中都有一个`$router`属性，这个属性有个push方法就可以做页面跳转。想要点击城市后跳转首页，就加入`this.$router.push('/') `

```
handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    }

```

这时，两个页面的联动就做完了。

#### Vuex的高级使用及localStorage

上节课把下面city写死了存在问题：选择了别的城市刷新后，页面还是北京。而实际当你访问一个网站时，下一次再访问，应该显示之前你选择的城市。

```
 state: {
    city: '北京'
  },

```

于是引入localStorage，可以帮助我们实现类似cookie的功能，实现本地存储。他的api比cookie更简单。

我们在index.js中做如下修改：

```
export default new Vuex.Store({
  state: {
    city: localStorage.city || '北京'
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
      localStorage.city = city
    }
  }
})

```

建立用localStorage时要包裹一个try catch，因为如果用户关闭了本地存储功能或者隐身模式，可能会导致浏览器抛出异常。

代码改为：

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
let defaultCity = '上海'
try {
  if (localStorage.city) {
    defaultCity = localStorage.city
  }
} catch (e) {}
export default new Vuex.Store({
  state: {
    city: defaultCity
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
      try {
        localStorage.city = city
      } catch (e) {}
    }
  }
})

```

实际上这部分代码应该分别拆分到state.js和mutations中去。

state.js

```
let defaultCity = '上海'
try {
  if (localStorage.city) {
    defaultCity = localStorage.city
  }
} catch (e) {}

export default {
  city: defaultCity
}


```

mutations.js

```
export default {
  changeCity (state, city) {
    state.city = city
    try {
      localStorage.city = city
    } catch (e) {}
  }
}


```

index.js

```
import Vue from 'vue'
import Vuex from 'vuex'
import state from './state'
import mutations from './mutations'

Vue.use(Vuex)

export default new Vuex.Store({
  state,
  mutations
})
```

这时候选择大于四位数的城市，发现页面出现问题。打开home下的conponents下的header.vue，对样式进行修正。header-right的宽度写死了，width改为min-width，如下

```
 min-width: 1.04rem
 padding: 0 .1rem
```

接下来进行代码优化，之前写的这一长串` {{this.$store.state.city}} `，vuex中给了更高级的api可以对代码进行优化。

```
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
```

mapState指的是把vuex中的数据映射到组件的computed属性中。我把city这个公用数据映射到名字叫做city的计算属性中，做好映射后，` {{this.$store.state.city}} `可直接写为` {{this.city}} `，

同样在list.vue中修改

```
computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
```

mapState中传入的内容可以是数组或者对象，上面的意思是我想把vuex中city这个公用数据映射到这个组件的计算属性里，映射后的名字叫做currentCity，上面就写成`{{this.currentCity}} `

同样里面也有mapMutations 

```
import { mapState, mapMutations } from 'vuex'

methods: {
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },

```

翻译一下：我们有一个mutation叫做changeCity，然后我把这个mutation映射到这个组件中，名字叫做changeCity的方法里，这时候如果要调用就可以改为

```
methods: {
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },

```

同时把search.vue中相应的也改过来。

getters的用法

```
export default new Vuex.Store({
  state,
  mutations,
  getters: {
    doubleCity (state) {
      return state.city + '' + state.city
    }
  }
})

```

在组件中

```
import { mapGetters } from 'vuex'

computed: {
    ...mapState(['city']),
    ...mapGetters(['doubleCity'])
  }
```

页面中用的时候`{{this.doubleCity}} `

state存放公共数据，actions中写异步方法，mutations中放的是同步的一些数据改变。

getters的作用有点类似于vue中computed计算属性的作用。当我们需要根据state中的数据算出新的数据时，就可以使用getters，这样可以避免数据的冗余。

module，当我们遇到非常复杂的业务场景，比如说在管理后台系统的时候，经常会有很多功能数据在vuex中进行存储，如果我们把所有的mutations数据都放在mutations.js这个文件中，这个文件会变得非常大。这个时候可以借助mudule对文件数据进行拆分。

创建不同的模块，A模块存储A模块相关的数据操作，B模块存储B模块相关的数据操作。然后在创建store的时候我们队store中的数据进行整合。通过module写代码可以使我们的代码具备更好的可维护性。因为当前项目只有city一个公用数据，就没必要把代码进行拆分。

使用keep-alive优化网页性能

city-keepalive

打开network，点击xhr，可以发现：每一次路由切换的时候，ajax都会发送请求，每次切换页面，这个组件都会被重新渲染，所以mouted这个钩子都会重新执行，那么这个ajax数据就会被重新获取。

每次都重新获取性能很低，解决方法：

在app.vue的router-view上包裹keep-alive标签，意思是，路由被加载过一次后，可以把路由内容放到内存中，下一次再进这个路由的时候不需要重新渲染这个组件，不需要重新执行钩子函数，只需要从内存中把以前的内容拿出来显示的可以了。

还存在的问题是，当我们选择北京时，底下应该选择北京的相关内容，选择别的城市，应该显示对应城市相关内容。这时候打开home.vue，之前发axios

```
getHomeInfo () {
      axios.get('/static/mock/index.json')
        .then(this.getHomeInfoSucc)
    },

```

我们在home.vue中改正

```
import { mapState } from 'vuex'

 computed: {
    ...mapState(['city'])
  },
  
  methods: {
    getHomeInfo () {
      axios.get('/api/index.json?city=' + this.city)
        .then(this.getHomeInfoSucc)
    },

```

修改后可以看到请求的参数部分带有城市参数。

当我们用keep-alive时，组件里面会多个生命周期函数activated

```
 mounted () {
    console.log('mouted')
    this.getHomeInfo()
  },
  activated () {
    console.log('activted')
  }

```

可以看到第一次刷新页面mouted和activated会执行，当我们点击城市列表后再回来，就只有activated会执行。当页面重新显示的时候，activated一定会执行。可以在页面每一次重新显示的时候判断当前城市和上一次的城市是否相同，如果不相同，就再发一次ajax请求，就可以解决之前遇到的问题。

```
data () {
    return {
      lastCity: '',
      swiperList: [],
      iconList: [],
      recommendList: [],
      weekendList: []
    }
  },
  
  
  mounted () {
    this.lastCity = this.city
    this.getHomeInfo()
  },
  activated () {
    if (this.lastCity !== this.city) {
      this.lastCity = this.city
      this.getHomeInfo()
    }
  }

```

这时，当你在城市列表直接返回首页城市未改变时，不会重新发送ajax请求，只有你城市改变了，回首页则会重新发送ajax请求。但是无论回到列表页多少次，列表页都不会再发city.json请求了，他只会发送一次请求。

### 网站详情页

景点详情页面的开发，主要包含渐隐渐显Header组件的制作，公用组件的拆分，路由参数的获取与处理，以及递归组件的使用。在详情页面，我们还会对通用动画效果进行代码封装。

#### 动态路由和banner布局

创建detail-banner分支。

做详情页，在recommend.vue的li外加一层`<router-link to="/detail"> `，发现颜色变化了，可以换一种写法，直接把li标签改为`<router-link to="/detail"> `，然后加一个tag="li"，

```
<ul>
      <router-link
        tag="li"
        class="item border-bottom"
        v-for="item of list"
        :key="item.id"
        :to="'/detail' + item.id"
      >
        <div class="item-img-wrapper">
          <img class="item-img" :src="item.imgUrl">
        </div>
        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
          <button class="item-button">查看详情</button>
        </div>
      </router-link>

```

配置动态路由

```
import Detail from '@/pages/detail/Detail'


export default new Router({
  routes: [{
    path: '/',
    name: 'Home',
    component: Home
  }, {
    path: '/city',
    name: 'City',
    component: City
  }, {
    path: '/detail/:id', //动态路由，id是会动态变化
    name: 'Detail',
    component: Detail
  }]
})


```

渐变效果

```
background-image: linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, .8))

```

#### 公用图片画廊组件拆分

创建common文件夹放gallary组件

#### 并在webpack.base.conf.js下配置路径

```
resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      'styles': resolve('src/assets/styles'),
      'common': resolve('src/common')
    }
  }

```

swiper分页的使用以及样式

```
<template>
  <div class="container">
    <div class="wrapper">
      <swiper :options="swiperOptions">
      <swiper-slide>
        <img class="gallary-img" src="http://img1.qunarzz.com/sight/p0/201404/23/04b92c99462687fa1ba45c1b  5ba4ad77.jpg_600x330_bf9c4904.jpg"/>
      </swiper-slide>
      <swiper-slide>
        <img class="gallary-img" src="http://img1.qunarzz.com/sight/p0/201404/23/04b92c99462687fa1ba45c1b5ba4ad77.jpg_800x800_70debc93.jpg"/>
      </swiper-slide>
      <div class="swiper-pagination"  slot="pagination"></div>
      </swiper>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CommonGallary',
  data () {
    return {
      swiperOptions: {
        pagination: '.swiper-pagination',
        paginationType: 'fraction'
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  .container >>> .swiper-container
    overflow: inherit
  .container
    display: flex
    flex-direction: column
    justify-content: center
    z-index: 99
    position: fixed
    left: 0
    right: 0
    top: 0
    bottom: 0
    background: #000
    .wrapper
      height: 0
      width: 100%
      padding-bottom: 100%
      .gallary-img
        width: 100%
      .swiper-pagination
        color: #fff
        bottom: -1rem
</style>


```

下面连个observer意思是这个swiper插件只要监听到这个元素或者父级元素发生dom结构变化时候，自己会自动自我刷新一次，就能解决swiper宽度计算问题

```
data () {
    return {
      swiperOptions: {
        pagination: '.swiper-pagination',
        paginationType: 'fraction',
        observeParents: true,
        observer: true
      }
    }
  }

```



#### 实现Header渐隐渐显效果

创建detail-header分支

```
<template>
  <div>
    <router-link
      tag="div"
      to="/"
      class="header-abs"
      v-show="showAbs"
    >
      <div class="iconfont header-abs-back icon-fanhui"></div>
    </router-link>
    <div
      class="header-fixed"
      v-show="!showAbs"
      :style="opacityStyle"
    >
      <router-link to="/">
        <div class="iconfont header-fixed-back icon-fanhui"></div>
      </router-link>
      景点详情
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .header-abs
    position: absolute
    left: .2rem
    top: .2rem
    width: .8rem
    height: .8rem
    line-height: .8rem
    border-radius: .4rem
    text-align: center
    background: rgba(0, 0, 0, .8)
    .header-abs-back
      color: #fff
      font-size: .4rem
  .header-fixed
    z-index: 2
    position: fixed
    top: 0
    left: 0
    right: 0
    height: $headerHeight
    line-height: $headerHeight
    text-align: center
    color: #fff
    background: $bgColor
    font-size: .32rem
    .header-fixed-back
      position: absolute
      top: 0
      left: 0
      width: .64rem
      text-align: center
      font-size: .4rem
      color: #fff
</style>


```

#### 对全局事件的解绑

使用`  window.addEventListener('scroll', this.handleScroll)`,组件是绑定在了全局的window对象上，在别的组件页面滚动也会触发事件。还提供了一个deactivated，是页面即将被隐藏，或页面被替换为新的页面时触发。

所以增加一段：

```
 deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }

```

将代码提交到之前的分支上，

git status

git branch

git add.

git commit -m 'fix problem'

git push

git checkout detail-header

git merge master

git push

#### 使用递归组件实现详情页列表

detail-list

递归组件就是在我组件的自身去调用这个组件自身，一个组件调用自己的时候，可以通过自己的名字来使用自己。如果自身有children，那我就把children当做list再传给我自己。做一个递归的循环。

```
<template>
  <div>
    <div
      class="item"
      v-for="(item, index) of list"
      :key="index"
    >
      <div class="item-title border-bottom">
        <span class="item-title-icon"></span>
        {{item.title}}
      </div>
      <div v-if="item.children">
        <detail-list :list="item.children"></detail-list>
      </div>
    </div>
  </div>
</template>

```

使用ajax动态获取详情页面数据

detail-ajax

注意当你访问某一id景点时候，需要获取该景点对应的数据，所以每次请求希望把这个id带给后端，而这个id是动态路由的参数，你在router中定义的动态路由，会把id存在id的动态变量中，在我们页面上就可以写：

```
methods: {
    getDetailInfo () {
      axios.get('api/detail.json?id=' + this.$route.params.id)
    }
  }

```

但是这样拼接参数比较麻烦，可以换一种写法：

```
methods: {
    getDetailInfo () {
      axios.get('api/detail.json?id=', {
        params: {
          id: this.$route.params.id
        }
      })
    }
  }

```



```
methods: {
    getDetailInfo () {
      axios.get('api/detail.json', {
        params: {
          id: this.$route.params.id
        }
      }).then(this.handleGetDataSucc)
    },
    handleGetDataSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        console.log(data)
      }
    }
  }

```



```
<div class="">
    <detail-banner
    :sightName="sightName"
    >

    </detail-banner>

data () {
    return {
      sightName: '',
      list: []
    }
  },

handleGetDataSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.sightName = data.sightName
      }

```

现在还存在问题：进去首页点别的景点，并没有重新取数据，此处和之前首页原理一样，因为detail页面通过keepalive做了缓存，所以mounted只会执行一次，如果想每次重新进页面都发送一次ajax请求的话，就必须配合使用一个activated这样一个生命周期钩子。这里换一种方式解决这个问题，打开app.vue组件，这里所有页面都用了keep-alive做了缓存，假设我想让详情页面不去做缓存，可在此处加一个exclude为组件的名字。

```
<keep-alive exclude="Detail">
      <router-view/>
    </keep-alive>

```

这样详情页面就可以始终拿到对应id内容了。

思考：每个组件里面的name是干嘛用的？

至少有三个用途：

1. 当我们做递归组件的时候会用到
2. 在页面上相对某个页面取消缓存的时候
3. vue开发者工具中显示组件的名字就取决于你name给的什么名字

这里还存在问题：拖动多个页面之间会互相影响。解决这个问题：

打开vue-router官网，左侧滚动行为目录，只需要复制这样一段代码：

```
scrollBehavior (to, from, savedPosition) {
  return { x: 0, y: 0 }
}

```

到代码的路由部分。

```
export default new Router({
  routes: [{
    path: '/',
    name: 'Home',
    component: Home
  }, {
    path: '/city',
    name: 'City',
    component: City
  }, {
    path: '/detail/:id',
    name: 'Detail',
    component: Detail
  }],
  scrollBehavior (to, from, savedPosition) {
    return { x: 0, y: 0 }
  }
})

```

意思是每次做路由切换的时候，都要先进入显示的页面，x轴初始位置为0，y轴初始位置也为0，也就是让页面切换的时候始终回到最顶部。

#### 在项目中加入基础动画

detail-animation

显示图片轮播组件的时候，做一个渐隐渐显的动画效果 。

在common下创建fade文件夹。

fade.vue

```
<template>
  <transition>
    <slot></slot>
  </transition>
</template>

<script>
export default {
  name: 'fade'
}
</script>

<style lang="stylus" scoped>
  .v-enter, .v-leave-to
    opacity: 0
  .v-enter-active, .v-leave-active
    transition: opacity .5s
</style>

```

在页面中使用，在banner.vue中引入FadeAnimation 

```
<fade-animation>
      <common-gallary
        :imgs="bannerImgs"
        v-show="showGallary"
        @close="handleGallaryClose"
      >
      </common-gallary>
    </fade-animation>


import FadeAnimation from 'common/fade/FadeAnimation'

components: {
    CommonGallary,
    FadeAnimation
  }

```

`common-gallary `会作为插槽的形式插入到fade-animation组件中，fade-animation组件中的slot代表的就是`common-gallary `，而我们在`common-gallary `外部加入了动画效果，当我们对`common-gallary `进行展示和隐藏的时候，就会有一个渐隐渐显的动画效果 。

## 项目的联调，测试与发布上线

本章将以公司级别项目的要求，给大家讲解当项目开发完成后，开发人员进行联调，测试，及发布的详细流程，同时点出过程中可能遇到的问题及修复方案。另外，还会给大家补充讲解异步组件的知识点，通过使用异步组件，我们可以大幅提高大型项目的首屏速度。

### 项目前后端联调

前后端联调时会删掉static中的mock文件夹，在config文件夹中修改index.js中

```
module.exports = {
  dev: {

    // Paths fiddler charles
    assetsSubDirectory: 'static',
    assetsPublicPath: '/project',
    proxyTable: {
      '/api': { //在此配置
        target: 'http://localhost:8080'
        pathRewrite: { //加一个配置项，希望把路径做一个替换，就是一旦请求的地址是以api开头的，那么
            '^/api': 'static/mock' //就把他替换到本地的static/mock文件夹下，这个功能是Paths webpack-dev-server提供的
        }
      }
    },


```

改为后台服务器端口，80端口，如果使用的http协议，80可以省略不写

```
module.exports = {
  dev: {
    // Paths 
    assetsSubDirectory: 'static',
    assetsPublicPath: '/project',
    proxyTable: {
      '/api': { //可以把前端api这个地址的请求代理转发给任何后端服务器，从而非常方便的实现前后端的联调
        target: 'http://localhost:80'
      }
    },


```

当你改变了config文件时，需要重启前端服务器。真实的公司项目中，上面的localhost地址可能需要改为ip地址，因为可能是跑在别人的电脑，或者外网。

记住如果是使用vue项目的前后端联调，就不需要使用fiddler charles这样的工具了。只需要使用proxyTable这个配置项把需要请求的后端地址写在这里就可以了。

### 真机测试

如果是windows操作系统，打开命令行，运行ipconfig，获取当前机器的ip地址，找到inet内网后的ip地址。

比如是192.168.1.105，那么在地址栏输入192.168.1.105:8080和访问localhost:8080是应该是一个页面，我们访问192.168.1.105:80是可以访问后端的php端口的，这里无法访问192.168.1.105:8080原因是我们前端的项目是通过webpack dev server启动的，webpack dev serve默认不支持通过ip的形式进行页面的访问，所以我们需要把他默认的配置项进行修改，打开项目，在根目录中找到文件package.json，我们每次执行npm run start或者npm run dev的时候，本质上是运行"webpack-dev-server --inline --progress "，也就是当我们启动一个webpack-dev-server，如果我们想要webpack-dev-server能够通过ip地址被访问的话，只需要在前面在加上配置项“--host 0.0.0.0”就可以了。

```
"dev": "webpack-dev-server --host 0.0.0.0 --inline --progress --config build/webpack.dev.conf.js",


```

这个时候，我们再通过ip地址192.168.1.105:8080访问我们的网站就可以了。这个只要手机和电脑在同一个局域网内，就可以使用手机输入192.168.1.105打开网页了。

存在一个bug，就是拖动abcd的时候，整个屏幕会跟着上下滚动，可以解决：

Alphabet.vue文件加一个事件修饰符：

```
 @touchstart.prevent="handleTouchStart"
```

如果手机是安卓的可能访问时有白屏，产生的原因是：

情况一：可能手机浏览器默认不支持promise这个东西，解决这个问题，需要安装第三方包cnpm install babel-polyfill --save。

在main.js中引入

```
import 'babel-polyfill'
```

情况二：是webpack dev server的问题。

### 打包上线

当我们做vue项目上线时，首先我们要在打开命令行，运行命令npm run build后，vue脚手架会自动对项目文件进行打包编译，形成浏览器可以直接运行的代码，同时这个代码也会是压缩后的代码。稍等一会，完成后命令行中就会显示build complete。这个时候在项目目录中就会多出一个dist的文件夹。这个目录的代码就是我们最终会上线的代码。

接着把dist目录拿出来，会吧这个目录给后端的同学。后端的同学会把这部分代码放到后台的服务器上。

可以找到php服务器的根路径，在应用程序的XAMPP中有一个htdocs，这个位置就是后台服务器的根路径，这个时候把前端生成的代码dist文件夹中的index.html和static放到htdocs中就行。

这个时候我们到浏览器输入localhost后回车，实际访问的是后端的服务器。后端的服务器已经有了前端的代码，所以他默认会把index.html页面显示出来，同时index.html上又引入了我们打包生成的css和js文件，那么整个前端的代码就可以在后端的服务器上完美的运行起来了。同时后端的服务器上还有后端提供的接口。我们就把前端的代码融合到后端的项目了。再把整个后端的项目上线，那么我们的项目也就完成了。

这是最简单的一个流程：

npm run build =》 dist目录 =》给到后端开发人员 =》扔到htdocs目录下，就可以了

如果你希望你最后dist目录下的文件最后放到htdocs中的project文件夹下运行时，那么就需要打开前端代码进行修改，打开traval，打开config里面的index.js后，在最底部可以看到最底部有个build配置项，里面有个 assetsPublicPath，把'/'替换成'project'，也就是我打包的项目要运行在后端的project目录下，改好后，关闭服务器，打开命令行，重新运行npm run build进行打包，打包完成后，可以把dist目录改为project，然后放到htdocs中。再打开浏览器进入locahost/project回车，就可以看到我们的项目页面。

```
build: {
    // Template for index.html
    index: path.resolve(__dirname, '../dist/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../dist'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
```

### 异步组件实现按需加载

生成的dist目录下有index.html，这里就是我们前端代码的一个入口html文件，还有一个static文件夹，里面有css文件夹（有一个css.map文件，是一个sourcemap文件，目的是帮助我们调试被压缩过后的css代码，他的意义不是特别的大，只是帮助我们在项目开发做调试的时候来使用，真正打包在线上有用的文件其实是这个css文件，这个css文件其实就是我们所有页面要用到的css文件，当你做webpack打包的时候，他会把所有的css样式打包到这里），js文件夹（里面有用的文件是app.js，manifest.js，vendor.js，manifest.js是webpack打包生成的一个配置文件，我们不关心里面的代码，vendor.js里面放的是各个组件公用的代码，app.js中放的是我们项目各个页面的业务逻辑代码）

我们打开浏览器用打开locoalhost/project，访问页面后打开network，选择js可以看到，里面就有app.js，manifest.js，vendor.js三个js文件，实际上当我们将异步组件，主要讲的是app.js文件，他放的是所有页面的业务逻辑。当你访问首页的时候，app.js会把首页，城市详情页等所有的代码都进行了加载，当我们的项目变得越来越大的时候，页面变得越来越多，app.js会变得越来越大，有可能到最后一个app.js打包完成后多大1mb以上，这个时候就需要我们通过异步组件对我们的代码进行优化。

当你在开发环境运行项目时，访问的localhost: 8080端口，他里面只有app.js一个文件，没有manifest.js和vendor.js。他一次一个app.js把所有代码都加载了，你再去其他的页面，他不会发同样的js请求了，我们现在要改成按需加载使用我们的组件，就是如果你访问首页，就只加载首页的代码，访问详情页，就加载详情页的代码，这样需要什么就加载什么，就是异步加载，可以打开项目router文件夹中的index.js文件，以前都是直接引入组件后直接用组件，现在我们可以把这部分代码全部改成异步形式，这个时候这样写：

```
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)

export default new Router({
  routes: [{
    path: '/',
    name: 'Home',
    component: () => import ('@/pages/home/Home')
  }, {
    path: '/city',
    name: 'City',
    component: () => import ('@/pages/city/City')
  }, {
    path: '/detail/:id',
    name: 'Detail',
    component: () => import ('@/pages/detail/Detail')
  }],
  scrollBehavior (to, from, savedPosition) {
    return { x: 0, y: 0 }
  }
})
```

这样就把以前同步加载代码编程异步加载的形式。

这样做访问哪个页面就只加载那一个页面逻辑就行了。不会加载其他页面的逻辑。

当我们的app.js文件很小的时候，不需要做异步的拆分，因为当你访问下一个页面，会请求下一个页面代码，会多一次http请求，http请求耗时，远比你首页多加载一些js代码代价要高。这个时候就不建议对app.js进行拆分，使用异步组件了。只有在app.js文件非常大的时候才要考虑对app.js文件进项拆分，使用异步加载代码。

不仅仅在路由中可以使用这种异步的形式，只要是我们的vue组件，都可以进行异步的加载，比如在首页home.vue中，举个例子

```
Components: {
    HomeHeader: () => import('./components/Header')
}
```

就是首页中异步加载header组件。因为现在app.js非常的小，这样使用反而会降低页面性能，只有当项目很庞大，app.js达到了几MB时，至少是1MB时，我们才需要使用异步加载组件。

## 安装与运行

```
git clone https://github.com/julyjia/Travel.git

cd Travel

npm install //安装依赖

npm run dev //服务端运行 访问 http://localhost:8080

npm run build  //项目打包 
```