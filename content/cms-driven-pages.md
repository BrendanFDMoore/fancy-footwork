<div style="text-align: center; margin-top:50px;">
![viewports](content/images/cms-diagram.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->
</div>

---
<!-- .element: style="text-align: center" -->

![Home](content/images/new-homepage-men.png)<!-- .element: style="box-shadow: none; margin-top: -35px" -->

---
<!-- .element: style="text-align: center" -->

![Totes](content/images/new-totes-plp.png)<!-- .element: style="box-shadow: none; margin-top: -35px" -->

---
<!-- .element: style="text-align: center" -->

![Women](content/images/new-women.png)<!-- .element: style="box-shadow: none; margin-top: -35px" -->

---

<p>
  Route: <code data-noescape>www.aldoshoes.com/us/en_us/<span style="font-weight:bold;">women</span></code>
</p>
<p>
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
<pre><code data-noescape>"uuid-00": {
  "content-modules": {
    "uuid-01": { "type": "top-story", ... },
    "uuid-02": { "type": "main-story", ... },
    "uuid-03": { "type": "highlights", ... },
  }
}</code></pre>
<div>
  <div style="left: -8.33%;text-align: center;float: left;width: 50%;z-index: -10;">
    <img style="border:none;box-shadow: none;max-height: 85%; max-width: 85%;margin-top: 5px;" data-src="content/images/transmogrify.png" alt="Transmogrify!">
    <!-- .element: class="fragment" data-fragment-index="1"-->
  </div>
  <div style="left: 31.25%;top: 75px;float: right;z-index: -10;width: 50%;">
    <p class="fragment" data-fragment-index="1" style="margin-top:20px;">...into React components</p>
<pre class="fragment" data-fragment-index="1"><code data-noescape>&lt;TopStory /&gt;
&lt;MainStory /&gt;
&lt;Highlights /&gt;</code></pre>
    <!-- .element: class="fragment" data-fragment-index="1"-->
  </div>
</div>

---

<p>Map CMS properties...</p>
<pre><code data-noescape>{
  "title": "Pretty in pastel",
  "featured-products": {
    "featured-product-0": { "id": "123" },
    "featured-product-1": { "id": "456" }
  }
}</code></pre>
<p class="fragment" data-fragment-index="0">
  ...to React component props
</p>
```
<h2>Pretty in pastel</h2>
<div>
  <ProductTile name="Stessy" url="/product/123" price="$100" />
  <ProductTile name="Nika" url="/product/456" price="$50" />
</div>
```
<!-- .element: class="fragment" data-fragment-index="0"-->

---

![Unclosed divs](content/images/girl-shaking-fist.gif)<!-- .element: style="height: 80vh; max-width: 100%; margin-top: -18px; box-shadow: none" -->

---

<pre><code data-noescape>"uuid-00": {
  "content-modules": {
    "uuid-01": { "type": "track-my-order" },
  }
}</code></pre>
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
<pre style="font-size:0.9em;"><code data-noescape><span style="opacity:0.5;">&lt;Route
  path="/"
  component={App}&gt;</span>
    <span style="font-weight:bold;">&lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;</span>
    <span style="opacity:0.5;">&lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;
    ...
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;
&lt;/Route&gt;</span>
</code></pre>

---

<!-- .element: data-transition="fade-in fade-out"-->
<pre style="font-size:0.9em;"><code data-noescape><span style="opacity:0.5;">&lt;Route
  path="/"
  component={App}&gt;
    &lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;</span>
    <span style="font-weight:bold;">&lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;</span>
    <span style="opacity:0.5;">...
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;
&lt;/Route&gt;</span>
</code></pre>

---

<!-- .element: data-transition="fade-in slide-out"-->
<pre style="font-size:0.9em;"><code data-noescape><span style="opacity:0.5;">&lt;Route
  path="/"
  component={App}&gt;
    &lt;Route
      path="/product/:code"
      component={ProductPage} /&gt;
    &lt;Route
      path="/checkout"
      component={CheckoutPage} /&gt;
    ...</span><span style="font-weight:bold;opacity:1.0;">
    &lt;Route
      path="&#42"
      component={CustomPage} /&gt;</span>
<span style="opacity:0.5;">&lt;/Route&gt;</span>
</code></pre>

---

<!-- .element: data-transition="slide-in fade-out"-->

<div class="diagram-wrapper">
  <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
  <div class="diagram is-loading" style="height: 360px">Loading...</div>
  <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
</div>

---

<!-- .element: data-transition="fade-in fade-out"-->

<div class="diagram-wrapper">
  <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
  <div class="diagram is-loaded" style="height: 360px">CMS MODULES</div>
  <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
</div>

---

<!-- .element: data-transition="fade-in fade-out"-->

<div class="diagram-wrapper">
  <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
  <div class="diagram is-loading" style="height: 360px">Loading...</div>
  <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
</div>

---

<!-- .element: data-transition="fade-in fade-out"-->

<div class="diagram-wrapper">
  <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
  <div class="diagram is-loaded" style="height: 360px">404 Page</div>
  <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
</div>

---

<div>
  <div style=" left: -8.33%; text-align: center; float: left; width: 50%; z-index: -10;">
    <div class="diagram-wrapper">
      <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
      <div class="diagram is-ecommerce" style="height: 175px">E-COMMERCE DATA</div>
      <div class="diagram is-loaded" style="height: 175px">CMS DATA</div>
      <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
    </div>
  </div>
  <div style="margin-top: 20px; left: 31.25%; top: 75px; float: right; text-align: center; z-index: -10; width: 50%;">
    <img style="border:1px solid #aaa; margin:0; box-shadow: 10px 10px 12px 0px rgba(0,0,0,0.75); max-height: 90%; max-width: 80%;"
 -  data-src="content/images/camylla-full-page-trim4.png" alt="Header">
  </div>
</div>

---

<!-- .element: data-transition="slide-in fade-out"-->

<div>
  <div style=" left: -8.33%; text-align: center; float: left; width: 50%; z-index: -10;">
    <div class="diagram-wrapper">
      <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
      <div class="diagram" style="height: 360px; display: flex; align-items: stretch; justify-content: space-between">
        <div class="diagram is-ecommerce" style="width: 60%; margin-right: 0px !important;">E-COMMERCE DATA</div>
        <div class="diagram-wrapper" style="width: calc(40% - 0px);">
          <div class="diagram is-ecommerce" style="height: 175px; margin-right: 0px !important; font-size: 24px !important;">E-COMMERCE DATA</div>
          <div class="diagram is-loaded" style="height: 175px; margin-right: 0px !important; font-size: 24px !important;">CMS DATA</div>
        </div>
      </div>
      <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
    </div>
  </div>
  <div style=" left: 31.25%; top: 75px; float: right; text-align: center; z-index: -10; width: 50%;">
    <img style="border:none;margin:0;box-shadow: none; max-height: 100%; max-width: 100%; "
   data-src="content/images/checkout-policy-step3.png" alt="Header">
  </div>
</div>

---

<!-- .element: data-transition="fade-in slide-out"-->

<div>
  <div style=" left: -8.33%; text-align: center; float: left; width: 50%; z-index: -10;">
    <div class="diagram-wrapper">
      <div class="diagram is-header-footer" style="height: 75px">HEADER</div>
      <div class="diagram" style="height: 360px; display: flex; align-items: stretch; justify-content: space-between">
        <div class="diagram is-ecommerce" style="width: 60%; margin-right: 0px !important;">E-COMMERCE DATA</div>
        <div class="diagram-wrapper" style="width: calc(40% - 0px);">
          <div class="diagram is-ecommerce" style="height: 175px; margin-right: 0px !important; font-size: 24px !important;">E-COMMERCE DATA</div>
          <div class="diagram is-not-loaded" style="height: 175px; margin-right: 0px !important; font-size: 24px !important;"></div>
        </div>
      </div>
      <div class="diagram is-header-footer" style="height: 75px">FOOTER</div>
    </div>
  </div>
  <div style=" left: 31.25%; top: 75px; float: right; text-align: center; z-index: -10; width: 50%;">
    <img style="border:none;margin:0;box-shadow: none; max-height: 100%; max-width: 100%; "
   data-src="content/images/checkout-policy-step4.png" alt="Header">
  </div>
</div>

---

<div style="text-align: center; margin-top:50px;">
![viewports](content/images/fry_money.jpeg)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->
</div>

---

<div style="text-align: center; margin-top:50px;">
![viewports](content/images/viewports.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px; box-shadow: none" -->
</div>

---

<!-- .element: data-transition="slide-in fade-out"-->

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

<p class="fragment" data-fragment-index="0">
  ...into a responsive image
</p>

```smalltalk
<img
  srcset="//media.aldoshoes.com/assets/shoename__400.jpg 400w,
          //media.aldoshoes.com/assets/shoename__1200.jpg 1200w" />
```
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<!-- .element: data-transition="fade-in fade-out"-->

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

...into a responsive image

<pre><code data-noescape class="smalltalk"><span style="opacity:0.5;">&lt;img
  srcset="//media.aldoshoes.com/assets/shoename__400.jpg 400w,
          //media.aldoshoes.com/assets/shoename__1200.jpg 1200w"</span>
  sizes="I don't know, I guess 500?" <span style="opacity:0.5;">/&gt;
</span></code></pre>

---

<!-- .element: data-transition="fade-in fade-out"-->

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

...into a responsive image

<pre><code data-noescape class="smalltalk"><span style="opacity:0.5;">&lt;img
  srcset="//media.aldoshoes.com/assets/shoename__400.jpg 400w,
          //media.aldoshoes.com/assets/shoename__1200.jpg 1200w"</span>
  sizes="521px" <span style="opacity:0.5;">/&gt;
</span></code></pre>

---
<!-- .element: style="text-align: center" -->

![Delivery](content/images/new-delivery.png)<!-- .element: style="box-shadow: none; margin-top: -35px" -->

---

<div style="margin-top:50px;">
  <div style="left: -8.33%;text-align: center;float: left;width: 50%;z-index: -10;">
    <div style="height:35vh;">
      <div style="text-align:center;margin:0;">
        <img style="border:none;margin:0;box-shadow: none; max-width:80%;" data-src="content/images/md-table.png" alt="Table">
      </div>
    </div>
    <div style="height:35vh;">
      <div style="text-align:center;margin:0;">
        <img style="border:none;margin:0;box-shadow: none; max-width:80%;" data-src="content/images/md-timeline.png" alt="Table">
      </div>
    </div>
  </div>
  <div style="left: 31.25%;top: 75px;float: right;z-index: -10;width: 50%;">
    <div style="height:35vh;">
      <div style="text-align:center;margin:0;">
        <img style="border:none;margin:0;box-shadow: none; max-width:80%;" data-src="content/images/md-list-paragraph.png" alt="Table">
      </div>
    </div>
    <div style="height:35vh;">
      <div style="text-align:center;margin:0;">
        <img style="border:none;margin:0;box-shadow: none; max-width:80%;" data-src="content/images/md-list-bold-header.png" alt="Table">
      </div>
    </div>
  </div>
</div>

---

<p style="text-align:center;">
![Checkout](content/images/progbook.jpg)<!-- .element: style="max-height: 70%; max-width: 70%;" -->
</p>

---

```
import ReactMarkdown from 'react-markdown';

import AldoList from 'components/markdown/list';
import AldoTable from 'components/markdown/table';

<ReactMarkdown
  renderers={ {
    List: AldoList,
    CodeBlock: AldoTable,
  } } />
```

---

<div style="text-align:center;margin:0;">
  <pre style="max-width:80%;"><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">&#96;&#96;&#96;
Shipping Method                         | Delivery Time      | Cost
--------------------------------------- | ------------------ | ----
&#91;Standard Shipping&#93;&#40;http://google.com &#41; | 5-7 business days  | $10
&#42;Express Shipping&#42;                      | 7-12 business days | $5
Ship to an ALDO Store                   | 7-12 business days | Free
&#96;&#96;&#96;</code></pre>
</div>

<div style="text-align:center;margin:0;">
  <pre style="max-width:80%; white-space: pre-wrap;"><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">&gt;1. Order placed
&gt;2. Order processed long title
&gt;3. Shipped
&gt;4. Received other long title</code></pre>
</div>

<div style="text-align:center;margin:0;">
  <pre style="max-width:80%; white-space: pre-wrap;"><code data-noescape class="markdown" style="font-size:0.8em;color:#000;">&#49;. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
&#50;. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. </code></pre>
</div>


---
<!-- .element: style="text-align: center" -->

![Ordering](content/images/new-ordering.png)<!-- .element: style="box-shadow: none; margin-top: -35px" -->

---
<!-- .element: style="text-align: center" -->

![Collection](content/images/new-floral-collection.png)<!-- .element: style="box-shadow: none; margin-top: -35px" -->
