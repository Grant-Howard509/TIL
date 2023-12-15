# Box Model

There are many types of box elements that can fit into two categories: `block` and `inline`.

Both `block` and `inline` have an outer and inner display type which can be set using the property `display`.

## Outer Display Type

Block elements have the outter display characteristics:

- The box element will break onto a new line.
- The width and height properties are applied
- Padding, margin and border will cause other elements to be pushed away from the box.
- If width is not specified, the box will extend in the inline direction to fill the space available in its container. In most cases, the box will become as wide as its container, filling up 100% of the space available.

Inline elements have the outter display characterisitics:

- The box will not break onto a new line.
- The width and height properties will not apply.
- Top and bottom padding, margins, and borders will apply but will not cause other inline boxes to move away from the box.
- Left and right padding, margins, and borders will apply and will cause other inline boxes to move away from the box.

## Inner Display Type

Elements inside of other inline or block elements will behave according to their type regardless of nesting. That being said, the inner display type can be change. For example, a block element can have a display type of `flex`. That element outter display type still behave like a block elements, but its inner display is a type of flex. Also, any children from this element will become a flex item by default.

The same concept applies to the inner display type of `grid`.

## Box Model?

The CSS box model refers to a block boxes and defines the different characteristics of the box: content, padding, border, and margin.

Inline boxes only use some of the behaviors define in the box model.

## Box Parts

The parts of a box model include:

- Content box: Where the content is displayed; properties inlcude `inline-size`, `block-size`, `width`, and `height` for sizing.
- Padding box: Sits around the content like whitespace; use property `padding` for sizing.
- Border box: Wraps around both padding and content; use propery `border` for sizing.
- Margin box: The outter layer, acts as whitespace and spacing between element; use property `margin` for sizing.

## Standard Box Model

If there is a given `width` and `height` applied to a box, any padding, border, and margin will add to the total size of the box.

For example consider the following:

```
 .box {
    width: 300px;
    height: 100px;
    padding: 100px;
    border: 100px;
    margin: 50px
 }
```

Here, the width of the box would not be 300px, instead will have a width of 550px (300 + 100 + 100 + 50). This logic applies to the height with the box height being 350px (100 + 100 + 100 + 50).

## Alternative Box Model

An alternative to the standard box model is the use of `border-box`. What `border-box` does is that it take the content width and height of the box and subtracts it how the amount of padding and border As a result, the box itself stays a consistant width and height.

Lets use the same example except with `border-box`.

```
 .box {
    /* Set border-box */
    box-sizing: border-box;

    width: 300px;
    height: 100px;
    padding: 100px;
    border: 100px;
    margin: 50px
 }
```

Now the width and height will add up to 300px by 100px. To see this in action check out this article by [MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)

## Margin Collapsing

When two box elements margins come into contact with one another, depending on whether a box is positive or negative determines a particular behavior.

These behavoirs include:

- Two positive margins will combine to become one margin. Its size will be equal to the largest individual margin.
- Two negative margins will collapse and the smallest (furthest from zero) value will be used.
- If one margin is negative, its value will be subtracted from the total.

## Box Model for Inline

Boxes that are inline can have their boxes sized using padding, border, and margin. However, the width and height properties do not apply and will be ignored.

Another note is that inline boxes will overlap other box elements vertically push content horizontally. This means when we add padding, border, or margin elements that are aligned vertically to the inline box will be overlapped while horizontal elements will be pushed away.

## Using inline-block

The display type `inline-block` allows an inline element to have some `block` level features. All inline-block elements will still align along side one another, but they will also have a `width` and `height` properties. Also, these elements will be able to push elements away both horizontally and verticlaly when the box size changes.

## Resources

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
