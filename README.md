# REACT CONTEXT API

The easiest way to create and consume context through your react application

Quick start:

```
$ yarn # npm install
$ yarn # npm start
````
## Steps

1. Create your app context

```javascript
	import React, {useState} from "react"
	const ThemeContext = React.createContext()
```
2. Create  functional component

```javascript
	function ThemeContextProvider(props){
		const [theme, setTheme] = useState("dark")
		
		function toggleTheme(){
			setTheme(theme => theme === "dark"? "light": "dark")
		}
		
		return(
			<ThemeContext.Provider value={{theme, toggleTheme}}>
				{props.children}
			</ThemeContext.Provider>
		)
	}
```
3. Named export The context and the function you created

```javascript
	export {ThemeContextProvider, ThemeContext}
```
4. Make the highest component the Provider 

```javascript

	import React from "react"
	import ReactDOM from "react-dom"

	import App from "./App"
	import {ThemeContextProvider} from "./themeContext"

	ReactDOM.render(
		<ThemeContextProvider>
			<App />
		</ThemeContextProvider>, 
		document.getElementById("root")
		)
```
5. Start consuming the context values( you exported) anywhere in your app using **useContext**

```javascript
		import React, {useContext} from "react"
		import {ThemeContext} from "./themeContext"

		function Header(props) {
		const {theme} = useContext(ThemeContext)
			return (
				<header className={`${theme}-theme`}>
					<h2>{theme === "light" ? "Light" : "Dark"} Theme</h2>
				</header>
			)    
		}

		export default Header
	```
```javascript
	import React, {useContext} from "react"
	import {ThemeContext} from "./themeContext"

	function Button(props) {
		const {theme, toggleTheme} = useContext(ThemeContext)
		return (
			<button 
				onClick={toggleTheme} 
				className={`${theme}-theme`}
			>
				Switch Theme
			</button>
			)    
		}

	export default Button
```

6. An now your components are using **Context API**
```javascript
	import React from "react"

	import Header from "./Header"
	import Button from "./Button"

	function App() {
		return (
			<div>
				<Header />
				<Button />
			</div>
		)
	}

	export default App
```




> Happy Coding!
