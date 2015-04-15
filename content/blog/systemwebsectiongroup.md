---
layout: post
title: 在Asp.Net2.0中可以方便的访问配置文件web.config,如判断debug设置，验证类型等。
comments: true
date: 2006-05-18
categories:
- ASP.NET
- Asp.net
---

<p>Asp.Net2.0中我们可以方便的访问配置文件中，.NetFrameWork2.0新增加了 SystemWebSectionGroup 类。<br />允许用户以编程方式访问配置文件的 <b>system.web</b> 组。<br />比如判断web.config内是否为 debug="true",或者判断身份验证形式<br /><br />    SystemWebSectionGroup ws = new SystemWebSectionGroup();<br />    CompilationSection cp = ws.Compilation;<br />    用cp.Debug;就可以得到compilation节内关于"debug"的配置<br />     AuthenticationSection  as = ws.Authentication; <br />    用 as.Mode  可以获取 authentication节中关于"mode"的配置，值为AuthenticationMode 枚举之一<br />AuthenticationMode的取值如下：<font size="2"> </font></p>
<div id="ctl00_LibFrame_ctl09"><table class="VSShowTableBorder" cellspacing="2" cellpadding="5" width="500"><tbody>
<tr>
<th><font size="2"> </font></th>
<th align="left" width="25%"><font size="2">成员名称</font></th>
<th align="left"><font size="2">说明</font></th>
</tr>
<tr valign="top">
<td><font size="2"> </font></td>
<td><b><font size="2">Forms</font></b></td>
<td><font size="2">将基于 ASP.NET 窗体的身份验证指定为身份验证模式。 </font></td>
</tr>
<tr valign="top">
<td><font size="2"> </font></td>
<td><b><font size="2">None</font></b></td>
<td><font size="2">不指定身份验证。 </font></td>
</tr>
<tr valign="top">
<td><font size="2"> </font></td>
<td><b><font size="2">Passport</font></b></td>
<td><font size="2">将 Microsoft Passport 指定为身份验证模式。 </font></td>
</tr>
<tr valign="top">
<td><font size="2"> </font></td>
<td><b><font size="2">Windows</font></b></td>
<td><font size="2">将 Windows 指定为身份验证模式。在使用 Internet 信息服务 (IIS) 身份验证方法（基本、简要、集成 Windows (NTLM/Kerberos) 或证书）时适用此模式。 </font></td>
</tr>
</tbody></table></div>
<p><font size="2">     <br /><strong><font color="#0000ff">附：SystemWebSectionGroup 类的公共属性:</font></strong></font></p>
<script type="text/Javascript">
var ExpCollDivStr=ExpCollDivStr;
ExpCollDivStr = ExpCollDivStr + "ctl00_LibFrame_ctl066893b77,";
var ExpCollImgStr = ExpCollImgStr;
 ExpCollImgStr = ExpCollImgStr + "ctl00_LibFrame_ctl06img,";
</script><p> </p>
<div class="section" id="ctl00_LibFrame_ctl066893b77" style="DISPLAY: block">
<p></p>
<div id="ctl00_LibFrame_ctl06"><table class="memberListTable" cellspacing="2" cellpadding="5" width="500">
<colgroup><font size="2"><col width="10%">
<col width="30%">
<col width="60%"></font></colgroup>
<tbody>
<tr>
<th style="BORDER-RIGHT-STYLE: none"><font size="2"> </font></th>
<th style="BORDER-RIGHT-STYLE: none; BORDER-LEFT-STYLE: none" align="left"><font size="2">名称 </font></th>
<th style="BORDER-LEFT-STYLE: none" align="left"><font size="2">说明 </font></th>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl07',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.anonymousidentification.aspx"><font size="2">AnonymousIdentification</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>anonymousIdentification</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl08',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.authentication.aspx"><font size="2">Authentication</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>authentication</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl09',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.authorization.aspx"><font size="2">Authorization</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>authorization</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl10',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.browsercaps.aspx"><font size="2">BrowserCaps</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>browserCaps</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl11',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.clienttarget.aspx"><font size="2">ClientTarget</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>clientTarget</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl12',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.compilation.aspx"><font size="2">Compilation</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>compilation</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl13',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.customerrors.aspx"><font size="2">CustomErrors</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>customErrors</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl14',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.deployment.aspx"><font size="2">Deployment</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>deployment</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl15',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.devicefilters.aspx"><font size="2">DeviceFilters</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>deviceFilters</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl16',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.globalization.aspx"><font size="2">Globalization</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>globalization</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl17',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.healthmonitoring.aspx"><font size="2">HealthMonitoring</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>healthMonitoring</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl18',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.hostingenvironment.aspx"><font size="2">HostingEnvironment</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>hostingEnvironment</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl19',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.httpcookies.aspx"><font size="2">HttpCookies</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>httpCookies</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl20',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.httphandlers.aspx"><font size="2">HttpHandlers</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>httpHandlers</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl21',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.httpmodules.aspx"><font size="2">HttpModules</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>httpModules</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl22',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.httpruntime.aspx"><font size="2">HttpRuntime</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>httpRuntime</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl23',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.identity.aspx"><font size="2">Identity</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>identity</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl24',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.isdeclarationrequired.aspx"><font size="2">IsDeclarationRequired</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取一个值，该值指示是否需要声明此 <b>ConfigurationSectionGroup</b> 对象。 （从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl25',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl26',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.isdeclared.aspx"><font size="2">IsDeclared</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取一个值，该值指示是否已声明此 <b>ConfigurationSectionGroup</b> 对象。（从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl27',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl28',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.machinekey.aspx"><font size="2">MachineKey</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>machineKey</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl29',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.membership.aspx"><font size="2">Membership</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>membership</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl30',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.mobilecontrols.aspx"><font size="2">MobileControls</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>mobileControls</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl31',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.name.aspx"><font size="2">Name</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取此 <b>ConfigurationSectionGroup</b> 对象的名称属性。（从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl32',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl33',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.pages.aspx"><font size="2">Pages</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>pages</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl34',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.processmodel.aspx"><font size="2">ProcessModel</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>processModel</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl35',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.profile.aspx"><font size="2">Profile</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>profile</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl36',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.protocols.aspx"><font size="2">Protocols</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>protocols</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl37',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.rolemanager.aspx"><font size="2">RoleManager</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>roleManager</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl38',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.sectiongroupname.aspx"><font size="2">SectionGroupName</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取与此 <b>ConfigurationSectionGroup</b> 关联的节组名称。（从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl39',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl40',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.sectiongroups.aspx"><font size="2">SectionGroups</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取一个包含所有 <b>ConfigurationSectionGroup</b> 对象的 <b>ConfigurationSectionGroup</b> 对象，这些对象是此 <b>ConfigurationSectionGroup</b> 对象的子对象。（从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl41',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl42',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.sections.aspx"><font size="2">Sections</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取一个 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl43',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectioncollection.aspx"><font size="2">ConfigurationSectionCollection</font></a><font size="2">，它包含此 <b>ConfigurationSectionGroup</b> 中的所有 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl44',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsection.aspx"><font size="2">ConfigurationSection</font></a><font size="2"> 对象。（从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl45',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl46',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.securitypolicy.aspx"><font size="2">SecurityPolicy</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>securityPolicy</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl47',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.sessionstate.aspx"><font size="2">SessionState</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>sessionState</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl48',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.sitemap.aspx"><font size="2">SiteMap</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>siteMap</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl49',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.trace.aspx"><font size="2">Trace</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>trace</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl50',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.trust.aspx"><font size="2">Trust</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>trust</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf" name="inheritedMember">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl51',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.type.aspx"><font size="2">Type</font></a><font size="2">  </font>
</td>
<td>
<font size="2">获取或设置此 <b>ConfigurationSectionGroup</b> 对象的类型。（从 </font><a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl52',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.configuration.configurationsectiongroup.aspx"><font size="2">ConfigurationSectionGroup</font></a><font size="2"> 继承。）</font>
</td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl53',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.urlmappings.aspx"><font size="2">UrlMappings</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>urlMappings</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl54',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.webcontrols.aspx"><font size="2">WebControls</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>webControls</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl55',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.webparts.aspx"><font size="2">WebParts</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>webParts</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl56',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.webservices.aspx"><font size="2">WebServices</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>webServices</b> 节。</font></td>
</tr>
<tr valign="top" notsupportedon="netcf">
<td class="imageCell"><font size="2"><img alt="Public property" src="/images/hbz_images/1712a73c-779d-4021-aaac-e307c6c085bd.png3"></font></td>
<td>
<a onclick="javascript:TrackThisClick('ctl00_LibFrame_ctl06','ctl00_LibFrame_ctl57',this);" href="http://msdn2.microsoft.com/zh-cn/library/system.web.configuration.systemwebsectiongroup.xhtmlconformance.aspx"><font size="2">XhtmlConformance</font></a><font size="2"> </font>
</td>
<td><font size="2">获取 <b>xhtmlConformance</b> 节。</font></td>
</tr>
</tbody>
</table></div>
<p></p>
</div>				
