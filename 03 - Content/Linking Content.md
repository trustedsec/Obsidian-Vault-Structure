---
creation date: September 7th 2021
last modified date: September 7th 2021
aliases: []
tags: #📖
---

Primary Categories: [[01 - Administration]]  
Secondary Categories:  [[02 - Obsidian]] - [[02 - Resources]]  
Links: [[Linking]] - [[Zettlekasten]] - [[Data Discovery]]  
Search Tag: #📖  

# [[Linking Content]]

# Description

1. Within Obsidian, links are the means by which data is structured and relationships are drawn. 

2. Obsidian allows the linking of content to a note at **3** levels ^0266aa

| Result                                     | Command                        | Example                     |
| ------------------------------------------ | ------------------------------ | --------------------------- |
| Link to an entire note                     | `[[name of the note]]`         | [[Linking Content]]         |
| Link to a notes heading                    | `[[name of the note#heading]]` | [[Linking Content#Details]] |
| Link to a block within a specified heading | `[[name of the note^blockname` | [[Linking Content#^0266aa]] | 

3. At each stage of linking, the relevant content can instead be embedded by adding the *!* prefix ^0834a4
	1. Example linking to the above: [[Linking Content#^0834a4]]
	2. As you can see above, a reference *ID* is added to the target block of text
	3. As you're linking, Obsidian will parse and present all possible headings/blocks for selection
 
	![[Pasted image 20210907120723.png]]

## How To Link?

1. Within the TrustedSec Obsidian vault, *links* are used as a replacement for what would more traditionally be considered *tags*. 

2. Example:
	1. Over time a vault grows and several links are created to a recurring category that is not yet created. Links with no associated note can be readily identified:
		1. from a note's preview pane as they'll be displayed with a faded text
		
![[Pasted image 20210907120756.png]]
		3. from the graph's view, where unlinked notes/nodes will appear in a different color



```ad-important
If you're using included CSS snippets nonexistant nodes become a bit more visable as they're colored dark red.
```

### Before:
![[Pasted image 20210907120838.png]]

### After:
![[Pasted image 20210907121102.png]]

4. "Unlinked Mentions" as these unlinked notes are refered to, can then be created simply by clicking the identified unlinked *link* or *node*

5. If you're using templates when creating new notes, the hierarchical folder structure above your new note is automatically applied to the note a series of links. Unlike [[Tagging Content|Tags]], several *links* should be added to new notes with the idea that more meaningful links creates more relationships/opportunity for relationships between notes. This process should ultimately lead to a natural distillation of categorical knowledge and thus a new category and MOC.



## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: September 7th 2021 (11:24 am)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
