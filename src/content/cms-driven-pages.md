
## What happens when you go to **aldoshoes.com/us/en_US/women**?

<div style="background: yellow; color: black">
ASSET NEEDED
<br>
Video of scrolling down women's page
</div>

Notes:
- Let's just jump right in and tell you a story - what happens when you go to aldoshoes.com/women?

---

## Step 1: Fetch CMS data

<p class="fragment" data-fragment-index="0">
  On route change, hit <code data-noescape>cms?page=**/women**&locale=**us**&language=**en_US**</code>
</p>

Get JSON back:<!-- .element: class="fragment" data-fragment-index="1" -->

```js
{
  "uuid-00": {
    "content-modules": {
      "uuid-01": { ... },
      "uuid-02": { ... },
      "uuid-03": { ... }
    }
  }
}
```
<!-- .element: class="fragment" data-fragment-index="1" -->

Notes:
- On a route change, we request CMS data for the new path 
- Get content modules data back as JSON

---

## Step 1: Fetch CMS data (cont'd)

<p class="fragment" data-fragment-index="0">
  Cache in redux store keyed on the path
</p>

<pre><code data-noescape>{
  cms: {
    "/checkout": { ... },
    "/men/footwear/sneakers": { ... },
    <span class="fragment" data-fragment-index="0">"/women":{  
      "content-uuid-24": {  
        "content-modules": [ ... ]
      }
    }</span>
  }
}</code></pre>

Notes:
- We check the redux store first before issuing a network request
- Browsing to a previously visited page should load CMS modules immediately
- This enables a better user experience & reduces the load on Aldo's infrastructure

---

## Step 2: React Router

<p class="fragment" data-fragment-index="0">
  Check declared routes
</p>

<p class="fragment" data-fragment-index="1">
  Match `/women` path to wildcard route, render `<DynamicPage />` component
</p>

<pre><code data-noescape>&lt;Route path="/" component={App}&gt;

  <span class="fragment" data-fragment-index="0">&lt;Route path="/product/:code" component={ProductPage} /&gt;
  &lt;Route path="/checkout" component={CheckoutPage} /&gt;
  ...</span>

  <span class="fragment" data-fragment-index="1">&lt;Route path="&#42" component={DynamicPage} /&gt;</span>

&lt;/Route&gt;
</code></pre>

Notes:
- Check routes we've defined for `react-redux-router`
- This evaluates the path against all our "fixed" pages like Products, Checkout, or the Store Locator
- We don't have very many routes here because we have so many custom CMS pages
- `/women` doesn't match any known routes, so it gets caught by the wildcard and we render the `<DynamicPage />` component

---

## Step 3: Render `<DynamicPage />`

<p class="fragment" data-fragment-index="0">
  Wait for completed request
</p>

<p class="fragment" data-fragment-index="1">
  Confirm data present, render `<CMSCustomPage />` component
</p>

<pre><code data-trim data-noescape>
function DynamicPage(props) {
  <span class="fragment" data-fragment-index="0">const {
    <span class="fragment" data-fragment-index="1">hasContentModules,</span>
    hasFetchedPage,
  } = props;

  if (!hasFetchedPage) {
    return &lt;Loader&gt;;
  }

  <span class="fragment" data-fragment-index="1">if (hasContentModules) {
    return &lt;CMSCustomPage /&gt;; // Pick me!
  }

  return &lt;NotFoundPage /&gt;;</span></span>
}
</code></pre>

Notes:
- First check if we've fetched data for the current route. If not, render a loading screen.
- If we have, check if we have content modules on the store. We got CMS data back for `/women`, so this is true.
- If we had hit a crazy route, like aldoshoes.com/banana, we would not have gotten any CMS data back, and we'd render the 404 page!

---

## Step 4: Map CMS modules to React components

<div style="background: yellow; color: black">
ASSET NEEDED
<br>
Video of various CMS components: Top Story, Main Story, Get Inspired
</div>

Notes:
- Aldo wanted a flexible, modular layout with the ability to mix and match components per page

---

## Step 4: Map CMS modules to React components (cont'd)

<p class="fragment" data-fragment-index="0">
  Turn CMS data...
</p>

<pre class="fragment" data-fragment-index="0"><code data-noescape>{
  "uuid-00": {
    "content-modules": {
      "uuid-01": { "type": "top-story", ... },
      "uuid-02": { "type": "main-story", ... },
      "uuid-03": { "type": "get-inspired", ... },
    }
  }
}
</code></pre>

<p class="fragment" data-fragment-index="1">
  ...into React components
</p>

