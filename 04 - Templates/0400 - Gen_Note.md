<%* 
var note;
var body;
var struct;
var dest;
var metadata;
var timestamps;

let validTitle = false;
let title = tp.file.title;

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////// Functions /////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////

// Name: getTitle
// Description: Ensure a valid title is supplied, or prompt user for title.
// Rename the created file from "Untitled" to what they've supplied.
// Supports both creating notes from "new note" or "ctrl + click"
async function setTitle() {

	if (await validateTitle(title)) 
	{
		console.log(`Title: "${title}" is valid`)
		await tp.file.rename(title);
	}
	else 
	{
		console.log("The supplied title was invalid.")
		title = await tp.system.prompt("Title of New Note");
		setTitle();
	}
}

// Name: validateTitle
// Description: Checks supplied string (title) against 'undefined' type , null 
// value, empty value and when the type is a string - we validate if it follows 
// the default naming scheme of 'Untitled #' - rejects assignment of any of these 
// cases
// Return: Boolean
async function validateTitle(noteTitle) {
	// if nothing was supplied, try again
	if (typeof noteTitle === 'undefined' || (typeof noteTitle === 'string' && noteTitle.includes('Untitled')) || noteTitle === null || noteTitle === "") 
	{
		console.log(noteTitle.includes('Untitled'))
		return false;
	} 
	else 
	{
		return true;
	}
}

// Name: getNoteStruct
// Description: Accepts the Search Tag (emoji) selected by the user
// and returns the appropriate note name which defines the categories
// body structure
// Return: String
async function getNoteStruct(noteTag) {
	var structName;
	console.log("Getting Struct MD for tag: " + noteTag);
	
	if (tag.startsWith('📕')) {
		structName = "[[0403 - Struct_TTP_Body]]";
		dest = "03 - Content";
		prefix = "";
	} else if (tag.startsWith('🧰')) {
		structName = "[[0404 - Struct_Tool_Body]]";
		dest = "03 - Content";
		prefix = "";
	} else if (tag.startsWith('💡')) {
		structName = "[[0405 - Struct_Idea_Body]]";
		dest = "03 - Content";
		prefix = "";
	} else if (tag.startsWith('📖')) {
		structName = "[[0406 - Struct_Documentation_Body]]";
		dest = "03 - Content";
		prefix = "";
	} else if (tag.startsWith('🗺')) {
		structName = "[[0409 - Struct_Secondary_Category_Body]]";
		dest = "02 - Secondary Categories";
		prefix = "02 - ";
	} else if (tag.startsWith('㊙️')) {
		structName = "[[0407 - Struct_Personal_Body]]";
		dest = "05 - Personal";
		prefix = "";
	} else {
		console.log("You selected an option outside what was expected.");
		console.log("Try again.");
	}
	return structName;
}

// Name: buildNote
// Description: Performs the actual concatenation of our discrete header, body and 
// footer note elements then handles the creation of the note itself.
async function buildNote(title,struct) {

	// Primary Note Elements\
	var metadata = await setMetadata(tag) + "\n";
	var header = await tp.file.include("[[0401 - Struct_Gen_Header]]") + "\n";
	var catHeader = await tp.file.include("[[0408 - Struct_Secondary_Category_Header]]") + "\n";
	var searchTag = "Search Tag: #" + tag + "  \n\n";
	var pageTitle = "# [[" + title + "]]  \n";
	var body = await tp.file.include(struct) + "\n"
	var resources = await tp.file.include("[[0402 - Struct_Gen_Resources]]") + "\n";
	var timestamps = await setTimestamps();
	
	console.log("Is the passed struct a complete template?");
	//TODO: 
	// Include logic to facilitate kickoff template etc
	// move resulting note to 05 - Personal
	if (!(await isCategory(struct))) {
		console.log("Should we link to the struct that was passed?");
		if (await ShouldLink(struct)) {
			console.log("linking it");
			// include header if the note should be linked
			note = metadata + header + searchTag + pageTitle + body + resources + timestamps
		} else {
			console.log("not linking it for reasons");
			// do not include header 
			note = metadata + searchTag + pageTitle + body + resources + timestamps
		}
	} else {
		console.log("the struct is a template");
		// if template, include only its contents
		note = catHeader + searchTag + pageTitle + body
	}
}

// Name: setMetdata
// Description: References templater file fields to build and assign the metdata
// element which will prefix all content files and permit dataview quering
// Returns: String
async function setMetadata(inTag) {
	var metadata = "---\ncreation date: " + tp.file.creation_date('MMMM Do YYYY') + "\nlast modified date: " + tp.file.last_modified_date('MMMM Do YYYY') + "\naliases: []\ntags: #" + inTag + "\n---\n";

	return metadata;
}

// Name: setTimestamps
// Description: Builds the timestamps element appended to note pages as they're built. Includes the definition of the Modified Date dynamic element which is updated when the page is edited and shown at the time of the page being rendered in preview mode.
async function setTimestamps() {
	var timestamps = "\nCreated Date: " + tp.file.creation_date('MMMM Do YYYY (hh:ss a)') + "\nLast Modified Date: " + tp.file.last_modified_date('MMMM Do YYYY (hh:ss a)');
	
	return timestamps;
}

// Name: isCategory
// Description: Determines whether or not the struct is related to a category
// by its name containing "category"
// Returns: Boolean
async function isCategory(struct) {
	// dont build out template elements, just reference
	if (struct.toLowerCase().includes('category')) {
		console.log("yes");
		return true;
	} 
	console.log("no");
	return false;
}

// Name: shouldLink
// Description: Determines whether or not the Struct_Gen_Header should be included
// on a new note based on a blacklist of struct names kept here.
// Returns: Boolean
async function ShouldLink(struct) {
	
	var dontLink = false;
	var dontLinkTerms = ["personal"]
	
	for (const structRoot of dontLinkTerms) {
  		console.log("Is " + structRoot + " in " + struct.toLowerCase() + "?");
		if (struct.toLowerCase().includes(structRoot.toLowerCase())) {
			console.log(structRoot.toLowerCase() + " was found in " + struct.toLowerCase());
			var dontLink = true;
		}
	}
	
	if(dontLink) {
		return false;
	} else {
		return true;
	}
}

//////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////// Main //////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////

// Present selection of Search Tags to user
let tag = await tp.system.suggester(["📕 (TTP)", "🧰 (Tool)", "💡 (Idea)", "📖 (Documentation)", "㊙️ (Personal)", "🗺 (Secondary Category)"], ["📕", "🧰", "💡", "📖", "㊙️", "🗺"], true) 

// Ensure the user isnt supplying an undefined or untitled note name
await setTitle(title);

// Get the Struct associated with the Search Tag selected
struct = await getNoteStruct(tag);

// move file to appropriate corresponding folder
await tp.file.move(dest + "/" + prefix + title);

//build the note
await buildNote(title,struct);
%><%* tR += `${note}` %>
