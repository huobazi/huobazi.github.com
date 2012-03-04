---
layout: post
title: ! '[2007最后一博]Url地址重写，利用HttpHander手工编译页面并按需生成静态HTML文件'
comments: true
date: 2007-12-31 16:28
categories:
- ASP.NET
- Asp.net
- HttpHander
- 代码片段
---

<p>很多朋友可能都讨论过ASP.NET中生成HTML的方法了，有按照模板用IO方法写文件</p>
<p>有在404错误页面内生成HTML的，有在Render内保存页面输出到HTML文件的。</p>
<p>今天我发一个配合Url重写利用HttpHander手工编译.aspx页面方法。</p>
<p>HTML文件的方法，可按需、“定时”的生成，以减轻数据库的访问。</p>
<p> </p>
<p><strong><span style="font-family: Courier New;">声明：下面的文字是本文不可缺少的部分，转载请保留，谢谢！</span></strong></p>
<p><span style="font-family: Courier New;">////////////////////////////////////////////////////</span></p>
<p><span style="font-family: Courier New;">作者：武眉博&lt;活靶子.NET&gt;</span></p>
<p>同时首发于：</p>
<p>    <a href="http://www.im286.com/" target="_blank"><span style="color: #0066aa; font-family: Courier New;">落伍者</span></a><span style="font-family: Courier New;">   &amp;&amp; </span><a href="http://www.cnblogs.com/" target="_blank"><span style="color: #0066aa; font-family: Courier New;">博客园</span></a><span style="font-family: Courier New;">  </span></p>
<p>    <a href="http://www.devedu.com/" target="_blank"><span style="color: #0066aa; font-family: Courier New;">开发者学院</span></a><span style="font-family: Courier New;">   &amp;&amp; </span><a href="http://www.aspxboy.com/" target="_blank"><span style="color: #0066aa; font-family: Courier New;">.Net男孩社区</span></a></p>
<p>知识点：<strong>UrlRewrite</strong>、 <strong>IHttpModule</strong>、 <strong>IHttpHander </strong>的编写</p>
<p>效果：</p>
<p><a href="http://www.devedu.com/Doc/DotNet/AspNet/default.2.aspx">http://www.devedu.com/Doc/DotNet/AspNet/default.2.aspx</a></p>
<p><a href="http://www.devedu.com/Doc/DotNet/AspNet/default.2.html">http://www.devedu.com/Doc/DotNet/AspNet/default.2.html</a></p>
<p>思路：</p>
<p>1 挂载“.aspx"的请求到自定义的Httphander内</p>
<p>2 配置URL重写规则</p>
<p>3 访问某.aspx文件时，在HttpHander内 根据配置确定是否应该生成</p>
<p> 接着...</p>
<p> if(需要生成)</p>
<p> {</p>
<p>  if(若已经生成html文件 )</p>
<p>  {</p>
<p>   if(文件并未过期)</p>
<p>   {</p>
<p>    则直接定向(Server.Transfer())。</p>
<p>   }</p>
<p>   else</p>
<p>   {</p>
<p>    删除HTML文件；</p>
<p>    重新编译.aspx（Page内数据库操作等等）</p>
<p>    生成HTML文件；</p>
<p>   }</p>
<p>  }</p>
<p>  else if(尚未生成文件)</p>
<p>  {</p>
<p>   生成Html。</p>
<p>  }</p>
<p> }</p>
<p> else</p>
<p> {</p>
<p>  则编译.aspx文件</p>
<p> }</p>
<p> </p>
<p>另：建议阅读一下dudu的blog中关于asp.net页面编译的讨论</p>
<p><a href="http://www.cnblogs.com/dudu/archive/2006/03/07/345107.html">http://www.cnblogs.com/dudu/archive/2006/03/07/345107.html</a></p>
<p><a href="http://www.cnblogs.com/dudu/archive/2006/03/07/344351.html">http://www.cnblogs.com/dudu/archive/2006/03/07/344351.html</a></p>
<p> </p>
<p>部分代码</p>
<div class="codeText">
<div class="codeHead">C#代码</div>
<ol class="dp-c">
<li class="alt"><span><span class="keyword">public</span><span> </span><span class="keyword">void</span><span> ProcessRequest(HttpContext context)   </span></span></li>
<li><span>        {   </span></li>
<li class="alt">
<span>            </span><span class="keyword">string</span><span> rawUrl = context.Request.RawUrl;   </span>
</li>
<li>
<span>            </span><span class="keyword">string</span><span> requestPath = context.Request.Path;   </span>
</li>
<li class="alt">
<span>            </span><span class="keyword">string</span><span> applicationPath = context.Request.ApplicationPath;   </span>
</li>
<li>
<span>            Url urlItem = </span><span class="keyword">null</span><span>;   </span>
</li>
<li class="alt"><span>  </span></li>
<li>
<span>            </span><span class="comment">//上下文中没有定义ToStaticUrlItem表示，此请求没有经过UrlRewrite,直接编译，不生成html </span><span>  </span>
</li>
<li class="alt">
<span>            </span><span class="comment">//参考UrlRewriteModule.cs </span><span>  </span>
</li>
<li>
<span>            </span><span class="keyword">if</span><span> (context.Items[</span><span class="string">"ToStaticUrlItem"</span><span>] == </span><span class="keyword">null</span><span>)   </span>
</li>
<li class="alt"><span>            {   </span></li>
<li>
<span>                </span><span class="keyword">if</span><span> (!File.Exists(context.Request.PhysicalPath))   </span>
</li>
<li class="alt"><span>                {   </span></li>
<li>
<span>                    </span><span class="keyword">throw</span><span> </span><span class="keyword">new</span><span> HttpException(404, </span><span class="string">"您访问的页面没有找到。"</span><span>);   </span>
</li>
<li class="alt"><span>                }   </span></li>
<li><span>  </span></li>
<li class="alt">
<span>                </span><span class="comment">// asp.net 1.1 采用下面方法编译页面 </span><span>  </span>
</li>
<li>
<span>                </span><span class="comment">//PageParser.GetCompiledPageInstance(requestPath, context.Request.PhysicalPath, context).ProcessRequest(context); </span><span>  </span>
</li>
<li class="alt">
<span>                IHttpHandler hander = BuildManager.CreateInstanceFromVirtualPath(requestPath, </span><span class="keyword">typeof</span><span>(Page)) </span><span class="keyword">as</span><span> IHttpHandler;   </span>
</li>
<li><span>                hander.ProcessRequest(context);   </span></li>
<li class="alt"><span>  </span></li>
<li>
<span>                </span><span class="keyword">return</span><span>;   </span>
</li>
<li class="alt"><span>            }   </span></li>
<li><span>  </span></li>
<li class="alt">
<span>            </span><span class="keyword">string</span><span> filePath;   </span>
</li>
<li><span>  </span></li>
<li class="alt">
<span>            urlItem = (Url)context.Items[</span><span class="string">"ToStaticUrlItem"</span><span>];   </span>
</li>
<li><span>  </span></li>
<li class="alt">
<span>            Regex regex = </span><span class="keyword">new</span><span> Regex(   </span>
</li>
<li><span>                Globals.ApplicationPath + urlItem.LookFor,   </span></li>
<li class="alt"><span>                RegexOptions.CultureInvariant | RegexOptions.Singleline | RegexOptions.Compiled | RegexOptions.IgnoreCase);   </span></li>
<li><span>  </span></li>
<li class="alt">
<span>            </span><span class="keyword">string</span><span> requestFile = regex.Replace(rawUrl, Globals.ApplicationPath + urlItem.WriteTo.Replace(</span><span class="string">"^"</span><span>, </span><span class="string">"&amp;"</span><span>));   </span>
</li>
<li><span>  </span></li>
<li class="alt">
<span>            </span><span class="keyword">if</span><span> (requestFile.IndexOf(</span><span class="string">"?"</span><span>) &gt; 0)   </span>
</li>
<li><span>            {   </span></li>
<li class="alt">
<span>                filePath = requestFile.Substring(0, requestFile.IndexOf(</span><span class="string">"?"</span><span>));   </span>
</li>
<li><span>            }   </span></li>
<li class="alt">
<span>            </span><span class="keyword">else</span><span>  </span>
</li>
<li><span>            {   </span></li>
<li class="alt"><span>                filePath = requestFile;   </span></li>
<li><span>            }   </span></li>
<li class="alt"><span>  </span></li>
<li>
<span>            </span><span class="keyword">string</span><span> inputFile = context.Request.PhysicalApplicationPath + filePath;   </span>
</li>
<li class="alt">
<span>            </span><span class="keyword">string</span><span> path = context.Request.PhysicalApplicationPath + rawUrl.ToLower().Replace(</span><span class="string">".aspx"</span><span>, </span><span class="string">".html"</span><span>);   </span>
</li>
<li>
<span>            </span><span class="keyword">if</span><span> (applicationPath != </span><span class="string">"/"</span><span>)   </span>
</li>
<li class="alt"><span>            {   </span></li>
<li>
<span>                inputFile = inputFile.Replace(applicationPath + </span><span class="string">"/"</span><span>, @</span><span class="string">"\"); </span> </li>
<li class="alt"><span><span class="string">                path = path.Replace(applicationPath + "</span><span>/</span><span class="string">", "</span><span class="string">").Replace("</span><span>/</span><span class="string">", @"</span><span>\</span><span class="string">"); </span> </span></li>
<li><span><span class="string">            } </span> </span></li>
<li class="alt"><span><span class="string">            else </span> </span></li>
<li><span><span class="string">            { </span> </span></li>
<li class="alt"><span><span class="string">                path = path.Replace("</span><span>/</span><span class="string">", @"</span><span>\</span><span class="string">"); </span> </span></li>
<li><span><span class="string">            } </span> </span></li>
<li class="alt"><span> </span></li>
<li><span><span class="string">            if (!urlItem.EnabledToStatic) </span> </span></li>
<li class="alt"><span><span class="string">            { </span> </span></li>
<li><span><span class="string">                // asp.net 1.1 采用下面方法编译页面 </span> </span></li>
<li class="alt"><span><span class="string">                //PageParser.GetCompiledPageInstance( filePath , inputFile , context ).ProcessRequest( context ); </span> </span></li>
<li><span><span class="string">                IHttpHandler hander = BuildManager.CreateInstanceFromVirtualPath(filePath, typeof(Page)) as IHttpHandler; </span> </span></li>
<li class="alt"><span><span class="string">                hander.ProcessRequest(context); </span> </span></li>
<li><span> </span></li>
<li class="alt"><span><span class="string">                return; </span> </span></li>
<li><span><span class="string">            } </span> </span></li>
<li class="alt"><span> </span></li>
<li><span><span class="string">            if (!File.Exists(path)) </span> </span></li>
<li class="alt"><span><span class="string">            { </span> </span></li>
<li><span><span class="string">                // asp.net 1.1 采用下面方法编译页面 </span> </span></li>
<li class="alt"><span><span class="string">                //PageParser.GetCompiledPageInstance( filePath , inputFile , context ).ProcessRequest( context ); </span> </span></li>
<li><span><span class="string">                IHttpHandler hander = BuildManager.CreateInstanceFromVirtualPath(filePath, typeof(Page)) as IHttpHandler; </span> </span></li>
<li class="alt"><span><span class="string">                hander.ProcessRequest(context); </span> </span></li>
<li><span><span class="string">                context.Response.Filter = new AspxBoy.BuildHtmlDemo.ToHtmlFilter(context.Response.Filter, path); </span> </span></li>
<li class="alt"><span> </span></li>
<li><span><span class="string">                return; </span> </span></li>
<li class="alt"><span><span class="string">            } </span> </span></li>
<li><span> </span></li>
<li class="alt"><span><span class="string">            if (urlItem.Minutes == Int32.MaxValue) </span> </span></li>
<li><span><span class="string">            { </span> </span></li>
<li class="alt"><span><span class="string">                context.Server.Transfer(rawUrl.ToLower().Replace("</span><span>.aspx</span><span class="string">", "</span><span>.html</span><span class="string">")); </span> </span></li>
<li><span><span class="string">            } </span> </span></li>
<li class="alt"><span><span class="string">            else </span> </span></li>
<li><span><span class="string">            { </span> </span></li>
<li class="alt"><span><span class="string">                FileInfo fileInfo = new FileInfo(path); </span> </span></li>
<li><span><span class="string">                if (fileInfo.LastWriteTime.AddMinutes((double)urlItem.Minutes) &lt; DateTime.Now) </span> </span></li>
<li class="alt"><span><span class="string">                { </span> </span></li>
<li><span><span class="string">                    fileInfo.Delete(); </span> </span></li>
<li class="alt"><span> </span></li>
<li><span><span class="string">                    // asp.net 1.1 采用下面方法编译页面 </span> </span></li>
<li class="alt"><span><span class="string">                    //PageParser.GetCompiledPageInstance( filePath , inputFile , context ).ProcessRequest( context ); </span> </span></li>
<li><span><span class="string">                    IHttpHandler hander = BuildManager.CreateInstanceFromVirtualPath(filePath, typeof(Page)) as IHttpHandler; </span> </span></li>
<li class="alt"><span><span class="string">                    hander.ProcessRequest(context); </span> </span></li>
<li><span><span class="string">                    context.Response.Filter = new AspxBoy.BuildHtmlDemo.ToHtmlFilter(context.Response.Filter, path); </span> </span></li>
<li class="alt"><span><span class="string">                } </span> </span></li>
<li><span><span class="string">                else </span> </span></li>
<li class="alt"><span><span class="string">                { </span> </span></li>
<li><span><span class="string">                    context.Server.Transfer(rawUrl.ToLower().Replace("</span><span>.aspx</span><span class="string">", "</span><span>.html"));   </span></span></li>
<li class="alt"><span>                }   </span></li>
<li>
<span>                </span><span class="keyword">return</span><span>;   </span>
</li>
<li class="alt"><span>            }   </span></li>
<li><span>        }  </span></li>
</ol>
<p> <br />示例项目下载：<a href="http://www.cnblogs.com/Files/huobazi/BuildHtmlDemo.rar">http://www.cnblogs.com/Files/huobazi/BuildHtmlDemo.rar</a><br /></p>
</div>				
