
---
layout: post
title: Yarn install on Mojave
date_string: 27 September 2019
---

If you're having issues in `yarn install` on Mojave, then it's probably down to the fact
that Mojave doesn't support different i386 architecture and anything that involves native
building, gems or node modules, seems to fail. The solution is to clean the slate and start
fresh. That's exactly what I had to do to fix the yarn installation errors:

```
rm yarn.lock
yarn cache clean
yarn install
```

These commands worked like a charm!

Hope it helps!
