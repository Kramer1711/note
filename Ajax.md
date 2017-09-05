# Ajax

标签（空格分隔）： js ajax

---
ajax解决的是web应用的越来越强大而出现的是等待，等待服务器响应，等待浏览器刷新，等待请求返回和生成新的页面。

介绍
---
### 1、什么是Ajax
>Ajax的全称是：Asynchronous  JavaScript  +  XML=异步 javascript + XML

Ajax不是一个技术，它是几种技术的结合体，每种技术都有其独特之处，合
在一起就成为了功能强大的新技术，用于创建快速动态网页的技术。

### 2、宏观Ajax
![宏观Ajax][2]
### 3、Ajax包括：
 >1. HTML，用于建立web表单
 >2. DOM，用于动态显示和交互
 >3. XML，使用XML做数据交互和操作
 >4. XmlHttpRequest，进行异步数据接收
 >5. JavaScript，将它们紧密的结合在一起


Ajax工作原理
---
Web应用程序的原理图，由客户端向服务器提交页面请求，再由服务器通过HTTP传给客户端生成浏览页面。服务器端承担大量的工作，客户端只负责显示。
![传统的Web应用程序原理图][3]
使用Ajax应用程序的工作原理如下图，可见通过Ajax在浏览器与用户交互方面有了很大改进，用户不用为提交Form表单而长时间等待服务器响应，提高用户体验度，而且通过Ajax也可以开发出更加华丽的Web交互页面。客户端界面和Ajax引擎都是在客户端运行，这样大量的服务器工作可以在Ajax引擎处实现，减轻了服务器端的负担。
![使用Ajax的Web应用程序原理图][4]

### Ajax的优缺点：

优点：

 > 1. 最大的一点是页面无刷新，用户的体验度更好。
 > 2. 异步与服务器交互，不需要打断用户操作，具有更快的响应能力。
 > 3. 减轻服务器和带宽的负担，节约空间和成本，ajax是“按需取数据”，可以最大程度的减轻对服务器造成的负担。
 > 4. 基于标准化的并被广泛应用的技术，不需要下载插件或者小程序。

缺点：
>1. 安全问题
>2. 对搜索引擎的支持比较弱。
>3. 破坏了程序的异常处理机制。
>4. 违背了url和资源定位的初衷。

实战
-----
例子：Java版异步验证用户名是否存在

js部分的代码：
``` javascript
<script type="text/javascript">  
    var xmlHttp;  
       
    function createXMLHttpRequest() {  
        //表示当前浏览器不是ie,如ns,firefox  
        if(window.XMLHttpRequest) {  
            xmlHttp = new XMLHttpRequest();  
        } else if (window.ActiveXObject) {  
            xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");  
        }  
    }  
      
    function validate(field) {  
        if (trim(field.value).length != 0) {  
            //创建Ajax核心对象XMLHttpRequest  
            createXMLHttpRequest();  
              
            var url = "user_validate.jsp?userId=" + trim(field.value) + "&time=" + new Date().getTime();  
              
            //设置请求方式为GET，设置请求的URL，设置为异步提交  
            xmlHttp.open("GET", url, true);  
              
            //将方法地址复制给onreadystatechange属性  
            //类似于电话号码  
            xmlHttp.onreadystatechange=callback;  
              
            //将设置信息发送到Ajax引擎  
            xmlHttp.send(null);  
        } else {  
            document.getElementById("spanUserId").innerHTML = "";  
        }     
    }  
    //回调函数  
    function callback() {  
          
        //Ajax引擎状态为成功  
        if (xmlHttp.readyState == 4) {  
            //HTTP协议状态为成功  
            if (xmlHttp.status == 200) {  
                if (trim(xmlHttp.responseText) != "") {  
                    document.getElementById("spanUserId").innerHTML = "<font color='red'>" + xmlHttp.responseText + "</font>"  
                }else {  
                    document.getElementById("spanUserId").innerHTML = "";  
                }  
            }else {  
                alert("请求失败，错误码=" + xmlHttp.status);  
            }  
        }  
    }  
</script>  
```
提交到user_validate.jsp页面的代码：
```java
<%@ page language="java" contentType="text/html; charset=GB18030"  
    pageEncoding="GB18030"%>  
<%@ page import="sysmgr.manager.*" %>  
  
<%  
    String userId = request.getParameter("userId");  
    if (UserManager.getInstance().findUserById(userId) != null) {  
        out.println("用户代码[" + userId + "]已经存在!");  
    }  
%>  
```
总结
---
Web开发一直在追求界面友好，人性化，较高的用户体验度以及更加美观等等，我相信只要从点点滴滴做起，任何问题都不是问题。


  [1]: http://img.blog.csdn.net/20140814192140794?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaml1cWl5dWxpYW5n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast
  [2]: http://img.blog.csdn.net/20151201214739872?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast
  [3]: http://img.blog.csdn.net/20140814211608784?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaml1cWl5dWxpYW5n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast
  [4]: http://img.blog.csdn.net/20140814211555883?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaml1cWl5dWxpYW5n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast