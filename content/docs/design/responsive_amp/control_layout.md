---
$title: Layout & media queries
$order: 1
toc: true
---
[TOC]


AMP supports both **media queries** &amp; **element queries**, plus comes with a powerful, built-in way to control the **layout** of individual elements. The `layout` attribute makes working with and creating fully responsive design much easier than if you'd use CSS alone.

## Responsive images, made easy

Create responsive images by specifying the `width` and `height`, setting layout to `responsive`,
and indicating with [`srcset`]({{g.doc('/content/docs/design/responsive_amp/art_direction.md', locale=doc.locale).url.path}})
which image asset to use based on varying screen sizes:

[sourcecode:html]
<amp-img
    src="/img/narrow.jpg"
    srcset="/img/wide.jpg 640w,
           /img/narrow.jpg 320w"
    width="1698"
    height="2911"
    layout="responsive"
    alt="an image">
</amp-img>
[/sourcecode]

This `amp-img` element automatically fits the width
of its container element,
and its height is automatically set to the aspect ratio
determined by the given width and height. Try it out by resizing this browser window:

<amp-img src="/static/img/background.jpg" width="1920" height="1080" layout="responsive"></amp-img>

Tip: See our side-by-side live demos of `amp-img`: [Live Demos on AMP By Example](https://ampbyexample.com/components/amp-img/).

## The layout attribute

The `layout` attribute gives you easy, per-element control over how your element
should render on screen. Many of these things are possible with pure CSS – but
they're much harder, and require a myriad of hacks. Use the `layout` attribute instead.

### Supported values for  the `layout` attribute

The following values can be used in the `layout` attribute:

<table>
  <thead>
    <tr>
      <th data-th="Layout type" class="col-thirty">Layout type</th>
      <th data-th="Width/height required" class="col-twenty">Width/<br>height required</th>
      <th data-th="Behavior">Behavior</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Layout type"><code>nodisplay</code></td>
      <td data-th="Description">No</td>
      <td data-th="Behavior">Element not displayed. This layout can be applied to every AMP element. The component takes up zero space on the screen as if its display style was none. It’s assumed that the element can display itself on user action, for example, <a href="/docs/reference/components/amp-lightbox.html"><code>amp-lightbox</code></a>.</td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>fixed</code></td>
      <td data-th="Description">Yes</td>
      <td data-th="Behavior">Element has a fixed width and height with no responsiveness supported. The only exceptions are <a href="/docs/reference/components/amp-pixel.html"><code>amp-pixel</code></a> and <a href="/docs/reference/components/amp-audio.html"><code>amp-audio</code></a> elements.</td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>responsive</code></td>
      <td data-th="Description">Yes</td>
      <td data-th="Behavior">Element sized to the width of its container element and resizes its height automatically to the aspect ratio given by width and height attributes. This layout works very well for most of AMP elements, including <a href="/docs/reference/components/amp-img.html"><code>amp-img</code></a>, <a href="/docs/reference/components/amp-video.html"><code>amp-video</code></a>. Available space depends on the parent element and can also be customized using <code>max-width</code> CSS.<p><strong>Note</strong>: Elements with <code>"layout=responsive"</code> have no intrinsic size. The size of the element is determined from its container element. To ensure your AMP element displays, you must specify a width and height for the  containing element. Do not specify <code>"display:table"</code> on the containing element as this overrides the display of the AMP element, rendering the AMP element invisible.</p></td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>fixed-height</code></td>
      <td data-th="Description">Height only</td>
      <td data-th="Behavior">Element takes the space available to it but keeps the height unchanged. This layout works well for elements such as <a href="/docs/reference/components/amp-carousel.html"><code>amp-carousel</code></a> that involves content positioned horizontally. The <code>width</code> attribute must not be present or must be equal to <code>auto</code>.</td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>fill</code></td>
      <td data-th="Description">No</td>
      <td data-th="Behavior">Element takes the space available to it, both width and height. In other words, the layout of a fill element matches its parent. For an element to fill its parent container, ensure the parent container specifies `position:relative` or `position:absolute`.</td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>container</code></td>
      <td data-th="Description">No</td>
      <td data-th="Behavior">Element lets its children define its size, much like a normal HTML <code>div</code>. The component is assumed to not have specific layout itself but only act as a container. Its children are rendered immediately.</td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>flex-item</code></td>
      <td data-th="Description">No</td>
      <td data-th="Behavior">Element and other elements in its parent take the parent container's remaining space when the parent is a flexible container (i.e., <code>display:flex</code>). The element size is determined by the parent element and the number of other elements inside the parent according to the <code>display:flex</code> CSS layout.</td>
    </tr>
    <tr>
      <td data-th="Layout type"><code>intrinsic</code></td>
      <td data-th="Description">Yes</td>
      <td data-th="Behavior">The element takes the space available to it and resizes its height automatically to the aspect ratio given by the <code>width</code> and <code>height</code> attributes <em>until</em> it reaches the element's natural size or reaches a CSS constraint (e.g., max-width). The width and height attributes must be present. This layout works very well for most AMP elements, including <code>amp-img</code>, <code>amp-carousel</code>, etc. The available space depends on the parent element and can also be customized using <code>max-width</code> CSS. This layout differs from <code>responsive</code> by having an intrinsic height and width. This is most apparent inside a floated element where a <code>responsive</code> layout will render 0x0 and an <code>intrinsic</code> layout will inflate to the smaller of its natural size or any CSS constraint. </td>
    </tr>
  </tbody>
</table>

Tip: Visit the [Demonstrating AMP layouts]({{g.doc('/content/docs/design/amp-html-layout/layouts_demonstrated.md', locale=doc.locale).url.path}}) page to see how the various layouts respond to screen resizing. You can also find more in [AMP By Example](https://ampbyexample.com/advanced/layout_system/).


### What if width and height are undefined?

In a few cases if `width` or `height` are not specified,
the AMP runtime can default these values as the following:

* [`amp-pixel`](/docs/reference/components/amp-pixel.html): Both width and height are defaulted to 0.
* [`amp-audio`](/docs/reference/components/amp-audio.html): The default width and height are inferred from browser.

### What if the <code>layout</code> attribute isn’t specified?

If the <code>layout</code> attribute isn't specified, AMP tries to infer or guess
the appropriate value:

<table>
  <thead>
    <tr>
      <th data-th="Rule">Rule</th>
      <th data-th="Inferred layout" class="col-thirty">Inferred layout</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Rule"><code>height</code> is present and <code>width</code> is absent or equals to <code>auto</code></td>
      <td data-th="Inferred layout"><code>fixed-height</code></td>
    </tr>
    <tr>
      <td data-th="Rule"><code>width</code> or <code>height</code> attributes are present along with the <code>sizes</code> attribute</td>
      <td data-th="Inferred layout"><code>responsive</code></td>
    </tr>
    <tr>
      <td data-th="Rule"><code>width</code> or <code>height</code> attributes are present</td>
      <td data-th="Inferred layout"><code>fixed</code></td>
    </tr>
    <tr>
      <td data-th="Rule"><code>width</code> and <code>height</code> are not present</td>
      <td data-th="Inferred layout"><code>container</code></td>
    </tr>
  </tbody>
</table>

## Using media queries

### CSS media queries

Use [`@media`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)
to control how the page layout looks and behaves, as you would do on any other website.
When the browser window changes size or orientation,
the media queries are re-evaluated and elements are hidden and shown
based on the new results.

Read on: Learn more about controlling layout by applying media queries in [Use CSS media queries for responsiveness](https://developers.google.com/web/fundamentals/design-and-ui/responsive/fundamentals/use-media-queries?hl=en).

### Element media queries

One extra feature for responsive design available in AMP is the `media` attribute.
This attribute can be used on every AMP element;
it works similar to media queries in your global stylesheet,
but only impacts the specific element on a single page.

For example, here we have 2 images with mutually exclusive media queries.

[sourcecode:html]
<amp-img
    media="(min-width: 650px)"
    src="wide.jpg"
    width=466
    height=355
    layout="responsive">
</amp-img>
[/sourcecode]

Depending on the screen width, one or the other will be fetched and rendered.

[sourcecode:html]
<amp-img
    media="(max-width: 649px)"
    src="narrow.jpg"
    width=527
    height=193
    layout="responsive">
</amp-img>
[/sourcecode]
