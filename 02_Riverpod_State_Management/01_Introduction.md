# **Riverpod** State Management

To learn state management and see how it works for yourself, you will continue working with the previous project. Before we start!

What do the terms **state** and **state management** mean?

- **State** is when a widget is active and has its data in memory.
- **State management** is, as the name implies, how you manage the state of your widgets and app.

Why do we need state management?

- Sometimes you need to share and pass the data (State) of the application between screens, and we used the constructor way to pass these data; the old approach is good when we have a few screens, but if you have many screens, and you want to pass the data between them, it will be complicated, so the **Riverpod** package will help us facilitate this matter.
- It will help to keep your code well-structured, so your code will become easy to read and maintain.

1. Download the old project from GitHub, then open the project by using the VS Code, and get the packages

> https://github.com/Northwest-content/flutter_notes_app/tree/main/notes_app

2. Get the packages

3. Go to the **pubspec.yaml** file

4. Add **flutter_riverpod** package, down **dependencies**, and don’t forget to get the packages again.

   ```yaml
   flutter_riverpod: ^0.14.0+3
   ```

5. Go to the **main.dart** file, import the **flutter_riverpod** package

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';
```

6. Replace the **void main** function with this,

```dart
void main() {
  runApp(ProviderScope(
    child: MyApp(),
  ));
}
```

7. If we want to build a large and scalable application, a good practice is to separate the logic from the interface design. So, we are going to create a folder called "**providers**", and this folder will contain the files that are responsible for the app logic.

​ So, in the **lib** folder, create a new folder, and name it “**providers**”

![screenshot](https://lh3.googleusercontent.com/7L9CGiSic-kMyLUdwJDsoirvZLazTh_7O9k68pIJ7mtLr2tc9qKKAlblvkYnC95csBXbMrnVIaz-OEu1hPYLPYHbsUnr-03SZSNma3liqNz7QBJFmHucSrV-Dv-ZfWXofyCca0xl)

8. Before we create a file that is responsible for the logic inside the **providers** folder, let's first figure out where the logic in our app is right now.

![screenshot](https://lh4.googleusercontent.com/eUjukQxmaBESf-CA_VmTNEJAc9D-Ppd5RpctRoWQLOTnTDm2yNBR4TdhaZvrMjv2ISgZ77u55Ja8iUMos7O-cD_UadiymORDR4Jg6Kxj4b1GrbtoSAEcvzqEy9AGoTXmpNYWxNhu)

You will find the logic we developed before is in the **home_page.dart** file, under the **\_HomePageState**. Also, under the **build** method, we have the interface design inside the widget tree.

9. As we said before it is good practice to separate the logic from the interface design, so we will create a new file inside the **providers** folder, and call it **note_provider.dart**

10. Inside the **note_provider.dart** file, create a new class, and name it **NoteProvider**. Also, extends the **ChangeNotifier** class.

```dart
class NoteProvider extends ChangeNotifier {

}
```

11. Because we used the **ChangeNotifier** class, we have to import the **flutter/material.dart** file.

```dart
import 'package:flutter/material.dart';
```

12. Then we are going to take the logic that we developed, and paste it inside the **NoteProvider** class.

Inside the **home_page.dart**, cut the logic, and paste it inside the **NoteProvider** class.

![screenshot](https://lh5.googleusercontent.com/yPb_FTtGX7F8nrAAldRmMOKq4OG0vo333f8YmOYZXtGjkbzsNdxVI1XYdVHEqq5Luv2rYau3AfwsyN7sh7af2KCacrsjCwMLui6GLftqfhNbNQ9kFzgBzqO2nJ9LzQMyW6quXFPH)

> **Note:** an errors will appear in the code, but do not worry we will solve these problems

13. Since we use the **Note** class, to create an object inside the **addNote** function, we need to import its file.

```dart
import '../models/note.dart';
```

14. With the old approach, we needed to call the **setState** method, in order to notify the **StatefulWidget**, to rebuild, or to design itself. But with the new approach, we are going to use the **notifyListeners** method that comes from the **ChangeNotifier** class.

Replace the **setState** method that inside the **addNote** function with **notifyListeners**

```dart
void addNote() {
    var note = Note(
      title: _titleTextEditingController.text,
      body: _bodyTextEditingController.text,
    );

    notes.insert(0, note);

    notifyListeners(); // <- Here
  }
```

15. We will also need the value of both the title and the body of the note; in the past, we were taking these values from the **TextEditingController** directly, but since we have separated the logic from the **home_page.dart**. To solve this issue, we will pass this issue by using the named argument inside the **addNote** function.

    Add these two named arguments inside the **addNote** function (**title** & **body**),

    ```dart
     void addNote({required String title, required String body}) {
        var note = Note(
          title: title,
          body: body,
        );

        notes.insert(0, note);

        notifyListeners();
    ```

    > Note: **String** type

16. After creating these two named arguments (**title** & **body**), use them inside the **Note** object.

```dart
  void addNote({required String title, required String body}) {
    var note = Note(
      title: title, // <- Here
      body: body, // <- Here
    );

    notes.insert(0, note);

    notifyListeners();
  }
```

17. After we created the **NoteProvider** class, we need to create a **changeNotifierProvider** variable.

![screenshot](https://lh4.googleusercontent.com/MrhiNfvcfOqObRwXLSuCcQt8shQUGjatT_-kQKc2llVN8dYrzU6cjYzFE3S7lGDjdnChdCKggucVgyR14DReDPTv2Z-B34229KwwyEf_nmnQFucWrYMCyp5k3yIPaoIigj3Xrt39)

Above the **class NoteProvider**, create the **noteProvider** variable;

```dart
final noteProvider = ChangeNotifierProvider(
  (ref) => NoteProvider(), // 1
);
```

> **Note:** here, we returned the **NoteProvider** that we created before.
