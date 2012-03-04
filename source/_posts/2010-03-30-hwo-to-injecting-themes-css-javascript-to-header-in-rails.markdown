---
layout: post
title: 在rails中不同的view不同皮肤下的js，css，注入js和css到head区域
comments: true
date: 2010-03-30 20:13
categories:
- LAMP
- Rails
- Ruby
- layout
- injecting
- dynamic
- ruby on rails
---

<p>利用layout可以很好实现这个需求.</p>
<p>在ApplicationHelper内加入如下代码：</p>
<div class="source" style='font-family: "[object HTMLOptionElement]","Consolas","Lucida Console","Courier New"; color: #e6e1dc; background-color: #111111;'>
<p><span style="color: #cc7833;">def</span> <span style="color: #ffc66d;">require_js</span>(<span style="color: #e6e1dc;">path</span>)<br />    <span style="color: #e6e1dc;">content_for</span> <span style="color: #a5c261;">:header_js</span> <span style="color: #cc7833;">do</span><br />      <span style="color: #e6e1dc;">include_js_tag</span> <span style="color: #e6e1dc;">path</span><br />    <span style="color: #cc7833;">end</span><br />  <span style="color: #cc7833;">end</span></p>
<p>  <span style="color: #cc7833;">def</span> <span style="color: #ffc66d;">require_css</span>(<span style="color: #e6e1dc;">path</span>)<br />    <span style="color: #e6e1dc;">content_for</span> <span style="color: #a5c261;">:header_css</span> <span style="color: #cc7833;">do</span><br />      <span style="color: #e6e1dc;">include_css_tag</span> <span style="color: #e6e1dc;">path</span><br />    <span style="color: #cc7833;">end</span><br />  <span style="color: #cc7833;">end</span></p>
<p>  <span style="color: #cc7833;">def</span> <span style="color: #ffc66d;">include_js_tag</span>(<span style="color: #e6e1dc;">path</span>)<br />    <span style="color: #cc7833;">if</span> <span style="color: #e6e1dc;">not</span> <span style="color: #e6e1dc;">path</span><span style="color: #e6e1dc;">.</span><span style="color: #e6e1dc;">starts_with?</span>(<span style="color: #a5c261;">"http:"</span>)<br />      <span style="color: #e6e1dc;">path</span> <span style="color: #e6e1dc;">=</span> <span style="color: #a5c261;">"/themes/</span><span style="color: #a5c261;">#{</span><span style="color: #6d9cbe;">@setting</span><span style="color: #e6e1dc;">[</span><span style="color: #a5c261;">:theme</span><span style="color: #e6e1dc;">]</span><span style="color: #a5c261;">}</span><span style="color: #a5c261;">/javascripts/"</span> <span style="color: #e6e1dc;">+</span> <span style="color: #e6e1dc;">path</span><br />    <span style="color: #cc7833;">end</span><br />    <span style="color: #e6e1dc;">javascript_include_tag</span> <span style="color: #e6e1dc;">path</span><br />  <span style="color: #cc7833;">end</span></p>
<p>   <span style="color: #cc7833;">def</span> <span style="color: #ffc66d;">include_css_tag</span>(<span style="color: #e6e1dc;">path</span>)<br />    <span style="color: #cc7833;">if</span> <span style="color: #e6e1dc;">not</span> <span style="color: #e6e1dc;">path</span><span style="color: #e6e1dc;">.</span><span style="color: #e6e1dc;">starts_with?</span>(<span style="color: #a5c261;">"http:"</span>)<br />      <span style="color: #e6e1dc;">path</span> <span style="color: #e6e1dc;">=</span> <span style="color: #a5c261;">"/themes/</span><span style="color: #a5c261;">#{</span><span style="color: #6d9cbe;">@setting</span><span style="color: #e6e1dc;">[</span><span style="color: #a5c261;">:theme</span><span style="color: #e6e1dc;">]</span><span style="color: #a5c261;">}</span><span style="color: #a5c261;">/stylesheets/"</span> <span style="color: #e6e1dc;">+</span> <span style="color: #e6e1dc;">path</span><br />    <span style="color: #cc7833;">end</span><br />    <span style="color: #e6e1dc;">stylesheet_link_tag</span> <span style="color: #e6e1dc;">path</span><br />  <span style="color: #cc7833;">end</span></p>
</div>
<p>(如果你要直接在view或者layout内引入css则可以&lt;%= include_css_tag "global.css" %&gt;，这样生成的路径是带有皮肤目录的）</p>
<p>接下来，修改你的layout的head，加入如下代码：</p>
<p><!--more--></p>
<p>&lt;%= yield :header_js %&gt;<br />&lt;%= yield :header_css %&gt;</p>
<p>然后在需要引入js的View内</p>
<p>&lt;% require_js "jquery/jquery.tools.min.js" %&gt;<br />&lt;% require_js "jquery/jquery.colorbox.min.js" %&gt;</p>
<p>最后run一下，你会看到会在html的head内生成如下html</p>
<p>&lt;script src="/themes/2010v1/javascripts/jquery/jquery.tools.min.js?1269949149" type="text/javascript"&gt;&lt;/script&gt;<br />&lt;script src="/themes/2010v1/javascripts/jquery/jquery.colorbox.min.js?1269949147" type="text/javascript"&gt;&lt;/script&gt;</p>
<p> </p>
<p> </p>				
