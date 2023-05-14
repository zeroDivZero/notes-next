# QUICK START

## Install

```sh
npm i react react-dom next
```

## Pages

Create folder `pages` at root and add to it pages as `js` or `jsx` files. Each file should export default component function for Next to render as main component of page.

```jsx
export default function HomePage() {
  return (
    <div>
      // ...
    </div>
  );
}
```

Page can be accessed at `https://{host}/{pageName}`.

### Example

```jsx
import { useState } from 'react';

function Header({ title }) {
  return <h1>{title ? title : 'Default title'}</h1>;
}

export default function HomePage() {
  const names = ['Ada Lovelace', 'Grace Hopper', 'Margaret Hamilton'];
  const [likes, setLikes] = useState(0);

  function handleClick() {
    setLikes(likes + 1);
  }

  return (
    <div>
      <Header title="Develop. Preview. Ship. 🚀" />
      <ul>
        {names.map((name) => (
          <li key={name}>{name}</li>
        ))}
      </ul>

      <button onClick={handleClick}>Like ({likes})</button>
    </div>
  );
}
```

## Test Run

In `package.json`, add `"dev": "next dev"` to `scripts` section.

Run:

```sh
npm run dev
```

Verify page at `http://localhost:3000/{pageName}`.

When editing component and save, change reflected real-time by feature **Fast Refresh** (enabled by default).

Next takes care of complex tooling like babel.
