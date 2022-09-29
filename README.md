# &lt;blink&gt; Polyfill

The HTML `<blink>` element has been deprecated for many years, but some of us nostalgic types still miss it. I've created this polyfill to bring back that functionality to modern browsers.

## Usage

Simply include the `blink-polyfill.js` file in your document anywhere before the first blink tag.

```
<script src="blink-polyfill.js"></script>
<blink>Hello World! I'm blinking!</blink>
```

## Note

Note that this is not a true polyfill. The W3 in its infinite wisdom [decided to disallow any custom HTML elements that don't contain a hyphen](https://discourse.wicg.io/t/custom-elements-not-requiring-hyphens-in-names/1439), because they might conflict with some future element. (Of course, modern JavaScript libraries create non-hyphen elements [ALL](https://reactjs.org/) [THE](https://vuejs.org/) [TIME](https://angular.io/), but who are we to argue with the W3?) As such, this _doesn't_ create a new element using `customElements.define`.

Instead, we're simply appending custom CSS to the `html` root, so the blink tag remains an `HTMLUnknownElement`. You can achieve exactly the same effect by inserting the following CSS into your stylesheet and save yourself a network lap... but where's the fun in that?

```css
blink {
  animation: 4s linear infinite html4_blink;
}
@keyframes html4_blink {
  0% {
   visibility: visible;
  }
  50% {
    visibility: hidden;
  }
  100% {
    visibility: hidden;
  }
}
```