---
creation date: September 7th 2021
last modified date: September 7th 2021
aliases: []
tags: #📖
---

Primary Categories: [[01 - Administration]]  
Secondary Categories:  [[02 - Obsidian]] - [[02 - Resources]]  
Links: [[CSS]] - [[Styling]] - [[Customization]]  
Search Tag: #📖  

# [[Obsidian - Custom CSS]]  

## Enabling Custom CSS Snippets:

To enable custom styling within Obsidian, you'll need to:
1. Create the associated 'snippets' folder within the obsidian vault filestructure. This folder can be created by going to `Settings > Appearences` and clicking on the folder icon (far right) shown below. This folder will be created within the `$VAULTPATH/.obsidian/` directory. 

![[Pasted image 20210907125248.png]]

2. Within the newly created `snippets` folder, create a single `.css` or several `.css` files with the descired snippets below. 

![[Pasted image 20210907125653.png]]


4. After the files are present within the file structure, again path to `Settings > Appearences` and click the `refresh` icon next to the folder icon we chose previously. All individual `.css` files should now be listed as toggle-able style options.

![[Pasted image 20210907125817.png]]



## Snippet Library:

### 1. Colorized Graph Nodes

#### Description
Recolor  `unresolved` or non-existent notes to show up in graph view as dark red (#CF4747).

While Obsidian exposes the ability to colorize the graph view using groups, there doesnt seem to yet be a way to colorize unresolved notes. For this we'll use a CSS snippet. 

#### CSS Snippet
```ad-example
title: Colorize Graph Nodes
collapse: Yes
icon: triforce

.graph-view.color-fill-unresolved { 
 color: #CF4747; !important
}
```

#### Example
![[Linking Content#Before]]
![[Linking Content#After]]



### 2. Colorized Tag Pills

#### Description
Add colored 'pill' styling around search tags.

#### CSS Snippet
```ad-example
title: Colorize Graph Nodes
collapse: Yes
icon: triforce

/* 
Pill-style colorized tags in preview AND editor panes
*/

a.tag,
div:not(.CodeMirror-activeline) > .CodeMirror-line span.cm-hashtag-begin,
div:not(.CodeMirror-activeline) > .CodeMirror-line span.cm-hashtag-end {
  background-color: var(--text-accent);
  border: none;
  color: white;
  font-size: 12px;
  padding: 1px 8px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  margin: 0px 0px;
  cursor: pointer;
  border-radius: 12px;
}

a.tag:hover {
  background-color: var(--text-accent-hover);
  color: white
}

div:not(.CodeMirror-activeline) > .CodeMirror-line span.cm-hashtag-begin {
  display: none;
}

div:not(.CodeMirror-activeline) > .CodeMirror-line span.cm-hashtag-end:before {
  content: '#';
}

.tag[href^="#obsidian"] {
  background-color: #4d3ca6;
}

.tag[href^="#important"] {
  background-color: red;
}

.tag[href^="#complete"] {
  background-color: green;
}

.tag[href^="#inprogress"] {
  background-color: orange;
}
```

#### Example
![[Pasted image 20210907122512.png]]


### 3. Current Line Focus

#### Description
Using the VIM community plugin, colors the current line in focus  when in insert mode for improved readability

#### CSS Snippet
```ad-example
~~~CSS
/* Modified by Christian (Chhrriissyy#6548). Original by MooddooM */
/* This version sets the line focus for both edit and insert mode. */
/* If you want to make it edit mode only, add the `.cm-fat-cursor` CSS class selector to both light & dark mode. /*

/* Cursor color in normal vim mode and opacity */
.cm-fat-cursor .CodeMirror-cursor, .cm-animate-fat-cursor {
    width: 0.5em;
    background: #d65d0e;
    opacity: 60% !important;
}

/* LIGHT MODE */
/*if you want the highlight to present in both normal and insert mode of vim*/
.theme-light /* .cm-fat-cursor */ .CodeMirror-activeline .CodeMirror-linebackground{
    background-color: #2f2f2f;
    opacity: 10%
}

/* DARK MODE */
.theme-dark /* .cm-fat-cursor */ .CodeMirror-activeline .CodeMirror-linebackground {
    background-color: #f1f1f1;
    opacity: 30%;
```

#### Example
![[highlight_currentline.gif]]


### 4. Enlarge Image on Hover

#### Description
In preview mode, enlarges images/gifs when you hover over them.

#### CSS Snippet
```ad-example
~~~CSS
.markdown-preview-view img {
  display: block;
  margin-top: 20pt;
  margin-bottom: 20pt;
  margin-left: auto;
  margin-right: auto;
  width: 50%;  /* experiment with values */
  transition:transform 0.25s ease;
}

.markdown-preview-view img:hover {
    -webkit-transform:scale(1.8); /* experiment with values */
    transform:scale(2);
    
}

```

#### Example
![[highlight_currentline 1.gif]]


### 5. Embed Without a Scroll Bar
#### Description
Embedded windows or references to Obsidian locations will render expanded and not within a static div size + scrollbar.

#### CSS Snippet
```ad-example
~~~CSS
/* Remove scroll bar from transclusions */
.markdown-preview-view .markdown-embed-content {
max-height: unset;
}
.markdown-preview-view .markdown-embed-content > .markdown-preview-view {
max-height: unset;
}

```


#### Example

![[Pasted image 20210907124937.png]]

### 6. External Resource Embed Styles

#### Description
Attempt to make externally embedded content  more responsive

#### CSS Snippet
```ad-example
~~~CSS
/* responsive img/iframe defintion */
[style*="--aspect-ratio"] > :first-child {
  width: 100%;
}

[style*="--aspect-ratio"] > img {  
  height: auto;
}

@supports (--custom:property) {
  [style*="--aspect-ratio"] {
    position: relative;
  }
  [style*="--aspect-ratio"]::before {
    content: "";
    display: block;
    padding-bottom: calc(100% / (var(--aspect-ratio)));
  }  
  [style*="--aspect-ratio"] > :first-child {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
  }  
}

```

#### Example
![[responsive_yt.gif]]


___

## Resources:

| Hyperlink                                                                | Info                                         |
| ------------------------------------------------------------------------ | -------------------------------------------- |
| [Obsidian Forums Showcase](https://forum.obsidian.md/c/share-showcase/9) | The source for several of the above snippets | 


Created Date: September 7th 2021 (12:02 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
