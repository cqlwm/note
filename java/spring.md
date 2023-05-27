# Test Blog

## title 2

### hi

以下是一个简单的商品卡片页面的HTML和CSS代码示例：

```html
<!DOCTYPE html>
<html>
<head>
	<title>商品卡片页面</title>
	<style>
		.card {
			border: 1px solid #ccc;
			border-radius: 5px;
			padding: 10px;
			width: 300px;
			margin: 10px;
			box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
		}

		.card img {
			width: 100%;
			height: auto;
			border-radius: 5px;
			margin-bottom: 10px;
		}

		.card h2 {
			font-size: 1.2rem;
			margin: 0;
			margin-bottom: 10px;
		}

		.card p {
			font-size: 1rem;
			margin: 0;
			margin-bottom: 10px;
		}

		.card .price {
			font-size: 1.2rem;
			font-weight: bold;
			color: #f00;
			margin: 0;
			margin-bottom: 10px;
		}

		.card button {
			background-color: #f00;
			color: #fff;
			border: none;
			border-radius: 5px;
			padding: 10px;
			cursor: pointer;
		}

		.card button:hover {
			background-color: #d00;
		}

		.card input[type="number"] {
			width: 50px;
			padding: 5px;
			border-radius: 5px;
			border: 1px solid #ccc;
			margin-right: 10px;
		}
	</style>
</head>
<body>
	<div class="card">
		<img src="https://via.placeholder.com/300x200" alt="商品图片">
		<h2>商品标题</h2>
		<p class="price">$99.99</p>
		<p>商品描述</p>
		<div>
			<input type="number" value="1" min="1">
			<button>添加到购物车</button>
		</div>
	</div>
</body>
</html>
```

这个示例中，我们使用了一个 `div` 元素来创建一个商品卡片。卡片的样式由 `.card` 类选择器定义。卡片包含一个商品图片，一个商品标题，商品价格，一个商品描述，以及一个添加到购物车按钮和一个数字框。

我们使用了 `img` 元素来显示商品图片，并使用 CSS 样式来设置图片的大小和圆角边框。商品标题和商品描述使用了 `h2` 和 `p` 元素，分别设置了不同的字体大小和边距。商品价格使用了 `.price` 类选择器来设置字体大小、加粗和颜色。

添加到购物车按钮使用了 `button` 元素，并设置了背景颜色、字体颜色、边框和圆角。当鼠标悬停在按钮上时，我们使用了 `:hover` 伪类选择器来改变的背景颜色。

最后，我们使用了 `input` 元素来创建一个数字框，用户可以在其中选择商品数量。我们设置了数字框的宽度、内边距、边框和圆角。