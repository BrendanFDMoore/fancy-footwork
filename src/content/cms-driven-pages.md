## CMS-Driven Pages

---

## What happens when you go to **aldoshoes.com/us/en_US/women**?

![Women's shoes](content/images/women.png)

Notes:
- The easiest way to explain this is to tell you a story, so let's talk about what happens when you go to the women's landing page on aldoshoes.com.

---

## Step 1: Fetch CMS data

- Hit api/cms?page=**/women**&locale=**us**&language=**en_US**
- Get JSON back:<!-- .element: class="fragment" data-fragment-index="1" -->

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

Match wildcard route to `<DynamicPage />` container

<pre><code data-noescape>&lt;Route path="/" component={App}&gt;
  <span class="fragment">&lt;Route path="/product/:code" component={ProductPage} /&gt;
  &lt;Route path="/checkout" component={CheckoutPage} /&gt;</span>
  <span class="fragment">&lt;Route path="&#42" component={DynamicPage} /&gt;</span>
&lt;/Route&gt;
</code></pre>

---

## Step 3: Render `<DynamicPage />`

- Using special separators, you can have "stacked" vertical slides. Press down to see the lower slides, or skip it by pressing right.

+++

## Skippable Vertical Section

- This has some extra information that can be skipped if you are short on time
- You debated excluding this anyways, didn't you?

---

## The Next Important Slide

- This is what you need to get to if you're running behind.
- Skip over the verticals and get here
