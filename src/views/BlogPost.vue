<template>
  <div class="section" id="blog-post">
    <div class="container">
			<h1 class="is-size-2 center">{{ post.title }}</h1>
			<figure class="center full">
				<img :src="post.featured_image" alt="">
			</figure>
			<h3 class="center">By {{ post.author.first_name }} {{ post.author.last_name }} - {{ post.created | moment("MMMM Do, YYYY") }}</h3>
			<div class="addthis_inline_share_toolbox"></div>
			<div class="content" v-html="post.body"></div>
			<div class="addthis_inline_share_toolbox mb30"></div>
    </div>
  </div>
</template>

<script>
  import { butter } from '@/buttercms'
  import * as Prism from '../prism.js'
  export default {
    name: 'blog-post',
    data() {
      return {
				post: {
					title: {},
					featured_image: {},
					author: {},
					created: {},
					body: {}
				}
      }
		},
    methods: {
      getPost() {
        butter.post.retrieve(this.$route.params.slug)
          .then((res) => {
            this.post = res.data.data
          }).catch((res) => {
						console.log(res)
					})
					.then(() => {
						window.Prism.highlightAll(false)
					})
      }
		},
    created() {
      this.getPost()
    }
  }
</script>

<style>
.center {
  text-align: center;
}
.full img {
  min-width: 500px;
}
.mb30 {
  margin-bottom: 30px;
}
div.code-toolbar>.toolbar a {
  color: #fff !important;
  font-size: 16px !important;
  padding-top: 7px !important;
  padding-bottom: 7px !important;
  padding-left: 10px !important;
  padding-right: 10px !important;
}

code[class*="language-"],
pre[class*="language-"] {
	color: #fafafa;
	background: none;
	font-family: Consolas, Monaco, 'Andale Mono', 'Ubuntu Mono', monospace;
	text-align: left;
	white-space: pre;
	word-spacing: normal;
	word-break: normal;
	word-wrap: normal;
	line-height: 1.5;

	-moz-tab-size: 4;
	-o-tab-size: 4;
	tab-size: 4;

	-webkit-hyphens: none;
	-moz-hyphens: none;
	-ms-hyphens: none;
	hyphens: none;

}

/* Code blocks */
pre[class*="language-"] {
	padding: 1em;
	margin: .5em 0;
	overflow: auto;
}

:not(pre) > code[class*="language-"],
pre[class*="language-"] {
	background: #222222;
}

/* Inline code */
:not(pre) > code[class*="language-"] {
	padding: .1em;
	border-radius: .3em;
	white-space: normal;
}

.keyword-import,
.keyword-export,
.keyword-from {
	color: #89DDFF !important;
}

.language-typescript .token.punctuation {
	color: #FFCC00 !important;
}

.language-typescript .token.operator {
	color: #C792EA !important;
}

.language-typescript .token.parameter {
	color: #FF5370 !important;
}

.language-typescript .token.builtin {
	color: #89DDFF !important;
}

.language-typescript .token.function {
	color: #6196cc !important;
}

.keyword-this {
	color: #FF5370 !important;
}

.token.comment,
.token.block-comment,
.token.prolog,
.token.doctype,
.token.cdata {
	color: #999;
}

.token.punctuation {
	color: #89DDFF;
}

.token.tag {
	color: #FF5370;
}
.token.attr-name,
.token.namespace,
.token.deleted {
	color: #C792EA;
}

.token.function-name {
	color: #6196cc;
}

.token.boolean,
.token.number,
.token.function {
	color: #f08d49;
}

.token.property,
.token.class-name,
.token.constant,
.token.symbol {
	color: #f8c555;
}

.token.selector,
.token.important,
.token.atrule,
.token.keyword,
.token.builtin {
	color: #cc99cd;
}

.token.string,
.token.char,
.token.attr-value,
.token.regex,
.token.variable {
	color: #7ec699;
}

.token.operator,
.token.entity,
.token.url {
	color: #67cdcc;
}

.token.important,
.token.bold {
	font-weight: bold;
}
.token.italic {
	font-style: italic;
}

