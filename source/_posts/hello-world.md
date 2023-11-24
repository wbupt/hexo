---
title: Hello World
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

···matlab

## 跳转页面成功

```matlab
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>需要验证码验证的页面</title>
	<script type="text/javascript" src="./gVerify.js"></script><!-- 引入验证码js文件 -->
</head>
<body>
	<h1>欢迎访问本网页</h1>
	<p>请输入下方验证码，验证成功后才能进入其他页面：</p>
	<form action="测试.html" method="get" onsubmit="return validate()">
		<input type="text" id="code_input" placeholder="请输入验证码">
		<canvas id="verifyCanvas"></canvas>
		<button type="submit">进入其他页面</button>
	</form>
	<script type="text/javascript">
		var verifyCode = new GVerify("verifyCanvas"); // 初始化验证码
		function validate(){
			var res = verifyCode.validate(document.getElementById("code_input").value); // 验证码验证结果
			if(res){ // 如果验证成功，跳转到其他页面
				return true;
			}
			alert("验证码错误，请重新输入");
			return false;
		}
	</script>
</body>
</html>

```

