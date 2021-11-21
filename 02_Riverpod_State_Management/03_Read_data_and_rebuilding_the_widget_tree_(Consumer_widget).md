# Read the data & rebuilding the widget tree (Consumer widget)

Because inside the note app, we have used a **ListView** widget and this widget displays the values of the **notes** variable. When the user adds a new note inside the **notes** variable, we need to rebuild the **ListView** widget again. Because of this reason we used the **notifyListeners()** method inside the **addNote** function that is inside the NoteProvider class.

![screenshot](https://lh6.googleusercontent.com/nC3U3-tpn1vQ5ONZgWJulQSRdMaN152lMFyfCaQ_FPN2eNVbLtD7_Yws53gNOPh-FFQoL8Tn6SHDYdeQhkb-xOp2GtAwEEZ80Zi5X7qR800YuEjI0_nvkz6S_2lSoyjydPRW5JCo)

20. Not only, we need to rebuild the widget tree, we also need to access the **notes** variable that is inside the **NoteProvider** class, and use it inside the **ListView** widget. So, the widget which will help us with accessing & rebuilding the widget tree is the **Consumer** widget.

![screenshot](https://lh6.googleusercontent.com/7IDdWwZzi-nLNt1-Bb_Gyoku3QPuWOhVvJJOh00R8WS4ddSkEnFEI_4i0r6i4VMEfOGosYID80nop7NZYLmHi_HtM-_LRmHt1e8fTMyOOMcpeTAxOAU-lckRLeYr8ff31uIfaTyT)

Cut the **ListView.builder**, then use the **Consumer** widget, and inside the builder named argument return & paste the **ListView.builder** that you cut before.

```dart
Consumer(
                builder: (context, watch, child) {
                  return ListView.builder(
                    shrinkWrap: true,
                    physics: const NeverScrollableScrollPhysics(),
                    itemCount: notes.length,
                    itemBuilder: (BuildContext context, int index) {
                      return NoteListTile(
                        note: notes[index],
                      );
                    },
                  );
                },
              ),
```

21. Since we are using the **notes** variable inside the **ListView** widget, we will use the **watch** argument, and create a **noteManager** variable inside the **builder** named argument.

![screenshot](https://lh3.googleusercontent.com/yQKjrLjIkbFHzAEt1RtBtslA1U10Fuai_4WjTGJ1e3hve-cbKO9nq5OSrLdxfC6MJpoTyrXH_-SwJDcF8FNQ0Mjmj-6tIHsY8zX7ZttdVOzCWEtBd1dlmSpg9y7_Av1lJ9RksI35)

```dart
 Consumer(
                builder: (context, watch, child) {

                  final noteManager = watch(noteProvider); // <- Here

                  return ListView.builder(
                    shrinkWrap: true,
                    physics: const NeverScrollableScrollPhysics(),
                    itemCount: notes.length,
                    itemBuilder: (BuildContext context, int index) {
                      return NoteListTile(
                        note: notes[index],
                      );
                    },
                  );
                },
              ),
```

> **Note:** the **watch()** method will rebuild the widget tree that the **Consumer** widget returns; it will rebuild this widget tree when the **notifyListeners()** is called.

22. After we are creating the **noteManager** variable, we will use it to access the data that is inside the **NoteProvider** class.

Replace the **itemCount: notes.length** to the **itemCount: noteManager.notes.length**,

```dart
 Consumer(
                builder: (context, watch, child) {
                  final noteManager = watch(noteProvider);

                  return ListView.builder(
                    shrinkWrap: true,
                    physics: const NeverScrollableScrollPhysics(),
                    itemCount: noteManager.notes.length, // <- Here
                    itemBuilder: (BuildContext context, int index) {
                      return NoteListTile(
                        note: notes[index],
                      );
                    },
                  );
                },
              ),
```

![screenshot](https://lh3.googleusercontent.com/YLoXcCwqF-aBTpkKlaAHb1boVEknu_lx3Dx-dPeo3yNuYmfef-IuxyUQ_P19wfXVFuopWrdRuSoTrcqn7X0zgkK_aZPxC_bhFijxbARJwtmrOnIK9FdWEivkPL39zQRIHCUmmKF5)

23. We can pass the selected note object inside the **NoteListTile,** but the best practice is to use the **selectedIndex** variable that we created inside the **NoteProvider** class before.

Go to the **note_provider.dart** file, create a new variable, and name it the **selectedIndex** variable.

```dart
class NoteProvider extends ChangeNotifier {
  var notes = [];

  var selectedIndex = -1; // <- Here

  void addNote({required String title, required String body}) {
    var note = Note(
      title: title,
      body: body,
    );

    notes.insert(0, note);

    notifyListeners();
  }
}
```

> **Note:** the value of the **selectedIndex** variable is **-1**, Just to indicate that there is no value selected. Later on, we will set the selected index to it.

Then, go to the **home_page.dart** file, and above the `return NoteListTile` change the value of the **selectedIndex** variable to the **index** value.

![screenshot](https://lh3.googleusercontent.com/UCqUt3P_D5MdB3UrDe9S3n2dT2wgI99hhxoGV-EDukew-iFoz1lirJfLTb3kSA0vkn1CQj8Z4R1myVTKUBP8KWbLYYym-x1kUh2RSdq9445TUk7Y7eIei32fSY54x14PCopIMaEq)

```dart
 Consumer(
                builder: (context, watch, child) {
                  final noteManager = watch(noteProvider);

                  return ListView.builder(
                    shrinkWrap: true,
                    physics: const NeverScrollableScrollPhysics(),
                    itemCount: noteManager.notes.length,
                    itemBuilder: (BuildContext context, int index) {

                      noteManager.selectedIndex = index; // <- Here

                      return NoteListTile(
                        note: notes[index],
                      );
                    },
                  );
                },
              ),
```

> **Note:** here we set the **index** value that the **ListView.builder** provided.

24. Because we no longer will use the **Constructor** to pass the object to other widgets or screens, and we will use the **riverpod** package.

Inside the **home_page.dart** file, remove the **note** named argument inside the **NoteListTile** widget.

```dart
 Consumer(
                builder: (context, watch, child) {
                  final noteManager = watch(noteProvider);

                  return ListView.builder(
                    shrinkWrap: true,
                    physics: const NeverScrollableScrollPhysics(),
                    itemCount: noteManager.notes.length,
                    itemBuilder: (BuildContext context, int index) {
                      noteManager.selectedIndex = index;

                      return NoteListTile(); // <- here
                    },
                  );
                },
              ),
```

Also, we will remove the **note** variable and the **Constructor** inside the **NoteListTile** and the **NotePage** widget.

![screenshot](https://lh4.googleusercontent.com/4nf6aaVYYxIYgURUDsStY_jIB-swPn0-FAHNlyStYXXnPT1Wmp6N86LRN9EUuXJ_h3p0AApXdxfq1tEZ20oxWWftGVTBvSD4yJNXELvWwZ1Q-FGP-86pVEkMGCl-O5ccX9w6X-rR)

25. Since we will need to use the **selectedIndex** variable & **notes** variable inside the **NoteListTile** to display the selected note, we will use the **Consumer** widget.

​ Import **flutter_riverpod.dart** & **note_provider.dart** fileinside **note_list_tile.dart** file

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';
import '../providers/note_provider.dart';
```

Then, go to the **note_list_tile.dart** file, and use the **Consumer** widget.

![screenshot](https://lh3.googleusercontent.com/PuDDvPEgmDRDA8pqlBvtSapWUb89JPYWzdF0b44tNAhfvnxhYuxaWTyjerF9dGNAngJ696xgF_nnn0LncnIKWaHT2lMz4_GhBjf9331CgxhLnZCm46SxyzeyQPj5RNfsOX46FgIu)

```dart
class NoteListTile extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer(
      builder: (context, watch, child) {
        return Padding(
          padding: const EdgeInsets.all(10.0),
          child: Card(
            elevation: 3,
            child: ListTile(
              leading: Icon(
                Icons.sticky_note_2_outlined,
                color: Theme.of(context).primaryColor,
              ),
              title: Text(note.title),
              onTap: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) {
                      return NotePage(
                        note: note,
                      );
                    },
                  ),
                );
              },
            ),
          ),
        );
      },
    );
  }
}
```

26. Then inside the **builder** named argument create the **noteManager** variable; later we will use this variable to access the **notes** & **selectedIndex** variable.

![screenshot](https://lh5.googleusercontent.com/lrbkMY5XV4PSntaK_f68cL7eik_nbmXT4WDeg8BUWIkWaieKPhlnA62OpUWrg5X6wrj8z37zbzuneO-gGdlYD9-1K6W-xRKJR9_xgjp2g-hOav5Huldy922kkdfqjKINycI_YAWO)

27. Create another variable, then name it **selectedNote**, and keep its value to **noteManager.notes[noteManager.selectedIndex]**

**![screenshot](https://lh4.googleusercontent.com/Q-zGh9H7gfGOMVRd89tVIh_PyaT_SlSZyC09Pvr4DRxkblHtF_pRPahlueSrXJst_G41RA5-PdLmUshH0_JO898EWG7upr3xTpxnBSxhLZw3vn3KFz2hweFFms0jiuYRzmW4WhET)**

```dart
class NoteListTile extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer(
      builder: (context, watch, child) {
        final noteManager = watch(noteProvider);

        final selectedNote = noteManager.notes[noteManager.selectedIndex]; // <- here

        return Padding(
          padding: const EdgeInsets.all(10.0),
          child: Card(
            elevation: 3,
            child: ListTile(
              leading: Icon(
                Icons.sticky_note_2_outlined,
                color: Theme.of(context).primaryColor,
              ),
              title: Text(note.title),
              onTap: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) {
                      return NotePage(
                        note: note,
                      );
                    },
                  ),
                );
              },
            ),
          ),
        );
      },
    );
  }
}
```

> **Note**: here we created a new variable; we keep its value to the selected note object by using the **notes** list variable, and we pass the **selectedIndex** inside it.

28. Then use the **selectedNote** variable, to display the **note title** inside the Text widget.

Replace note.title to **selectedNote.title** inside the **Text** widget,

```dart
Text(selectedNote.title),
```

![screenshot](https://lh3.googleusercontent.com/i71JD6CQ1NHAhHSbB0rZ1coN4cHdy6DednqUDf-ZMveXSwupmkSMFkiTjB8KJODj0HdPXjjjlCz6ubCDYzcM6fUVgfa8KCfYfiol2p9O87T8JG-r3W5sdCK1Z9OdcImpX_8Ix3Ru)

Also, remove the **note** named argument inside the **NotePage** widget because we no longer will use the **Constructor** to pass the data to the pages.

```dart
class NoteListTile extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer(
      builder: (context, watch, child) {
        final noteManager = watch(noteProvider);

        final selectedNote =
            noteManager.notes[noteManager.selectedIndex];

        return Padding(
          padding: const EdgeInsets.all(10.0),
          child: Card(
            elevation: 3,
            child: ListTile(
              leading: Icon(
                Icons.sticky_note_2_outlined,
                color: Theme.of(context).primaryColor,
              ),
              title: Text(selectedNote.title),
              onTap: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) {
                      return NotePage();  // <- here
                    },
                  ),
                );
              },
            ),
          ),
        );
      },
    );
  }
}
```

29. We will do the same process inside the **note_page.dart** file.

    - Two steps:

    1. Import the **flutter_riverpod.dart** & **note_provider.dart** files inside the **note_page.dart** file.

       > ```dart
       > import 'package:flutter_riverpod/flutter_riverpod.dart';
       > import '../providers/note_provider.dart';
       > ```

    2. Then use the **Consumer** widget to access the values that are inside the **NoteProvider**.

Replace the **NotePage** widget with the code below

```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';
import '../providers/note_provider.dart';

