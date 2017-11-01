title: Vue 动态组件
author: Ao
date: 2017-08-08 17:26:15
tags:
---
<div><p>翻译自 <a href="https://link.juejin.im?target=https%3A%2F%2Fcoligo.io%2Fdynamic-components-in-vuejs%2F" target="_blank" rel="nofollow noopener noreferrer">Dynamic Components in Vue.js</a></p>
<p>这篇文章将会教你如何使用Vue中的<a href="https://link.juejin.im?target=http%3A%2F%2Fcn.vuejs.org%2Fguide%2Fcomponents.html%23u52A8_u6001_u7EC4_u4EF6" target="_blank" rel="nofollow noopener noreferrer">动态组件</a>。当创建小型的单页应用时，这些小型应用可能并不需要vue-router来控制路由，我们只想简单地切换不同的组件来达到不同的展示效果。<br><a></a></p>
<p><img src="https://user-gold-cdn.xitu.io/2016/11/29/ec713d14e8c651b1f465981025a9a268?imageView2/0/w/1280/h/960" alt="" style=""></p>
<p>Vue中的动态组件要求你指定一个挂载点，在这个挂载点下你可以动态地切换组件。在这篇教程中，我们将通过几个例子来展示如何使用动态组件。我们会创建一个动态组件，学习使用keep-alive指令参数，最后我们还会在组件的切换之间添加一些过渡效果。下面开始吧：</p>
<h2><a href="https://link.juejin.im?target=http%3A%2F%2Fylcui.top%2F2016%2F08%2F08%2F%25E3%2580%2590%25E7%25BF%25BB%25E8%25AF%2591%25E3%2580%2591Vue%25E5%258A%25A8%25E6%2580%2581%25E7%25BB%2584%25E4%25BB%25B6%2F%23%E5%88%9B%E5%BB%BA%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6" title="创建动态组件" target="_blank" rel="nofollow noopener noreferrer"></a>创建动态组件</h2><p>假设我们正在为一个Blog做个简单的导航栏，我们想添加两个页面：</p>
<ul>
<li>一个用于管理已经存在的博客文章</li>
<li>一个用于创建新的博客文章</li>
</ul>
<p>稍后，我们会组件化这两个页面。现在，让我们从头一步步来吧，我们把这个简单的应用挂载到body下：</p>


<pre><code class="hljs css"><span class="hljs-selector-tag">new</span> <span class="hljs-selector-tag">Vue</span>({
  <span class="hljs-attribute">el</span>: <span class="hljs-string">'body'</span>
})</code></pre>

 

<p>添加导航栏，在头部引入<a href="https://link.juejin.im?target=http%3A%2F%2Fcdn.bootcss.com%2Fbootstrap%2F3.3.6%2Fcss%2Fbootstrap.min.css" target="_blank" rel="nofollow noopener noreferrer">BootStrop 3.3.6</a>：</p>


<pre><code class="hljs sql"><div class="header clearfix">
  <nav>
    <ul class="nav nav-pills pull-right">
      <li role="presentation">
        <a href="https://link.juejin.im?target=javascript%3Avoid(0)" target="_blank" rel="nofollow noopener noreferrer">Manage Posts</a>
      </li>
      <li role="presentation">
        <a href="https://link.juejin.im?target=javascript%3Avoid(0)" target="_blank" rel="nofollow noopener noreferrer"><span class="hljs-keyword">Create</span> Post</a>
      </li>
    </ul>
  </nav>
  <h3 class="text-muted"><span class="hljs-keyword">Admin</span> Panel</h3>
</div>
<div class="container">
  
</div></code></pre>



<p>运行程序，我们会得到如下图所示的效果：</p>
<p><img src="https://user-gold-cdn.xitu.io/2016/11/29/d84bc4f141f8195f8bdbeb1f271d56be?imageView2/0/w/1280/h/960" alt="" style=""></p>
<p>现在，我们这个小小的应用已经有了一个大概的结构，下面我们开始创建两个组件：一个用于管理已经存在的博客文章，一个用于创建新的博客文章。如果你还不了解如何在Vue中创建组件，建议你看看<a href="https://link.juejin.im?target=https%3A%2F%2Fcoligo.io%2Fdynamic-components-in-vuejs%2F" target="_blank" rel="nofollow noopener noreferrer">这个教程</a>，或者看官方的教程，那里已经说得够明白了。</p>
<p>下面创建一个<code>manage-posts</code>组件，并模拟一些文章标题数据：</p>


