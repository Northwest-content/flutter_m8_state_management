# Read the data only (context.read method) 



18. Right now, we centered the data top of the tree widget, and to access it we need to use the **riverpod** package.

    

Since we are going to use this data inside the **home_page.dart** file, we need to import the     **riverpod** package, and the **NoteProvider**.

Import the **riverpod** package inside the **home_page.dart** file,

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';	
import '../providers/note_provider.dart';
```



19. To use the **addNote** function that is inside the **note_provider.dart** file, use the **context.read** method.

    > **context.read** method helps you to read the methods and variables that are inside the provider without rebuilding the widget tree.



​	Go to the **IconButton** widget, and change the **onPressed** named argument to

```dart
IconButton(
                      iconSize: 32,
                      icon: Icon(
                        Icons.add_box,
                        color: Theme.of(context).primaryColor,
                      ),
                      onPressed: () {

		// Here
                        context.read(noteProvider).addNote(
                              title: _titleTextEditingController.text,
                              body: _bodyTextEditingController.text,
                            );
                      },
                    ),
```

> **Note:** the **context.read** method needs one argument which is the provider that you created before; then you can access all variables and methods that you created inside the provider file. So, in our case we import the **addNote** method; this method needs two named arguments (**title** & **body**), and we used the **TextEditingController.text** values.

