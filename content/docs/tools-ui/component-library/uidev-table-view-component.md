---
linktitle: Table View
title: O3DE UI Table View Component
description: Learn how to use the O3DE UI table view component to present columns of structured data in O3DE tools and Gems.
toc: true
---

Use the **table view** component to present multiple columns of structured data in a table format. By default, this component employs sortable columns and "zebra striping" - where the background color of rows alternate - to help you create an easily readable, scannable, and sortable presentation of data.

![component table view example](/images/tools-ui/component-table-view-example.png)

{{< note >}}
`AzQtComponents::TableView` actually derives from `QTreeView`, not `QTableView`, to provide more customization over the size of rows.
{{< /note >}}

## Basic table view

![component table view basic](/images/tools-ui/component-table-view-basic.png)

Create a simple logging table view.

{{< note >}}
If a table view is combined with a [tree view](/docs/tools-ui/component-library/uidev-tree-view-component), you might need to turn off zebra striping in one of the widgets using the setAlternatingRowColors(false) function.
{{< /note >}}

### Example

```cpp
#include <AzQtComponents/Components/Widgets/TableView.h>
#include <AzToolsFramework/UI/Logging/LogTableModel.h>
#include <AzToolsFramework/UI/Logging/LogLine.h>
#include <QDateTime>

// Create a log table model for this example.
auto logModel = new AzToolsFramework::Logging::LogTableModel(this);

// Create the table view.
auto tableView = new AzQtComponents::TableView(parent);

// Set the model for the table.
tableView->setModel(logModel);

// Add a few lines of sample data.
logModel->AppendLine(
    AzToolsFramework::Logging::LogLine(
        "An informative message for debugging purposes.",
        "Window",
        AzToolsFramework::Logging::LogLine::TYPE_MESSAGE,
        QDateTime::currentMSecsSinceEpoch()));

logModel->AppendLine(
    AzToolsFramework::Logging::LogLine(
        "A warning message for things that may not have gone as expected.",
        "Window",
        AzToolsFramework::Logging::LogLine::TYPE_WARNING,
        QDateTime::currentMSecsSinceEpoch()));

logModel->AppendLine(
    AzToolsFramework::Logging::LogLine(
        "Critical error message, something went wrong.",
        "Window",
        AzToolsFramework::Logging::LogLine::TYPE_ERROR,
        QDateTime::currentMSecsSinceEpoch()));
```

## C++ API reference

For details on the **table view** API, see the following topic in the [O3DE UI Extensions C++ API Reference](/docs/api/frameworks/azqtcomponents/namespace_az_qt_components.html):
+  [AzQtComponents::TableView](/docs/api/frameworks/azqtcomponents/class_az_qt_components_1_1_table_view.html)

Relevant Qt documentation includes the following topics:
+  [QTreeView Class](https://doc.qt.io/qt-5/qtreeview.html)
+  [QAbstractListModel Class](https://doc.qt.io/qt-5/qabstractlistmodel.html)
