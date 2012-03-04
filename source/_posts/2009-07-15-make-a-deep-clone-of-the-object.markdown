---
layout: post
title: C#中如何深度克隆一个对象？
comments: true
date: 2009-07-15 17:18
categories:
- ASP.NET
- Asp.net
- .Net其他
- C#
- 代码片段
---

<p>如何深度克隆一个对象？</p>
<p>普通版:</p>
<pre>
        public static object CloneObject( object obj )
        {
            using ( MemoryStream memStream = new MemoryStream( ) )
            {
                BinaryFormatter binaryFormatter = new BinaryFormatter( null ,
                     new StreamingContext( StreamingContextStates.Clone ) );
                binaryFormatter.Serialize( memStream , obj );
                memStream.Seek( 0 , SeekOrigin.Begin );
                return binaryFormatter.Deserialize( memStream );
            }
        }
</pre>
<p>泛型版：</p>
<p><!--more--></p>
<pre>public  static  T  Clone&lt;T&gt;(T  obj)
{
        T  ret  =  default(T);
        if  (obj  !=  null)
        {
                XmlSerializer  cloner  =  new  XmlSerializer(typeof(T));
                MemoryStream  stream  =  new  MemoryStream();
                cloner.Serialize(stream,  obj);
                stream.Seek(0,  SeekOrigin.Begin);
                ret  =  (T)cloner.Deserialize(stream);
        }
        return  ret;
}</pre>				
