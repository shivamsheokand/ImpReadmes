# commands for create expo projects

## step 1 : create expo project.

create first managed expo app.

```bash
npx expo init firstProject
cd firstProject
```

second way.

```bash
npx create-expo-project myNewProject
cd myNewProject
```

## convert to ware project

```bash
npx expo prebuild
npx expo prebuild --platform ios
```

create wareexpo project.

- for typescript

```bash
npx create-expo-app@latest ProjectName -t blank@sdk-49
npx create-expo-app@latest --template tabs@50
```

```bash
-sdk 50 and above

npx expo install expo-router react-native-safe-area-context react-native-screens expo-linking expo-constants expo-status-bar

-sdk 49 and below

npx expo install expo-router react-native-safe-area-context react-native-screens expo-linking expo-constants expo-status-bar react-native-gesture-handler
```

- setup entry point

### sdk 49 and above

- For the property main, use the expo-router/entry as its value in the package.json. The initial client file is app/\_layout.js.

```bash package.json
{
  "main": "expo-router/entry"
}

```

- sdk 48

```bash
-package.json
{
  "main": "index.js"
}
-index.js

import 'expo-router/entry';

```

## Modify project configuration

```bash
-app.json
{
  "scheme": "your-app-scheme"
}

```

## If you are developing your app for web, install the following dependencies:

```bash
npx expo install react-native-web react-dom
```

- Then, enable Metro web support by adding the following to your app config:

```bash
-app.json
{
  "web": {
    "bundler": "metro"
        }
}
```

## Modify babel.config.js

### sdk 50 and above

- Ensure you use babel-preset-expo as the preset, in the babel.config.js file or delete the file:

```bash
-bable.config.js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
  };
};
```

- If you're upgrading from a version of Expo Router that is older than v3, remove the plugins: ['expo-router/babel']. expo-router/babel was merged in babel-preset-expo in SDK 50 (Expo Router v3).

## sdk 49 and below

- Add expo-router/babel plugin as the last item in the plugins array to your project's babel.config.js:

```bash
-bable.confing.js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['expo-router/babel'],
  };
};
```

# Clear bundler cache

```bash
npx expo start -c
```

## Install dependencies for web support

```bash
npx expo install react-dom react-native-web
```

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
 content: ['./app/**/*.{js,jsx,ts,tsx}', './components/**/*.{js,jsx,ts,tsx}'],
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
    argv
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