class NotePage extends StatefulWidget {
  @override
  _NotePageState createState() => _NotePageState();
}

class _NotePageState extends State<NotePage> {
  @override
  Widget build(BuildContext context) {
    return Consumer(builder: (context, watch, child) {
      final noteManager = watch(noteProvider);
      final selectedNote = noteManager.notes[noteManager.selectedIndex];

      return Scaffold(
        appBar: AppBar(
          title: Text(
            selectedNote.title,
            style: TextStyle(fontWeight: FontWeight.bold),
          ),
          backgroundColor: Theme.of(context).primaryColor,
        ),
        body: Card(
          elevation: 4,
          child: Center(
            child: Text(
              selectedNote.body,
              style: TextStyle(
                fontSize: 18,
              ),
            ),
          ),
        ),
      );
    });
  }
}
```

**Then run the app ^\_^**

![screenshot](https://lh6.googleusercontent.com/L3bE8f6cnDg7_8l84y4L2htEF6njv3GjgAA7EIgWdCNGmFavvkDSvVCadR7Q8j8_DqecmzYtE3QsboME_y-qdQwzJtDbhmiIvWY-NlyINJbmhYk7ilBFDfBiiPbXW518rURggRRz)

![screenshot](https://lh6.googleusercontent.com/-3urOR1FVaBWCyVe5MkximX1SMUWaqt5XQ8kDabiVg3l5XvTqPpMkGME3mPmbGjv4IZlxXTPQ10x81_tv0Kd7CErUL8xjC8uzAS9jRofYcPrDifemnDTPbEljLQ53dPsM5QsOjJY)
