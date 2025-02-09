# Screen Object Model

- Popular design pattern, helps us to reduce code duplication & improves test maintenance
- Extract page information in separate file
- Advantages
  - Code separation
  - Single source of repository
  - Readability
- Setting up screen object
  - Store selectors
  - Create screen helper functions

```js
class AddNoteScreen {
  get theSkipButton() {
    return $(
      '//*[@resource-id="com.socialnmobile.dictapps.notepad.color.note:id/btn_start_skip"]'
    );
  }
}

module.exports = new AddNoteScreen();
//es6 way with babel- export default new AddNoteScreen();

// to call it in test
//import it
// with Babel - import AddNoteScreen from "../screenobjects/android/add-note.screen";
// without Babel - const AddNoteScreen = require("../screenobjects/android/add-note.screen");
//call function then selector

await addNoteScreen.skipBtn;
```