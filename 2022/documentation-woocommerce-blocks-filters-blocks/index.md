---
title: "Documentation: Woocommerce-Blocks Filters Blocks"
date: "2022-10-09"
---

**useCollection:** Appears to be a base hook. Which appears to be coming from [this file](http://assets/js/base/context/hooks/collections/use-collection.ts). Described as a hook for wiring up a component to a collection route. "Queries are performed using useCollection hooks"

**useQueryStateByContext**: A custom hook that exposes the current query state and a setter for the query state store for the given context. "Query State" is a wp.data store that keeps track of an arbitrary object of query keys and their values.

**displayedOptions**: Current state of useState(?) which is being modified by setDisplayedOptions

**setDisplayedOptions**: A function which fills in the "dummy/Lorem Ipsum" data of the default value of displayedOptions which uses a useState hook to instantiate the variable. Takes in the parameter 'newOptions'.

**useEffect**: A hook which acts as a Side Effect. Takes in two parameters, the first is a function, the second is an array. In the array is a list of values/vars that if the state changes of the value/var the useEffect hook is ran. Also, if the array of the 2nd param is empty it effectively acts as a onMount hook.

**useCallback**: Only recreates the function of the const when the value of one of the array of dependencies changes. useCallback is most useful for speedy function creation or "referential equality".
