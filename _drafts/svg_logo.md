---
title: SVG Logo
layout: post
tag: design development
---

The logo for DIPPAM was designed by XXX.

It was made to look like a stack of records, arranged to resemble the island of Ireland.  The linear gradient fill represents migration away from the island.

Since the project houses three distinct collections (EPPI, IED and VMR), it was also designed so that the fill colour could be swapped to match the brand colours of each collection.

When updating the site I didn't have the source files to hand, only a bitmap that had to be resized.  Given the simple geometry of the logo, I wanted to try encoding it as SVG.

SVG wasn't broadly supported when the first version of the site launched.  Browser filters were required, and in some browsers it wasn't supported at all.  Now, however, we can use it.

I used [Inkscape](https://inkscape.org/) to trace the outline and then optimised the result by hand.  This is the output from Inkscape:

```

```

And this is after removing the unnecessary elements:

```
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 570" version="1.1">
	<defs>
		<linearGradient id="c" x1="0%" y1="10%" x2="100%" y2="20%">
			<stop offset="0%" style="stop-opacity: 0"/>
			<stop offset="80%" style="stop-opacity: 0.9"/>
		</linearGradient>
	</defs>
	<g style="fill: url(#c)">
		<path d="m 87,0   296,0  40,180 -296,0 z"/>
		<path d="m 0,375  425,0  0,-180 -400,0 z"/>
		<path d="m 76,392 348,0 -40,180 -370,0 z"/>
	</g>
</svg>
```

The following CSS is also used:

```
svg { height: 3em; width: 3em; }
stop { stop-color: #060; }
```

# Viewbox

# Path Simplication

# Linear Gradient

# Dynamic Colouring

The linear gradient is applied to all graphic elements by applying it directly to the <g> element.

The stop colour of the linear gradient is specified in CSS.

Q: Can a linear gradient be expressed in CSS alone?

Q: Does it need to be embedded in the document for this to work?

# SVG Resources

- 