```
<TopStory />
<MainStory />
<GetInspired />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

Notes:
- Each CMS module has a type. We map that type to a React component.
- React's component-based architecture is a great fit for our modular CMS design.

---

## Step 4: Build CMS components: `<TopStory />`

<div style="background: yellow; color: black">
ASSET NEEDED
<br>
Video of flipping through TopStory slides and clicking on a featured product to get to its product page
(Let's keep it simple and not show any TopStory modules with video)
</div>

Notes:
- It's a carousel (joke about how designers love carousels)
- Title, description, call to action button
- Front and back assets
- Products with prices (need to be up to date)

---

### `<TopStory />` Step 1: Configure assets

<div style="background: yellow; color: black">
ASSET NEEDED
<br>
This asset should stress the importance of responsive images.
We could either show Aldo assets at a different size, or pictures of the website on different devices.
</div>

Notes:
- Let's start with the assets. Assets are a big deal to Aldo, because they allow us to showcase a product and its available accessories, but with a large mobile user base, we needed to always load the smallest possible asset.

---

### `<TopStory />` Step 1: Configure assets (cont'd)

<p class="fragment" data-fragment-index="0">
  Turn CMS image props...
</p>

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

<p class="fragment" data-fragment-index="1">
  ...into responsive image (with a little help from `lazysizes`)
</p>

```
<img
  class="lazyload"
  data-sizes="auto"
  data-srcset="//media.aldoshoes.com/assets/pastel__400 400w,
               //media.aldoshoes.com/assets/pastel__1200 1200w" />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

Notes:
- The CMS gives us a list of the available dimensions for each image, plus a URL with wildcard for each dimension set.
- We plug this data into an image and use the library `lazysizes` to determine the width of the current image, so we always load the smallest possible image.
- This allows us to harness the HTML5 native image element, which will find the smallest image for a given size, without having to hardcode sizes - `lazysizes` will dynamically set the size after the component is rendered.

---

### `<TopStory />` Step 2: Fetch product data
<div style="background: yellow; color: black">
ASSET NEEDED
<br>
Two product tiles: One regular, one on sale
</div>

Notes:
- Most of our CMS modules are designed to lead people to product pages

---

### `<TopStory />` Step 2: Fetch product data (cont'd)

<p class="fragment" data-fragment-index="0">
  Get product IDs
</p>

```js
{
  "featured-products": {
    "featured-product-0": { "id": "123" },
    "featured-product-1": { "id": "456" }
  }
}
```
<!-- .element: class="fragment" data-fragment-index="0"-->

<p class="fragment" data-fragment-index="1">
  Get details from <code data-noescape>api/product-details?codes=**123**,**456**</code>
</ProductTile>

<p class="fragment" data-fragment-index="2">
  Render `<ProductTile />` components
</ProductTile>

```
<ProductTile
  name="Stessy"
  url="/product/123"
  price="$100"
  salePrice="$50" />

<ProductTile
  name="Nika"
  url="/product/456"
  price="$20" />
```
<!-- .element: class="fragment" data-fragment-index="2"-->

---

### `<TopStory />` Step 3: Render `<TopStory />` component

<p class="fragment" data-fragment-index="0">
  Render assets
</p>

<p class="fragment" data-fragment-index="1">
  Render products
</p>

<p class="fragment" data-fragment-index="2">
  Map properties
</p>

<pre><code data-noescape>&lt;div className="top-story"&gt;
  &lt;div className="top-story__slide"&gt;

    <span class="fragment" data-fragment-index="2">&lt;h2&gt;{title}&lt;/h2&gt;</span>
    <span class="fragment" data-fragment-index="2">&lt;p&gt;{content}&lt;/p&gt;</span>
    <span class="fragment" data-fragment-index="2">&lt;Link to="ctaLink"&gt;{ctaTitle}&lt;/Link&gt;</span>

    <span class="fragment" data-fragment-index="0">&lt;Img {...imageProps} /&gt;</span>

    <span class="fragment" data-fragment-index="1">&lt;FeaturedProducts {...featuredProductProps} /&gt;</span>

  &lt;/div&gt;
  &lt;div className="top-story__slide"&gt;...&lt;/div&gt;
&lt;/div&gt;</code></pre>

---

## Step 6: Put it all together

<p class="fragment" data-fragment-index="0">
  App header and footer
</p>

<p class="fragment" data-fragment-index="1">
  CMS modules
</p>

<pre><code data-noescape>&lt;body&gt;

  <span class="fragment" data-fragment-index="0">&lt;Header /&gt;</span>

  &lt;main&gt;

    <span class="fragment" data-fragment-index="1">&lt;TopStory /&gt;
    &lt;MainStory /&gt;
    &lt;GetInspired /&gt;
    &lt;TrackOrder /&gt;</span>

  &lt;/main&gt;</span>

  <span class="fragment" data-fragment-index="0">&lt;Footer /&gt;</span>

&lt;/body&gt;</code></pre>

---

<div style="background: yellow; color: black">
Repeat asset of scrolling down women's page
</div>
