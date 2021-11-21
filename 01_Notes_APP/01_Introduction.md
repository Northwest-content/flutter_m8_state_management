# Notes APP

In this example, we will create a note app. First, we will create this app by using the regular way that we learned before which is the **setState** way, and later we will learn how to use the **riverpod** state management.

![screenshot](https://lh4.googleusercontent.com/EAvD9sEoDIgIxq0XwnPAWS_ZWmgkQLYlUZoWqsKTre2p33DrCOny9LPg3fyBsK7uLSd6nHPZtQyA8SgVv7woM6D7SsLhVpu5TR8u8yWltfaSgVcrYueOKgEwqf7sf4uSi97vnvTa)

We will learn how to use:

    - **insert** & **removeAt** list methods
    - **SingleChildScrollView** widget
    - **Riverpod** state management.
    - **FloatingActionButton** widget

1. Download the starter project from GitHub, then open the project by using the VS Code, and get the packages.

> https://github.com/Northwest-content/flutter_notes_app_starter

2. Inside the project, we will have three folders,
   1. **models**, inside this folder we created a **Note** model, and it has two values; **title** value & **body** value.
   2. **widgets**, inside this folder, we created a note list tile, and we will use it later to display the note details.
3. Inside the **Pages** folder, you will find two pages that you will use in the note app.
   1. **home_page.dart**, here you will find the user interface for the home screen.
   2. **note_page.dart**, here we will display the note details.
