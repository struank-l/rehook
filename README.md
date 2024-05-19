<div align='center'><img src="./src/assets/icon.png"/></div>

<h3 align='center'>Copy, Paste & Customize your hook.</h3>
<h4 align='center'><a href="https://github.com/alamenai/rehook/tree/main/src/hooks" target="_blank" >Browse hooks</a></h4>

# What is Rehook?

A collection of **custom** and **reusable** hooks designed to streamline your development process by eliminating the need to repeatedly implement the same hooks across different projects. With Rehook, all it takes is a simple **copy**, **paste**, and **customize** the code based on your needs.

<b>It's not a library or a package to install.</b>

## FAQ

<details>
  <summary>Why it's not a library or a package?</summary>
    <br/>
  <p>I mean you do not install it as a dependency. It is not available or distributed via npm.
    <a href="https://github.com/alamenai/rehook/tree/main/src/hooks" target="_blank" >Pick the hook </a> you need. Copy and paste the code into your project and customize it based on your needs. The code is yours.</p>
     The idea behind this is to give you ownership and control over the code, allowing you to change, remove or add more code.
</details>

<details>
  <summary>Do you plan to publish it as npm package?</summary>
    <br/>
  <p>No. I have no plans to publish it as an npm package.</p>
</details>

<details>
  <summary>Which frameworks are supported</summary>
    <br/>
  <p>I would say any framework that supports React.</p>
</details>

<details>
  <summary>How can I add it to my project?</summary>
    <br/>
  <p>This project is written in TypeScript. I recommend using TypeScript for your projects as well. Create a folder named <code>hooks</code> inside your project and pick a hook from this <a href='https://github.com/alamenai/rehook/tree/main/src/hooks'>list</a> that solves your problem, then import it inside your component. That's it!</p>
</details>

# Hooks

## 1. Use Cookie

Use Cookie allows you to manage the web cookies.

### Add hook

