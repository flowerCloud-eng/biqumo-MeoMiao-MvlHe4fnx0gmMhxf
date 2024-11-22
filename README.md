
## 前言


最近一直在使用 DjangoStarter 开发各种小项目，之前我是比较喜欢前后端分离的，后端用 Ninja API，前端 nextjs，开发起来也挺舒服的，交互体验也比较好。


不过我在网上冲浪的时候也了解到有 htmx 和 alpine.js 这些和 Django 很搭配的轻量级前端开发库，于是来新的玩具项目里尝试一下。*(本文先来试试 alpine.js，以最近正在开发的 LiveChat 聊天项目为例)*


Django template 这种后端渲染的开发方式是很方便的，不过有时候又需要在页面上做一些交互，老一点的项目会选择 jQuery，不过现在都停止维护了，我自然不可能选择这个；我用的比较多的是在页面里引入 vue.js 来做简单的交互，可以在一定程度上代替 jQuery，后面甚至还引入了 react，直接写 jsx，不过没有 webpack，直接引入 babel 来渲染，性能有点差。


参考：在 HTML 中引入 React 和 JSX


传统的前端框架如 React、Vue.js 和 Angular 功能强大，但对于一些中小型项目或简单的交互需求而言，它们可能显得过于笨重，学习曲线也较为陡峭。这就促使开发者们寻找一种既轻量又灵活的解决方案，能够在不引入大量复杂性的情况下实现动态交互。


**Alpine.js** 正是在这样的背景下诞生的。它是一款轻量级的 JavaScript 框架，旨在提供像 Vue.js 和 React 那样的声明式和可组合的特性，但却以极简的方式实现。Alpine.js 允许开发者直接在 HTML 模板中嵌入交互逻辑，无需复杂的构建工具和配置，即可实现丰富的动态效果。


## 关于 LiveChat 项目


