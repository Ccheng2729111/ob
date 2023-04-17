#react #pendding #Permanent 

在react新版本中[[hooks]] 概念非常重要

在React中，如果在**`useEffect`**的依赖数组中使用一个函数，该函数会在每次渲染时都被创建，可能会导致不必要的重新渲染。为了避免这种情况，可以使用**`useCallback`**来记忆这个函数，以便在依赖项不变的情况下避免重新创建该函数。

使用**`useCallback`**的语法如下：

```
jsxCopy code
const memoizedCallback = useCallback(
  () => {
    // function logic
  },
  [dependencies],
);

```

其中，第一个参数是需要记忆的函数，第二个参数是该函数依赖的变量数组，当依赖项发生变化时，该函数会被重新创建。

以下是一个在**`useEffect`**中使用**`useCallback`**的示例：

```
jsxCopy code
import React, { useState, useEffect, useCallback } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  useEffect(() => {
    console.log('Effect ran');
    increment();
  }, [increment]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

```

在上面的示例中，**`increment`**函数被定义为一个记忆函数，并传递给了**`useEffect`**的依赖项数组中。这样，在**`useEffect`**内部调用**`increment`**时，它不会在每次渲染时被重新创建。

注意，只有在函数的结果会影响到渲染结果的情况下才需要使用**`useCallback`**，否则会造成不必要的代码复杂度。