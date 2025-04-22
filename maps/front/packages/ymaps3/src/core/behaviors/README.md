All behaviors of the map is fully separate modules. It handles DOM events on html element of the map and changes map state accordingly.
Map exposes wide range of APIs to manipulate with it's state. You can freely use any getters in your behavior. Setters could be used for single-time changes. For continuous changing of map state, it's highly recommended to use `animate` and `animateForDuration` methods. In this case state changes will be synchronized with internal rendering loop (and browser RAF).
This two methods allows several behaviors to run together. So, state of the map could be changed by other behaviors in between steps. Please consider this while using animate. E.g. it could be a good idea to compute delta of map state that should be done on current step, then apply it to fresh state, instead of overriding map state by some pre-calculated absolute values.

Notes:
Currently map drag behavior uses absolute positioning. On 'dragStart' we find world point where mouse is, and then during the drag we keep cursor in that point.
It's also possible to use mouse offset for dragging. But in this case finding correct zoom point (for zoom) become more tricky:

- While dragging we shall use pointer position which was used for last dragging.
- While NOT dragging - use current pointer position.
  While using drag offset seems to be more correct, using absolute positioning allows us to get more stable behavior on drag and to get rid of additional component that is required for syncing mouse position between drag and zoom behaviors.
