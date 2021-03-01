# openliberty-maven-plugin-multimodule
Demo case for using liberty maven plugin in cascade projects

## Changes made by scottkurz
1. You originally had the child configuring liberty-maven-plugin via `pluginManagement` and the parent via `plugins`.  
I switched this around to a more typical: parent -> `pluginManagement`, child -> `plugins`.
2. I removed the executions and just used plugin-level configuration
3. I added this attribute to customize the merge behavior:
```xml
 <copyDependencies combine.children="append">
```
along with a `<dependencyGroup>` wrapper to make the merge a bit cleaner.  (You could've done the same customization without the `<dependencyGroup>` and it should work even though the merge is a bit uglier if you look at the effective POM.)

### Unimportant changes
I also reformatted, bumped LMP to 3.3.4 and switched the child to use a Derby dep.. none of which really matters.
