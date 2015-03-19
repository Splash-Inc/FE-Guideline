There are too many things at web pages and only one way to style these: CSS. The nature of CSS makes easy things out of control. BEM is an approach to write better CSS.

## Wtf is BEM?
BEM is simply a naming methodology for CSS classes. And it makes your CSS more meaningful and scalable with few simple rules. Also it's currently best way to write CSS with a team.

## Why BEM?
CSS is really hard to scale. If you're not careful enough, you can find yourself repeating, easily. For instance if you're writing a class for a state of an element like `.red` you could forget about it's a global class. Somebody or you could override it and broke your component. Also, any changes made on HTML structure may require an immediate, mirror change in CSS as well.

## How to BEM?
BEM has three level: Block, Element, Modifier. Let's see what are these:

### Block
Block is the shallowest level of your component. Block is the container or context of element itself. You might have a header, footer, sidebar or post; all of these represent blocks in BEM.

### Element
Element is simply a piece of block. It represents the elements of a block. For example if you have a navigation block, each navigation link is an element of your block. But it could be also thought as a block itself because it's also modifiable.

### Modifier
When a block appears more than once in your page, each with a slightly different state, these states represents a modifier in BEM. When using modifiers you should be careful not to repeat yourself. It's just a modifier and probably overwrite some property of your block/element. Modifiers must contain only state-specific rules.

When using CSS pre-processors like SASS or LESS, you should be careful about nesting. Actually there is no place for nesting in BEM way. Nesting is what makes your CSS code repeatable. For instance if you have a button with a selector like `.post > .header > p > button.delete` it's very though to use this button some other place without worrying about keeping the code modular and `DRY`.

## Enough talk, let's see some code
In this example we have a navigation that have items with red and white colors.

```css
/* Navigation block */
.navigation {
    width: 100%;
    height: 50px;
}

/* Navigation block's item */
.navigation__item {
    display: inline-block;
    color: white;
}

/* A state of item */
.navigation__item--red {
    color: red;
}
```

Double underscore `__` represents an element. You should add this after a block name. Only a block can have an element.

Double hyphen `--` represents a modifier. It comes after blocks or elements.

If you are using LESS or SASS you could write same example in the following way:

```less
.navigation {
    width: 100%;
    height: 50px;

    &__item {
        display: inline-block;
        color: white;

        &--red {
            color: red;
        }
    }
}
```

Another Example:

```less
.blog-post {
    color: RosyBrown;
    float: left;
    width: 50%;

    &__header {
        border-bottom: 1px solid AliceBlue;
    }
    &__content {
        padding: 10px;
    }

    &--featured {
        color: SandyBrown;
        float: none;
        width: 100%;

        .blog-post__header {
            border-bottom: none;
        }
    }
}
```

## When using BEM;
 - Be careful about global CSS classes. Try to avoid any global modifier like `.red`.

 - Don't use element selectors. i.e: use `.navigation-item` instead of `ul li`.

 - Make blocks as **flexible** as you can. It also helps to responsiveness.

## Common Questions
### Why double hyphen?
Because writing CSS class names with **camelCase is a bad way** and sometimes you have to write class with two word. These words should be separated with single hypen `-`. So, writing `modifiers` with a single hypen would lead to confusions. i.e: Is it a part of block name or a modifier?

### Could `element` also be another block?
Simply YES. But be careful with that. If you think each `element` is also a global block you're probably in a wrong way.
