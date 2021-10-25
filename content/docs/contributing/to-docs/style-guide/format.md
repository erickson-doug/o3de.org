---
title: Formatting Documentation for Open 3D Engine
description: A reference for all of the typesetting and formatting rules for the Open 3D Engine (O3DE) documentation.
linktitle: Formatting
weight: 200
toc: true
---

With Markdown, sometimes there are multiple methods to achieve the same result. For example, you can enclose words in underscores (`_`) or asterisks (`*`) to create italics. In these situations, it is best to use one method throughout the documentation. To keep both the documentation Markdown source files, and the O3DE documentation on-page presentation consistent, adhere to the following basic documentation standards.

## Topic headings

Use a series of hashes (`#`) to define section headings. The H1 heading is taken from the metadata `title` element, which displays as the on-page title. Use standard capitalization, not sentence capitalization, for both the metadata title (`title`), the table-of-contents title (`linkTitle`).

Section titles should be an H2 (`##`) heading, and use sentence case for the section title.

Subsection titles should start with an H3 (`###`) heading, and use sentence case for the subsection title.

Example:

```markdown
---
linkTitle: Page Title
title: An O3DE Documentation Page Title
description: A topic about an Open 3D Engine feature.
weight: 100
toc: true
---

## H2 for the first section title (Sentence title capitalization)

### H3 for a sub-section title (Sentence title capitalization)

...

## H2 for the second section title (Sentence title capitalization)

### H3 for sub-section title (Sentence title capitalization)

#### H4 for sub-section of a sub-section title (Sentence title capitalization)

```

{{< note >}}
A table of contents for the page is automatically generated in the right gutter using the on-page headings if the `toc` Front Matter variable is set to `true`.
{{< /note >}}

## Links

Write links without the file extentension *.md*.

| Relative link | Result |
| - | - |
| `[...](./)` | Returns to the current directory's index page. |
| `[...](page-linked-from-index)` | Links from the index page to a page in the index's directory. |
| `[...](./page-linked-from-non-index)` | Links from any page to a page in the same directory. |
| `[...](forward-directory-linked-from-index/)` | Links from the index page to a subdirectory of the index. |
| `[...](./forward-directory-linked-from-non-index/)` | Links from any page to a subdirectory of the current page. |
| `[...](../)` | Returns to the index of the previous directory. |
| `[...](../link-to-page-in-previous-directory)` | Links from any page to a page in the previous directory. |

## Tables

Table example:

```markdown
| Default column| Right-aligned column | Center-aligned column | Left-aligned column |
| - | -: | :-: | :- |
| Row | entry | entry | entry |
| Row | entry | entry | entry |
| Row with missing entry | entry | | entry |
```

Table result:

| Default column| Right-aligned column | Center-aligned column | Left-aligned column |
| - | -: | :-: | :- |
| Row | entry | entry | entry |
| Row | entry | entry | entry |
| Row with missing entry | entry | | entry |

## Tabs

Tabs example:


```
{{</* tabs name="name-for-this-group-of-tabs" */>}}
{{%/* tab name="First tab" */%}}

First tab's content.

{{%/* /tab */%}}
{{%/* tab name="Second tab" */%}}

Second tab's content.

{{%/* /tab */%}}
{{</* /tabs */>}}
```


Tabs result:

{{< tabs name="tabs-example" >}}
{{% tab name="First tab" %}}

First tab's content.

{{% /tab %}}
{{% tab name="Second tab" %}}

Second tab's content.

{{% /tab %}}
{{< /tabs >}}

## Text format

There can be multiple methods to achieve the same result in Markdown. Adhere to the following standards to make both the Markdown source files and the on-page documentation much easier for readers to parse at a glance. Consistency in the Markdown source format also aids automation efforts for documentation.

### Bold text

To bold text, enclose the text in double asterisks (`**`).

Bold example:

```markdown
This is **bold** text.
```

Bold result:

This is **bold** text.

### Italic text

To italicize text, enclose the text in a single asterisk (`*`).

Italic example:

```markdown
This is *italic* text.
```

Italic result:

This is *italic* text.

### Inline code

To format text as inline code, enclose the text in a single backtick (`` ` ``).

Inline code example:

```markdown
This is `code` text.
```

Inline code result:

This is `code` text.

### Code block

Use code blocks for multi-line code. Some languages are supported for syntax highlighting. The language is specified after the opening back-ticks (` ``` `) of the code block.

Code block example:

````none
```python
# Use the 'request' find the type of job via 'jobKey' to determine what to do
def on_process_job(args):
    try:
        # Get request information
        request = args[0]
         ...
```
````

Code block result:

```python
# Use the 'request' find the type of job via 'jobKey' to determine what to do
def on_process_job(args):
    try:
        # Get request information
        request = args[0]
         ...
```

