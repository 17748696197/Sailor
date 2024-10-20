<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个人主页</title>
    <link rel="stylesheet" href="/src/demo/bootstrap-5.3.3-dist/css/bootstrap.min.css">
    <!-- 自定义样式文件 -->
    <link rel="stylesheet" href="css/style.css">
    <link rel="stylesheet" href="bili.css">
        <!-- Stylesheets -->
    <link rel="stylesheet" href="help.css">

  	<!--[if lt IE 9]>
  	  <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
  	  <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
  	<![endif]--> 

	<!-- Font icons --> 
    <link rel="stylesheet" href="icon-fonts/fontawesome-5.8.1/css/all.min.css">

	   <!-- Google Font -->
    <link href="https://fonts.googleapis.com/css?family=Poppins:400,500,600,700,900" rel="stylesheet">

    <style>
        /* 使标题浮动在 banner 上 */
        header {
            position: absolute;
            top: 4%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
            text-align: center;
            color: white;
        }

        header h1 {
            font-size: 3rem;
            font-weight: bold;
            text-shadow: 2px 2px 10px rgba(0, 0, 0, 0); /* 增加标题的阴影 */
        }

        /* 目录链接放置在 banner 的右上角 */
        nav {
            position: absolute;
            top: 10px;
            right: 20px;
            background-color: rgba(255, 255, 255, 0.8);
            padding: 10px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            z-index: 10; /* 保证导航栏浮动在 banner 图片之上 */
        }

        nav ul {
            list-style: none;
            margin: 0;
            padding: 0;
            text-align: right;
        }

        nav ul li {
            margin-bottom: 10px;
        }

        nav ul li a {
            text-decoration: none;
            color: #333;
            font-weight: bold;
            padding: 5px 10px;
        }

        nav ul li a:hover {
            color: #007bff;
            text-decoration: underline;
        }

        .banner {
            position: relative;
            width: 100%;
            height: 160px; /* 设置 banner 高度 */
            overflow: hidden;
        }

        .image img {
            width: 100%;
            height: auto;
        }
    </style>
</head>
<body>

<header>
    <h1>欢迎来到我的个人主页</h1>
    <!-- Menu -->
		<div class="menu">
			<span></span>
			<span></span>
		</div>
</header>

<!-- 右上角的导航目录，浮动在 banner 上 -->
	<div class="right-menu">
		<div class="menu-close"></div>
		<div class="page-menu">
			<ul>
				<li><a data-type="ajax-load" href="index.html">Home</a></li>
				<li><a data-type="ajax-load" href="about.html">About</a></li>
				<li><a data-type="ajax-load" href="contact.html">Contact</a></li>
		</div>
	</div>
		

<div class="banner">
    <div class="image"><img src="./css/images/bg.png" alt="背景图像"></div>
    <div class="image"><img src="./css/images/girl1.png" alt="人物图像"></div>
    <div class="image"><img src="./css/images/grassland.png" alt="草原图像"></div>
    <div class="image"><img src="./css/images/mushroom.png" alt="蘑菇图像"></div>
    <div class="image"><img src="./css/images/spirit.png" alt="精灵图像"></div>
    <div class="image"><img src="./css/images/leaf.png" alt="叶子图像"></div>
</div>

<script>
    let x = 0;
    let x_new = 0;
    let x_offset = 0;

    let banner = document.querySelector('.banner');
    let images = document.querySelectorAll('.image');

    let window_width = document.documentElement.clientWidth;
    let step = window_width / 2 / 5;

    let data_images = [
        { x: 0, b: 4 },
        { x: 0, b: 0 },
        { x: 0, b: 1 },
        { x: 0, b: 4 },
        { x: 0, b: 5 },
        { x: 0, b: 6 },
    ]

    let init = () => {
        for (const key in images) {
            if (images.hasOwnProperty(key)) {
                const element = images[key];
                const element_data = data_images[key];
                element.children[0].style = 'transition: .2s linear; transform: translate(' + element_data.x + 'px); filter: blur(' + element_data.b + 'px);';
            }
        }
    }

    banner.addEventListener('mouseover', (e) => {
        x = e.clientX;
    });

    banner.addEventListener("mousemove", (e) => {
        x_new = e.clientX;
        x_offset = x - x_new;
        for (const key in images) {
            if (images.hasOwnProperty(key)) {
                let level = (6 - parseInt(key)) * 10;
                const element = images[key];
                const element_data = data_images[key];
                let b_new = Math.abs(element_data.b + (x_offset / step));
                let l_new = 0 - (x_offset / level);
                element.children[0].style = 'transform: translate(' + l_new + 'px); filter: blur(' + b_new + 'px);';
            }
        }
    });

    banner.addEventListener("mouseout", (e) => {
        init();
    });

    blink_index = 0;
    timeout = 4000;
    let blink = () => {
        if (blink_index == 4) {
            blink_index = 1;
            timeout = 4000;
        } else {
            blink_index += 1;
            timeout = 30;
        }

        images[1].children[0].src = './css/images/girl' + blink_index + '.png';
        setTimeout(() => {
            blink();
        }, timeout);
    }

    window.onload = () => {
        init();
        blink();
    }
</script>

<div class="container mt-5">
    <h2>主页内容</h2>
    <p>欢迎来到我的个人主页，这是一个简短的介绍。</p>
</div>

        <script src="js/jquery-2.1.4.min.js"></script>
		<script src="js/plugins.js"></script>
		<script src="js/main.js"></script>
</body>
</html>
