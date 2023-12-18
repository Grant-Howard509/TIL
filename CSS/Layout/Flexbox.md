# Flexbox

## What is Flexbox

Flexbox is a layout method that arranges items into columns and rows. It is a one dimensional layout where items inside the flexbox expand or shrink in accordance to the window space avaiable.

## How to Create a Flexbox?

Take a look at this example:

```
    <section>
        <article>...</article>
        <article>...</article>
        <article>...</article>
    </section>
```

We can see that there is a element of `section` that contains three `article` elements. If we want to what to layout all of the `article` tags, we must create a flex element out of their parent, `section`. The `section` element will be the flex container with its children as flex items, in this case the `article` elements. To do this, we set the `display` property on `section` to type `flex`.

```
    section {
        display: flex;
    }
```

The sections outter display still has the same normal flow as a block item, however, its inner children (inner display) are to be treated as flex items.

## The Flex Model

Flex items have two axes:

- The `main axis`
- The `cross axis`

The `main axis` refers to the direction the flex items are layout in. Items can be layout as a row (horizontally) or as a column (vertically).

The `cross axis` is the perpendicular axis to the main axis layout direction.

The parent element that has the `display: flex;` property is called the `flex container`.

Elements inside of teh `flex container` are called `flex items`.

## Flex Direction

The property `flex-direction` determines what direction the `main axis` runs. Values for `flex-direction` include: column, row, row-reverse, and column-reverse.

This property must be added to the `flex container` in order to work.

## Flex Wrap

The property `flex-wrap` can be added to the `flex-container` which will handle overflowing of flex items. This will adjust the children to fit the container regardless of container size.

## Flex Flow Shorthand

A shorthand method for both properties `flex-direction` and `flex-wrap` exist called `flex-flow`. In the example below, both selectors do the exact same styling to the element but `flex-flow` only does it in one singular line.

```
    /* flex-direction and flex-wrap */
    section {
        flex-direction: row;
        flex-wrap: wrap;
    }

    /* flex-flow */
    section {
        flex-flow: row wrap;
    }
```

## Flexible Sizing of Flex Items

Adding the property `flex: 1;` to all flex item will indicate that we want all flex items to take up an equal amount of space along the `main axis`. This includes equal spacing after margin and padding are set to the flex items.

Lets look at the following example:

```
HTML:
    <section>
        <article>...</article>
        <article>...</article>
        <article>...</article>
    </section>

CSS:
    article {
        flex: 1;
    }

    article.nth-of-type(3) {
        flex: 2;
    }
```

The last flex item in section is recieving twice as much space compared to the items before it. The space avaiable is divided by their total units of each flex item, in this case 4 (1 + 1 + 2 = 4). The first two items take 1/4 of the total avaiable space while the last items takes 2/4 (or 1/2) of the avaiable space.

Another feature with the property `flex` is setting the flex items minimum size as such:

```
    article {
        flex: 1 200px;
    }

    article:nth-of-type(3) {
        flex: 2 200px;
    }
```

The flex items here are each first given the 200px worth of space, after each has 200px, the portional units of space are then calculated.

## Flex: Shorhand vs Longhand

The property `flex` used above is a shorthand that addresses 3 different property values:

- flex-grow: Sets the proportion units like the examples above.
- flex-shirnk: Uses portional units to specify when a flex item needs to shrink in order to prevent overflow.
- flex-basis: Sets the minimum flex item size like the examples above.

## Horizontal and Vertical Alignment

Properties `justify-content` and `align-items` are used to align flex items both across the main/cross axes. The `justify-content` property is used for the main axis and the `align-items` property is for the `cross-axis`.

## Ordering Flex Items
