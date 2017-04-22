# Fixed pages with CMS Supplemental Content

Notes:
- For more carefully defined pages that need some small bits easily adjustable

---

## Checkout Policies

![Checkout](content/images/checkout-1.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

Notes:
- These policies are accordians, rendered from CMS modules
- There are vertical slides with expansion, press DOWN

+++

## Checkout Policies

![Checkout](content/images/checkout-2.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

+++

## Checkout Policies

![Checkout](content/images/checkout-3.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

---

## Order Confirmation

![Checkout](content/images/order-confirmation.png)<!-- .element: style="max-height: 70%; max-width: 70%; margin-top: -18px;" -->

Notes:
Order confirmation page

---

## What happens when you go to **aldoshoes.com/us/en_US/checkout**?

---

## Step 1: Fetch CMS data

<p class="fragment" data-fragment-index="0">
  On route change, hit <code data-noescape>cms?page=**/checkout**&locale=**us**&language=**en_US**</code>
</p>

Get JSON back:<!-- .element: class="fragment" data-fragment-index="1" -->

```js
{
  "content-uuid-01": {
    "content-modules": {
      "uuid-02": { 
        "type": "accordion",
        "content-modules": {
          "uuid-03": { "type": "accordion-entry" },
          "uuid-04": { "type": "accordion-entry" },
        }
      },
    }
  }
}
```
<!-- .element: class="fragment" data-fragment-index="1" -->

Just like the custom page, but fewer modules, and generally less nesting.<!-- .element: class="fragment" data-fragment-index="2" -->

Notes:
- Data goes into the redux store

---

## Step 2: React Router

<p class="fragment" data-fragment-index="0">
  Check declared routes
</p>

<p class="fragment" data-fragment-index="1">
  Match `/checkout` path to declared route, render `<CheckoutPage />` component
</p>

<pre><code data-noescape>&lt;Route path="/" component={App}&gt;

  <span class="fragment" data-fragment-index="0">&lt;Route path="/product/:code" component={ProductPage} /&gt;</span>
  <span class="fragment" data-fragment-index="1">&lt;Route path="/store-locator" component={CheckoutPage} /&gt;</span>
  <span class="fragment" data-fragment-index="1">...</span>
  <span class="fragment" data-fragment-index="2">&lt;Route path="/checkout" component={CheckoutPage} /&gt;</span>
  <span class="fragment" data-fragment-index="2">...</span>

  <span class="fragment" data-fragment-index="3">&lt;Route path="&#42" component={DynamicPage} /&gt;</span>

&lt;/Route&gt;
</code></pre>

<p class="fragment" data-fragment-index="3">
  Since we matched a route earlier, `DynamicPage` never comes into play.
</p>

Notes:
- Check declared routes
- Checkout *does* match a declared route, so we use the defined handler/component

---

## Step 3: Render `<CheckoutPage />`

<p class="fragment" data-fragment-index="0">
  All the fixed components can render immediately...
</p>

<p class="fragment" data-fragment-index="2">
  ... and then we render the Policy CMS modules.
</p>

<pre><code data-trim data-noescape>
function CheckoutPage(props) {
  <span class="fragment" data-fragment-index="0">const {
    cartDetailsProps,
    <span class="fragment" data-fragment-index="3">policyCmsModules,</span>
  } = props;</span>
  ...
  return (
    &lt;div&gt;
    <span class="fragment" data-fragment-index="0">
      &lt;CartDetails { ...cartDetailsProps } /&gt;
      &lt;UserDetailsStep /&gt;
      &lt;ShippingStep /&gt;
      &lt;PaymentStep /&gt;
      &lt;ReviewStep /&gt;
      <span class="fragment" data-fragment-index="3">&lt;PolicyDetails contentModules={ policyCmsModules } /&gt;</span>
    </span>
    &lt;/div&gt;
  )
  </span>
}
</code></pre>

Notes:
- We can render pretty much everything without any modules
- We DO NOT wait or show a loader.
- If the CMS data fails, customers can still buy shoes
- React will re-render when the module data lands in the redux store and we bubble it up through the prop selectors

---

## Step 4: Render `<PolicyDetails />` with the CMS Modules

<p class="fragment" data-fragment-index="0">
  Internally, this works more or less the same as the Dynamic CMS pages
</p>

<pre><code data-trim data-noescape>
function PolicyDetailsAccordion({
  contentModules,
  options,
}) {
  return (
    &lt;div&gt;
    <span class="fragment" data-fragment-index="1">
      { buildCmsModules(contentModules, <span class="fragment" data-fragment-index="2">{ options }</span>) }
    </span>
    &lt;/div&gt;
  );
}
</code></pre>

<p class="fragment" data-fragment-index="1">
  `buildCmsModules` is the same core function <span class="fragment" data-fragment-index="2">... of course there is always a bit of hidden complexity.</span>
</p>

Notes:
- None for now

---

## Step 5: Put it all together

<p class="fragment" data-fragment-index="0">
  Fixed page components<span class="fragment" data-fragment-index="1">, and CMS Modules.</span>
</p>

<pre><code data-noescape>
&lt;CheckoutPage&gt;
<span class="fragment" data-fragment-index="0">
  &lt;CartDetails { ...cartDetailsProps } /&gt;
  &lt;UserDetailsStep /&gt;
  &lt;ShippingStep /&gt;
  &lt;PaymentStep /&gt;
  &lt;ReviewStep /&gt;
</span>
<span class="fragment" data-fragment-index="1">
  &lt;PolicyDetails&gt; 
    &lt;Accordion&gt;
      &lt;AccordionItem1 /&gt;
      &lt;AccordionItem2 /&gt;
    &lt;/Accordion&gt;
  &lt;/PolicyDetails&gt;
</span>
&lt;/CheckoutPage&gt;
</code></pre>

---

## Summary

- Dynamic content can be built into any fixed page<!-- .element: class="fragment" -->
- Unlike custom pages, we generally do not wait.<!-- .element: class="fragment" -->
- Fixed content takes priority<!-- .element: class="fragment" -->
- React + redux allow us to redraw when we get CMS data<!-- .element: class="fragment" -->