其实这个项目用到的技术和上次的文章 [使用 Django\-Channels 实现 websocket 通信\+大模型对话](https://github.com) 里差不多，不过这个是多人聊天，不是和大模型对话。


项目还在开发中，放个简单的截图，现在实现了文本和语音聊天。


[![](https://img2024.cnblogs.com/blog/866942/202411/866942-20241121220603546-1156067591.png)](https://github.com)


## 关于 Alpine.js


Alpine.js 是一款轻量级的 JavaScript 框架，旨在为开发者提供一种简单、高效的方法来为网页添加交互功能。它受到了 Vue.js 的启发，但比 Vue.js 更加轻量和简洁。通过直接在 HTML 模板中嵌入简洁的指令，Alpine.js 允许开发者以最小的代码量实现动态交互，而无需引入庞大的框架或复杂的构建工具。


官网: [https://alpinejs.dev/](https://github.com):[MeoMiao 萌喵加速](https://biqumo.org)


### 发展背景


Alpine.js 由开发者 Caleb Porzio 在 2020 年推出，旨在填补 jQuery 和现代前端框架之间的空白。它结合了 jQuery 的直接性和 Vue.js 的声明式优点，提供了一种简洁而强大的工具来构建交互式网页。


### 核心特点


* **轻量级**：核心库大小仅为几 KB，不会显著增加页面的加载时间，非常适合对性能有严格要求的项目。
* **直观的语法**：使用类似于 Vue.js 的指令（如 `x-data`、`x-bind`、`x-on` 等），让开发者可以直接在 HTML 中编写交互逻辑，代码更直观易读。
* **易于集成**：无需配置复杂的构建工具或项目结构，只需引入 Alpine.js 的脚本文件，即可在任何现有项目中使用。
* **声明式渲染**：采用声明式编程风格，专注于描述界面应该“是什么”而非“如何”更新，大大简化了开发流程。
* **灵活性强**：适用于从简单的交互效果到中等复杂度的网页应用，能够满足大多数前端开发需求。


### 与其他框架的比较


#### 与 Vue.js 和 React 相比


* **体积更小**：Alpine.js 的大小仅为 Vue.js 和 React 的一个零头，更加轻量。
* **学习曲线平缓**：不需要学习复杂的框架概念或 JSX 语法，熟悉 HTML 和基本的 JavaScript 即可上手。
* **无需构建工具**：省去了 Webpack、Babel 等构建工具的配置，降低了项目的复杂度。


#### 与 jQuery 相比


* **现代化的编程方式**：Alpine.js 采用声明式渲染和数据绑定，避免了繁琐的 DOM 操作。
* **更好的可维护性**：代码结构清晰，逻辑与视图紧密结合，方便后期维护和迭代。


### 适用场景


* **小型项目或组件**：当项目不需要庞大的框架时，Alpine.js 是理想的选择。
* **现有项目的增强**：在传统的后端渲染项目中，想要添加一些动态交互，可以直接引入 Alpine.js，无需重构项目结构。
* **快速原型开发**：适合于需要快速验证想法或构建原型的场景。


## 安装


相比起需要 webpack 的 vue 和 react 项目，使用 alpine.js 非常容易，只需要在 HTML 里引入一个 js 文件就行了


### 使用 CDN


最简单的就是在页面底部添加 js 引用，直接用 jsdelivr CDN



```
<html>
    <head>
        ...
 
        <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js">script>
    head>
    ...
html>

```

### 使用本地资源


DjangoStarter 使用 npm 来管理前端资源，所以在 DjangoStarter 里整合会多一点步骤，不过也很简单的


首先使用 npm 来安装依赖



```
pnpm i alpinejs

```

npm 安装完是在 `node_modules` 里面，DjangoStarter 使用 gulp 来收集前端资源，所以接下来需要把 alpinejs 添加到 gulp 任务里。


编辑 `gulpfile.js`



```
// 使用 npm 下载的前端组件包
const libs = [
  {name: 'alpinejs', dist: './node_modules/alpinejs/dist/**/*.*'},
]

```

运行 gulp 任务收集静态资源



```
gulp move

```

这样 alpinejs 就在项目的 static 目录，可以在模板里引用了


编辑模板，引入静态资源，记得要加载 static 这个 template tag



```
{% load static %}

<html>
  <body>
    
    <script defer src="{% static 'lib/alpinejs/dist/cdn.min.js' %}">script>
    {% block extra_js %}{% endblock %}
  body>
html>

```

这样就搞定了，看似很复杂，实际上这些是在初始化项目的时候做的，接下来我也会把 alpinejs 和 htmx 整合到 DjangoStarter 新版本里面，所以这些步骤实际开发中是不需要重复去做的。


## 初始化


在需要使用 alpinejs 接管的元素添加 `x-data` 属性


就像这样



```
<div class="grid grid-cols-1 lg:grid-cols-4 gap-2 mb-4" x-data="chatApp()">
div>

```

然后 `chatApp()` 在 js 里定义



```
function chatApp() {
  return {
    messages: [],
    init() {
      // 初始化代码
    },
  }
}

```

代码已经简化过了，比较容易阅读


## 消息框


直接上代码会比较直观了解到我们是如何使用 alpinejs 开发的


后端渲染也能组件化，我编写了一个 `messages_container.html` 组件



```

<div x-ref="messages"
     class="flex-1 space-y-4 overflow-y-auto rounded-xl bg-slate-200 px-4 py-2 text-sm leading-6 text-slate-900 shadow-sm dark:bg-slate-900 dark:text-slate-300 sm:text-base sm:leading-7">
  <template x-for="item in messages">
    <div>
      <template x-if="item.role==='system'">
        <div class="text-center text-sm text-gray-500" x-text="item.message">div>
      template>
      <template x-if="item.role==='user'">
        <div class="flex flex-row-reverse items-start gap-2">
          <div class="p-2 h-12 w-12 rounded-full bg-blue-500 flex justify-center items-center">
            <i class="fa-solid fa-user text-white">i>
          div>
          <div class="flex min-h-[85px] rounded-b-xl rounded-tl-xl bg-slate-50 p-4 dark:bg-slate-800 sm:min-h-0 sm:max-w-md md:max-w-2xl">
            <template x-if="item.type==='text'">
              <p x-text="item.message">p>
            template>
            <template x-if="item.type==='audio'">
              <div class="flex flex-col gap-2">
                <div>Audio <span x-text="item.length">span>sdiv>
                <button type="button" @click="playAudio(item)"
                        class="px-3 py-2 text-xs font-medium text-center inline-flex gap-2 items-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800 ">
                  <i class="fa-solid fa-play text-white"> i>
                  play
                button>
              div>
            template>
          div>
        div>
      template>
      <template x-if="item.role==='ai'">
        <div class="flex items-start gap-2">
          <div class="p-2 h-12 w-12 rounded-full bg-blue-500 flex justify-center items-center">
            <i class="fa-solid fa-robot text-white"> i>
          div>
          <div class="flex rounded-b-xl rounded-tr-xl bg-slate-50 p-4 dark:bg-slate-800 sm:max-w-md md:max-w-2xl">
            <p x-text="item.message"> p>
          div>
        div>
      template>
    div>
  template>
div>

```

可以看到这里面使用几个不属于标准HTML的属性和元素


* x\-ref
* x\-for
* x\-if
* template


接下来一个个介绍


### x\-ref


这个和 vue、react 里的有点像


相当于直接使用 `getElementById` 或者 `querySelector` 来访问元素


这里主要是要实现消息自动滚动到底部（这个等下再介绍）


### x\-for 和 x\-if


顾名思义，就是循环和判断，和 vue 的用法差不多


#### 注意


* 这俩语句只能搭配 template 元素使用
* template 元素里只能有一个元素
* x\-if 只能在有 x\-data 的元素下才能生效


### x\-text


显示消息的时候，不像 vue 使用 `{item.message}` 来渲染，而是使用了 `x-text` 指令



```
<p x-text="item.message">p>

```

这个指令可以设置元素内的文本，同理还有 `x-html` 指令，可以直接设置 `innerHtml`


## 实现消息自动滚动到底部


来回忆一下之前在 react 里是咋实现的



```
React.useEffect(() => {
  // 自动滚动到消息容器底部
  messagesRef.current.scrollIntoView({behavior: 'smooth'})
}, [messages]);

```

通过使用 useEffect hook，监听 messages 的变化，有变化的时候就滚动到底部


在 alpine.js 里同样能实现监听，编辑 `chatApp` 里面的 `init()` 方法，使用 `$watch` 魔法属性



```
init() {
  this.$watch('messages', () => {
    console.log('$watch messages changed', this.messages)

    // 滚动到最新消息
    this.$nextTick(() => {
      // this.$refs.messages.scrollIntoView({behavior: 'smooth'});
      // 另一种方法滚动到底部
      this.$refs.messages.scrollTop = this.$ refs.messages.scrollHeight;
    });
  })
}

```

这里改成 `scrollTop = scrollHeight` 来实现滚动到底部，之前用过的 `scrollIntoView` 似乎不生效


### Magic Properties


`$` 开头的在 alpine.js 里叫做 magic property ，很多功能都是通过这类属性来实现的。


常用魔法属性：


* **`$el`**：当前元素的引用。
* **`$refs`**：引用其他带有`x-ref`指令的元素。
* **`$event`**：当前事件对象。
* **`$nextTick`**：在下一次DOM更新后执行函数。


## 输入框与数据绑定


继续来通过代码来了解 Alpine.js 的核心概念


来看代码



```
<form class="mt-2">
  <label for="chat-input" class="sr-only">Enter your promptlabel>
  <div class="relative">
    <button
            type="button" @click="audioMode=!audioMode"
            class="absolute inset-y-0 left-0 flex items-center pl-6 text-slate-500 hover:text-blue-600 dark:text-slate-400 dark:hover:text-blue-600"
            >
      <i class="fa-solid fa-microphone text-2xl">i>
      <span class="sr-only">use voice inputspan>
    button>
    <textarea
              id="chat-input"
              class="block w-full resize-none rounded-xl border-none bg-slate-200 p-4 pl-14 pr-20 text-sm text-slate-900 focus:outline-none focus:ring-1 focus:ring-blue-400 dark:bg-slate-900 dark:text-slate-200 dark:placeholder-slate-400 dark:focus:ring-blue-600 sm:text-base"
              placeholder="Please enter your message"
              rows="1"
              required
              x-model="message"
              :disabled="!receiver"
              @keydown.enter.prevent="sendMessage()"
              >textarea>
    <button
            type="button" @click="sendMessage()" :disabled="!receiver"
            class="absolute bottom-2 right-2.5 rounded-lg bg-blue-700 px-4 py-2 text-sm font-medium text-slate-200 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800 sm:text-base"
            >
      Send <span class="sr-only">Sendspan>
    button>
  div>
form>

```

### 数据双向绑定


首先是数据绑定，这个与 Vue、Blazor 非常像


这个项目的输入框使用了  元素，使用 `x-model` 指令实现表单输入和数据状态之间的双向绑定。


#### 修饰符


* **`.lazy`**：在`change`事件而非`input`事件时更新数据。
* **`.debounce`**：为输入事件添加防抖，例如 `x-model.debounce.500ms="query"`


### 属性绑定


使用 `x-bind` 指令（可简写为`:`），可以将数据绑定到元素的属性上，实现属性的动态更新。


在上面的代码中，体现为  和 `Alpine.js 通过 x-on 指令（也可以简写为 @）来监听DOM事件，并触发相应的处理函数。


比如



```
<button @click="sendMessage()">
  发送信息
button>

```

#### 修饰符


Alpine.js 支持事件修饰符，用于控制事件的行为：


* .prevent：调用 event.preventDefault()。
* .stop：调用 event.stopPropagation()。
* .window：监听全局 window 对象的事件。


例如



```
<button @click.prevent="sendMessage()">
  发送信息
button>

```

老生常谈的防抖与节流，也是有的



```
<input @input.debounce.500ms="fetchResults">

```

节流



```
<div @scroll.window.throttle.750ms="handleScroll">...div>

```

## 扩展


本项目用到的 Alpine.js 的功能不多，我看了下官网这个库的功能还挺丰富的，这里介绍几个。


### 全局状态管理


同样是使用魔法属性实现的


以切换深色模式为例（搬运了一下官网的例子）



```
<button x-data @click="$store.darkMode.toggle()">Toggle Dark Modebutton>

...

<div x-data :class="$store.darkMode.on && 'bg-black'">
  ...
div>


<script>
  document.addEventListener('alpine:init', () => {
    Alpine.store('darkMode', {
      on: false,

      toggle() {
        this.on = ! this.on
      }
    })
  })
script>

```

### 动画


使用 x-transition 指令可以实现动画，不过目前可以用的动画不多，真要动画还是用 tailwindcss 或者直接写 CSS 吧



```
<div x-data="{ open: false }">
    <button @click="open = ! open">Togglebutton>
 
    <div x-show="open" x-transition>
        Hello 👋
    div>
div>

```

### 更多


写到这里的时候，我把 alpine.js 文档读了一遍，还有更多其他的功能就不一一复读了，都是跟交互有关的，例如：


* 用于实现 modal 的 x-teleport 指令
* 批量创建元素的搭配生成 id 的 x-id 指令
* 跨标签页状态插件（基于 localStorage）
* 还有很多插件都是用于实现交互的（dropdown、collapse、sort这类）


alpine.js 提供的这些扩展可以让我们实现需要的组件，不过很多功能我还是搭配组件库（例如 flowbite 之类基于 tailwindcss 的库）来做，避免造轮子


## 如何发送语音？


这里再引申一下，这个 LiveChat 项目不单可以发文本，还能发语音。


语音相对于文本还是麻烦一些的，我这里也只是 demo 版本，还不太完善。


### 录音


主要使用 MediaRecorder 来实现录音，浏览器上会弹出来权限申请，用户允许了才能开始录音。


参考 MDN 文档: [https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder](https://github.com)


开始录音



```
// 开始录音
startRecording() {
  navigator.mediaDevices.getUserMedia({audio: true})
    .then(stream => {
    this.audioStream = stream;
    this.mediaRecorder = new MediaRecorder(stream);

    this.mediaRecorder.ondataavailable = event => {
      this.audioChunks.push(event.data);
    };

    this.mediaRecorder.onstop = () => {
      const audioBlob = new Blob(this.audioChunks, {type: 'audio/wav'});
      const reader = new FileReader();
      reader.onloadend = () => {
        const arrayBuffer = reader.result;

        // 创建 AudioContext 实例
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();

        // 解码音频数据
        audioContext.decodeAudioData(arrayBuffer)
          .then((audioBuffer) => {
          const duration = audioBuffer.duration;
          console.log(`音频时长：${duration} 秒`);
          this.socket.send(arrayBuffer);
          this.messages.push(new Message(
            'user', audioBuffer, 'audio', duration
          ))
          audioContext.close();
        })
          .catch((error) => {
          console.error('解码音频数据出错', error);
        })
      }
      reader.readAsArrayBuffer(audioBlob);
      this.audioChunks = [];
    };

    this.mediaRecorder.start();
    console.log("录音已开始");
  })
    .catch(err => {
    console.error("获取麦克风权限失败: ", err);
  });
}

```

停止录音



```
// 停止录音
stopRecording() {
  if (this.mediaRecorder) {
    this.mediaRecorder.stop();
    // 停止麦克风流
    this.audioStream.getTracks().forEach(track => track.stop());
    console.log("录音已停止");
  }
}

```

### 播放音频



```
playAudio(message) {
  console.log('playAudio', message)
  if (message.type === 'audio' && message.message) {
    const audioContext = new (window.AudioContext || window.webkitAudioContext)();
    const source = audioContext.createBufferSource();
    source.buffer = message.message;
    source.connect(audioContext.destination);
    source.start(0);
  }
}

```

## 小结


前端框架层出不穷，项目越做越大，alpine.js 和 htmx 这种库是反其道而行，可以用最简单的方法来开发现代化的 web 应用。


接下来我会把这俩东西加入新版 DjangoStarter 里，这才是最适合全站开发者的技术~`

