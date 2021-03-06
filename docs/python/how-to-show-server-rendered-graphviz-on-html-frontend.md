---
author: ''
category: Python
date: '2020-10-08'
summary: ''
title: How to show server rendered graphviz on html frontend
---
# How to show server rendered graphviz on html frontend

I have been trying to render server side generated graphviz graphics on the frontend.
I don't want to generate static image files I want the image generated on the fly and shown on a django frontend template.

The [graphviz output docs](https://graphviz.readthedocs.io/en/stable/manual.html#piped-output) mention that the graph can be output with:

    graph = Digraph(format='svg')
    graph.edge('Hello', 'World')
    context_data['graph'] = graph.pipe().decode('utf-8')

I did this and rendered it in the template with:

    {{ graph }}

And what was shown on the screen was:

    <?xml version="1.0" encoding="UTF-8" standalone="no"?> <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"> <!-- Generated by graphviz version 2.44.1 (20200629.0846) --> <!-- Pages: 1 --> <svg width="74pt" height="116pt" viewBox="0.00 0.00 74.29 116.00" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"> <g id="graph0" class="graph" transform="scale(1 1) rotate(0) translate(4 112)"> <polygon fill="white" stroke="transparent" points="-4,4 -4,-112 70.29,-112 70.29,4 -4,4"/> <!-- Hello --> <g id="node1" class="node"> <title>Hello</title> <ellipse fill="none" stroke="black" cx="33.15" cy="-90" rx="30.59" ry="18"/> <text text-anchor="middle" x="33.15" y="-86.3" font-family="Times,serif" font-size="14.00">Hello</text> </g> <!-- World --> <g id="node2" class="node"> <title>World</title> <ellipse fill="none" stroke="black" cx="33.15" cy="-18" rx="33.29" ry="18"/> <text text-anchor="middle" x="33.15" y="-14.3" font-family="Times,serif" font-size="14.00">World</text> </g> <!-- Hello&#45;&gt;World --> <g id="edge1" class="edge"> <title>Hello&#45;&gt;World</title> <path fill="none" stroke="black" d="M33.15,-71.7C33.15,-63.98 33.15,-54.71 33.15,-46.11"/> <polygon fill="black" stroke="black" points="36.65,-46.1 33.15,-36.1 29.65,-46.1 36.65,-46.1"/> </g> </g> </svg> 

## The Fix

So just ensure that the raw output (without escaping) of the svg is rendered using [django's `safe` tag](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/#std:templatefilter-safe):

    {{ graph | safe }}
