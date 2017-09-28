+++
title = "Writing inline demos"
weight = 3
+++

There are some issues with {{% pattern "CodePen embedding" %}}, like them not working offline. They also come with CodePen branding, which will clash with the pattern you're trying to illustrate.

**Infusion** offers another option: a special `demo` shortcode that allows you to write HTML, CSS, and JavaScript directly into the markdown file. The outputted demo is encapsulated using Shadow DOM, so you don't have to worry about broken styles and global JS.

Here's the example code for an inline demo of a toggle button:

{{<codeBlock lang="html">}}
&#x7b;{&lt;demo>}}
&lt;button aria-pressed="false">Toggle Me&lt;/button>
&lt;style>
button {
    background: DarkCyan;
    color: white;
    border: 0;
    font-size: 1.5rem;
    padding: 0.5em 1em;
    border-right: 5px solid #000;
    border-bottom: 5px solid #000;
}

[aria-pressed="true"] {
  border: 0;
  border-top: 5px solid #000;
  border-left: 5px solid #000;
}
&lt;/style>
&lt;script>
var toggle = demo.querySelector('[aria-pressed]');

toggle.addEventListener('click', (e) => {  
  let pressed = e.target.getAttribute('aria-pressed') === 'true';
  e.target.setAttribute('aria-pressed', !pressed);
});
&lt;/script>
&#x7b;{&lt;/demo>}}
{{</codeBlock>}}

Note the `demo.querySelector` on line `21`. **Infusion** automatically provides `demo`, representing the root node of the demo. It's like the `document` keyword but for a demo's subtree.

Here's a live demo of&hellip; the demo:

{{<demo>}}
<button aria-pressed="false">Toggle Me</button>
<style>
button {
    background: DarkCyan;
    color: white;
    border: 0;
    border-radius: 0.25em;
    font-size: 1.5rem;
    padding: 0.5em 1em;
    border-right: 5px solid #000;
    border-bottom: 5px solid #000;
}

[aria-pressed="true"] {
  border: 0;
  border-top: 5px solid #000;
  border-left: 5px solid #000;
}
</style>
<script>
var toggle = demo.querySelector('[aria-pressed]');

toggle.addEventListener('click', function () {  
  var pressed = this.getAttribute('aria-pressed') === 'true';
  this.setAttribute('aria-pressed', !pressed);
});
</script>
{{</demo>}}

## Launch in a separate window

The "Launch in separate window" button takes the demo code and pushes it to a new browser window. This serves two purposes:

* It provides a fallback for browsers that do not support Shadow DOM encapsulation (a warning message will replace the inline demo).
* It creates an isolated test case for the demo, allowing you to run browser extensions and bookmarklets on the the demo code and _just_ the demo code.

## Captioned demos

It's possible to give your demo a caption using an accessible `<figure>` and `<figcaption>` structure. All _you_ need to do is supply a `caption` attribute. For example:

{{<codeBlock lang="html">}}
&#x7b;{&lt;demo caption="A basic button element">}}
&lt;!-- demo code here -->
&#x7b;{&lt;/demo>}}
{{</codeBlock>}}

Along with the standard `figure` shortcodes (described in {{% pattern "Including images" %}}), demo figures are numbered automatically according to their order in the page. You can use markdown syntax in the caption text value.

## Background colors

Sometimes your component will be expected to appear in a context where the parent element has a background color. You can add a backgroundColor for your demo block using the `backgroundColor` attribute. Any valid CSS color value is acceptable:

{{<codeBlock lang="html">}}
&#x7b;{&lt;demo backgroundColor="hsla(163, 100%, 50%, 0.43)">}}
&lt;!-- demo code here -->
&#x7b;{&lt;/demo>}}
{{</codeBlock>}}
