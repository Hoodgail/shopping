<script lang="ts">
	const checkpoint: {
		container?: HTMLElement;
		body?: HTMLElement;
	} = {};
	let headerDropdown: HTMLElement;

	function dropdownExit() {}
	function dropdown(node: HTMLElement) {
		function mouseexit() {
			const { container, body } = checkpoint;
			if (!container || !body) return;

			container.insertAdjacentElement('beforeend', body);
		}
		function mouseenter() {
			console.log(node);
			mouseexit();

			const body = <HTMLElement>this.querySelector('.body');
			checkpoint.container = this;
			checkpoint.body = body;

			console.log(headerDropdown, body);
			headerDropdown.insertAdjacentElement('beforeend', body);
		}
		node.addEventListener('mouseenter', mouseenter);
		// node.addEventListener('mouseleave', mouseexit);
		return {
			destroy() {
				node.removeEventListener('mouseenter', mouseenter);
				// node.removeEventListener('mouseleave', mouseexit);
			}
		};
	}
	function d(node: HTMLElement) {
		function onfocus() {}
		node.addEventListener('mousedown', onfocus);
		node.addEventListener('focus', onfocus);
		return {
			destroy() {
				node.removeEventListener('mousedown', onfocus);
			}
		};
	}
</script>

<header on:focus={(e) => console.log(e, this)} use:d tabindex="0">
	<div class="main">
		<div data-left>
			<a href="/">Shoping Site</a>
		</div>
		<div data-center>
			<div class="dropdown" use:dropdown>
				<div class="header">
					<a href="">Shop</a>
				</div>
				<div class="body">
					<a href="/shop/mens">Men's</a>
					<a href="/shop/womens">Women's</a>
					<a href="/shop/Jewerely">Jewelery</a>
					<a href="/shop/Electronics">Electronics</a>
				</div>
			</div>
			<a href="">Our Story</a>
			<a href="">Find store</a>
		</div>
		<div data-right>
			<div class="input-wrapper">
				<input type="text" placeholder="Search" on:keypress={() => {}} />
			</div>
			<select name="" id="language">
				<option value="English">English</option>
			</select>
			<div>cart</div>
		</div>
	</div>
	<div class="dropdown-container" bind:this={headerDropdown} />
</header>

<style lang="scss">
	a {
		color: inherit;
		text-decoration: none;
	}
	header {
		background-color: lavender;
		.main {
			display: flex;
			justify-content: space-between;
			align-items: center;
			height: 5.5rem;
			padding: var(--padding);
			> * {
				flex: 1;
				gap: 10px;
			}
			.dropdown {
				.body {
					display: none;
				}
			}
		}
		.dropdown-container {
			// &:empty {
			// 	display: none;
			// }
			backdrop-filter: sepia(10%) contrast(102%);
			.body {
				width: 50%;
				margin-inline: auto;
				display: flex;
				justify-content: space-around;
				padding: 15px; // 1.5
				gap: 50px;
				// color: white;
				// filter: brightness(80%);
				// background-color: blue;
			}
		}
	}
	@font-face {
		font-family: 'MyWebFont';
		src: url('/fonts/Monoton-Regular.ttf') format('truetype');
		src: url('/fonts/RubikMoonrocks-Regular.ttf') format('truetype');
		src: url('/fonts/Rye-Regular.ttf') format('truetype');
	}

	[data-left] {
		font-family: MyWebFont;
		font-size: 25px;
	}

	[data-center] {
		display: flex;
		justify-content: space-around;
	}
	[data-right] {
		display: flex;
		justify-content: flex-end;
	}
	.input-wrapper {
		user-select: none;
		border: 1px solid gray;
		border-radius: 3px;
		height: 30px;
		background-color: rgb(255, 255, 255, 0.5);
		padding: 0 10px;
		&:hover {
			background-color: rgb(255, 255, 255, 0.7);
		}
		// box-sizing: border-box;
		input {
			width: 100%;
			height: 100%;
			outline: none;
			border: none;
			background-color: transparent;
		}
	}
	.input-wrapper:before {
		content: url(image.jpg);
		// content: '';
		display: block;
		position: absolute;
		width: 100px;
		height: 100px;
		pointer-events: none;
		// background-color: black;
		right: 0;
		input {
			width: 100%;
			height: 100%;
		}
	}
</style>
