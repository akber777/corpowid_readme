# Corpowid Accessibility Widget

<p align="center">
  <img src="https://www.corpowid.com/themes/corpowid/assets/img/logo.svg" alt="Corpowid Logo" width="200"/>
</p>

A comprehensive accessibility solution for your React Native applications. Provide advanced accessibility features to your users with an easy-to-integrate widget.

## Features

- 🌙 Dark Mode / Light Mode toggle
- 📱 Font size adjustment
- ↔️ Text alignment (left, center, right)
- ↕️ Line height adjustment
- ⇹ Letter spacing control
- 🖼️ Image visibility toggle
- 🎯 Accessible touch areas
- ⌨️ Keyboard-friendly inputs
- 📜 Accessible scroll views
- 🔄 Third-party library support
- 🌐 Text translation with selection
- 📝 Accessible HTML rendering

## Translation Feature

The widget comes with built-in translation capabilities enabled by default. Users can select any text to translate it when the translation feature is active. Developers can disable text selection for specific components when needed:

```jsx
import { AccessibilityText } from '@corpowid/accessibility-widget';

function MyComponent() {
  return (
    <>
      {/* This text can be selected for translation (default behavior) */}
      <AccessibilityText>
        This text can be selected for translation by default
      </AccessibilityText>

      {/* Disable text selection for this component */}
      <AccessibilityText allowSelection={false}>
        This text cannot be selected for translation
      </AccessibilityText>
    </>
  );
}
```

Translation features:
- Text selection is enabled by default when translation is active
- Supports multiple languages
- Developers can disable selection with `allowSelection={false}`
- Customizable selection colors with `selectionColor` and `selectionColorDarkMode` props

Example with custom selection colors:
```jsx
<AccessibilityText 
  selectionColor="#007AFF"
  selectionColorDarkMode="#0A84FF"
>
  Select this text to translate (enabled by default)
</AccessibilityText>
```

## Installation

```bash
npm install @corpowid/accessibility-widget
```

## Basic Usage

1. Wrap your root component with `AccessibilityProvider`:

```jsx
import { AccessibilityProvider } from '@corpowid/accessibility-widget';

export default function App() {
  return (
    <AccessibilityProvider
      apiKey="YOUR_API_KEY_HERE"
    >
      <YourApp />
    </AccessibilityProvider>
  );
}
```

2. Use the accessible components:

```jsx
import {
  AccessibilityText,
  AccessibilityView,
  AccessibilityButton,
  AccessibilityImage,
  AccessibilityTextInput,
  AccessibilityScrollView,
  AccessibilityTouchableOpacity,
  AccessibilityPressable,
  AccessibilityKeyboardAvoiding
} from '@corpowid/accessibility-widget';

export default function MyScreen() {
  return (
    <AccessibilityView>
      <AccessibilityText>Hello World!</AccessibilityText>
    </AccessibilityView>
  );
}
```

## Using Third-Party Components

The `AccessibilityRenderExternal` component provides two ways to integrate third-party components:

### 1. Simple Integration

If your third-party component supports the `style` prop, dark mode will be handled automatically:

```jsx
import { AccessibilityRenderExternal } from '@corpowid/accessibility-widget';
import { ThirdPartyComponent } from 'some-library';

function MyComponent() {
  return (
    <AccessibilityRenderExternal
      renderItem={() => (
        <ThirdPartyComponent
          style={{
            backgroundColor: '#fff', // Will automatically switch in dark mode
            // Other styles...
          }}
        />
      )}
    />
  );
}
```

### 2. Advanced Customization

If your component doesn't support the `style` prop or you need custom dark mode handling, you can use the props provided by renderItem:

```jsx
import { AccessibilityRenderExternal } from '@corpowid/accessibility-widget';
import { ThirdPartyCalendar } from 'some-calendar-library';

function MyCalendar() {
  return (
    <AccessibilityRenderExternal
      renderItem={(props) => (
        <ThirdPartyCalendar
          style={{
            fontSize: props.fontSize || 16,
            textAlign: props.textAlign || 'left',
            letterSpacing: props.letterSpacing || 0,
            lineHeight: props.lineHeight || 20
          }}
          theme={{
            backgroundColor: props.darkMode ? '#000' : '#fff',
            textColor: props.darkMode ? '#fff' : '#000'
          }}
          hideImages={props.hideImages}
          language={props.language}
        />
      )}
    />
  );
}
```

### 3. Third-Party Image Libraries

For third-party image components that need to respect the widget's image visibility settings, use `AccessibilityRenderImageExternal`:

```jsx
import { AccessibilityRenderImageExternal } from '@corpowid/accessibility-widget';
import { ThirdPartyImage } from 'some-image-library';

function MyImage() {
  return (
     <AccessibilityRenderImageExternal>
      <ThirdPartyImage source={{ uri: "https://example.com/image.jpg" }} />
    </AccessibilityRenderImageExternal>
  );
}
```

## Rendering Accessible HTML Content

To ensure accessibility when rendering HTML content, use `AccessibilityRenderHtmlExternal`:

```jsx
import AccessibilityRenderHtmlExternal from '@corpowid/accessibility-widget';
import RenderHtml from 'react-native-render-html';
import { useWindowDimensions } from 'react-native';

export default function MyComponent() {
  const { width } = useWindowDimensions();
  
  return (
    <AccessibilityRenderHtmlExternal>
      <RenderHtml 
        contentWidth={width}
        source={{ html: '<p>This is an accessible HTML paragraph.</p>' }}
      />
    </AccessibilityRenderHtmlExternal>
  );
}
```

This component ensures that HTML content rendered within your app follows accessibility guidelines, including font adjustments, dark mode support, and custom styling.

## License

MIT
