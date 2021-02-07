# css-helpers

## Positioning elements

### Margin
Use on block elements that have a defined width

#### Center element horizontally: 
```css
.element {
    margin: 0 auto;
    width: 100px;
}
```

#### Move element to the end of the page 
```css
.element {
    margin-left: auto;
    width: 100px;
}
```

### Grid 

#### Move element to center horizontally and vertically
```css
.element {
    display: grid;
    place-items: start;
}
```

## Responsive design

### Grid

#### Makes container responsive without media queries

```css
/// or auto-fill
.element {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
```

### rem/em

#### Changes default font size
```css
//1rem=10px(10/16*100=62.5)
html {
	box-sizing: border-box;
	font-size: 62.5%;
}

//1rem=9px(9/16*100=56.25)
@media only screen and (max-width: 75em) {
	html {
		font-size: 56.25%;
	}
}

//1rem=8px(8/16*100=50)
@media only screen and (max-width: 56.25em) {
	html {
		font-size: 50%;
	}
}

//1rem=12px(12/16*100=75)
@media only screen and (min-width: 112.5em) {
	html {
		font-size: 75%;
	}
}
```

## Image/Background

### Blend mode 

#### Adds cool blending mode to background image 
```css
.element {
    background-image: url(backgroundImageUrl);
    background-color: green;
    background-blend-mode: hard-light;
}
```

### Clip-path

#### Allows to make custom shapes(online generator https://bennettfeely.com/clippy/)
```css
.element {
    clip-path: polygon(0 0, 100% 0, 100% 53%, 0 86%);
}
```

### Gradient

#### Adds custom transition between two or more colors
```css
.element {
    background-image:linear-gradient(to right bottom,
        rgba(218, 120, 102, 0.8),
        rgba(255, 99, 71, 0.7)),
        url(backgroundImageUrl});
}
```
## Dark/Light mode 

### Filter + background

#### Change page colors to dark or light

```css
.element {
    background: black;
    filter: invert(1) hue-rotate(180deg);
}
```


## Styled-components 


### Custom helpers

#### Responsive helper
```js
import { css } from "styled-components";

export const responsive = (device, style) => {
    let mixin;
    switch (device) {
        case 'phone': //600px
            mixin = css`@media only screen and (max-width: 37.5rem) { ${style} }`;
            break;
        case 'tablet-port': //900px
            mixin = css`@media only screen and (max-width: 56.25rem) { ${style} }`;       
            break;
        case 'tablet-land': //1200px
            mixin = css`@media only screen and (max-width: 75rem) { ${style} }`;
            break;
        case 'big-desktop': //1800px
            mixin = css`@media only screen and (min-width: 112.5rem) { ${style} }`;            
            break;
        default:
            break;
    }
    return mixin;
};
```

#### Usage
```js
export const Header = styled.div`
    grid-column: 3 / 11;
    ${responsive('phone',`    
        grid-column: 1 / -1;
    `)}
`;
```
