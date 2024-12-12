you should not force yourself to hunt duplicated lines of code.  
  
Although a very simple principle—in principle—DRY is often misinterpreted as the necessity to never repeat the exact same thing twice at all in a project. This is impractical and usually counterproductive, and can lead to forced abstractions, over-thought and -engineered code, and unusual dependencies.  
  
The key isn’t to avoid all repetition, but to normalise and abstract meaningful repetition. If two things happen to share the same declarations coincidentally, then we needn’t DRY anything out; that repetition is purely circumstantial and cannot be shared or abstracted.  
  
[https://cssguidelin.es/#dry](https://cssguidelin.es/#dry)  
  
In short, only DRY code that is actually thematically related. Do not try to reduce purely coincidental repetition: duplication is better than the wrong abstraction.