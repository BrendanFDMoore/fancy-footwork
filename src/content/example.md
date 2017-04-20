<!-- .slide: data-background="../content/images/title-slide.jpg" -->

## Above the Line Title

# Center Line Title

---

## Numbered List

<!-- You don't need to manage the numbers -->
1. First Bullet
  1. Numbered sub-bullet 1
  1. Numbered sub-bullet 2
1. Second Bullet
1. Third Bullet
 - Unnumbered sub-bullet
1. Press S for speaker mode with notes

Notes:
- You can write notes for yourself here.
- Audience won't see this.
- You also get a timer.

---

## List with incremental reveal / fragments

- Show first bullet at the start
- Increment second bullet <!-- .element: class="fragment" -->
- Increment third bullet <!-- .element: class="fragment" -->
- Surprise fourth bullet <!-- .element: class="fragment" -->

---

## Code snippets

- Setting some context for `SomeModule` in `some.file.js`


#####_src/path/to/some.file.js_
```js
import { SomeModule } from 'some-package';

const someFunction = (param) => {
  if (param && param.flag) {
    return SomeModule.FuncA(param.data);
  } else {
    return SomeModule.FuncB(param.data);
  }
}
```

---

## Vertical Sections

- Using special separators, you can have "stacked" vertical slides. Press down to see the lower slides, or skip it by pressing right.

+++

## Skippable Vertical Section

- This has some extra information that can be skipped if you are short on time
- You debated excluding this anyways, didn't you?

---

## The Next Important Slide

- This is what you need to get to if you're running behind.
- Skip over the verticals and get here
