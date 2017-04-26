
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
  "content-uuid-01": {
    "content-modules": {
      "uuid-01": { ... },
      "uuid-02": { ... },
      "uuid-03": { ... },
      "uuid-04": { ... }
    }
  }
}
```
<!-- .element: class="fragment" data-fragment-index="1" -->

Notes:
- Request CMS data on route change
- Get list of content modules

---

## Step 1: Fetch CMS data (cont'd)

<p class="fragment" data-fragment-index="0">
  Cache in redux
</p>

<pre><code data-noescape>{
  cms: {
    <span class="fragment" data-fragment-index="0">"/women":{  
      "content-uuid-24": {  
        "content-modules": [ ... ]
      }
    },</span>
    "/men/footwear/sneakers": { ... },
    "/checkout": { ... }
  }
}</code></pre>

Notes:
- We check here first before issuing a network request
- Browsing to a previously page should load CMS modules instantly
- Better UX & reduces load on Aldo servers

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
  &lt;Route path="/checkout" component={CheckoutPage} /&gt;</span>

  <span class="fragment" data-fragment-index="1">&lt;Route path="&#42" component={DynamicPage} /&gt;</span>

&lt;/Route&gt;
</code></pre>

Notes:
- Check declared routes
- We don't have many routes because we have so many CMS pages
- `/women` doesn't match, so render the `<DynamicPage />` component

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
  "content-uuid-01": {
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
Video of flipping through TopStory slides and clicking on a featured product to get to its product page
(Let's keep it simple and not show any TopStory modules with video)
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
- We plug this data into an image and use the library lazysizes to determine the width of the current image, so we always load the smaller possible image.

---

### `<TopStory />` Step 2: Fetch product data
<div style="background: yellow; color: black">
ASSET NEEDED
<br>
Two product tiles: One regular, one on sale
</div>

Notes:

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

## Summary

- Infinite arbitrary pages<!-- .element: class="fragment" -->
- No deployment<!-- .element: class="fragment" -->
- Localized<!-- .element: class="fragment" -->
- Responsive images<!-- .element: class="fragment" -->
- Up-to-date product data<!-- .element: class="fragment" -->
