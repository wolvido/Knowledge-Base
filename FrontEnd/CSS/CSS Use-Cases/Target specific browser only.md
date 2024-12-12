---
keywords: css target specific browser only
---
#css

Target firefox only:
```css
@supports (-moz-appearance:none) {
    .class {
        color: black;
    }
}
```

Target Webkit browsers only:
```css
@media screen and (-webkit-min-device-pixel-ratio:0) {
    .class {
        color: white;
    }
}
```

for more specific browsers, check:
```css
/** Internet Explorer */
@media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
	div {
	display: block;
	}
}

/** Microsoft Edge */
@supports (-ms-ime-align: auto) {
	div {
	display: block;
	}
}

/** Mozilla Firefox */
@-moz-document url-prefix() {
	div
	display: block;
	}
}

/** Safari */
@media not all and (min-resolution: 0.001dpcm) {
	div
	display: block;
	}
}

/** Chrominum */
@media screen and (-webkit-min-device-pixel-ratio: 0) and (min-resolution: 0.001dpcm) {
	div:not(*:root) {
	display: block;
	}
}
```