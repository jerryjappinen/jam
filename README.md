# Jam: JavaScript-based language for markup

I can't belive this hasn't been done before. Here you go then.

Jam, short for **Ja**vaScript **markup**, is a JS-like language that compiles into standards-compliant HTML. It is primarily targeted towards web application development, but can be used in any context where preprocessing HTML seems like a good idea.

The syntax is heavily inspired by JavaScipt and CSS - the dominating languages used with a markup language on the web. It is designed from the get-go to be well suited for modern frontend development, especially with Vue.js and its single-file component compiler.

## What Jam looks like

```jam
form.my-class (@submit.prevent: onSubmit) {

	// Jam is not ideal for inline markup, but it can be done
	p {
		'Please fill in this input form' br
		'(But do ' strong { 'not' } ' take too long)'
	}

	// You could also use Markdown
	markdown {
		Please fill in this input form<br>
		(But do **not** take too long)
	}

	// Or fall back to HTML
	raw {
		<p>
			Please fill in this input form<br>
			(But do <strong>not</strong> take too long)
		</p>
	}

	// Some basic tags
	p {
		input (
			v-model: myProp
		)

		input (type: 'submit')
	}

}
```

As the standard file extension, '.jam' is used.

## The Jam toolchain

- Webpack plugin
- CLI
- The parser as a node module

## Background

Currently web development centers around three core pillars: HTML (structure), CSS (styling) and JavaScript (logic). This is how it looks:

```CSS
.foo {
	color: red;
}
```

```html
<pre>
	<code class="foo">This text is red</code>
</pre>
```

```javascript
const foo = []
if (bar) {
	foo.push('bar')
}
```

If you really look into it, the XML syntax seems like the odd man out.

In recent years we've seen a lot of innovation when it comes to frontend development and technologies: CSS preprocessors, many markup languages that compile into HTML, dynamic data binding in HTML, [JSX's]() JS-based markup, render functions written in vanilla JS and much more.

I've never found anything that I'd really prefer over standard HTML, given how in any practical development scenario you will always deal with learning materials centered around the standard toolchain which includes vanilla HTML. Still, the XML syntax is labor-intensive and doesn't have the greatest solution to dynamic bindings.

Handlebars is pretty good, but the syntax is still quite esoteric if your perspective is centered around CSS and JS. There are some weird aspects that have to be patched in by developers who want to stay true to HTML, such as in Vue's binding syntax where expression appear inside quotes, and are escaped by placing a colon _before the property name_. In JavaScript, string literals appear in quotes.

Many languages already provide a nested, indented syntax such as Slim and Pug, but those just replace weird XML syntax with another weird syntax. Curly braces is where it's at if you ask me.

This is where Jam comes in. Turns out, HTML markup can be presented quite nicely in similar syntax with CSS and JS. Jam's design goal is to provide a markup language for application development with a familiar syntax that works well for frequent use of bindings and expressions. It should be suited for both one-time preprocessing as well as declaring component markup in the context of frontend application development. One of our primary design goals is to work well with Vue.js.
