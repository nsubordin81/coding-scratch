# CLaude's teachings

## React Three Fiber and React in general

React's Declarative Model vs. Imperative Animation
React's Declarative Model
React uses a declarative programming paradigm, which means:

You describe what you want, not how to achieve it
UI is a function of state - UI = f(state)
React handles the updates by comparing the desired UI with the current UI
In a truly declarative approach:

You define the UI structure
When state changes, React reconciles the difference
You don't directly manipulate DOM elements
For example, in React you would write:

Here you're declaring what the UI should look like for any given state value, rather than imperatively manipulating DOM elements.

Why Animation Frames Don't Fit Well
Animation frames and physics updates pose several challenges to the declarative model:

1. Continuous Updates Outside React's Flow
   Animation frames occur at ~60fps, independently of React's render cycles. React's reconciliation process isn't designed to run at animation speeds. If you tried to update state 60 times per second:

You'd trigger 60 render cycles per second
The reconciliation overhead would be substantial
You might miss frames due to React's batching 2. Direct Object Manipulation
Physics engines and 3D libraries like Three.js have their own object models that need direct manipulation:

Trying to make this declarative would mean:

Problems with the declarative approach here:

The rotation needs to be continuously updated every frame
Physics engines need to know the delta/change each frame, not just the end state
The physics engine has its own update loop and state 3. Performance Considerations
For high-performance animations and physics:

Bypassing React's reconciliation process is necessary
Direct object manipulation is much faster
Some operations (like matrix calculations) would be inefficient to express declaratively 4. Timing and Synchronization
Animation often depends on precise timing:

Frame-to-frame deltas are important
Physics simulations require synchronized updates
Animation sequences need to be coordinated
This timing coordination is difficult to express purely with declarative state updates.

The Ref Solution
This is why React provides refs as an "escape hatch" from the declarative model. With refs:

You maintain React's component structure
You get direct access to the underlying object instances
You can manipulate those instances imperatively in animation loops
You avoid unnecessary reconciliation for frame-by-frame updates
In your specific code:

This is the perfect compromise - React handles the component structure and lifecycle, while the ref gives you the imperative control needed for smooth animation and physics integration.
