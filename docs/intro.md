---
sidebar_position: 1
---

# Getting Started

Get started by **creating a new site**.

Or **try Chakra Components** with **[chakra-components](https://chakra-components.netlify.app)**.

### Installation

To use Chakra UI in your project, run one of the following commands in your terminal:

```shell
npm i @chakra-ui/react @chakra-ui/icons @emotion/react @emotion/styled framer-motion react-icons react-hook-form
```

or

```shell
yarn add @chakra-ui/react @chakra-ui/icons @emotion/react @emotion/styled framer-motion react-icons react-hook-form
```

After installing Chakra UI, you need to set up the ChakraProvider at the root of your application. This can be either in your index.jsx, index.tsx or App.jsx depending on the framework you use.

```jsx
import * as React from "react";

// 1. import `ChakraProvider` component
import { ChakraProvider } from "@chakra-ui/react";

function App() {
  // 2. Wrap ChakraProvider at the root of your app
  return (
    <ChakraProvider>
      <TheRestOfYourApplication />
    </ChakraProvider>
  );
}
```
