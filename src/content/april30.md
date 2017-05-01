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

<pre class="fragment" data-fragment-index="0"><code data-noescape>{
  "uuid-00": {
    "content-modules": {
      "uuid-01": { "type": "top-story", ... },
      "uuid-02": { "type": "main-story", ... },
      "uuid-03": { "type": "highlights", ... },
    }
  }
}
</code></pre>

<p class="fragment" data-fragment-index="1" style="text-align:center;">
  ![Checkout](content/images/transmogrify.png)<!-- .element: style="max-height: 10%; max-width: 30%;" -->
</p>

```
<TopStory />
<MainStory />
<Highlights />
```
<!-- .element: class="fragment" data-fragment-index="2"-->

---

<pre><code data-noescape>&lt;Route path="/" component={App}&gt;
  &lt;Route path="/product/:code" component={ProductPage} /&gt;
  &lt;Route path="/checkout" component={CheckoutPage} /&gt;
  ...
  <span style="font-weight:bold;">
  &lt;Route path="&#42" component={CustomPage} /&gt;
  </span>
&lt;/Route&gt;
</code></pre>

---
<!-- .element: data-transition="fade-in fade-out"-->
<div class="fragment" data-fragment-index="0" style="text-align:center;margin:0;border:1px solid #fff">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-header.png" alt="Header"><!-- .element: class="fragment" data-fragment-index="0"-->
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/loading2.gif" alt="Loading"><!-- .element: class="fragment" data-fragment-index="1"-->
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer"><!-- .element: class="fragment" data-fragment-index="2"-->
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
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/loading2.gif" alt="Loading">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer">
</div>

---
<!-- .element: data-transition="fade-in fade-out"-->
<div style="text-align:center;margin:0;border:1px solid #fff">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-header.png" alt="Header">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-404.png" alt="Body">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/women-landing-footer.png" alt="Footer">
</div>

---

```js
{
  "front-asset": {
    "dimensions": [
      { "h": "400", "w": "400" },
      { "h": "1200", "w": "1200" }
    ],
    "url": "//media.aldoshoes.com/assets/pastel__[dimension].jpg"
  }
}
```
<!-- .element: class="fragment" data-fragment-index="0"-->

```
<img
  class="lazyload"
  data-sizes="auto"
  data-srcset="//media.aldoshoes.com/assets/pastel__400 400w,
               //media.aldoshoes.com/assets/pastel__1200 1200w" />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

Notes:
* Turn CMS image props...
* ...into responsive image (with a little help from `lazysizes`)

---

<div style="text-align:center;margin:0;margin-top:50px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-table.png" alt="Table">
</div>

---

<div style="text-align:center;margin:0;margin-top:50px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-timeline.png" alt="Timeline">
</div>

---

<div style="text-align:center;margin:0;margin-top:50px;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-paragraph.png" alt="List with paragraphs">
</div>

---

<div style="text-align:center;margin:0;margin-top:50px;">
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
<pre><code data-noescape style="font-size:0.8em;">
&#96;&#96;&#96;
Shipping Method                         | Delivery Time      | Cost
--------------------------------------- | ------------------ | ----
&#91;Standard Shipping&#93;&#40;http://google.com &#41; | 5-7 business days  | $10
&#42;Express Shipping&#42;                      | 7-12 business days | $5
Ship to an ALDO Store                   | 7-12 business days | Free
&#96;&#96;&#96;
</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="text-align:center;margin:0;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-timeline.png" alt="Timeline">
</div>
<pre><code data-noescape>
&#96;&#96;&#96;
&gt; 1. Order placed
&gt; 2. Order processed long title
&gt; 3. Shipped
&gt; 4. Received other long title
&#96;&#96;&#96;
</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="text-align:center;margin:0;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-paragraph.png" alt="List with paragraphs">
</div>
<pre><code data-noescape style="font-size:0.8em;">&#96;&#96;&#96;
&#49;. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
&#50;. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
&#96;&#96;&#96;</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->

---

<div style="text-align:center;margin:0;">
<img style="border:none;margin:0;box-shadow: none;" data-src="content/images/md-list-bold-header.png" alt="List with bold header">
</div>
<pre><code data-noescape style="font-size:0.8em;">&#96;&#96;&#96;
&#49;. Print out a mailing label
&nbsp;
   Search for an item or browse the site.
&#50;. Place your items for return in a box.
&nbsp;
   Choose the colour and size and select “Add to Bag”
&#51;. Mail your package
&nbsp;
   Start the checkout process by selecting “Checkout” at your shopping bag.
&#96;&#96;&#96;</code></pre>
<!-- .element: class="fragment" data-fragment-index="0"-->
