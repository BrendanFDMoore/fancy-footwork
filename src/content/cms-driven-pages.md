## CMS-Driven Pages

---

![Women's shoes](content/images/home.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

---

![Women's shoes](content/images/plp.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

---

![Women's shoes](content/images/women.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

---

## What happens when you go to **aldoshoes.com/us/en_US/women**?

Notes:
- The easiest way to explain this is to tell you a story, so let's talk about what happens when you go to the women's landing page on aldoshoes.com.

---

## Step 1: Fetch CMS data

<p class="fragment" data-fragment-index="0">
  On route change, hit api/cms?page=**/women**&locale=**us**&language=**en_US**
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
- Every time our app gets a new route, we fire off a request to the CMS for data associated with the new path in the given storefront (in this case US English).
- If the CMS has data for that page, we'll need a list of content modules back.
- If not, we'll get nothing.
- For now, we just need to keep track of the fact we got a response.

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
- This is a simplification of our application's routes
- But we do have fewer than you might think, because we have so many pages generated entirely by the CMS
- `/women` doesn't match any of our declared routes, so we'll render the `<DynamicPage />` component

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

<p class="fragment" data-fragment-index="0">
  Turn CMS data...
</p>

<pre class="fragment" data-fragment-index="0"><code data-noescape>{
  "content-uuid-01": {
    "content-modules": {
      "uuid-01": { "type": "top-story", ... },
      "uuid-01": { "type": "main-story", ... },
      "uuid-01": { "type": "get-inspired", ... },
      "uuid-01": { "type": "track-order", ... },
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
<TrackOrder />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

---

## Step 5: Render React components

---

![Women's shoes](content/images/top-story.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

Notes:
- Some features to highlight...
- Title and description
- Front and back images
- Products with prices (need to be up to date)

---

### `<TopStory />` Step 1: Configure assets

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

---

### `<TopStory />` Step 2: Fetch product data

<p class="fragment" data-fragment-index="0">
  Turn product IDs...
</p>

```js
{
  "featured-products": {
    "feature-product-0": {
      "id": "123",
    },
    "feature-product-1": {
      "id": "456",
    }
  }
}
```
<!-- .element: class="fragment" data-fragment-index="0"-->

<p class="fragment" data-fragment-index="1">
  ...into `<ProductTile />` components
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
  price="$40" />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

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
  CMS wrapper
</p>

<p class="fragment" data-fragment-index="2">
  CMS modules
</p>

<pre><code data-noescape>&lt;body&gt;

  <span class="fragment" data-fragment-index="0">&lt;Header /&gt;</span>

  <span class="fragment" data-fragment-index="1">&lt;main className="cms-page"&gt;

    <span class="fragment" data-fragment-index="2">&lt;TopStory /&gt;
    &lt;MainStory /&gt;
    &lt;GetInspired /&gt;
    &lt;TrackOrder /&gt;</span>
    
  &lt;/main&gt;</span>

  <span class="fragment" data-fragment-index="0">&lt;Footer /&gt;</span>

&lt;/body&gt;</code></pre>
