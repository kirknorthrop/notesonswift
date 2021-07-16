Different State Handlers and a description of how they are used.

`@State` - State should hold the instantiation of a primitive. It's the initial version, the actual variable, not just a reference. So when the view goes away, so will it. It’s where the memory for the variable lives, if you like. 

`@StateObject` - StateObjects are the same as state, but for objects - ie not primitives.

`@Binding` - A binding is a way of passing a `@State` to another view by ref rather than by val.
- This is not just for @ObservableObject properties, it can be used with @State, @AppStorage and @SceneStorage as well

`@ObservedObject` - If you passed a `@StateObject` to another view, then you'd define it as an `@ObservedObject` in that new view. Much like `@State` and `@Binding` you store in `@StateObject` and pass by ref to `@ObservedObject`

`@Published` - Published items exist on items that implement the `ObservableObject` protocol. They'll force an update of a SwiftUI View when they are updated.




@EnvironmentObject:
- This is passed to all children views that access it automatically
- Based on type, meaning you can only pass one object per type (@EnvironmentObject var settings: TimerSettings loads the only TimerSettings object stored in the environment, no need to name it or anything)
- Useful for data that is almost universal (accessed across many child views)
- Can be injected at the first view and accessed as needed without having to pass it again


What @Published actually does:
It basically means "Before changing this property, call objectWillChange.send()".
'cause the way Views know to re-render is by subscribing to on objectWillChange.
