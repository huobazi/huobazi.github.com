---
layout: post
title: 如何判断一个类型是nullable类型，并得知它的原始类型
comments: true
date: 2009-07-30 20:04
categories:
- ORM
- .Net其他
- 代码片段
- Nullable
- 泛型
---

<p>有些时候我们需要判断某个类型是否是Nullable类型，并且可能需要知道它的原始类型，<br />比如在做些ORM相关工作时，就需要这方面的应用，如下代码使用可以实现这个要求</p>
<p><!--more--></p>
<pre>class Program
    {
        static void Main( string[] args )
        {
            RL( );

            Type type =  typeof( DateTime? );
            Type originalType;

            if ( IsNullable( type , out originalType ) )
            {
                WL( originalType.ToString( ) );
            }
            else
            {
                WL( "NOT Nullable" );
            }

            type =  typeof( DateTime );

            if ( IsNullable( type , out originalType ) )
            {
                WL( originalType.ToString( ) );
            }
            else
            {
                WL( "NOT Nullable" );
            }

            RL( );
        }

        private static bool IsNullable( Type p , out Type originalType )
        {
            bool result = false;

            if ( p.IsGenericType &amp;&amp; p.GetGenericTypeDefinition( ) == typeof( Nullable&lt;&gt; ) )
            {
                result = true;
                originalType = p.GetGenericArguments( )[0];
            }
            else
            {
                originalType = null;
            }

            return result;
        }

        #region Helper methods

        private static void WL( object text , params object[] args )
        {
            Console.WriteLine( text.ToString( ) , args );
        }

        private static void RL( )
        {
            Console.ReadLine( );
        }

        private static void Break( )
        {
            System.Diagnostics.Debugger.Break( );
        }

        #endregion
    }

<pre></pre><p></p></pre>				
