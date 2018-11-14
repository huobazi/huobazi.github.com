---
layout: post
title: 'How to,在iOS中点击文本框以外区域，隐藏键盘'
comments: true
date: 2011-12-09
tags:
- 闲言碎语
- 代码片段
- iOS
- iPhone
- 键盘
- OC
---

<p>当点击文本框以外部分时，隐藏键盘，实现很简单，加个Category就可以了，代码如下：</p>
<p><!--more--></p>
<div class="source" style="font-family: '[object HTMLOptionElement]', Consolas, 'Lucida Console', 'Courier New'; color: #e6e1dc; background-color: #111111; ">
<p><span style="color: #cc7833; font-style: italic; ">#import &lt;UIKit/UIKit.h&gt;</span><br /><span style="color: #cc7833; ">@interface</span> <span style="color: #e6e1dc; ">UITextField</span> <span style="color: #e6e1dc; ">(HideKeyBoard)</span><br /><span style="color: #e6e1dc; ">-</span>(<span style="color: #da4939; ">void</span>)<span style="color: #e6e1dc; ">hideKeyBoard:</span>(<span style="color: #e6e1dc; ">UIView</span> <span style="color: #e6e1dc; ">*</span>)<span style="color: #e6e1dc; ">view</span>;<br /><span style="color: #cc7833; ">@end</span></p>
<p><span style="color: #cc7833; font-style: italic; ">#import "UITextField+HideKeyBoard.h"</span></p>
<p><span style="color: #cc7833; ">@implementation</span> <span style="color: #e6e1dc; ">UITextField</span> <span style="color: #e6e1dc; ">(HideKeyBoard)</span><br /><span style="color: #e6e1dc; ">-</span> (<span style="color: #da4939; ">void</span>) <span style="color: #e6e1dc; ">hideKeyBoard:</span>(<span style="color: #e6e1dc; ">UIView</span><span style="color: #e6e1dc; ">*</span>)<span style="color: #e6e1dc; ">view</span><span style="color: #e6e1dc; ">{</span><br />    <span style="color: #e6e1dc; ">UITapGestureRecognizer</span> <span style="color: #e6e1dc; ">*</span><span style="color: #e6e1dc; ">tap</span> <span style="color: #e6e1dc; ">=</span> <span style="color: #e6e1dc; ">[[</span><span style="color: #e6e1dc; ">UITapGestureRecognizer</span> <span style="color: #e6e1dc; ">alloc</span><span style="color: #e6e1dc; ">]</span><br />                                   <span style="color: #e6e1dc; ">initWithTarget:</span><span style="color: #e6e1dc; ">self</span><br />                                   <span style="color: #e6e1dc; ">action:</span><span style="color: #cc7833; ">@selector</span>(<span style="color: #e6e1dc; ">doHideKeyBoard</span><span style="color: #e6e1dc; ">)];</span><br />   <br />    <span style="color: #e6e1dc; ">tap</span><span style="color: #e6e1dc; ">.</span><span style="color: #e6e1dc; ">numberOfTapsRequired</span> <span style="color: #e6e1dc; ">=</span> <span style="color: #a5c261; ">1</span>;<br />    <span style="color: #e6e1dc; ">[</span><span style="color: #e6e1dc; ">view</span>  <span style="color: #e6e1dc; ">addGestureRecognizer:</span> <span style="color: #e6e1dc; ">tap</span><span style="color: #e6e1dc; ">];</span><br />    <span style="color: #e6e1dc; ">[</span><span style="color: #e6e1dc; ">tap</span> <span style="color: #e6e1dc; ">setCancelsTouchesInView:</span><span style="color: #e6e1dc; ">NO</span><span style="color: #e6e1dc; ">];</span><br />    <span style="color: #e6e1dc; ">[</span><span style="color: #e6e1dc; ">tap</span> <span style="color: #e6e1dc; ">release</span><span style="color: #e6e1dc; ">];</span><br /><span style="color: #e6e1dc; ">}</span></p>
<p><span style="color: #e6e1dc; ">-</span> (<span style="color: #da4939; ">void</span>)<span style="color: #e6e1dc; ">doHideKeyBoard</span><span style="color: #e6e1dc; ">{</span><br />    <span style="color: #e6e1dc; ">[</span><span style="color: #e6e1dc; ">self</span> <span style="color: #e6e1dc; ">resignFirstResponder</span><span style="color: #e6e1dc; ">];</span><br /><span style="color: #e6e1dc; ">}</span><br /><span style="color: #cc7833; ">@end</span></p>
<p><span style="color: #e6e1dc; ">-</span> (<span style="color: #da4939; ">void</span>)<span style="color: #e6e1dc; ">viewDidLoad</span><br /><span style="color: #e6e1dc; ">{</span><br />    <span style="color: #e6e1dc; ">[</span><span style="color: #e6e1dc; ">super</span> <span style="color: #e6e1dc; ">viewDidLoad</span><span style="color: #e6e1dc; ">];</span><br />    <span style="color: #bc9458; font-style: italic; ">// Do any additional setup after loading the view from its nib.</span><br />    <span style="color: #e6e1dc; ">[</span><span style="color: #e6e1dc; ">self</span><span style="color: #e6e1dc; ">.</span><span style="color: #e6e1dc; ">txtInput</span> <span style="color: #e6e1dc; ">hideKeyBoard:</span><span style="color: #e6e1dc; ">self</span><span style="color: #e6e1dc; ">.</span><span style="color: #e6e1dc; ">view</span><span style="color: #e6e1dc; ">];</span><br /><span style="color: #e6e1dc; ">}</span></p>
</div>
<p>see also: <a href="https://gist.github.com/1450404">https://gist.github.com/1450404</a></p>				
