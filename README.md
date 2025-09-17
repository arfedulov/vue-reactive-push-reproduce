# vue-reactive-push-reproduce

For reproducing go through the following steps:
```
npm i
npm run dev
```
- Look at "example with ref()".
- Click (1) button
- See that item was added (that's correct)
- Click (2) button
- See that item was added and there is no warnings (that's incorrect, because the array is readonly)
- Click (3) button
- See that item was not added and there is a warning in console "Set operation on key "items" failed: target is readonly" (that's correct)

So, the problem is that an object wrapped in `readonly()` stays mutable by `Array.prototype.push()` call on its property.
This is only the case when we create object like this `readonly({ myArray: ref([]) })`. There is no problem if we create object
like this `readonly(reactive({ myArray: [] }))`, as you can see in "example with reactive()".

My expectation is that the array always stays immutable when wrapped in `readonly()`.