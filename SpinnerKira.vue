<template>
	<div class="half-circle-spinner" :style="spinnerStyle">
		<div class="circle circle-1" :style="circle1Style"></div>
		<div class="circle circle-2" :style="circle2Style"></div>
		<div class="atom-spinner">
			<div class="spinner-inner">
				<div class="spinner-line"></div>
				<div class="spinner-line"></div>
				<div class="spinner-line"></div>
				<!--Chrome renders little circles malformed :(-->
				<div class="spinner-circle">&#9679;</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'HalfCircleSpinner',
	props: {
		animationDuration: {
			type: Number,
			default: 1000,
		},
		size: {
			type: Number,
			default: 112,
		},
		color: {
			type: String,
			default: '#7f9cf5',
		},
	},
	computed: {
		spinnerStyle() {
			return {
				height: `${this.size}px`,
				width: `${this.size}px`,
			}
		},
		circleStyle() {
			return {
				borderWidth: `${this.size / 16}px`,
				animationDuration: `${this.animationDuration}ms`,
			}
		},
		circle1Style() {
			return Object.assign(
				{
					borderTopColor: this.color,
				},
				this.circleStyle
			)
		},
		circle2Style() {
			return Object.assign(
				{
					borderBottomColor: this.color,
				},
				this.circleStyle
			)
		},
	},
}
</script>

<style scoped>
.color {
	@apply bg-indigo-500 bg-indigo-400 bg-pink-500;
}

.half-circle-spinner,
.half-circle-spinner * {
	box-sizing: border-box;
}
.half-circle-spinner {
	width: 60px;
	height: 60px;
	border-radius: 100%;
	position: relative;
}
.half-circle-spinner .circle {
	content: '';
	position: absolute;
	width: 100%;
	height: 100%;
	border-radius: 100%;
	border: calc(60px / 10) solid transparent;
}
.half-circle-spinner .circle.circle-1 {
	border-top-color: #667eea;
	animation: half-circle-spinner-animation 1s infinite;
}
.half-circle-spinner .circle.circle-2 {
	border-bottom-color: #667eea;
	animation: half-circle-spinner-animation 1s infinite alternate;
}
@keyframes half-circle-spinner-animation {
	0% {
		transform: rotate(0deg);
	}
	100% {
		transform: rotate(360deg);
	}
}
.atom-spinner,
.atom-spinner * {
	box-sizing: border-box;
}

.atom-spinner {
	height: 100%;
	width: 100%;
	overflow: hidden;
}

.atom-spinner .spinner-inner {
	position: relative;
	display: block;
	height: 100%;
	width: 100%;
}

.atom-spinner .spinner-circle {
	display: block;
	position: absolute;
	color: #ed64a6;
	font-size: calc(50px * 0.24);
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}

.atom-spinner .spinner-line {
	position: absolute;
	left: 15%;
	top: 15%;
	width: 70%;
	height: 70%;
	border-radius: 50%;
	animation-duration: 2s;
	border-left-width: calc(75px / 15);
	border-top-width: calc(75px / 15);
	border-left-color: #7f9cf5;
	border-left-style: solid;
	border-top-style: solid;
	border-top-color: transparent;
}

.atom-spinner .spinner-line:nth-child(1) {
	animation: atom-spinner-animation-1 1450ms linear infinite;
	transform: rotateZ(120deg) rotateX(66deg) rotateZ(0deg);
}

.atom-spinner .spinner-line:nth-child(2) {
	animation: atom-spinner-animation-2 1450ms linear infinite;
	transform: rotateZ(240deg) rotateX(66deg) rotateZ(0deg);
}

.atom-spinner .spinner-line:nth-child(3) {
	animation: atom-spinner-animation-3 1450ms linear infinite;
	transform: rotateZ(360deg) rotateX(66deg) rotateZ(0deg);
}

@keyframes atom-spinner-animation-1 {
	100% {
		transform: rotateZ(120deg) rotateX(66deg) rotateZ(360deg);
	}
}

@keyframes atom-spinner-animation-2 {
	100% {
		transform: rotateZ(240deg) rotateX(66deg) rotateZ(360deg);
	}
}

@keyframes atom-spinner-animation-3 {
	100% {
		transform: rotateZ(360deg) rotateX(66deg) rotateZ(360deg);
	}
}
</style>
