---
creation date: September 7th 2021
last modified date: September 7th 2021
aliases: []
tags: #📖
---

Primary Categories: [[01 - Administration]]  
Secondary Categories:  [[02 - Obsidian]] - [[02 - Resources]]  
Links: [[Automation]] - [[Templates]] - [[Github]]  
Search Tag: #📖  

# [[Templater]]

## Description:

[Templater](https://github.com/SilentVoid13/Templater) is a template language that lets you insert **variables** and **functions** results into your [Obsidian](https://obsidian.md/) notes. 

![templater_demo](https://raw.githubusercontent.com/SilentVoid13/Templater/master/imgs/templater_demo.gif)

## How we'll use Templater
- Prompt for the Search tag on note creation
- Prompt for title on note creation
- Add date *created* automatically
- Update *last updated* automatically
- Move the note to the appropriate location
 	- 02 - Secondary Categories
	- 03 - Content
	- 05 - Personal

## Installation:

1. Templater is a registered Obsidian [[02 - Plugins#Community Plugins]] and can be installed directly from `Settings > Community Plugins > Browse`

## Configuration

```ad-info
### Not Seeing this stylized in *PREVIEW* mode?
#### Try installing the community plugin, 'Admonition'

1. *Template Folder Location*: 04 - Templates
2. *Trigger Templater on New File Creation*: True
3. *Empty File Template*: 04 - Templates/0400 - Gen_Note
```

To help manage **incomplete**, **NULL**, or **'Untitled'** notes, it can  be helpful to assign `Settings > Files & Links > Folder to Create New Notes in` to `.trash`. Since our **0400 - Gen_Note** template handles moving successfully created notes to their appropriate folders, the categories listed above will automatically end up in trash. 

___

# Resources:

| Hyperlink                                                                 | Info |
| ------------------------------------------------------------------------- | ---- |
| [Templater Github Repo](https://github.com/SilentVoid13/Templater)        |      |
| [Templater Documentation](https://silentvoid13.github.io/Templater/docs/) |      |

Created Date: September 7th 2021 (11:24 am)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>