2. Create a file `use-cookie.ts` and copy & paste the code from [use-cookie](https://github.com/alamenai/rehook/blob/main/src/hooks/use-cookie.ts).

### Usage

#### Add new cookie

```jsx
import './App.css'
import { getCookie, setCookie } from './hooks/use-cookie'

function App() {
    const addCookie = (key: string, value: string, options: any) => {
        setCookie('pass-key', 'xyz', options)
    }

    return (
        <div style={{ display: 'flex', gap: 10 }}>
            <button onClick={addCookie('pass-key', 'xyz', {})}>Add Cookie</button>
        </div>
    )
}

export default App

```

![image](https://github.com/alamenai/rehook/assets/20143684/dc7b3c1e-5d1f-4ea4-9af0-b764653b1017)

#### Get a cookie

```jsx
import './App.css'
import { getCookie } from './hooks/use-cookie'

function App() {
    const logCookie = (key: string) => () => {
        const cookie = getCookie(key)
        console.log(cookie) // output: xyz
    }

    return (
        <div style={{ display: 'flex', gap: 10 }}>
            <button onClick={logCookie('pass-key')}>Log Cookie</button>
        </div>
    )
}

export default App


```

#### API

##### `setCookie`

**Desscription**

**Type**

Function

**Parameters**

-   `key`:_string_
-   `value`:_string_
-   `options`:_CookieOptions_

## 2. Use Unsaved Form Changes

The useUnsavedFormChanges hook is a custom React hook designed to track unsaved changes in a form. It provides functionalities to monitor changes made to form data and alert users if they attempt to leave the page without saving.

### Add hook

2. Create a file `use-usaved-form-changes.ts` and copy & paste the code from [use-unsaved-form-changes](https://github.com/alamenai/rehook/blob/main/src/hooks/use-unsaved-form-changes.ts).

### Usage

#### Track unsaved changes

```jsx

import { useUnsavedFormChanges } from './hooks/use-unsaved-form-changes'
import { useState, SyntheticEvent } from 'react'

function App() {
    const [formData, setFormData] = useState('') // Assuming your form data is stored in state
    const { setFormChanged } = useUnsavedFormChanges()

    const handleChange = (event: SyntheticEvent<HTMLInputElement>) => {
        // Update form data and mark as changed
        setFormData(event.currentTarget.value)
        setFormChanged(true)
    }

    return (
        <div style={{ display: 'flex', flexDirection: 'column', marginLeft: 900, gap: 10, fontSize: 24 }}>
            <input
                type="text"
                name="example"
                value={formData}
                onChange={handleChange}
                style={{ height: 44, width: 280, fontSize: 18, paddingInline: 12 }}
            />
            <button>Save</button>
        </div>
    )
}

export default App

```

##### `setFormChanged(newValue: boolean): void`

**Desscription**

The `setFormChanged` function is a part of the custom hook useUnsavedFormChanges. It is responsible for updating the state to indicate whether the form has been changed or not.

When invoked with a boolean value (true or false), it updates the internal state accordingly, reflecting whether changes have been made to the form data.

**Parameters**

`newValue (boolean)`: The new value indicating whether the form has been changed (true) or not (false).

**Returns**

`void`: This function does not return any value.

##### `isFormChanged: booleand`

**Desscription**

The `isFormChanged` variable is a part of the custom hook useUnsavedFormChanges. It represents whether the form has been changed or not. When the form data is modified, this variable is updated accordingly to indicate that changes have been made.

**Returns**

`boolean`: The current state of whether the form has been changed. If changes have been made to the form data, it returns true; otherwise, it returns false.

## 3.  useQueryParams

This custom hook provides functionalities for managing query parameters in the URL.


### Add hook

2. Create a file `use-query-params.ts` and copy & paste the code from [useQueryParams](https://github.com/alamenai/rehook/blob/main/src/hooks/use-query-params.ts).

### Usage

```tsx

import { useQueryParams } from './hooks/use-query-params'
import { useEffect, useState } from 'react'

function App() {
    const { urlParams, set, setEncoded } = useQueryParams()
    const [name, setName] = useState('')
    const [age, setAge] = useState('')
    const [profession, setProfession] = useState('')
    const [country, setCountry] = useState('')

    useEffect(() => {
        setName(urlParams.get('name') || '')
        setAge(urlParams.get('age') || '')
        setProfession(urlParams.get('profession') || '')
        setCountry(urlParams.get('country') || '')
    }, [urlParams])

    const handleSetParams = () => {
        set('name', 'alaeddine')
        set('age', 30)
    }

    const handleSetEncodedParams = () => {
        const person = { profession: 'engineer', country: 'Algeria' }
        setEncoded(person)
    }

    return (
        <div style={{ display: 'flex', flexDirection: 'column', alignItems: 'center', marginLeft: 200 }}>
            <div style={{ display: 'flex', flexDirection: 'column', gap: 20 }}>
                <button onClick={handleSetParams}>Set Params</button>
                <button onClick={handleSetEncodedParams}>Set Encoded Params</button>
            </div>
            <p>Name: {name}</p>
            <p>Age: {age}</p>
            <p>Profession: {profession}</p>
            <p>Country: {country}</p>
        </div>
    )
}

export default App

```
### API

**Rertuns**

`get(param: string)`: `string | undefined`

##### Description

Retrieves the value of a specific query parameter from the URL.

##### Parameters

`param (string)`: The name of the query parameter to retrieve.

##### Returns

`string | undefined`: The value of the specified query parameter if found; otherwise, undefined.

**Returns**

`getAll(): Map<string, string>`

##### Description

Retrieves all query parameters from the URL as a map.

##### Returns

`Map<string, string>:` A map containing all query parameters, where the keys are parameter names and the values are parameter values.
`set(key: string, value:` string | number): void

###### Description

Sets a query parameter in the URL to the specified value.

###### Parameters

`key (string)`: The name of the query parameter to set.
`value (string | number)`: The value to set for the query parameter.

**Returns**

`setEncoded(obj: { [s: string]: string | number } | ArrayLike<string>): void`: This function does not return any value.

###### Description

Sets multiple query parameters in the URL based on the provided object or array.

###### Parameters

`obj ({ [s: string]: string | number } | ArrayLike<string>)`: An object or array containing key-value pairs of query parameters to set.

#### Returns

`void`: This function does not return any value.
