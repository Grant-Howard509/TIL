# CSS Specificity

MDN Web Docs defines specificity as "the algorithm used by browsers to determine the CSS declaration that is the most relevant to an element, which in turn, determines the property value to apply to the element". How this algorithm works and how the browser determines what property value to apply will be covered here.

How does specificity work?

Specificity is used as a weighted system to determine what property value is used. The three columns used are ID, CLASS, and TYPE. Each column of the 3 columns are written as ID-CLASS-TYPE (0-0-0) with the left most number being the highest weight value.

## ID

ID selectors, such as `#exampleID`, are the highest specificity with a score of `1-0-0` for each ID value. Since a HTML tag can only have one ID, the highest the ID column can go is `1-0-0` for each tag.

## CLASS

The class column includes class selectors but also attribute selectors like `[type='checkbox']` and pseudo-classes like `:hover`. Each class, attribute, and pseudo-class selector is worth a weight of `0-1-0` on the specificity scale. Consider the following: `.example:hover { PROPERTIES }` this selector would have a specificity score of `0-2-0` because we have one class selector and one pseudo-class selector.

## TYPE

The type column includes both type selectors like `p` or `h1`, and pseudo-elements such as `::before`. For each type and pseudo-element selector, the specificity score is `0-0-1`.

## How Does Specificity Work?

Consider the following example:

```
HTML:
  <div id="example">
       <span class="description"> Some description here </span>
  </div>


CSS:


   #example {
       font-size: 2rem;
   }


   .description {
       font-size: 1.5rem;
   }
```

Here we see a div tag with the id of `example` and its child span with a class of `description`. One could assume that since the selector `.description` is farther down the cascade, its properties would be applied. However, on second evaluation, the developer will notice that the spans content remains a font size of 2rem. This is because the selector `#example` has a specificity score of `1-0-0` and `.description` only has a specificity score of `0-1-0` which has a lower weight than `#example`. Nonetheless, the selector `.description` can still override `#example` property values by having a higher specificity score. We can do this by adding an id.

Here is the solution:

```
HTML:
  <div id="example">
       <span id="specificity" class="description"> Some description here </span>
  </div>


CSS:


   score: 1-0-0
   #example {
       font-size: 2rem;
   }


   score: 1-1-0
   #specificity .description {
       font-size: 1.5rem;
   }
```

Now we could have just had `#specificity` to override the property values from `#example`, but wanted to make it clear how the specificity score is calculated. The more specific we get with our selectors, the higher the specificity score.

## Resources

[MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
