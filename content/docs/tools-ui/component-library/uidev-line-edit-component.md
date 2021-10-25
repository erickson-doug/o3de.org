---
linktitle: Line Edit
title: O3DE UI Line Edit Component
description: Use the O3DE UI line edit component to capture free-form text from the user.
toc: true
---

The **line edit** component is one of several types of input boxes offered by the Qt and O3DE UI libraries. Use the line edit component to enable users to enter free-form text. Be mindful of the length of text intended for a field, and always pair with a useful, clear label.

## Anatomy of the line edit widget

 **Line edit** widgets have several customization options. Standard features including the following elements:

![component line edit anatomy](/images/tools-ui/component-line-edit-anatomy.png)

1.  **Label**

    While not technically part of the widget, you should give input boxes a label in the UI layout.

1.  **Placeholder text**

    (Optional) Hint text set in the UI, or using `setPlaceholderText()`, appears here when the widget text is empty.

1.  **Input box**

    Text entered by the user, or that you set using `setText()`, appears here.

1.  **Tooltip**

    (Optional) If you set tooltip text for the widget, it will appear near where the user hovers.

    ![component line edit anatomy clear](/images/tools-ui/component-line-edit-anatomy-clear.png)

1.  **Clear button**

    (Optional) If you enable the clear button for the widget, it will appear when the input box is not empty. When users choose the clear button, the input box returns to an empty value.

    ![component line edit anatomy error state](/images/tools-ui/component-line-edit-anatomy-error-state.png)

1.  **Error state indicator**

    (Optional) If you set a validator for the input box, and validation fails, an error state indicator icon appears at the end of the input box, before the clear button.

1.  **Error tooltip**

    (Optional) When an error state exists, if an error message has been set for the widget, it will appear near where the user hovers. This tooltip appears in place of the normal tooltip text while an error state exists. If you don't set the error message, the default error tooltip text is "Invalid input".

## Basic line edit

![component line edit basic](/images/tools-ui/component-line-edit-basic.png)

A simple **line edit** component starts with the `QLineEdit` Qt widget. You can set additional options by changing widget settings in the Qt Designer or in code.

### Example

```cpp
#include <QLineEdit>

// Create a new line edit widget.
QLineEdit* lineEdit = new QLineEdit(parent);

// Set the placeholder text.
lineEdit->setPlaceholderText("Hint text");

// Enable the clear button.
lineEdit->setClearButtonEnabled(true);

// Then add lineEdit to a UI layout as needed.
```

## Line edit with search

![component line edit search style](/images/tools-ui/component-line-edit-search-style.png)

The `AzQtComponents::LineEdit` class provides several static style functions that apply a style to a `QLineEdit` widget. One example is the search style, which adds a search icon. Additional styles are documented in the API reference for [AzQtComponents::LineEdit](/docs/api/frameworks/azqtcomponents/class_az_qt_components_1_1_line_edit.html).

### Example

```cpp
#include <AzQtComponents/Components/Widgets/LineEdit.h>
#include <QLineEdit>

// Add a search icon.
AzQtComponents::LineEdit::applySearchStyle(lineEdit);

// Listen for changes to the text by the user.
connect(lineEdit, &QLineEdit::textEdited, this, [](const QString& newText) {
    // Perform the search as the user is typing.
});
```

## Listening for line edit changes

The following examples demonstrate how to listen for various types of text changes in a `QLineEdit` widget.

### Example

```cpp
#include <QLineEdit>

// Listen for changes to the text, either by the user or when setText() is called.
connect(lineEdit, &QLineEdit::textChanged, this, [](const QString& newText) {
    // Handle text change.
});

// Listen for changes to the text by the user.
connect(lineEdit, &QLineEdit::textEdited, this, [](const QString& newText) {
    // Handle when user changes the text.
});

// Listen for when the Return or Enter key has been pressed, or when the input box loses focus.
connect(lineEdit, &QLineEdit::editingFinished, this, [lineEdit]() {
    // New text can be retrieved from lineEdit->text().
});
```

## Line edit as a drop target

![component line edit drop target style](/images/tools-ui/component-line-edit-drop-target-style.png)

The following examples demonstrate how to apply or remove the drop target style to a `QLineEdit` widget.

### Example

```cpp
#include <AzQtComponents/Components/Widgets/LineEdit.h>
#include <QLineEdit>

// To show the QLineEdit as a valid drop target:
AzQtComponents::LineEdit::applyDropTargetStyle(lineEdit, true);

// To show the QLineEdit as an invalid drop target:
AzQtComponents::LineEdit::applyDropTargetStyle(lineEdit, false);

// To clear the drop target style:
AzQtComponents::LineEdit::removeDropTargetStyle(lineEdit);
```

## Line edit with validator

![component line edit error state](/images/tools-ui/component-line-edit-error-state.png)

In the following example, both a validator and an error message for the error tooltip have been defined. The standard tooltip appears when a mouse hovers over the widget. The error tooltip appears when a mouse hovers over the widget while an error state exists.

Error states occur when a validator has been set and its validation has failed.

### Example

```cpp
#include <AzQtComponents/Components/Widgets/LineEdit.h>
#include <QLineEdit>
#include <QDoubleValidator>

// Define and set the validator.
auto validator = new QDoubleValidator(lineEdit);
validator->setNotation(QDoubleValidator::StandardNotation);
validator->setTop(4.0);
validator->setBottom(3.0);
lineEdit->setValidator(validator);

// Set the error tooltip text.
AzQtComponents::LineEdit::setErrorMessage(lineEdit, QStringLiteral("Value must be between 3.0 and 4.0"));
```

## Disabled line edit

![component line edit disabled](/images/tools-ui/component-line-edit-disabled.png)

In the following example, the widget and its features have been disabled in code.

### Example

```cpp
#include <QLineEdit>

// Disable the widget.
lineEdit->setEnabled(false);
```

## C++ API reference

For details on the **line edit** API, see the following topic in the [O3DE UI Extensions C++ API Reference](/docs/api/frameworks/azqtcomponents/namespace_az_qt_components.html):
+  [AzQtComponents::LineEdit](/docs/api/frameworks/azqtcomponents/class_az_qt_components_1_1_line_edit.html)

Relevant Qt documentation includes the following topics:
+  [QLineEdit Class](https://doc.qt.io/qt-5/qlineedit.html)

## Related links

For components related to the **line edit** component, see the following topics:
+  [Browse edit](./uidev-browse-edit-component)
+  [Spinbox](./uidev-spinbox-component)
