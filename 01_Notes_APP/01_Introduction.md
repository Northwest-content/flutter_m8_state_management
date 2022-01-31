## Notes APP

In this example, we will create a note app. First, we will create this app by using the regular way that we learned before which is the **setState** way, and later we will learn how to use the **riverpod** state management.

![118641025-4463b400-b79f-11eb-86b6-710b39e55993](https://user-images.githubusercontent.com/8784343/151873677-ddf6d9e2-f771-4e87-a8ae-b2743ab154a9.png)

We will learn how to use:

- **insert** & **removeAt** list methods
- **SingleChildScrollView** widget
- **Riverpod** state management.
- **FloatingActionButton** widget

1. Download the [starter project from GitHub](https://github.com/Northwest-content/flutter_notes_app_starter), then open the project by using the VS Code, and get the packages.

2. Inside the project, we will have three folders,
   1. **`models`**, inside this folder we created a **`Note`** model, and it has two values; **`title`** value & **`body`** value.
   2. **`widgets`**, inside this folder, we created a note list tile, and we will use it later to display the note details.
3. Inside the **`Pages`** folder, you will find two pages that you will use in the note app.
   1. **`home_page.dart`**, here you will find the user interface for the home screen.
   2. **`note_page.dart`**, here we will display the note details.
