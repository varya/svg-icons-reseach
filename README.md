# Research on using SVG icons in real projects

THIS DOCUMENT IS BEING DEVELOPED

## The goal
To find out a better way in using icons (SVG, fonts, PNG) for websites in 2015+.

## Requirements
- Responsive (2)
- Zoomable (3)
- Good performance (3)
- Modifyable from CSS (2)
- Saving (2)
- Browser support (2)
- Possibility of having a fallback (3)
- Easy to develop/maintain (2 or 1)
- Evolving options (2)

Legend:

| need |                    |
|------|--------------------|
| 3    | must have          |
| 2    | very nice to have  |
| 1    | just a good option |

### Requrements in details

#### Responsive

An icon may look differently on different screens. The bigger is the screen, the bigger can be an icon. And being bigger it also can be *more detailed*.

For example,

![](img/responsive-icons.png)

#### Zoomable

An icon should look nicely when a user zooms page.

#### Modifyable from CSS

An icon can be modifiable from the parent document's CSS. With this approach it is possible to provide small changes using the same icon.

Modifications can be of different volume, such as:

- change icon's size
- change icon's filling color
- change icon's parts
  - change color of different parts of icon
  - hide different parts and
  - provide transformations for different parts of icon

## Known tecnologies

### PNG

#### Responsive PNG

One icon cannot look differently on different screen sizes. It is only possible to provide different icons with diffent media quesries in CSS.

##### What is wrong with this solution

2-3 pictures for different variants of the same icon (or 2-3 items in sprite) make a user to download more.

It is not possible to use a responsive PNG icon inlined in HTML.

#### Zoomable PNG

Does not work, an icon will be pixelated for bigger scales.

#### Modifyable from CSS

It is not possible to change a PNG icon from CSS.

You can change the size, but teh result will be pixelated. Changing the color or modifying the source of icon is not possible at all.

### Font

#### Responsive Font

One icon cannot look differently on different screen sizes. It is only possible to provide different icons with diffent media quesries in CSS. The "symbol" should only be provided in CSS.

##### What is wrong with this solution

Requires a symbols in font for every version of icon (meaning 2-3 symbols for every icon).

It is not possible to use a responsive Font icon inlined in HTML.

#### Zoomable Font

Works perfect!

#### Modifyable from CSS

Modifying Font icon from CSS is partly doable. You can change its size and filling color. Modifying the source is not possible.

### SVG

Vector format for images.

#### Responsive SVG

SVG document can contain CSS, including media queries. This makes it adjustable to different screen sizes, orientations and so on.

#### Zoomable SVG

Works perfect!

#### Good performance

##### When inresting inline as a fragment

When using an icon from SVG sprite with a fragment technique (`<use ... xlink:href="link-to-file#fragment"`), it renders only the inserted element.

It is impossible to insert an SVG fragment from another host. Only relativ parts are supported.

##### When using SVG sprite as a background

It is possible to use CDN.

The whole SVG sheet is rendered (even if only a part of it is shown visibly). As SVG is not very fast, rendering the whole sprite at once brings big performance issues. This needs to be proven with numbers, no one measured yet, but a lot of experts say so.

#### Modifyable from CSS

An SVG icon can have its own embedded CSS. So, some things (such as different view for different screen sizes) can be achieved with it.

Weather an SVG icon can be modifyable from the parent document CSS, depends on how this icon was placed into the document.

Modifying inner parts of SVG is only possible if the icon was placed into HTML inline with `<svg>` tag. For example,

```
<svg class="icon icon-database" viewBox="0 0 32 32"><use xlink:href="sprite.svg#database"></use></svg>
```

Demo: http://varya.me/svg-sprites-experiment/

##### When using SVG sprite as a background

Modifying SVG parts is **not possible** when SVG sprite is used as a background with shifted possition.

##### Context problems

When having a set of SVG icon with embedded CSS, we can build a sprite of them and bring this CSS into it.

However, inserting SVG item into HTML with `<use>` tag will not bring embedded styles into teh document (even if the `<style>` element is a child of the imported). To be able to apply embedded sprite styles to the inserted parts of SVG, these styles should be parsed out of SVG source and placed into parent document's styles. (There can be a toll to make it automatically).

##### IE problems

IE does not support `use`. So, when using SVG sprites, there should be a Font or PNG fallback for IE. So, it brings the corresponding limits of modifying icon parts from the document CSS.

## Information

* https://useiconic.com/<br/>
  Explains the nice things of SVG solution
  
## Source
* https://useiconic.com/guides/using-iconic-responsively/