.token.entity {
	cursor: help;
}

.token.inserted {
	color: green;
}

pre[data-line] {
	position: relative;
	padding: 1em 0 1em 3em;
}

.line-highlight {
	position: absolute;
	left: 0;
	right: 0;
	padding: inherit 0;
	margin-top: 1em; /* Same as .prism’s padding-top */

	background: hsla(24, 20%, 50%,.08);
	background: linear-gradient(to right, hsla(24, 20%, 50%,.1) 70%, hsla(24, 20%, 50%,0));

	pointer-events: none;

	line-height: inherit;
	white-space: pre;
}

	.line-highlight:before,
	.line-highlight[data-end]:after {
		content: attr(data-start);
		position: absolute;
		top: .4em;
		left: .6em;
		min-width: 1em;
		padding: 0 .5em;
		background-color: hsla(24, 20%, 50%,.4);
		color: hsl(24, 20%, 95%);
		font: bold 65%/1.5 sans-serif;
		text-align: center;
		vertical-align: .3em;
		border-radius: 999px;
		text-shadow: none;
		box-shadow: 0 1px white;
	}

	.line-highlight[data-end]:after {
		content: attr(data-end);
		top: auto;
		bottom: .4em;
	}

.line-numbers .line-highlight:before,
.line-numbers .line-highlight:after {
	content: none;
}

pre[class*="language-"].line-numbers {
	position: relative;
	padding-left: 3.8em;
	counter-reset: linenumber;
}

pre[class*="language-"].line-numbers > code {
	position: relative;
	white-space: inherit;
}

.line-numbers .line-numbers-rows {
	position: absolute;
	pointer-events: none;
	top: 0;
	font-size: 100%;
	left: -3.8em;
	width: 3em; /* works for line-numbers below 1000 lines */
	letter-spacing: -1px;
	border-right: 1px solid #999;

	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

}

	.line-numbers-rows > span {
		pointer-events: none;
		display: block;
		counter-increment: linenumber;
	}

		.line-numbers-rows > span:before {
			content: counter(linenumber);
			color: #999;
			display: block;
			padding-right: 0.8em;
			text-align: right;
		}

div.code-toolbar {
	position: relative;
}

div.code-toolbar > .toolbar {
	position: absolute;
	top: .3em;
	right: .2em;
	transition: opacity 0.3s ease-in-out;
	opacity: 0;
}

div.code-toolbar:hover > .toolbar {
	opacity: 1;
}

div.code-toolbar > .toolbar .toolbar-item {
	display: inline-block;
}

div.code-toolbar > .toolbar a {
	cursor: pointer;
}

div.code-toolbar > .toolbar button {
	background: none;
	border: 0;
	color: inherit;
	font: inherit;
	line-height: normal;
	overflow: visible;
	padding: 0;
	-webkit-user-select: none; /* for button */
	-moz-user-select: none;
	-ms-user-select: none;
}

div.code-toolbar > .toolbar a,
div.code-toolbar > .toolbar button,
div.code-toolbar > .toolbar span {
	color: #bbb;
	font-size: .8em;
	padding: 0 .5em;
	background: #f5f2f0;
	background: rgba(224, 224, 224, 0.2);
	box-shadow: 0 2px 0 0 rgba(0,0,0,0.2);
	border-radius: .5em;
}

div.code-toolbar > .toolbar a:hover,
div.code-toolbar > .toolbar a:focus,
div.code-toolbar > .toolbar button:hover,
div.code-toolbar > .toolbar button:focus,
div.code-toolbar > .toolbar span:hover,
div.code-toolbar > .toolbar span:focus {
	color: inherit;
	text-decoration: none;
}

/* Fallback, in case JS does not run, to ensure the code is at least visible */
[class*='lang-'] script[type='text/plain'],
[class*='language-'] script[type='text/plain'],
script[type='text/plain'][class*='lang-'],
script[type='text/plain'][class*='language-'] {
	display: block;
	font: 100% Consolas, Monaco, monospace;
	white-space: pre;
	overflow: auto;
}
</style>