{{< note >}}
Syntax highlighting in the code block should conform to the [contrast guidelines.](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0&showtechniques=141%2C143#contrast-minimum)
{{< /note >}}

When writing code blocks, make sure to include a language identifier. For C++ code blocks, use the `cpp` identifier.

### Mark placeholders with angle brackets

Use angle brackets for placeholders. Use the text within the brackets to tell the reader what a placeholder represents. For example:

```shell
git push origin <your-branch-name>
```

### Bold user interface elements

Do | Don't
:--| :-----
Choose **Edit**. | Click "Edit".
.. the **Play** button. | ... the Play button.

### Bold input combinations

Do | Don't
:--| :-----
Press **Enter**. | Press "Enter".
.. **right-click** the asset name ... | ... right-click the asset name ...
Hold **CTRL+SHIFT** ... | Hold `Control + Shift` ...

### Bold proper application names

For the first introduction of an application name on a page, use **bold** text. Subsequent references to the application on the page should not be bold.

Example:

**O3DE Editor** is the primary development environment for .... Open O3DE Editor by launching it from...

Do | Don't
:--| :-----
Open **Material Editor**. | Open the Material Editor.
In **Asset Processor**, right-click... | In "Asset Processor", right-click...

### Italicize new term introductions and definitions

Do | Don't
:--| :-----
... to create *image based lighting (IBL)*. | ... to create **image based lighting (IBL)**.
A *prefab* is a collection of entities ... | A "prefab" is a collection of entities ...

### Quotes and punctuation placement

When the quote is contained within a sentence, place the punctuation outside the quote.

Do | Don't
:--| :-----
... assets that are "game-ready". | ... assets that are "game-ready."
... process called "rigging". | ... process called "rigging."

When the quote is a complete sentence, place the punctuation inside the quote.

> "Focus is a matter of deciding what things you're not going to do." - John Carmack

### Code style for filenames, directories, and paths

All paths should be platform agnostic and use `/` path separators. When using relative paths, give the reader context to understand what the path is relative to.

Do | Don't
:--| :-----
Open the project's `bootstrap.cfg` file. | Open the project's bootstrap.cfg file.
... in the `/<project>/levels` directory. | ... in the /\<project\>/levels directory.
Open the `/<project>/game.cfg` file. | Open the /\<project\>/game.cfg file.

### Code style for inline code and commands

Do | Don't
:--| :-----
... set `enable_memory_tracking = True`. | ... set **enable_memory_tracking** = "True".
... enter the command `dump_vars`. | ... enter the command dump_vars.

### Code style for variable names, API objects, namespaces, and so on

Do | Don't
:--| :-----
... value of the `sys_maxfps` field. | ... value of the "sys_maxfps" field.
... use the `WorldRequestBus`. | ... use the "WorldRequestBus".
... in `AZ::Data::AssetData` derived classes. | ... in **AZ::Data::AssetData** derived classes.

### Bold property names, and inline code their values

Do | Don't
:--| :-----
Set the **Color** property to `255,0,0`. | Set the Color property to "255,0,0".
For **Intensity Mode**, select `Candela`. | For `Intensity Mode`, select Candela.
Valid **Mass** values range from `0` to `Infinity`. | Valid Mass values range from `0` to Infinity.

### Don't include the command prompt

Do | Don't
:--| :-----
`cmake --build ...` | `C:\> cmake --build ...`

### Separate commands from output

```shell
cmake --build <MyProject> --config profile --target Editor -- /m
```

The output is similar to this:

```console
Microsoft (R) Build Engine version 16.9.0+57a23d249 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

  Checking Build System
  Building Custom Rule D:/O3DE/Code/Framework/AzCore/CMakeLists.txt
  unity_16_cxx.cxx
  unity_20_cxx.cxx
  unity_19_cxx.cxx
  unity_24_cxx.cxx
  unity_23_cxx.cxx
```

## Lists

Use ordered lists when the order of the items is significant, such as a procedure of sequential steps. Use unordered lists if the order of the items is arbitrary, such as a list of assets.

If the list is longer than four items, or if the list contains call-out shortcode or an image, add newlines between each list element to improve readability.

### Ordered lists

Use `1.` to delineate items in ordered lists. Goldmark automatically numbers the items in the list. Ordered lists are used for procedures.

Ordered list example:

```markdown
1. Step one
1. Step two
1. Step three
1. Step four
```

Ordered list result:

1. Step one
1. Step two
1. Step three
1. Step four

### Unordered lists

Use `*` to delineate items in unordered lists.

Unordered list example:

```markdown
* Item one
* Item two
* Item three
```

Unordered list result:

* Item one
* Item two
* Item three

### Nested lists

Indent four spaces to nest a list. Nested lists are often used for sub-steps or requirements lists in a procedure.

Nested list example:

```markdown
1. Step one
1. Step two
    * Item one
    * Item two
    * Item three
1. Step three
```

Nested list result:

1. Step one
1. Step two
    * Item one
    * Item two
    * Item three
1. Step three

### Definition lists

Use definition lists for content that lists a pair of terms and their definitions. For example, a glossary.
  
Definition list example:

```markdown
First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.
```

Definition list result:

First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.
