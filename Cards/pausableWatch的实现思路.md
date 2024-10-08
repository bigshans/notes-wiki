#+TAGS: #vue #pausableWatch 

```javascript
import { ref, watch, readonly } from "vue";
export const watchPausable = (
    source,
    callback,
    options
) => {
    const isActive = ref(true);
    const stopWatch = watch(source, (...argv) => {
        if (isActive.value) {
            callback(...argv);
        }
    });
    const resume = () => {
        isActive.value = true;
    };
    const stop = () => {
        stopWatch();
        isActive.value = false;
    };
    return {
        isActive: readonly(isActive),
        resume,
        stop,
        stopWatch,
    };
};
export { watchPausable as pausableWatch };
```