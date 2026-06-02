# React Navigation

Before using we have to set configuration
```bash
# Installing in current project
pnpm add @react-navigation/native
pnpm dlx expo install react-native-screens react-native-safe-area-context

# For stack navigation
pnpm add @react-navigation/native-stack
pnpm add @react-navigation/elements
```
### To use native stack
- The Container `<NavigationContainer>` as root, usually at app.jsx to manage back tracking.
- The Screen `<Stack.Screen>` is route declaration

```jsx
export default function HomeScreen({ navigation, route }) {
  return (
    <Button 
      title="Go to Edit Screen" 
      onPress={() => navigation.navigate('EditNote')} // <-- Used to move
    />
  );
}
```

### To use elements (react navigation)

|Element Component|	What it does|	80/20 Use Case|
| -  | - | - |
|`<Header />`|	A pure React UI component that renders a standard mobile top-navigation header bar.|	You want a header on a screen that isn't inside a Stack Navigator, or you are building a fully custom drawer layout.
|`<HeaderBackButton />`|	The standard back arrow component that handles native platform styles (looks like a chevron on iOS, a straight arrow on Android) |	You are hiding the default header (headerShown: false) to build a completely custom top bar, but you still need a native-looking back arrow that safely calls navigation.goBack().

Note: 
\
Since, expo is not supporting react navigation. So, I am not trying it. 
\ 
I will look into expo-router
\
# Expo Router
- It is built on top of react native screens. 
- file based navigation
- Fast and optimised

## Installation
```bash
pnpm dlx expo install expo-router react-native-safe-area-context react-native-screens expo-linking expo-constants expo-status-bar
```
In package.json to to set src/app/_layout.tsx as entry client
```js
{
  "main": "expo-router/entry"
}
```
For deep linking (opens app directly for `instagram://profile`) and typed routes (avoids not available links)
```js
{
  "expo": {
    "scheme": "your-app-scheme",
    "experiments": {
      "typedRoutes": true
    }
  }
}
```

For using aliases instead of relative paths -
short import paths like `@/components/button`
`@` maps to `src/`

```js
{
  "extends": "expo/tsconfig.base",
  "compilerOptions": {
    "strict": true,
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["**/*.ts", "**/*.tsx", ".expo/types/**/*.ts", "expo-env.d.ts"]
}
```

## Some Important rules to follow

1. All screens/pages are files inside the src/app directory
2. All pages have a URL
3. First index.tsx is the initial route
4. Root _layout.tsx replaces App.jsx/tsx
5. Default template uses platform-specific tabs
6. Non-navigation components live outside the src/app directory (components, hooks etc)
7. Customizing [stack](https://docs.expo.dev/router/advanced/stack/ "Full Information") and [tab navigators](https://docs.expo.dev/router/advanced/tabs/ "Full Description")

### Static and Dynamic Routes
In file based routing, dynamic routes can be created using brackets.
\
[Direct Best link](https://docs.expo.dev/router/basics/notation/)
to understand

## Initiate routing
### Stacks
In every `app/` there is `index.tsx` which is page and `_layout.tsx` which acts as master component to wait till home is loaded.
<details>
<summary> An example </summary>

```jsx
import { useFonts } from 'expo-font';
import { Stack } from 'expo-router';
import * as SplashScreen from 'expo-splash-screen';
import { useEffect } from 'react';

SplashScreen.preventAutoHideAsync();

export default function RootLayout() {
  const [loaded] = useFonts({
    SpaceMono: require('@/assets/fonts/SpaceMono-Regular.ttf'),
  });

  useEffect(() => {
    if (loaded) {
      SplashScreen.hide();
    }
  }, [loaded]);

  if (!loaded) {
    return null;
  }
    // when everything loaded return stack
  return <Stack />;
}
```

</details>

### Tabs
Tab routing can be done with file based routing using `app/(tabs)/_layout.jsx`
```
app/
├── _layout.jsx        <-- (The Root Layout file you showed earlier)
├── index.jsx          <-- (Main landing index file)
└── (tabs)/            <-- Parent folder with parentheses
    ├── _layout.jsx    <-- Uses the Standard <Tabs /> code from Option 1 above
    ├── index.jsx      <-- The screen file for Tab 1 (e.g., your Note List)
    └── settings.jsx   <-- The screen file for Tab 2

```
<details>
<summary>
Simple tabs
</summary>

```jsx
// In (tabs)/_layout.tsx
import { Tabs } from 'expo-router';
import { Ionicons } from '@expo/vector-icons';

export default function TabLayout() {
  return (
    <Tabs screenOptions={{ headerShown: false }}>
      <Tabs.Screen 
        name="index" 
        options={{
          title: 'Home',
          tabBarIcon: ({ color }) => <Ionicons name="home" size={24} color={color} />,
        }} 
      />
      <Tabs.Screen 
        name="settings" 
        options={{
          title: 'Settings',
          tabBarIcon: ({ color }) => <Ionicons name="settings" size={24} color={color} />,
        }} 
      />
    </Tabs>
  );
}
```
</details>