<pre><code class="hljs haskell"><span class="hljs-type">Vue</span>
.component('manage-posts', {
  template: '#manage-template',
  <span class="hljs-class"><span class="hljs-keyword">data</span>: function() {
    <span class="hljs-title">return</span> {
      <span class="hljs-title">posts</span>: [
        '<span class="hljs-type">Vue</span>.<span class="hljs-title">js</span>: <span class="hljs-type">The</span> <span class="hljs-type">Basics</span>',
        '<span class="hljs-type">Vue</span>.<span class="hljs-title">js</span> <span class="hljs-type">Components</span>',
        '<span class="hljs-type">Server</span> <span class="hljs-type">Side</span> <span class="hljs-type">Rendering</span> <span class="hljs-title">with</span> <span class="hljs-type">Vue</span>',
        '<span class="hljs-type">Vue</span> + <span class="hljs-type">Firebase</span>'
      ]
    }</span>
  }
})</code></pre>

<p>接着为组件<code>manage-posts</code>创建一个模板：</p>

<pre><code class="hljs"><template id="manage-template"></template></code></pre>


<p><img src="https://user-gold-cdn.xitu.io/2016/11/29/eb0c391f556ed90e1f22f0ffb4b1e7dd?imageView2/0/w/1280/h/960" alt="" style=""></p>
<p>目前为止，我们已经有了导航栏和<code>mange-posts</code>组件，下面我们添加<code>create-post</code>组件，并把它们结合起来：</p>

<pre><code class="hljs sql">Vue.component('<span class="hljs-keyword">create</span>-post<span class="hljs-string">', {
  template: '</span>#<span class="hljs-keyword">create</span>-<span class="hljs-keyword">template</span><span class="hljs-string">'
})</span></code></pre>



<p>模板：</p>

<pre><code class="hljs"><template id="create-template"></template></code></pre>


<p><img src="https://user-gold-cdn.xitu.io/2016/11/29/731e983132a27b38d35b681c908ce17b?imageView2/0/w/1280/h/960" alt="" style=""></p>
<p>好了，组件都已准备完毕，下面我们进入本文重点：把这些组件制作成动态组件。</p>
<p>当一个用户点击<strong>Manage Posts</strong>按钮，我们想让Vue渲染manage-posts组件。同样的，当点击<strong>Create Post</strong>按钮，渲染create-post组件，</p>
<p>实现动态组件我们需要<code><component></component></code>元素，我们把它当做动态组件的挂载点，然后在该元素上通过<code>is</code>属性指定我们需要渲染的组件。如此，我们可以通过下面的方式渲染manage-post组件：</p>

<pre><code class="hljs"><div class="container">
  
  <component is="manage-posts"></component>
</div></code></pre>
<p>效果图如下：</p>
<p><img src="https://user-gold-cdn.xitu.io/2016/11/29/84cc80b518f5581e5730df0dd4f026f8?imageView2/0/w/1280/h/960" alt="" style=""></p>
<p>然而，这种硬编码的方式似乎不是所谓地<strong>动态</strong>，我们目前仍然无法通过点击不同的按钮来展示不同的组件。</p>
<p>聪明的你也许已经想到了Vue的数据绑定。我们只需在data中定义一个名为currentView的属性，然后再对is属性进行数据绑定就行了，很简单：</p>


<pre><code class="hljs less"><span class="hljs-selector-tag">new</span> <span class="hljs-selector-tag">Vue</span>({
  <span class="hljs-attribute">el</span>: <span class="hljs-string">'body'</span>,
  <span class="hljs-attribute">data</span>: {
    <span class="hljs-attribute">currentView</span>: <span class="hljs-string">'manage-posts'</span>
  }
})</code></pre>
<pre><code class="hljs"><div class="container">
  
  <component :is="currentView"></component>
</div></code></pre>
<p>最后，我们再给导航栏的两个按钮添加点击事件，这样用户每次点击即不同的按钮都会改变currentView的值，从而显示不同的组件：</p>

<pre><code class="hljs r"><span class="hljs-keyword">...</span>
<li role="presentation">
  <a href="#" @click="currentView='manage-posts'">Manage Posts</a>
</li>
<li role="presentation">
  <a href="#" @click="currentView='create-post'">Create Post</a>
</li>
<span class="hljs-keyword">...</span></code></pre>


