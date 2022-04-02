# React Hooks

I was brushing up few of the hooks online.. here are the notes collected.. 

## Important Hooks

- useState
- useEffect
- useReducer
- useRef
- useContext

### useReducer

useReducer seems little complex.. let me put the code here

```jsx
//declaring
var defaultState = {
	people: [],
	showModel: false,
	modelContent: ""
};
const [state, dispatch] = useReducer(reducer, defaultState);

//dispatching action. always call dispatch to update the state
dispatch({ type: "LOAD_DATA" });

//reducer function - always return a state
const reducer = (state, action) => {
	if (action.type == "LOAD_DATA") {
		return {
			...state,
			people: [...people, newPeople],
			showModel: true,
			modelContent: "Added new person"
		};
	}
}
```

### useContext
Context - is addressing property drilling issue. 

```jsx
const PersonContext = React.CreateContext()
// two components - providers, consumers

//provider
<PersonContext.Provider value={removePerson}>
	<h3>title</h3>
	<listOfPeople />
</PersonContext>
//declare removePerson method here.. 


const ListOfPeople = () = {
	<SinglePerson />
}

//consumer
const SinglePerson = () => {
	let { removePerson } = useContext(PersonContext);

	// use the removePerson method
}
```

### React.Memo
This is used to optimise the multiple re-rendering.. 
If we use React.memo infant of the functional component.. then the property values are memorised and it will only render if it gets changed.. 

It works on the property data..

### useCallback
As like memo call-back stops re-rendering based on the function prop..

```jsx
const addToCart = useCallback(() => {
  setCart(cart + 1);
}, [cart]);

//another scenario
const getProducts = useCallback(async () => {
  const response = await fetch(url);
  const products = await response.json();
  setProducts(products);
  setLoading(false);
}, [url]);
``` 

### useMemo

```jsx
const mostExpensive = useMemo(() => calculateMostExpensive(products), [
  products,
]);

//Old usage
<h1>Most Expensive : ${çalculateMostExpensive(products)}</h1>
// to new
<h1>Most Expensive : ${mostExpensive}</h1>
```

