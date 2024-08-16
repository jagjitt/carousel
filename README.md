# carousel


## Complexities of CSS transitions
CSS transitions which involve removal of the animated elements at the end can be quite tricky to implement well. The element needs to stay in the DOM for the duration of the transition, then be removed. Removing the element typically requires JavaScript intervention. You need to coordinate the CSS transition duration with the JavaScript timing for element removal, which can lead to synchronization issues.

If a transition is cancelled or interrupted (e.g., by quickly toggling a state), you need to handle these cases gracefully, potentially removing the element immediately or reverting to a different state.

Determining how to handle events on elements that are transitioning out can be tricky. Should they still be interactive? How do you prevent unintended interactions?

It is hard to build transitions that involve entering and leaving the DOM when using declarative UI frameworks because these frameworks render based the UI on the current state. Transitions usually involve displaying both current and new states at the same time, which means your UI code has to include both current + new state values and include the logic for transitioning between them correctly and with the right timing. These can be quite complex to implement correctly after accounting for the scenarios listed above.

## How to transition
Since the current and new images do not affect DOM layout, the CSS transform property is a perfect choice for transitioning because of:

GPU acceleration: Many browsers can offload transform operations to the GPU, resulting in smoother animations and better overall performance.
Reduced repaints: CSS transforms don't trigger repaints of the entire page layout, unlike changes to properties like like left and margin.
Assuming we're transitioning from the first image to the second image, the transition can be executed as such:

The current image is the default state and starts without any CSS transforms. It ends with transform: transformX(-100%) (displaced to the left, hidden out of view).
The next image starts with a CSS transform of transform: transformX(100%) (displaced to the right, hidden out of view). It ends without any CSS transforms since it is meant to end with the default state and replace the current image.

## Accessibility (A11y)
All images should have alt text that describes the image to support accessibility. It will be read out loud by screen readers and is also used by search engines.
Add appropriate aria-labels to the buttons since the buttons do not have visible labels.
