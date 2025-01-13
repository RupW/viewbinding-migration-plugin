# viewbinding-migration-plugin
A Plugin for Android Studio to help with migrating from synthetic properties to ViewBinding.

## Installation
- Download *.jar from latest release.
- In Android Studio: Preferences > Plugins > Install Plugin from Disk.

## Usage
- Invoke the Rename Variables for ViewBinding action inside of any Kotlin file.
- The kotlin synthetic import statements should still be present before using.
- Usage inside files that are already using ViewBinding is possible, but pointless.
<img width="574" alt="Screenshot 2022-11-25 at 11 38 55 copy" src="https://user-images.githubusercontent.com/110387111/204012928-2097d56a-8436-42fc-8d23-4df042004895.png">
<img width="593" alt="Screenshot 2022-11-25 at 10 39 23" src="https://user-images.githubusercontent.com/110387111/204012932-2aa8b4e1-791a-44ee-bddd-7a4ca876fb94.png">

## Known Issues
- Current build is compatible with Android Studio Iguana only, and not above.
- Does not match properties referenced as `this.propertyName` or `view.propertyName`.
- Does not match properties in switch expression result clauses, i.e.
  ```kotlin
      private fun getTextField(field: FormFieldEnum): TextInputLayout {
        return when (field) {
            FormFieldEnum.FIRST_NAME -> firstName /* not matched */
  ```
- After a successful rename, the IDE will be left with "Val cannot be reassigned" errors.
  - This looks like an IntelliJ issue - it persists even after reloading.
- I have examples where it has lost the first fragment of a snake-case name :-/

## Notes
- Synthetic properties work when called on a super-view. These must be manually wired up to the correct child view 
  binding (once it's been identified).
- This includes included views that don't have an ID. View binding will not generate properties for these until 
  you add an ID.
