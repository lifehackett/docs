--- 
id: component-compositions
title: Compositions
--- 

'Compositions' are, essentially, small apps that exhibit and test a component in various potential usages.
They serve as a way to run manual and automated integration tests, before such integrations are done by consumers of that component.

Moreover, a component's composition is a way to demonstrate that component for other developers looking to use it, and non-developers, such as designers and product managers, looking to inspect it.

Adding compositions to a component is done by creating a file in the component's directory, using the `*.composition.*` pattern.

For example:

```shell {3}
└── ui/button
    ├── index.tsx
    ├── button.composition.tsx
    └── button.tsx
```

Each composition is a standard usage of a component (requiring no special syntax) that is exported with a name.

For example, the following is a composition of the 'button' component.

```js
import React from 'react';
import { Button } from './button';

export const BasicButton = () => {
  return <Button text="click me" />;
};
```
