# Setting Up NativeWind with Expo and Tailwind CSS

## Step 1: Create Expo App

First, create your Expo app:

```bash
npx create-expo-app my-app
cd my-app
```

## Step 2: Install Dependencies

Install NativeWind and Tailwind CSS:

```bash
yarn add nativewind
yarn add --dev tailwindcss@^3.3.2
```

Initialize Tailwind CSS:

```bash
npx tailwindcss init
```

## Step 3: Configure Tailwind CSS

Modify your `tailwind.config.js` to include paths to your React Native files:

```javascript
// tailwind.config.js

module.exports = {
  content: ["./App.{js,jsx,ts,tsx}", "./<custom directory>/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## Step 4: Configure Babel

Update your `babel.config.js` to include the NativeWind Babel plugin:

```javascript
// babel.config.js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ["babel-preset-expo"],
    plugins: ["nativewind/babel"],
  };
};
```

## Step 5: Install PostCSS and Configure Webpack

Install PostCSS and necessary loaders:

```bash
yarn add postcss@8.4.23
npm i -D postcss-loader@4.2.0 @expo/webpack-config
```

Update your `webpack.config.js` to include PostCSS loader:

```javascript
// webpack.config.js
const createExpoWebpackConfigAsync = require("@expo/webpack-config");

module.exports = async function (env, argv) {
  const config = await createExpoWebpackConfigAsync(
    {
      ...env,
      babel: {
        dangerouslyAddModulePathsToTranspile: ["nativewind"],
      },
    },
    argv,
  );

  config.module.rules.push({
    test: /\.css$/i,
    use: ["postcss-loader"],
  });

  return config;
};
```

## Step 6: Finalize Installation

Finalize your installation by running:

```bash
yarn start
```

Your Expo app with NativeWind and Tailwind CSS should now be up and running!
