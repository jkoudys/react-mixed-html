# react-mixed-html
React component that allows you to mix HTML children as siblings &amp; parents of React elements.

## Why?
There are several projects out there already that let you sanitize and render HTML into a React component. These tend to be all or nothing approaches, mimicking the `dangerouslySetInnerHTML` builtin approach, with a little bit of stripping dangerous tags out (e.g. `<script>`, `<link>`, `<iframe>`, etc.) If that's all you want to do, go with another project.

This project isn't meant for new projects, or as a final stage. Rather, it's a stable approach that will allow you to incrementally migrate all your old `.ejs`, server-rendered html (e.g. from an old PHP page), jQuery that renders into a jQuery element via `$.fn.html`, etc.

I've endeavored to efficiently attach these common methods of view rendering in, so you can mix HTML next to your `createElement`s, and even write fragments so other Components can live as children.

e.g.
```javascript
import { createElement as ce } from 'react';
import MixedHtml from 'mixed-html';

const safeTags = ['p', 'span', 'mark', 'b', 'i', 'strong', 'em', 'ul', 'li', 'h1', 'h2', 'h3'];

const MyComponent = ({ name, rank, serialNo }) => (
  ce(MixedHtml, { tagName: 'div', safeTags },
    `<h1>Hello, ${name}!</h1>`,
    `<ul>
      <li>Your rank is ${rank}</li>`,
    ce('li', null, 'Your serial number is: ', serialNo),
    `</ul>`,
  )
);
```

Obviously you wouldn't write a new site this way, but if the HTML is either user-supplied, or part of a large-scale migration, this can speed things along by letting you quickly wrap up your old HTML as React components.
