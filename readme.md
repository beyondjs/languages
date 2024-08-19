# `beyond-js/languages`

This package provides a reactive system for managing the current language in a multilingual application. It handles
language detection, setting, and change events, making it easy to integrate language configuration into your project.

## Features

-   Reactive language management.
-   Supports custom default and supported languages.
-   Automatically detects and sets language based on the device’s settings or previously configured values.
-   Persistence using `localStorage` for language preference.
-   Built-in event system to react to language changes.

## Installation

Install the package using npm or yarn:

```bash
npm install beyond-js/languages
```

or

```bash
yarn add beyond-js/languages
```

## Usage

### Initializing the Language Manager

The language management system is initialized automatically when you create an instance of the `Languages` class. The
class fetches the language configuration from your project’s configuration file.

```typescript
import { languages } from 'beyond-js/languages';

// Wait until the language configuration is ready
await languages.ready;

// Access the current language
console.log(languages.current);
```

### Configuration

The `Languages` class reads language specifications from a configuration file in your project. The configuration should
define the default language and the supported languages:

```json
{
	"languages": {
		"default": "en",
		"supported": ["en", "es", "fr", "de"]
	}
}
```

### Language Properties

-   **`languages.current`**: Returns the currently selected language.
-   **`languages.default`**: Returns the default language specified in the configuration.
-   **`languages.supported`**: Returns a set of supported languages.
-   **`languages.ready`**: A promise that resolves when the configuration is loaded.
-   **`languages.fetched`**: Indicates if the configuration has been fetched.

### Setting the Current Language

You can change the current language using the following code:

```typescript
languages.current = 'es'; // Change the language to Spanish
```

### Handling Language Change Events

The package uses an event system that allows you to listen to changes in the language setting:

```typescript
languages.on('change', () => {
	console.log('Language has been changed to:', languages.current);
});
```

## API Reference

### `Languages` Class

#### Properties

-   **`current: string`**  
    Gets or sets the current language.

-   **`default: string`**  
    The default language specified in the configuration.

-   **`supported: Set<string>`**  
    The set of supported languages.

-   **`ready: Promise<void>`**  
    A promise that resolves when the language configuration is ready.

-   **`fetched: boolean`**  
    Indicates whether the configuration has been fetched.

#### Methods

-   **`on(event: string, callback: () => void): void`**  
    Registers an event listener for language change events.

## Example

```typescript
import { languages } from 'beyond-js/languages';

async function initialize() {
	await languages.ready;

	console.log('Current language:', languages.current);

	languages.on('change', () => {
		console.log('Language changed to:', languages.current);
	});

	languages.current = 'fr'; // Change language to French
}

initialize();
```

## License

This package is licensed under the MIT License.
