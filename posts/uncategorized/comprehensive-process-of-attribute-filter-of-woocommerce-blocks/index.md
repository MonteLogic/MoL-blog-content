---
title: "Comprehensive Process of  attribute-filter of WooCommerce Blocks."
date: "2022-10-13"
---

Okay the main thing is attributeTerms. Which is declared as results from a useCollection hooks call as:

```
namespace: '/wc/store/v1',
resourceName: 'products/attributes/terms',
// What is the attributeObject
resourceValues: [ attributeObject?.id || 0 ],
shouldSelect: blockAttributes.attributeId > 0,
```

attributeTerms is then an object which is iterated upon. Then that object is the initial load then it is refreshed based on DOM events.

...

For the showing of the count:

```
// Okay, so the line below is what shows the count of each arrtibute. showCounts is a boolean, if it evaluates false then the component is going to output the count variable. 
count={ blockAttributes.showCounts ? count : null }
```

.....

I think, that the block for the all products which the attribute filter modifies is using the Attributes of the block. I will be using Attributes to refer to the Attributes of a block and attributes to refer to the attributes of a product.

So, the all products block loads the info on the editing side via the V2 API and then the user on the editing side, saves the post and then that is then saved as Attributes of the block. Then on the frontend it iterates through the saved products. Then I think the attribute filter, can view that through Attributes and then reduce it that way.
