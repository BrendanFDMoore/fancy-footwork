## Home page
![Home](content/images/home.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->

---

## Now Trending Handbags
![PLP](content/images/plp.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->

---

## Women's styles landing page
![Women](content/images/women.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->

---

<p>
  Route: <code data-noescape>www.aldoshoes.com/us/en_us/<span style="font-weight:bold;">women</span></code>
</p>
<p class="fragment" data-fragment-index="0">
  API request: <code data-noescape>/api/cms?page=/<span style="font-weight:bold;">women</span>&locale=<span style="font-weight:bold;">us</span>&language=<span style="font-weight:bold;">en_US</span></code>
</p>

<pre><code data-noescape><span class="fragment" data-fragment-index="2">{
  cms: {
    "/checkout": { ... },
    "/men/footwear/sneakers": { ... },
    "/women":{</span>
      <span class="fragment" data-fragment-index="1">"uuid-00": {  
        "content-modules": {
          "uuid-01": { ... },
          "uuid-02": { ... },
          "uuid-03": { ... }
        }
      }</span><span class="fragment" data-fragment-index="2">
    },
    "/women/footwear/flats": { ... }
  }
}</span></code></pre>
<!-- .element: class="fragment" data-fragment-index="1" -->

Notes:
- On a route change, we request CMS data for the new path 
- Get content modules data back as JSON

---

Transform CMS data...
<pre class="fragment" data-fragment-index="0"><code data-noescape>"uuid-00": {
  "content-modules": {
    "uuid-01": { "type": "top-story", ... },
    "uuid-02": { "type": "main-story", ... },
    "uuid-03": { "type": "highlights", ... },
  }
}</code></pre>
<div>
  <div style="left: -8.33%;text-align: center;float: left;width: 50%;z-index: -10;">
    <img style="border:none;box-shadow: none;max-height: 85%; max-width: 85%;" data-src="content/images/transmogrify.png" alt="Transmogrify!">
    <!-- .element: class="fragment" data-fragment-index="1"-->
  </div>
  <div style="left: 31.25%;top: 75px;float: right;z-index: -10;width: 50%;">
    <p class="fragment" data-fragment-index="2" style="margin-top:20px;">...into React components</p>
<pre class="fragment" data-fragment-index="2"><code data-noescape>&lt;TopStory /&gt;
&lt;MainStory /&gt;
&lt;Highlights /&gt;</code></pre>
    <!-- .element: class="fragment" data-fragment-index="2"-->
  </div>
</div>

---

![Unclosed divs](content/images/girl-shaking-fist.gif)<!-- .element: style="height: 80vh; max-width: 100%; margin-top: -18px; box-shadow: none" -->

---

<p>Map CMS properties...</p>
<pre class="fragment" data-fragment-index="0"><code data-noescape>{
  "title": "Pretty in pastel",
  "featured-products": {
    "featured-product-0": { "id": "123" },
    "featured-product-1": { "id": "456" }
  }
}</code></pre>
<p class="fragment" data-fragment-index="1">
  ...to React component props
</p>
```
<h2>Pretty in pastel</h2>
<div className='my-cms-modules__products'>
  <ProductTile name="Stessy" url="/product/123" price="$100" />
  <ProductTile name="Nika" url="/product/456" price="$50" />
</div>
```
<!-- .element: class="fragment" data-fragment-index="1"-->

---

![track-order](content/images/track-order.png)

---

<!-- .element: data-transition="slide-in fade-out"-->
<pre style="font-size:0.9em;"><code data-noescape>&lt;Route
  path="/"
  component={App}&gt;
    &lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;
    &lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;
    ...
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;
&lt;/Route&gt;
</code></pre>

---

<!-- .element: data-transition="fade-in fade-out"-->
<pre style="font-size:0.9em;"><code data-noescape>&lt;Route
  path="/"
  component={App}&gt;
    <span style="font-weight:bold;">&lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;</span>
    &lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;
    ...
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;
&lt;/Route&gt;
</code></pre>

---

<!-- .element: data-transition="fade-in fade-out"-->
<pre style="font-size:0.9em;"><code data-noescape>&lt;Route
  path="/"
  component={App}&gt;
    &lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;
    <span style="font-weight:bold;">&lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;</span>
    ...
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;
&lt;/Route&gt;
</code></pre>

---

<!-- .element: data-transition="fade-in slide-out"-->
<pre style="font-size:0.9em;"><code data-noescape>&lt;Route
  path="/"
  component={App}&gt;
    &lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;
    &lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;
    ...<span style="font-weight:bold;">
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;</span>
&lt;/Route&gt;
</code></pre>

---

<!-- .element: data-transition="slide-in fade-out"-->
<div style="text-align:center;margin:0;border:1px solid #fff">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-header.png" alt="Header">
<img style="border:none;margin:0;box-shadow: none;margin-top:40px;margin-bottom:40px;" data-src="content/images/loading2.gif" alt="Loading"><!-- .element: class="fragment" data-fragment-index="2"-->
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer"><!-- .element: class="fragment" data-fragment-index="1"-->
</div>

---
<!-- .element: data-transition="fade-in fade-out"-->
<div style="text-align:center;margin:0;border:1px solid #fff">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-header.png" alt="Header">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-body.png" alt="Body">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer">
</div>

---
<!-- .element: data-transition="fade-in fade-out"-->
<div style="text-align:center;margin:0;border:1px solid #fff">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-header.png" alt="Header">
<img style="border:none;margin:0;box-shadow: none;margin-top:40px;margin-bottom:40px;" data-src="content/images/loading2.gif" alt="Loading">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer">
</div>

---
<!-- .element: data-transition="fade-in slide-out"-->
<div style="text-align:center;margin:0;border:1px solid #fff">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-header.png" alt="Header">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-404.png" alt="Body">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer">
</div>

---

![more-from-collection](content/images/more-from-collection.png)<!-- .element: style="max-height: 90%; max-width: 90%; margin-top: -18px; box-shadow: none" -->

---

[checkout policy goes here]

---

<div style="font-size: 126px; color: black; text-align: center; margin-top:100px;">
   💪
</div>

---

<div style="text-align: center; margin-top:50px;">
![viewports](content/images/viewports.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->
</div>

---

<p>Turn CMS image props...</p>

```js
  "image-asset": {
    "dimensions": [
      { "h": "400", "w": "400" },
      { "h": "1200", "w": "1200" }
    ],
    "url": "//media.aldoshoes.com/assets/shoename__[dimension].jpg"
  }
```
<!-- .element: class="fragment" data-fragment-index="0"-->

<p class="fragment" data-fragment-index="1">
  ...into a responsive image
</p>

```
<img
  class="lazyload"
  data-sizes="auto"
  data-srcset="//media.aldoshoes.com/assets/shoename__400 400w,
               //media.aldoshoes.com/assets/shoename__1200 1200w" />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

Notes:
- The CMS gives us a list of the available dimensions for each image, plus a URL with wildcard for each dimension set.
- We plug this data into an image and use the library `lazysizes` to determine the width of the current image, so we always load the smallest possible image.
- This allows us to harness the HTML5 native image element, which will find the smallest image for a given size, without having to hardcode sizes - `lazysizes` will dynamically set the size after the component is rendered.

---

---

<div style="text-align:center;margin:0;margin-top:100px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-table.png" alt="Table">
</div>

---

<div style="text-align:center;margin:0;margin-top:100px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-timeline.png" alt="Timeline">
</div>

---

<div style="text-align:center;margin:0;margin-top:100px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-paragraph.png" alt="List with paragraphs">
</div>

---

<div style="text-align:center;margin:0;margin-top:100px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-bold-header.png" alt="List with bold header">
</div>

---

<p style="text-align:center;">
![Checkout](content/images/progbook.jpg)<!-- .element: style="max-height: 70%; max-width: 70%;" -->
</p>


---

<div style="text-align:center;margin:0;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-table.png" alt="Table">
</div>
<pre><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">
Shipping Method                         | Delivery Time      | Cost
--------------------------------------- | ------------------ | ----
&#91;Standard Shipping&#93;&#40;http://google.com &#41; | 5-7 business days  | $10
&#42;Express Shipping&#42;                      | 7-12 business days | $5
Ship to an ALDO Store                   | 7-12 business days | Free
</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="text-align:center;margin:0;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-timeline.png" alt="Timeline">
</div>
<pre><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">&gt; 1. Order placed
&gt; 2. Order processed long title
&gt; 3. Shipped
&gt; 4. Received other long title</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="text-align:center;margin:0;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-paragraph.png" alt="List with paragraphs">
</div>
<pre><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">&#49;. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
&#50;. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="text-align:center;margin:0;"><img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-bold-header.png" alt="List with bold header"></div>
<pre><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">&#49;. Print out a mailing label
&nbsp;
   Search for an item or browse the site.
&#50;. Place your items for return in a box.
&nbsp;
   Choose the colour and size and select “Add to Bag”
&#51;. Mail your package
&nbsp;
   Start the checkout process by selecting “Checkout” at your shopping bag.</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="font-size: 126px; color: black; text-align: center; margin-top:100px;">
   🎉
</div>

---

<div style="text-align: center;">
  ![Stessy](content/images/stessy.gif)<!-- .element: style="box-shadow: none" -->
</div>