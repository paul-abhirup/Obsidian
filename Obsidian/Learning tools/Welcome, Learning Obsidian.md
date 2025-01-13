This is your new *vault*.

Make a note of something, [[Learning Obsidian]], or try [the Importer](https://help.obsidian.md/Plugins/Importer)!

When you're ready, delete this note and make the vault your own.

using vim for editing

|                                                        |                          |
| ------------------------------------------------------ | ------------------------ |
| Move the cursor to the beginning of the current line   | `Home`                   |
| Move the cursor to the end of the current line         | `End`                    |
|                                                        |                          |
| Extend selection to the beginning of the previous word | `Ctrl+Shift+Left arrow`  |
| Extend selection to the end of the next word           | `Ctrl+Shift+Right arrow` |
| Extend selection to the beginning of the current line  | `Shift+Home`             |
| Extend selection to the end of the current line        | `Shift+End`              |
| Extend selection to the beginning of the note          | `Ctrl+Shift+Home`        |
| Extend selection to the end of the note                | `Ctrl+Shift+End`         |
| Extend selection one page up                           | `Shift+Page up`          |
| Extend selection one page down                         | `Shift+Page down`        |
|                                                        |                          |
Basic formatting -----
paragraph

Heading
# h1
###### h6

| Style                  | Syntax                 | Example                                  | Output                                 |
| ---------------------- | ---------------------- | ---------------------------------------- | -------------------------------------- |
| Bold                   | `** **` or `__ __`     | `**Bold text**`                          | **Bold text**                          |
| Italic                 | `* *` or `_ _`         | `*Italic text*`                          | _Italic text_                          |
| Strikethrough          | `~~ ~~`                | `~~Striked out text~~`                   | ~~Striked out text~~                   |
| Highlight              | `== ==`                | `==Highlighted text==`                   | ==Highlighted text==                   |
| Bold and nested italic | `** **` and `_ _`      | `**Bold text and _nested italic_ text**` | **Bold text and _nested italic_ text** |
| Bold and italic        | `*** ***` or `___ ___` | `***Bold and italic text***`             | **_Bold and italic text_**             |

Internal links
- Wikilink: `[[Three laws of motion]]`
- Markdown: `[Three laws of motion](Three%20laws%20of%20motion.md)`

External link
[Google](https://www.google.com)

External images 
adding ! symbol before an external link 
![Engelbart](https://history-computer.com/ModernComputer/Basis/images/Engelbart.jpg)

Quotes --
adding a > symbols before the text 
> Human beings face ever more complex and urgent problems, and their effectiveness in dealing with these problems is a matter that is critical to the stability and continued progress of society. 
> \- Doug Engelbart, 1961

# Unordered list
You can create an unordered list by adding a `-`, `*`, or `+` before the tex

# Ordered List 
1. First 
2. Second
3. Third

Task List 
- [x] completed task
- [ ] incomplete task

Nesting lists
1. first list 
	1. use tab to shift
	2. nested list 
2. 2nd list 
	1. use shift+tab
	2. to move to beginning
3. or double enter works 

use tab or shift+tab or double enter

 ---
Horizontal rule
***
You can use three or more stars `***`, hyphens `---`, or underscore `___` on its own line to add a horizontal bar. You can also separate symbols using spaces.

inline code ` inline code `
code block 
```js
code block
```

# comments 
This is an %%inline%% comment. 
%%
This is a block comment. Block comments can span multiple lines. 
%%

# footnotes
This is a simple footnote[^1]. 
[^1]: This is the referenced text.
[^2]: Add 2 spaces at the start of each new line. This lets you write footnotes that span multiple lines. 
[^note]: Named footnotes still appear as numbers, but can make it easier to identify and link references.
You can also use inline footnotes. ^[This is an inline footnote.]
# Tables 

| Syntax          | Description                                                                                                               |
| --------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `[[Link]]`      | [Internal links](https://help.obsidian.md/Linking+notes+and+files/Internal+links)                                         |
| `![[Link]]`     | [Embed files](https://help.obsidian.md/Linking+notes+and+files/Embed+files)                                               |
| `![[Link#^id]]` | [Block references](https://help.obsidian.md/Linking+notes+and+files/Internal+links#Link%20to%20a%20block%20in%20a%20note) |
| `^id`           | [Defining a block](https://help.obsidian.md/Linking+notes+and+files/Internal+links#Link%20to%20a%20block%20in%20a%20note) |
| `%%Text%%`      | [Comments](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Comments)                              |
| `~~Text~~`      | [Strikethroughs](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Styling%20text)                  |
| `==Text==`      | [Highlights](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Styling%20text)                      |
| ` ``` `         | [Code blocks](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Code%20blocks)                      |
| `- [ ]`         | [Incomplete task](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Task%20lists)                   |
| `- [x]`         | [Completed task](https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax#Task%20lists)                    |
| `> [!note]`     | [Callouts](https://help.obsidian.md/Editing+and+formatting/Callouts)                                                      |
| (see link)      | [Tables](https://help.obsidian.md/Editing+and+formatting/Advanced+formatting+syntax#Tables)                               |

