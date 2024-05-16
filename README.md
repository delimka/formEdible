```markdown
# @delimka/formedible 

The @delimka/formedible library is the practical component of my bachelor's thesis for form validation with basic configuration options.
## Features

- **Flexible Validation Rules**: Support for a wide range of validation rules including required fields, minimum/maximum length, custom regex, and custom logic validation.
- **Asynchronous Validation**: Support for asynchronous validation for fields requiring server-side validation.
- **Group Validation**: Validate fields as a group, allowing for complex validation scenarios like password matching.
- **Custom Error Messages**: Define custom error messages for each validation rule to provide a better user experience.
- **Extensive Configuration Options**: Every aspect of the validation process can be customized to fit your form's requirements.

## Installation

Install @delimka/formedible with npm:

```bash
npm install @delimka/formedible


Or with yarn:

```bash
yarn add @delimka/formedible
```

## Table of Contents
1. [Introduction](#introduction)
2. [Features](#features)
3. [Installation](#installation)
4. [Usage](#usage)
   - [Basic Usage](#basic-usage)
   - [Advanced Usage](#advanced-usage)
5. [Examples](#examples-and-components)
6. [Contributing](#contributing)
7. [License](#license)

## Introduction

The @delimka/formedible library is the practical component of my bachelor's thesis. It leverages React's native hooks to provide an intuitive and declarative way to handle forms without the overhead of additional dependencies.

## Features

### Dynamic Form Handling
FormEdible is built to dynamically manage the state of your forms in React applications. It automates the tedious processes involved in handling form submissions, including the dynamic addition and removal of fields. This makes it ideal for situations where form fields need to change based on user interaction.

### Comprehensive Validation
FormEdible supports a wide range of validations out of the box, including required fields, email formatting, URL validation, phone number formats, and custom regex patterns. Moreover, it provides advanced validations such as conditional validations where the validation rules can depend on the values of other fields in the form.

### Asynchronous Validation
The library allows for asynchronous validation functions, enabling integration with server-side checks (like username availability) without complicating the client-side logic. This feature ensures that your forms can handle complex validation scenarios, providing feedback to users in real-time.

### Customizable Feedback Mechanisms
Developers can customize validation messages and the behavior of the form upon validation events. Callbacks for validation start, success, and error events are provided, allowing fine-grained control over the user experience during form interactions.

### State Management with React Hooks
By leveraging React hooks, FormEdible manages form state efficiently without requiring external state management libraries. This reduces the overhead and keeps your project lighter and faster.

### Extensible and Configurable
Every aspect of FormEdible is designed to be easily configurable. This includes setting initial values, configuring field-specific validations, anddefining how group validations should behave. The library’s API is designed to be extended, allowing developers to add custom functionalities as needed.

### Detailed Features Section

#### 1. Comprehensive Validation

FormEdible supports a wide range of built-in validation types, making it easy to ensure data integrity in your forms. Below is a table describing some type of validation available:

| Validation Type    | Description                                                                   | Example Configuration                          |
|--------------------|-------------------------------------------------------------------------------|------------------------------------------------|
| `isRequired`       | Ensures the field must not be empty.                                          | `{ isRequired: true }`                         |
| `isMinLength`      | Specifies the minimum length for the field's value.                           | `{ isMinLength: 3 }`                           |
| `isMaxLength`      | Specifies the maximum length for the field's value.                           | `{ isMaxLength: 20 }`                          |
| `isEqualTo`        | Requires the field's value to match another specified field's value.          | `{ isEqualTo: 'confirmPassword' }`             |
| `isNotEqual`       | Requires the field's value not to match another specified field's value.      | `{ isNotEqual: 'currentPassword' }`            |
| `isEmail`          | Validates that the field's value conforms to a valid email format.            | `{ isEmail: true }`                            |
| `isPhone`          | Validates that the field's value conforms to a valid phone number format.     | `{ isPhone: true }`                            |
| `isDate`           | Validates that the field's value matches a valid date format (YYYY-MM-DD).    | `{ isDate: true }`                             |
| `isUrl`            | Validates that the field's value is a valid URL.                              | `{ isUrl: true }`                              |
| `customValidate`   | Allows for custom function validations for complex scenarios.                 | `{ customValidate: value => value.startsWith('A') }` |
| `condition`        | Allows conditional validations based on other field values.                   | `{ condition: 'greaterThan', conditionValue: 'age' }` |

These validation types provide the flexibility to handle nearly any data validation requirement your forms may need.

#### 2. Simplified State Management with React Hooks

FormEdible leverages React hooks to simplify state management in forms, eliminating the need for external state management libraries and reducing boilerplate. The table below illustrates how FormEdible streamlines form state management:

| Feature                   | Description                                                                   | Benefits                                                                 |
|---------------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **Hooks-Based Architecture** | Uses React's `useReducer` and `useEffect` for local state management.        | - Reduces the complexity of managing form state.<br>- Integrates easily with existing React applications.                     |
| **Single Source of Truth**  | Maintains form state centrally within the hook, accessible to all components. | - Simplifies debugging and testing.<br>- Ensures consistency across components.                                                |
| **Immutable State Updates** | Utilizes functional updates to ensure state immutability.                     | - Prevents side effects and bugs related to state mutations.<br>- Enhances performance by avoiding unnecessary re-renders.     |
| **Asynchronous Support**    | Supports asynchronous validation and field updates.                           | - Allows for real-time validation against server-side constraints.<br>- Facilitates dynamic form adjustments based on user input. |


## Installation

Installing FormEdible is straightforward and can be done using npm or yarn, depending on your preference. Below are the instructions for both methods:

### Using npm:

Open your terminal and run the following command in your project directory:

```bash
npm install formedible
```

### Using yarn:

If you prefer using yarn, run this command instead:

```bash
yarn add formedible
```

### Peer Dependencies

FormEdible is built on React, so make sure that your project is set up with React 16.8.0 or higher, as it relies on hooks. If React is not yet installed in your project, you can install it via npm or yarn:

```bash
npm install react@^16.8.0 react-dom@^16.8.0
```

or

```bash
yarn add react@^16.8.0 react-dom@^16.8.0
```

### TypeScript Support

FormEdible includes TypeScript definitions out of the box, so there's no need for additional installation steps to use it in a TypeScript project. Just ensure your TypeScript version is compatible.

---
## Usage

FormEdible is designed to be easy to use with intuitive setup steps. Here’s how you can get started:

### Basic Usage

#### Setting Up a Form

To use FormEdible, you need to import the hook from the library and define your form configuration.

1. **Import the useFormedible Hook:**

```jsx
import { useFormedible } from 'formedible';
```

2. **Define the Configuration for Your Form:**

Create a configuration object where keys are the names of the form fields and the values are configuration objects for each field.

```jsx
const formConfig = {
  username: {
    isRequired: true,
    isMinLength: 3,
    isMaxLength: 20,
    messages: {
      isRequired: "Username is required",
      isMinLength: "Username must be at least 3 characters",
      isMaxLength: "Username must be no more than 20 characters"
    }
  },
  email: {
    isRequired: true,
    isEmail: true,
    messages: {
      isRequired: "Email is required",
      isEmail: "Please enter a valid email address"
    }
  }
};
```

3. **Initialize the Form Hook:**

```jsx
const { state, dispatch, validateSingleField, addField, removeField, validateAllFields, trigger } = useFormedible({
  configs: formConfig
});
```

4. **Create the Form Component:**

```jsx
function MyForm() {
  const handleSubmit = async (event) => {
    event.preventDefault();
    const isValid = await trigger();
    if (isValid) {
      console.log("Form data:", state.values);
      // Handle form submission
    } else {
      console.error("Validation errors:", state.errors);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="username"
        value={state.values.username || ''}
        onChange={(e) => dispatch({ type: 'CHANGE', payload: { field: e.target.name, value: e.target.value } })}
        onBlur={() => validateSingleField('username')}
      />
      {state.errors.username && <span>{state.errors.username}</span>}

      <input
        name="email"
        value={state.values.email || ''}
        onChange={(e) => dispatch({ type: 'CHANGE', payload: { field: e.target.name, value: e.target.value } })}
        onBlur={() => validateSingleField('email')}
      />
      {state.errors.email && <span>{state.errors.email}</span>}

      <button type="submit">Submit</button>
    </form>
  );
}
```

### Methods and Functions

Here’s a table describing some of the primary methods and functions provided by FormEdible:

| Method/Function       | Description                                                            |
|-----------------------|------------------------------------------------------------------------|
| `validateSingleField` | Validates a single field based on the provided field name.             |
| `addField`            | Adds a new field dynamically to the form with the specified settings.  |
| `removeField`         | Removes a specified field from the form.                               |
| `validateAllFields`   | Validates all fields in the form at once.                              |
| `trigger`             | Triggers validation for all or specified fields and returns validation results. |

These functions are part of the object returned by the `useFormedible` hook and are essential for managing the form state and validation.

---

### Available Validations Table

Here’s a detailed look at the types of validations you can implement with FormEdible:

| Validation Type    | Description                                                                   | Example Usage                                        |
|--------------------|-------------------------------------------------------------------------------|------------------------------------------------------|
| `isRequired`       | Field must not be empty.                                                      | `{ isRequired: true }`                               |
| `isMinLength`      | Minimum length for the field's value.                                         | `{ isMinLength: 3 }`                                 |
| `isMaxLength`      | Maximum length for the field's value.                                         | `{ isMaxLength: 20 }`                                |
| `isEqualTo`        | The field's value must match another field's value.                           | `{ isEqualTo: 'confirmPassword' }`                   |
| `isNotEqual`       | The field's value must not match another field's value.                       | `{ isNotEqual: 'currentPassword' }`                  |
| `isEmail`          | The field's value must be a valid email format.                               | `{ isEmail: true }`                                  |
| `isPhone`          | The field's value must be a valid phone number format.                        | `{ isPhone: true }`                                  |
| `isDate`           | The field's value must be a valid date format (YYYY-MM-DD).                   | `{ isDate: true }`                                   |
| `isUrl`            | The field's value must be a valid URL format.                                 | `{ isUrl: true }`                                    |
| `customValidate`   | Custom function for complex validations.                                      | `{ customValidate: (value) => value.startsWith('A')}`|
| `condition`        | Apply conditional validation based on another field's value.                  | `{ condition: 'greaterThan', conditionValue: 'age' }`|

Let's detail the functionality of the conditional validation with a table that outlines the different types of conditional validations supported by FormEdible. This table will help you understand how each condition is applied and the expected input and behavior:

### Conditional Validations Table

| Condition Type   | Description                                                         | Required Parameters                      | Example Usage                                   |
|------------------|---------------------------------------------------------------------|------------------------------------------|-------------------------------------------------|
| `greaterThan`    | Ensures the field's value is greater than another field's value.    | `conditionValue`: Field to compare with  | `{ condition: 'greaterThan', conditionValue: 'minimumAge' }` |
| `lessThan`       | Ensures the field's value is less than another field's value.       | `conditionValue`: Field to compare with  | `{ condition: 'lessThan', conditionValue: 'maximumAge' }` |
| `between`        | Ensures the field's value is between two specified values.          | `conditionValue`: [minValue, maxValue]   | `{ condition: 'between', conditionValue: [18, 60] }` |
| `matches`        | Ensures the field's value matches a specified regular expression.   | `conditionValue`: RegExp                 | `{ condition: 'matches', conditionValue: /^[a-zA-Z]+$/ }` |
| `custom`         | Applies a custom function for validation.                           | `conditionValue`: Function               | `{ condition: 'custom', conditionValue: (value) => value.startsWith('A') }` |

Handle more complex validation scenarios where the requirement for a field depends on other fields:

```jsx
const conditionalValidationConfig = {
  discountCode: {
    isRequired: true,
    condition: 'greaterThan',
    conditionValue: 'amount',
    conditionMessage: "Discount only applies for amounts greater than $100"
  }
};
```


## Advanced Usage

### Handling Complex Form Structures

FormEdible is designed to handle complex form structures including nested fields and dynamic sections. This capability makes it especially useful for enterprise-level applications where forms can become highly dynamic and dependent on user data.

#### Dynamic Field Manipulation

You can add or remove fields on the fly based on user interactions, such as adding multiple addresses or contacts in a single form. Here's how you can handle such scenarios:

```jsx
function DynamicForm() {
  const { state, addField, removeField, dispatch } = useFormedible({ configs: initialConfigs });

  const handleAddField = () => {
    addField({
      name: `newField_${new Date().getTime()}`, // Unique name for the field
      isRequired: true,
      messages: { isRequired: "This field is required" }
    });
  };

  const handleRemoveField = (fieldName) => {
    removeField(fieldName);
  };

  // Render logic here
}
```

### Asynchronous Validation with `asyncValidate`

Asynchronous validation (`asyncValidate`) in FormEdible allows you to integrate server-side checks into your form validation process. This feature is crucial for scenarios where validation criteria cannot be confirmed purely through client-side logic, such as checking the availability of a username or email address in your database.

### Concept

The `asyncValidate` function is specified within the field configuration and is executed after all synchronous validations pass. This function should return a promise that resolves to a string (the error message) if validation fails, or `null` if validation succeeds.

### Example Usage

Here's a simple example of how to use `asyncValidate` to check if a username is already taken:

```jsx
const formConfig = {
  username: {
    isRequired: true,
    asyncValidate: async (value) => {
      const response = await fetch(`/api/check-username?username=${encodeURIComponent(value)}`);
      const { isAvailable } = await response.json();
      return isAvailable ? null : "Username is already taken.";
    },
    messages: {
      isRequired: "Username is required"
    }
  }
};

function UsernameForm() {
  const { state, dispatch, trigger } = useFormedible({ configs: formConfig });

  const handleSubmit = async (event) => {
    event.preventDefault();
    const isValid = await trigger();  // This triggers both sync and async validations

    if (isValid) {
      console.log("Username is available and the form is valid!");
    } else {
      console.error("Validation errors:", state.errors);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="username"
        value={state.values.username || ''}
        onChange={(e) => dispatch({ type: 'CHANGE', payload: { field: 'username', value: e.target.value } })}
      />
      {state.errors.username && <span className="error">{state.errors.username}</span>}
      <button type="submit">Check Availability</button>
    </form>
  );
}
```


### Group Validations

Group validations in FormEdible enable you to apply rules across multiple fields, which is useful when the validity of one field depends on values from others. This feature is especially valuable in complex forms requiring coordinated input across several fields.

#### Example Usage

Imagine a form where the user must enter at least one form of contact information, either a phone number or an email address. Here's how you might set up group validations to ensure that at least one of these fields is filled:

```jsx
// Define the form configuration for email and phone
const formConfig = {
  email: {
    isRequired: false,
    isEmail: true,
    messages: {
      isEmail: "Please enter a valid email address"
    }
  },
  phone: {
    isRequired: false,
    isPhone: true,
    messages: {
      isPhone: "Please enter a valid phone number"
    }
  }
};

// Group validation to ensure at least one contact method is provided
function validateContactInfo(values) {
  if (!values.email && !values.phone) {
    return "At least one contact method is required: email or phone.";
  }
  return null;
}

function ContactForm() {
  const { state, dispatch, trigger } = useFormedible({ configs: formConfig });

  const handleSubmit = async (event) => {
    event.preventDefault();
    const isValid = await trigger();  // Triggers individual field validations
    const groupError = validateContactInfo(state.values);  // Check group validation

    if (isValid && !groupError) {
      console.log("Form data:", state.values);
    } else {
      console.error("Validation errors:", state.errors, "Group Error:", groupError);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        name="email"
        placeholder="Email"
        value={state.values.email || ''}
        onChange={(e) => dispatch({ type: 'CHANGE', payload: { field: 'email', value: e.target.value } })}
      />
      <input
        type="tel"
        name="phone"
        placeholder="Phone Number"
        value={state.values.phone || ''}
        onChange={(e) => dispatch({ type: 'CHANGE', payload: { field: 'phone', value: e.target.value } })}
      />
      {groupError && <span className="error">{groupError}</span>}
      <button type="submit">Submit</button>
    </form>
  );
}
```

This example illustrates how to set up a form with group validations using FormEdible, ensuring that users provide necessary contact information by fulfilling at least one of the specified conditions.

### Custom Validation Functions

FormEdible allows you to define custom validation functions, providing flexibility to implement specific validation rules that go beyond standard validation options. These custom functions enable you to add unique constraints tailored to your application's requirements.

#### Implementation

To implement a custom validation function, you define it within the `customValidate` property of your field configuration. The function receives two arguments:
- **value:** The current value of the field being validated.
- **allValues:** An object containing all current values of the form, allowing cross-field validation.

#### Example Usage

In the following example, we implement a custom validation for a username field. The validation rule is that the username should not start with the prefix 'admin', which might be reserved for system-generated accounts or administrators.

```jsx
const formConfig = {
  username: {
    customValidate: (value, allValues) => {
      // Check if the username starts with 'admin'
      if (value.startsWith('admin')) {
        return "Username cannot start with 'admin'.";
      }

      // Optional: Additional complex logic can be implemented here
      // For example, you might want to ensure that the username and email fields are not identical
      if (value === allValues.email) {
        return "Username and email cannot be the same.";
      }

      // Return null if no errors are found
      return null;
    },
    messages: {
      customValidate: "Custom validation failed", // This is an optional default error message if not returned by customValidate function
    }
  }
};
```

#### Key Points

- **Flexibility:** Custom validators can access and perform logic based on the entire form state, not just the field they are associated with.
- **Dynamic Feedback:** These functions can return specific error messages, making it clear to users what adjustments they need to make.
- **Reusability:** Define these functions externally and reuse them across different forms or components within your application to keep your code DRY.


### Available Validations Table

Here’s a detailed look at the types of validations you can implement with FormEdible:

| Validation Type    | Description                                                                   | Example Usage                                        |
|--------------------|-------------------------------------------------------------------------------|------------------------------------------------------|
| `isRequired`       | Field must not be empty.                                                      | `{ isRequired: true }`                               |
| `isMinLength`      | Minimum length for the field's value.                                         | `{ isMinLength: 3 }`                                 |
| `isMaxLength`      | Maximum length for the field's value.                                         | `{ isMaxLength: 20 }`                                |
| `isEqualTo`        | The field's value must match another field's value.                           | `{ isEqualTo: 'confirmPassword' }`                   |
| `isNotEqual`       | The field's value must not match another field's value.                       | `{ isNotEqual: 'currentPassword' }`                  |
| `isEmail`          | The field's value must be a valid email format.                               | `{ isEmail: true }`                                  |
| `isPhone`          | The field's value must be a valid phone number format.                        | `{ isPhone: true }`                                  |
| `isDate`           | The field's value must be a valid date format (YYYY-MM-DD).                   | `{ isDate: true }`                                   |
| `isUrl`            | The field's value must be a valid URL format.                                 | `{ isUrl: true }`                                    |
| `customValidate`   | Custom function for complex validations.                                      | `{ customValidate: (value) => value.startsWith('A')}`|
| `condition`        | Apply conditional validation based on another field's value.                  | `{ condition: 'greaterThan', conditionValue: 'age' }`|



## Examples and components


## Live preview of usage Zod and React-hook-form in comparison with FormEdible
Live preview: https://formedible-react-hook-form-zod.web.app/
