# State management
In javascript, the data is stored in **memory phase** on runtime. 
\
When the scope is deleted or the app reloads, everything vanish.
\
In React, the data is stored in variables, but react depends on **rerender** and **reconciliation**. Storing data in variables and updating it with javascript doesn't rerender, so to trigger re-render, there are **hooks** and we store variables in **state** on runtime.
### Single source of truth

Now the problem arises when *we unmount the component, the state vanishes*. So to avoid this problem, data is passed to central component which act as a single source of truth. Every component which requires the specific data, it will define props and update the data in central component.
```jsx
import React, { useState } from 'react';
import ChildComponent from './ChildComponent';

function App() {
  // Central State
  const [user, setUser] = useState({ name: 'Alice', role: 'Admin' });

  // Function to update central state
  const updateUserRole = (newRole) => {
    setUser({ ...user, role: newRole });
  };

  return (
    <div style={{ padding: '20px' }}>
      <h1>Central App</h1>
      <p>Current User: {user.name} ({user.role})</p>
      <hr />
      {/* Passing state and updater function as props */}
      <ChildComponent user={user} onRoleChange={updateUserRole} />
    </div>
  );
}

export default App;

// Child Component =========
import React from 'react';

function ChildComponent({ user, onRoleChange }) {
  return (
    <div style={{ border: '1px solid #ccc', padding: '15px' }}>
      <h3>Child Component</h3>
      <p>Received Prop: {user.name} is an {user.role}</p>
      
      {/* Triggering the central update via the passed function */}
      <button onClick={() => onRoleChange('Editor')}>
        Change Role to Editor
      </button>
    </div>
  );
}

export default ChildComponent;
```

Now, we have some problems ;
1. Prop Drilling
- Even if a very small, deeply nested component need a state, app has to provide state with update function to child, grand-child, and so on.
2. Unnecessary Re-renders
- when central state updates, every child down the line re-renders
3. Violation of Single Responsibility & Tight Coupling
- It requires specific props structure and callbacks
4. Hard to debug

