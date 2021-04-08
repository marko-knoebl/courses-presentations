# Basic example: slideshow

## Basic example: slideshow

example _slideshow_ app that demonstrates:

- component definition as a function
- component state (image id)
- JSX template language: mix of JavaScript and XML

## Basic example: slideshow

```jsx
import { useState } from 'react';

const baseUrl = 'https://picsum.photos/300/200?image=';
function SlideshowApp() {
  const [img, setImg] = useState(0);
  const imgUrl = baseUrl + img.toString();
  return (
    <div>
      <h1>Image {img}</h1>
      <button onClick={() => setImg(0)}>start</button>
      <button onClick={() => setImg(img - 1)}>prev</button>
      <img src={imgUrl} alt="slideshow" />
      <button onClick={() => setImg(img + 1)}>next</button>
    </div>
  );
}
export default SlideshowApp;
```

can be tried on <https://codesandbox.io>

## Basic example: slideshow

```jsx
function SlideshowApp() {
  // ...
}
```

A component is defined as a function that returns an XML tree

The function is called every time the component needs to be (re-)rendered

## Basic example: slideshow

<!-- prettier-ignore -->
```jsx
  const [img, setImg] = useState(0);
  const imgUrl = baseUrl + img.toString();
```

A component can have internal state entries

`useState` returns the current state entry and a corresponding setter on every render

Other values (like `imgUrl`) can be derived from the state values

## Basic example: slideshow

<!-- prettier-ignore -->
```jsx
  return (
    <div>
      ...
    </div>
  );
```

An XML tag switches from JavaScript to XML mode

## Basic example: slideshow

<!-- prettier-ignore -->
```jsx
      <h1>Image {img}</h1>
```

A curly brace switches back to JavaScript

## Basic example: slideshow

<!-- prettier-ignore -->
```jsx
      <button onClick={() => setImg(0)}>start</button>
      <button onClick={() => setImg(img - 1)}>prev</button>
      <img src={imgUrl} alt="slideshow" />
      <button onClick={() => setImg(img + 1)}>next</button>
```

Event handlers can be defined as JavaScript functions
