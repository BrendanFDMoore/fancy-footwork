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

On route change, hit api/cms?page=**/women**&locale=**us**&language=**en_US**

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

Match `/women` path to wildcard route, render `<DynamicPage />` container

<pre><code data-noescape>&lt;Route path="/" component={App}&gt;
  <span class="fragment">&lt;Route path="/product/:code" component={ProductPage} /&gt;
  &lt;Route path="/checkout" component={CheckoutPage} /&gt;</span>
  <span class="fragment">&lt;Route path="&#42" component={DynamicPage} /&gt;</span>
&lt;/Route&gt;
</code></pre>

Notes:
- This is a simplification of our application's routes
- But we do have fewer than you might think, because we have so many pages generated entirely by the CMS
- `/women` doesn't match any of our declared routes, so we'll render the `<DynamicPage />` container

---

## Step 3: Render `<DynamicPage />`

Determine content has loaded, render `<CMSCustomPage />` container

<pre><code data-trim data-noescape>
function DynamicPage(props) {
  const {
    <span class="fragment" data-fragment-index="1">hasContentModules,</span>
    hasFetchedPage,
  } = props;

  if (!hasFetchedPage) {
    return &lt;Loader&gt;;
  }

  <span class="fragment" data-fragment-index="1">if (hasContentModules) {
    return &lt;CMSCustomPage /&gt;; // Pick me!
  }

  return &lt;NotFoundPage /&gt;;</span>
}
</code></pre>

Notes:
- First check if we've fetched data for the current route. If not, render a loading screen.
- If we have, check if we have content modules on the store. We got CMS data back for `/women`, so this is true.
- If we had hit a crazy route, like aldoshoes.com/banana, we would not have gotten any CMS data back, and we'd render the 404 page!

---

## Step 4: Map CMS modules to Redux containers

Turn CMS data...

<pre><code data-noescape>{
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
  ...into Redux containers
</p>

```
<TopStory />
<MainStory />
<GetInspired />
<TrackOrder />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

---

## Step 4: Render CMS container - `<TopStory />`

---

![Women's shoes](content/images/top-story.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

Notes:
- Some features to highlight...
- Title and description
- Front and back images
- Products with prices (need to be up to date)

---

### Configure assets

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

```
<img
  class="lazyload"
  data-sizes="auto"
  data-srcset="//media.aldoshoes.com/assets/pastel__400 400w,
               //media.aldoshoes.com/assets/pastel__1200 1200w" />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

<p class="fragment" data-fragment-index="1">
  (With a little help from `lazysizes`)
</p>

---

### Fetch product data

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

```
<img
  class="lazyload"
  data-sizes="auto"
  data-srcset="//media.aldoshoes.com/assets/pastel__400 400w,
               //media.aldoshoes.com/assets/pastel__1200 1200w" />
```
<!-- .element: class="fragment" data-fragment-index="1"-->

<p class="fragment" data-fragment-index="1">
  (With a little help from `lazysizes`)
</p>

---

### Map properties

Turn CMS properties...

```js
{
  "looks": {
    "look-0": {
      "title": "Pretty In Pastel",
      "content": "Light hues, heavy on style",
      "cta": {
        "title": "Shop",
        "link": "/women/pastels",
      },
      "front-asset": { ... },
      "back-asset": { ... },
      "featured-products": { ... }
    },
    "look-1": { ... }
  }
}
```

<p class="fragment" data-fragment-index="1">
  ...into `<TopStory />` component
</p>

```
<div className="top-story">
  <div className="top-story__slide">
    <h2>{title}</h2>
    <p>{content}</p>
    <Link to="ctaLink">{ctaTitle}</Link>
    <Img {...imageProps} />
    <FeatureProducts {...featuredProductProps} />
  </div>
  <div className="top-story__slide">...</div>
</div>
```
<!-- .element: class="fragment" data-fragment-index="1"-->
