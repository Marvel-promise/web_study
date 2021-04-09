# web_study
<%--
  Created by IntelliJ IDEA.
  User: Administrator
  Date: 2021/3/29
  Time: 19:34
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <meta charset="utf-8"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <title>用户登录页面</title>
    <link rel="stylesheet" href="css/footer.css">
    <link href="css/bootstrap.min.css" rel="stylesheet">
    <script src="js/jquery-2.2.4.min.js"></script>
    <script src="js/bootstrap.min.js"></script>
    <script type="text/javascript" src="js/include.js"></script>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .my_div{
            margin: 5px;
            padding: 5px;
        }
        .font_color{
            color: white;
        }
    </style>
    <script type="text/javascript">
        $(function () {
            $("#checkCode").click(function () {
                document.getElementById("checkCode").src="${pageContext.request.contextPath}/checkCodeServlet?time="+new Date().getTime();
            });
            $("#submit").click(function () {
                    $.post("LoginUserServlet",$("#LoginFrom").serialize(),function (data) {
                            if (data.flag){
                                $.get("/index.jsp")
                            }else{
                                $("#log_msg").innerHTML="用户名或密码错误";
                                $("#log_msg").removeAttr("visibility");
                            }
                    });
            });

            // $("#username").onblur()
            /*$("#username").click(function () {
                alert("确定")
            })*/
           /* $("#submit").click(function () {
                if (document.getElementById("username") == null){
                    alert("用户名不能为空");
                }else if(document.getElementById("password") == null){
                    alert("密码不能为空");
                }else if(document.getElementById("inputCheckCode") == null){
                    alert("验证码未填写");
                }
            });*/
            /*$("#username").onblur="function () {\n" +
                "                    var span=document.getElementById(\"namespan\");\n" +
                "                    if (document.getElementById(\"username\") == null){\n" +
                "                        span.css(\"background\",\"red\");\n" +
                "                        span.innerHTML=\"用户名不能为空\";\n" +
                "                        span.slideDown(\"slow\");\n" +
                "                    }else{\n" +
                "                        span.slideUp(\"slow\");\n" +
                "                    }\n" +
                "                }";
            $("#password").onblur = "function () {\n" +
                "                    var span=document.getElementById(\"passpan\");\n" +
                "                    if (document.getElementById(\"password\") == null){\n" +
                "                        span.css(\"background\",\"red\");\n" +
                "                        span.innerHTML=\"密码不能为空\";\n" +
                "                        span.slideDown(\"slow\");\n" +
                "                    }else{\n" +
                "                        span.slideUp(\"slow\");\n" +
                "                    }\n" +
                "                }";
            $("#inputCheckCode").onblur=''*/
        })
    </script>
</head>
<body>
<div id="header"></div>
<div style="width: 100%;height: 100%; background: url(images/login_img.jpg); background-size: 100% 100%;position:relative;">
    <div style=";width: 30%; height: 360px; position: absolute;right: 50px;bottom: 30px" >
        <div align="center">
            <form id="LoginFrom">
                <div class="my_div">
                    <label for="username" class="font_color"><h3>用户名：</h3></label>
                    <input type="text" onblur="checkname()" name="username" placeholder="请输入用户名" id="username"style="height: 45px;width: 200px">
                   <br> <span id="namespan" style="color: white;height: 10px;width: 10px"></span>
                </div>
                <div class="my_div">
                    <label for="password" class="font_color"><h3>密 &nbsp;码：</h3></label>
                    <input type="password" onblur="checkpass()" name="password" placeholder="请输入密码" id="password" style="height: 45px;width: 200px">
                    <br> <span id="passpan" style="color: white;height: 10px;width: 10px"></span>
                </div>
                <div class="my_div">
            <span>
                <label for="checkCode" class="font_color"><h3>验证码：</h3></label>
            <input type="text" name="checkCode" id="inputCheckCode"  placeholder="验证码" style="height: 45px;width: 120px" >
            <img src="${pageContext.request.contextPath}/checkCodeServlet" id="checkCode"
                 title="看不清换一张" name="checkCode" style="width: 75px;height: 45px">
                <span id="codespan"></span>
            </span>
                </div>
                <div class="my_div">
                    <input type="button" value="登录" name="login" id="submit" style="width: 150px;height: 45px">
                </div>
            </form>
            <div align="center" class="my_div">
                <a href="${pageContext.request.contextPath}/register.jsp">新用户注册</a> |
                <a href="#">找回密码</a>
            </div>
            <span id="log_msg" visibility="hidden" style="width: 150px;height: 450px;background: #f40"></span>
        </div>
</div>
</div>
<div id="footer"></div>
</body>
<script type="text/javascript">
    function checkname() {
        var namespan = document.getElementById("namespan");
        if($("#username").val() == null || $("#username").val() == ""){
            namespan.innerHTML="用户名不能为空";
            $("#namespan").show();
        }else{
            $("#namespan").hide();
        }
    }
    function checkpass() {
        var namespan = document.getElementById("passpan");
        if($("#password").val() == null || $("#password").val() == ""){
            namespan.innerHTML="密码不能为空";
            $("#passpan").show();
        }else{
            $("#passpan").hide();
        }
    }
</script>
</html>
