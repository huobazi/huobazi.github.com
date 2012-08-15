---
layout: post
published: treu
title: 自定义控件实现广告内容后期加载，以及NamingContainer层次的应用
comments: true
date: 2007-08-05 13:49
categories:
- ASP.NET
- Asp.net
- 自定义控件
- NamingContainer
---

<p>自定义控件：广告内容后期加载。以及NamingContainer层次的应用<br />网站上的广告内容可能会因加载过慢而导致整个网页加载过慢<br />我们可以考虑将广告内全部放在网页最底部，等整个页面加载完毕後<br />再采用javascript使其显示，考虑给控件一个TargetContainerID标识<br />控件广告内容将要被显示的容器ID，然后从控件自己所处的 开始向上查找该ID<br />所指定的控件，(我们只向上找而没有向下找，并且没有处理某层次的<br />子NamingContainer,所以不一定能够找到，这里没有考虑从Page对象向下递归查找<br />主要考虑为了提高性能),如果没有找到，则考虑给用户一个事件让用户自己处理TargetContainer</p>
<p>下面的自定义控件对此实现了封装:</p>

<!--more-->

```
	//------------------------------------------------------------------------------
	//
	// Copyright (c) www.AspxBoy.com All rights reserved.
	//
	//------------------------------------------------------------------------------
	namespace HBZ.Ads.Controls
	{
		using System;
		using System.ComponentModel;
		using System.Web;
		using System.Web.UI;
		using System.Web.UI.WebControls;
		using HBZ.Ads;
		using System.Collections.Generic;
		using System.Text;
		[Designer( typeof( HBZ.Ads.Controls.AdRotatorDesigner ) )]
		public class AdRotator : WebControl
		{
			private Dictionary findControlHelperCacheList = new Dictionary( );
			private readonly string scriptFormat = " var {0}_target = document.getElementById(\"{0}\"); var {1}_base = document.getElementById(\"{1}\"); if ({0}_target)  {0}_target.innerHTML = {1}_base.innerHTML; if ({0}_target)  {1}_base.innerHTML = \"\"; ";
			private static readonly object eventObj = new object( );
			public event FindTargetContainerEventHandler FindTargetContainer
			{
				add
				{
					Events.AddHandler( eventObj , value );
				}
				remove
				{
					Events.RemoveHandler( eventObj , value );
				}
			}
			public AdRotator( )
			: base( HtmlTextWriterTag.Span )
			{
			}
			[TypeConverter( typeof( ValidatedControlConverter ) )]
			[DefaultValue( "" ) , Category( "Data" ) , Description( "广告位后期加载后显示的位置的控件ID" )]
			[IDReferenceProperty]
			public string TargetContainerID
			{
				get
				{
					return (string)this.ViewState[ "TargetContainerID" ] ?? string.Empty;
				}
				set
				{
					this.ViewState[ "TargetContainerID" ] = value;
				}
			}
			[Bindable( true ) , Category( "Data" ) , DefaultValue( "" ) , Description( "广告位的默认内容" )]
			public string DefaultContent
			{
				get
				{
					return (string)this.ViewState[ "DefaultContent" ] ?? "广告位招租";
				}
				set
				{
					this.ViewState[ "DefaultContent" ] = value;
				}
			}
			protected override void OnPreRender( EventArgs e )
			{
				base.OnPreRender( e );
				if ( !string.IsNullOrEmpty( TargetContainerID ) )
				{
					this.Style.Add( HtmlTextWriterStyle.Display , "none" );
					ClientScriptManager cs = Page.ClientScript;
					if ( !cs.IsStartupScriptRegistered( this.ClientID ) )
					{
						cs.RegisterStartupScript( this.GetType( ) , this.ClientID , GetLazyLoadingScript( ) , true );
					}
				}
			}
			protected virtual string GetLazyLoadingScript( )
			{
				Control target = FindControlHelper( TargetContainerID );
				if ( target == null )
				{
					throw new TargetContainerNotFoundException( );
				}
				StringBuilder sb = new StringBuilder( );
				sb.AppendFormat( scriptFormat , target.ClientID , this.ClientID );
				return sb.ToString( );
			}
			protected virtual void RenderAdvertisement( Advertisement ad , HtmlTextWriter writer )
			{
				// 广告内容
			}
			protected override void RenderContents( HtmlTextWriter writer )
			{
				// call RenderAdvertisement method
			}
			protected Control FindControlHelper( string id )
			{
				Control c = null;
				if ( findControlHelperCacheList.ContainsKey( id ) )
				{
					c = findControlHelperCacheList[ id ];
				}
				else
				{
					c = base.FindControl( id ); // 注意：我们从自己开始向上沿NamingContainer层次查找
					Control nc = NamingContainer;
					while ( ( null == c ) && ( null != nc ) )
					{
						c = nc.FindControl( id );
						nc = nc.NamingContainer;
					}
					if ( null == c )
					{
						// 因为我们是从自己开始向上沿NamingContainer层次查找，而没有向下找，
						// 并且没有找每一层NamingContainer内的其他NamingContainer,
						// 所以这种查找有可能出现没有找到id对应的控件
						// 当没此时有找到时，激发FindTargetContainer事件交给用户自己设定Target Container Control
						FindTargetContainerEventArgs args = new FindTargetContainerEventArgs( id );
						OnFindTargetContainer( args );
						c = args.Control;
					}
					if ( null != c )
					{
						findControlHelperCacheList[ id ] = c;
					}
				}
				return c;
			}
			protected virtual void OnFindTargetContainer( FindTargetContainerEventArgs e )
			{
				FindTargetContainerEventHandler hander = Events[ eventObj ] as FindTargetContainerEventHandler;
				if ( hander != null )
				{
					hander( this , e );
				}
			}
		}
		public delegate void FindTargetContainerEventHandler( object src , FindTargetContainerEventArgs e );
		public class FindTargetContainerEventArgs : EventArgs
		{
			private string controlID;
			private Control control;
			public FindTargetContainerEventArgs( string controlId )
			{
				controlID = controlId;
			}
			public string ControlID
			{
				get
				{
					return controlID;
				}
			}
			public Control Control
			{
				get
				{
					return control;
				}
				set
				{
					control = value;
				}
			}
		}
		public class TargetContainerNotFoundException : Exception
		{
			string exceptionMessage = string.Empty;
			public TargetContainerNotFoundException( )
			: this( "TargetContainerID所指定的控件没有找到！您或许应该处理一下FindTargetContainer事件" )
			{
			}
			public TargetContainerNotFoundException( string message )
			: base( message )
			{
				this.exceptionMessage = message;
			}
			public override string Message
			{
				get
				{
					if ( exceptionMessage != null )
					{
						return exceptionMessage;
					}
					return base.Message;
				}
			}
		}
	}
	```