<p>下面是完整的代码：</p>
<iframe width="100%" height="300" src="//jsfiddle.net/coligo/mfxb9aeh/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
<h2><a href="https://link.juejin.im?target=http%3A%2F%2Fylcui.top%2F2016%2F08%2F08%2F%25E3%2580%2590%25E7%25BF%25BB%25E8%25AF%2591%25E3%2580%2591Vue%25E5%258A%25A8%25E6%2580%2581%25E7%25BB%2584%25E4%25BB%25B6%2F%23keep-alive" title="keep-alive" target="_blank" rel="nofollow noopener noreferrer"></a>keep-alive</h2><p>目前我们已经知道了如何创建动态组件，下面我们说说更加重要的keep-alive。</p>
<p>现在当我们每次点击按钮切换组件时，旧的组件就会被销毁而新的组件会被渲染出来。</p>
<p>这样一来就存在一个问题，旧的组件因为被销毁从而丢失了所有的状态，当重新渲染这个组件时不得不重新调用它所需要的API来获取已经发表的文章（这里我们假设是从服务器获取文章）。为了避免这个问题，我们可以使用keep-alive指令参数来把切出去的组件保留在内存中，以保留它的状态或避免重新渲染：</p>

<pre><code class="hljs http">
<div class="container">
<span class="undefined">  
  </span><component :is="currentView" keep-alive=""></component><span class="undefined">
</span></div></code></pre>



<p>在下面，我们可以验证被切出去的组件是否被保存在了内存中。我们可以在create-post组件中输入一些内容，接着切换组件，然后再切换回来。你会发现，我们输入的内容还在。</p>
<iframe width="100%" height="300" src="//jsfiddle.net/coligo/43kxkm3d/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
<p>如果你的组件需要调用很多API或者渲染时需要大量的数据，那么这个指令参数会很有用。</p>
<h2><a href="https://link.juejin.im?target=http%3A%2F%2Fylcui.top%2F2016%2F08%2F08%2F%25E3%2580%2590%25E7%25BF%25BB%25E8%25AF%2591%25E3%2580%2591Vue%25E5%258A%25A8%25E6%2580%2581%25E7%25BB%2584%25E4%25BB%25B6%2F%23%E7%BB%84%E4%BB%B6%E9%97%B4%E7%9A%84%E8%BF%87%E6%B8%A1" title="组件间的过渡" target="_blank" rel="nofollow noopener noreferrer"></a>组件间的过渡</h2><p>下面，我们在组件切换间添加一些过度效果。</p>
<p>在组件的挂载点上，增加<code>transition</code>属性，我们使用简单的淡入淡出的过渡效果。</p>



<pre><code class="hljs"><div class="container">
  <component :is="currentView" transition="fade" transition-mode="out-in"></component>
</div></code></pre>


<p>添加CSS过渡控制：</p>

<pre><code class="hljs css"><span class="hljs-selector-class">.fade-transition</span> {
  <span class="hljs-attribute">transition</span>: opacity <span class="hljs-number">0.2s</span> ease;
}
<span class="hljs-selector-class">.fade-enter</span>, <span class="hljs-selector-class">.fade-leave</span> {
  <span class="hljs-attribute">opacity</span>: <span class="hljs-number">0</span>;
}</code></pre>


<p>OK了：</p><iframe width="100%" height="300" src="//jsfiddle.net/coligo/8mdso9fj/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

<p>你可能已经注意到了<code>transition-mode="out-in"</code>。这个属性告诉Vue，我们希望旧的组件先淡出，然后新的组件再淡入。否则的话，就会同时出现两个组件，一个淡出一个淡入，看上去相当别扭。</p>
<h2><a href="https://link.juejin.im?target=http%3A%2F%2Fylcui.top%2F2016%2F08%2F08%2F%25E3%2580%2590%25E7%25BF%25BB%25E8%25AF%2591%25E3%2580%2591Vue%25E5%258A%25A8%25E6%2580%2581%25E7%25BB%2584%25E4%25BB%25B6%2F%23%E7%BB%93%E6%9D%9F%E8%AF%AD" title="结束语" target="_blank" rel="nofollow noopener noreferrer"></a>结束语</h2><p>希望这篇教程能使你学会如何使用动态组件。这篇教程并不是为了说明动态组件可以替代<a href="https://link.juejin.im?target=http%3A%2F%2Frouter.vuejs.org%2Fzh-cn%2Findex.html" target="_blank" rel="nofollow noopener noreferrer">vue-router</a>，vue-router具有更多更有用的特性。对于一些简单的组件切换，我想动态组件可能会更合适。为了构建更好的SPA我觉得你应该学习一下vue-router。</p>
</div>