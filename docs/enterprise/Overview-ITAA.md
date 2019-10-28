# IBM IT Architect Assistant User Guide
**IBM IT Architect Assistant** (Architect Assistant) is a simple web-based tool to assist an Architect in designing a solution by finding the best/relevant/potential architectural solutions and/or patterns and customizing them for specific needs.

At its core, **Architect Assistant** is both a solution model authoring tool as well as a searchable repository of authored solution architectures/models.

The Documentation is organized in the following sections:
- [Terminology](#terminology)  
- [Getting Started](#getting-started) 
- [Major sections: Workspace and Search](#workspace-search-and-dashboard)
- [Search](#search) 
- [Architecture Cards](#architecture-card-elements)  
- [Workspace Details](#workspace---private-collaboration-and-bookmarks)
- [Basic authoring of architecture artifacts](#authoring)
- [Reuse, Copy and Paste](#copy-and-paste)
- [Import and Export](#import-and-export)
- [Collaboration](#collaboration)
- [Detailed authoring - by artifact type](./Artifact-Details-ITAA.md) 


## Terminology
Before diving into details about Architect Assistant it is important to understand some key terminology used throughout the documentation.  

**Logical Asset Repositories** -- Today there are 3 logical repositories of architectures: **Public**, this contains curated, read-only architectures that can be discovered via search; **Private**, every user has a set of private assets that they own, that by default are read-write and not discoverable by other users; **As-Is**, any private asset can be set as discoverable (marked As-Is) by the owner. As-Is assets are searchable and anyone following the link to an As-Is asset will be added as a "Viewer" collaborator.  

**Collaboration Roles** -- All architectures have an **owner**. For private (and thus also As-Is) architectures there can be a set of collaborators. A collaborator is a user that has a set of permissions for the architecture. The roles are:  
- **Viewer** -- has read-only access to the architecture  
- **Editor** -- can make changes to any content of the architecture  
- **Admin** -- is an editor that can also change the role of any collaborator.  
- **Owner** -- is the only user that can delete the architecture.  
An owner can explicitly "invite" collaborators and assign corresponding role to each. There also is the ability to create and manage groups of users for purpose of collaboration. (Note for all **Public** assets, all users are implicitly **Viewers** and no one is an Editor or Admin).  

**Artifact** -- An architecture (asset) is comprised of a set of artifacts that are typed. The standard set of artifacts are displayed in the architecture's Table of Contents (**TOC**). Many of the artifact types can have 0 to n **artifact instances**.  Examples of artifacts include Business Challenge, System Context, Functional Requirement, etc.  Most of the artifacts correspond to a technical work product.

**Shared Elements** -- The building blocks of an architecture are a set of architectural elements. Each of these elements have a specific type along with a set of attributes. Many of the architecture elements contribute to and are referenced within multiple artifacts and artifact instances. As such it is important that these elements are shared (i.e., by reference). The implication is that each shared element must have a unique name within the architecture. To enforce this constraint the tool will flag as an error anytime a new element is created and given a name already in use in the architecture.  This error forces the user to either bind to (reference) the currently existing shared element or if the user needs to reference a different architecture element, supply the new element with a unique name. For example, adding a new Logical Node to an AOD IT System View instance and giving it the name **Security Services** when a Logical Node with that name already exists (perhaps on a different diagram instance) results in an error (duplicate name error). To resolve this the user can click on the **Select from existing** button and point to the existing Logical Node, indicating you are reusing the same element. Alternatively a different (unique) name can be assigned. Either approach will remove the error.

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide-v11))


## Getting Started

Getting started with Architect Assistant depends on your usage intent. The most common usage intents are:  
- Search for and review an existing and accessible architecture. This scenario may be to support an architect understanding about what assets are available and/or specific details about any particular architecture.  
- Author a new or existing architecture.  

In each case the fundamental construct is an architecture. An architecture is comprised of a set of interrelated artifacts many of which share a set of elemental architecture building blocks (or elements). The best way to visualize this structure is through Architect Assistant's Table of Contents for any architecture.

![Architect Assistant - Table of Contents](../../images/CA-TOC-2.1.png)

This standard structure directly supports the details of a specific solution architecture, but can also be used to manage a set architecture building blocks which are described as a **architecture pattern** within the tool.  This may be a library of reusable standard *parts* or a more integrated set of reusable content.  These *architecture patterns* typical get used as a source resource for copying a subset of the pattern asset into a target architecture.  This is useful to be able to consistently use these building blocks in multiple architecture

An architecture is what is addressable via search, can be edited, copied or deleted. In Architect Assistant, an architecture can be selected via a **card** that will appear in either your workspace or in the search area. 

## Workspace, Search, and [Dashboard]
When a user logs into Architect Assistant they are presented with two (2) or potentially three (3) tabs.  
![Main Navigation](../../images/main-navigation-ITAA.png)

The two primary tabs (sections) of the tool are **Workspace** and **Search**. **Search** is used to discover existing assets found in the Public and As-Is repositories. **Workspace** is where a user has access to a specific set of architectures. If a user is the owner of 1 or more architectures that are discoverable via search, then the **Dashboard** tab will be available.  The Dashboard provides information about who has made copies of the user's "published" architectures. 

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

### Search
When a user navigates to the Search page, they are presented with the **top trending public assets** along with a search bar.  

![Search Page](../../images/ITAA-search.png)

Currently the search is made against a set of keywords and tags as well as the text of the Title of the architecture.  Each architecture can have a set of tags associated with them. These include the applicable **Industry(ies), Technology(ies), and Tags**.  



![Basic Architecture card - Search result](../../images/asset-card-search.png)



In the above image, it can be seen that the tags are displayed on the architecture **card**. The corresponding search terms can be typed into the search text box and/or can be selected from the Catalog.

![Search Page](../../images/ITAA-search-catalog.png)

The architectures returned in a search result set are either **public, readonly (curated)** assets or are **private, As-Is** assets. 

### As-Is
Any user of the system can choose to have a private architecture that they own, discoverable via search. This property is enabled/disabled via the architecture information page.  The information page is accessible via the info toolbar button of an open architecture. This architecture information page is where an asset owner can change the architecture name and other attributes such as client, opportunity number, tags, etc.

![Info toolbar icon](../../images/Info-toolbar-button.png)

If you are the architecture's owner and you currently have edit control on the architecture, the **Share As-Is** slider control is enabled to turn **On** or **Off**.  When on, there is a "shareable" URL available for copy.

![Share As-Is control](../../images/As-Is-Control.png)

This shareable link has a special format. The URL will be of the form &lt;Architect Assistant server&gt;/architectures/**Social**/...  When a URL of this form is used to access the identified architecture, two actions occur prior to redirecting to a URL where **Social** is replaced by **Collaboration**.  First a check is made to see if the target architecture still has "As-Is" property enabled. If not, the URL is rejected. If the architecture does have "As-Is" property enabled, a check is made to see if the logged in user is currently a "collaborator" for the target architecture and if not, they are added as a *Viewer* on the architecture's collaboration team. Then the URL is rewritten and forwarded, resulting in opening the architecture from the user's Collaboration Workspace tab.

Any architecture returned via search will have a minimum of "Viewer" access for all users. Thus the architecture card's additional menu will include **Copy**.  This permits the user to create a complete copy of the architecture by supplying a new unique name for the resulting Copy.

![Create a personal copy](../../images/copy-architecture-form.png)

This is a fundamental operation to support rapid reuse of an asset. Once you have created a personal copy it can then be tailored to meet your needs. Many of the public, curated architectures are Reference Architectures or Reference Solutions, ideal for tailoring and generating a specific solution architecture. 

### Search Filters

The result of a search produces a set of cards for the architectures matching the search keywords. There are a set of filters available to select a subset of the returned search result. These include filtering between showing curated vs. As-Is architectures. It also includes selection of asset type (Solution Architecture, Reference Architecture or Architecture Pattern).

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

### Architecture Card Elements

In all contexts an Architecture card has many of the same elements displayed. The architecture name is prominent on the top left with an "additional menu" identified via the ellipses **...** in the upper right corner. The color of the top half of the card along with the text and icon at the bottom of the colored section identify the type of asset. In the bottom half of the card (when you are not hovering over it), you will see a set of optional tags. And at the bottom you may see 0-2 *metrics* displayed, depending on context and whether or not the architecture is As-Is or a public curated architecture.

![Basic Architecture card - Search result](../../images/asset-card-search.png)

In the card above, you see a public *reference architecture*. As such there are two displayed metrics. The first, *copied* will be associated with both public assets and As-Is assets. It shows the number of unique copies that have been made by users. The second metric, *Rank*, is unique to public assets. Rank is computed daily and rank orders all public assets based on the number of copied made during the past 30 days. So in the example, 9/19 indicates this architecture had the 9th most number of copies made in the past 30 days when comparing all 19 public assets. Non-searchable architectures will not have any metrics computed or displayed on the corresponding architecture card.

When you hover over an architecture card, the display changes.

![Architecture card - hover view](../../images/asset-card-hover.png)

The display will provide the architecture name and then two buttons, **Open** and **Quick View**. Clicking on **Quick View** opens up a summary panel on the right side of the browser. This quick view will include Type, Name, Tags, the Overview text and a list of the populated Artifacts.  If this is a private asset, the information about the owner will also be displayed.  The bottom of this Quick View is the **View Detail** button which performs the same operation as the **Open** button on the main card.

Clicking on **Open** will then open the architecture, displaying the Table of Contents (TOC) on the left side and the details of the selected artifact (selected in the TOC) in the main section. By default, the asset opens to the **Overview** artifact. When you open an architecture, you may open it in View mode (readonly) or in Edit mode. Opening in Edit mode at a minimum requires being an Editor or Owner of the corresponding Architecture.

### Typical Use Case from Search

In general, if you choose to open an architecture discovered via search you will open in **View mode**. And most will use this detail viewing as an opportunity to decide how they wish to use the asset. When an architecture is open on the primary TOC view (i.e., not within an artifact instance), there are a set of toolbar buttons available on the upper right part of the display, immediately under the Workspace and Search tabs. Two of these are more commonly used while reviewing a discovered architecture. 

![Bookmark and Copy toolbar buttons](../../images/bookmark-copy-toolbar-buttons-2.1.png)

First, the bookmark button, which allows you to add a link to this architecture to your bookmarks to either locate it more quickly later or to reference the asset for fine-grained copy and paste. Second is the copy button that allows you to create your own **private read-write** copy of the complete architecture. If you choose to create a private copy, you will supply a unique architecture name and optionally provide client name, opportunity number and tags.  Once the copy has been created you will be taken to your Private Workspace view where you can then open this newly created copy.

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

### Workspace - Private, Collaboration, and Bookmarks

The Workspace is an area in which a set of Architectures, referenced by the user, can be located. The default workspace tab, your **Private Workspace**, maintains all architectures owned by you. These are read-write assets that will typically be associated with specific solution designs that you are working on. The default sort order is by name, you can temporarily select to sort by most recently modified. You can also filter the list of architectures visible by selecting 0 or more Client Names and 0 or more Tags. This makes it very easy to locate specific architectures within your workspace.

![Main Navigation](../../images/main-navigation-ITAA.png)

The second workspace tab is labeled **Collaboration**. Here you will find all architectures that have been shared with you. These are architectures owned by someone else and they have either explicitly shared access with you by adding you as a collaborator or they have chosen to share the architecture anonymously by marking it **As-Is**. Once you follow a link to open an As-Is architecture you are immediately added as a Viewer on that architecture. 

How you work with architectures in the Collaboration tab is dependent on the nature of the sharing. An owner may share access to an architecture to either provide you with awareness or to elicit feedback (review and/or comments). There is an explicit capability whereby you can leave comments on any architecture you have access to.  The comments are associated with an artifact type and are tagged with your email address (as comment author) along with a timestamp of when the comment was made. 

You might be given **Editor** rights to an architecture whereby you can become a co-author on the architecture, sharing a single **pen** indicating who has edit control at any point in time. Lastly, by having access (of any kind) to an architecture, provides you with the ability to create a private copy which you can then independently customize for your own purposes.

The third workspace tab is labeled **Bookmarks** and provide links to discoverable architectures that you have chosen to bookmark.  These are particularly useful to reference an asset which you will use to copy from. Generally you will be copying a small portion of the architecture, e.g. as an interaction pattern from one of its diagrams.

Back on the private workspace where you find the set of architectures you own, there are a set of options available to you on the "more" **...** menu. Always available on all architectures everywhere is **Copy**.  This requests a new copy of the architecture to be created, owned by the invoker. Scenarios for copying include implicit versioning or starting a new project with an initial starting point. In addition, as an owner of an asset you will have the ability to select **Delete** off of the same menu. Finally, in the current release, if you are and editor or owner of an asset and there are at least 2 editors, then this menu will have an item to control access to edit privileges. The menu will either contain **Get pen and lock** or if you already are the designated editor (holder of the pen) the menu item will be **Return pen** whereby you can relinquish editing control. 

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

## Authoring

If you have edit control, when you open the architecture you will be able to author any of the contained artifacts.  Earlier we showed the standard TOC for an architecture. Let's classify the individual artifacts to help setup common user experience for authoring. First, there are artifacts that have exactly one instance and thus edit them directly and another set of artifacts in which you will edit individual artifact instances. The Overview, Business Challenge, and System Context each only have a single instance. So when selecting these artifacts in the TOC, the directly editable content appear on the right side with the ability to **save** your changes. Both the Overview and Business Challenge are rich text based artifacts, so the "editor" is a lightweight rich text enabled text box. The System Context is a diagram and thus the editor is the tool's MxGraph-based diagram editor. All other artifacts support multiple instances, so selecting such an artifact (for example Functional Requirements) will lead to the right side being a list (card style) of the currently existing instances plus a card-like control (**Plus sign**) that you can click on to create a new instance.

![Artifact Instance List](../../images/artifact-instance-list.png)

Clicking on the Add instance button will prompt for the minimal set of properties to uniquely define the instance (usually just name, but sometimes also an id). From a basic user experience perspective, there are four types of artifacts and therefore artifact instance types: 1) Form-based text artifacts, 2) Free form text artifacts, 3) Diagram artifacts, and 4) a diagram overlay artifact. 

### Form-based text artifact types
The first type includes: Use Cases, Functional Requirements, Non-Functional Requirements, Architecture Decisions, Architecture Principles, Risk, Assumptions, Issues, and Dependencies.  These typically would be viewed outside the tool as tables each with a very specific structure (attributes) based on the information represented by the artifact type where each row (or record) corresponds to a single artifact instance. Since the editor is form-based, you will have individual fields (attributes) editable by their own UI control.  In some cases, an attribute value may be a reference to an architectural element, typically presented via a drop-down list.

![Form Based Editor - Functional Requirement](../../images/fr-editor-form.png)

### Free form text artifacts
The second type of artifact from a UI perspective includes **Notes**. Notes are intended to easily allow any miscellaneous content to be attached or associated with an architecture that otherwise doesn't have a structured artifact prescribed. Each Note is a standalone entity which includes Rich Text (including embedded images) along with file attachments. Here the editor is a specialized rich text editor. There is an option to create (manage) a set of labels or tags that can then be added to Notes. The visible Note instances can then be filtered based on the applied labels.

### Diagrams
The third type of artifact provides the richest user experience. These are specialized diagram types all of which are delivered by a custom *MxGraph-based* diagram editor. MxGraph is an open source framework that delivers client side JavaScript diagramming capabilities.

![System Context Diagram - MxGraph Editor](../../images/system-context-diagram.png)

Above is a System Context diagram in Architect Assistant. Let's look at the various parts of the editor. 

The top two rows include the menu and toolbar controls.  These are only present when the diagram is open in edit mode. If you are just viewing a diagram, these elements won't appear on screen (including the explicit save button). 

Next on the left hand side you will find a set of drawing palettes. These supply the elements that can be added to the drawing canvas (the main part of the editor and where the diagram resides). In Architect Assistant, the top most palette will have a name that specifies the type of diagram, and includes all of the *architectural elements *that can be added to the diagram.  In this case the **System Context Palette** includes a Human Actor symbol, an IT System Actor symbol, a Target System symbol and a Connector symbol. Each of these symbols, when added to the diagram, will be associated with an architecture element (core model element) each of which have an associated set of attributes dependent on the element type. 

The attributes for a model element appear within the Attribute tab of the **format panel** typically visible to the right of the diagram (canvas).  For example, in the diagram above you see the purple IT System symbol, named DDoS System, selected. Since the selected item represents an architectural element, there is an Attributes tab on the format panel that displays the attributes of the associated architectural element. In this case the type of architectural element is an **Actor** with Name, *DDoS System*; Description, "*new description imported*"; and a Type of *IT System*.

In addition to the diagram specific palette, there will always be an *Annotation* palette.  This palette contains a set of common shapes. Adding a symbol from the annotation palette onto the diagram just adds that shape to the diagram. This shape is NOT associated with any architectural element.  Thus annotations are just used to add style to the diagram.

Below is the same System Context diagram, with the pink cloud shape selected. Note that the format panel only shows the Style, Text and Arrange tabs; the Attributes tab is missing.

![System Context Diagram - Annotation](../../images/annotation-symbol-selected.png)

A few diagram types have additional palettes available beyond the diagram specific palette and the annotation palette. Those will be detailed in sections specific to those diagram types.

In general you add something from a palette onto the drawing canvas via a drag operation. Select a symbol and drag from the palette to where you want to place it on the canvas. If you just click on a symbol, the symbol will get added at a random location on the canvas. All non-line/connector symbols have a "bounding box" which includes anchor points where connections can be made by the endpoint of a line/connector symbol. When connecting the end of a connector to a symbol you will want to see a "green" connection dot or green bounding box outline appear before releasing the mouse to make the connection. Otherwise, you will have just moved the line's endpoint without accomplishing making a connection.

![Connecting symbols](../../images/making-connection.png)

The start state for the above graphic is a connector (highlighted in red along with error message) whose one endpoint is not connected. The arrow head end has been grabbed using the mouse and the mouse moves over the edge of the target system. When positioned properly, you see the anchor points (the tiny blue 'x's), and the "hot green dot" shows a selected anchor is active. Releasing the mouse will make the connection (as per earlier version of the diagram) and the error will be removed.

#### Quick Connect
In the case of the System Context diagram (and many more of the diagram types), there is exactly one type of connector supported on the diagram. In these cases it is not necessary to explicitly drag the connector from the palette onto the canvas and then connect each end. Instead, with nothing selected on the diagram, hover the mouse over the bounding box for a symbol you which to have as the starting point for a connector. Once you get the green outline or green circle, click the mouse and then move over the boundary of the destination symbol. Once you get the destination symbol (outline or circle) to turn green, release the mouse.  This will add the connector while connecting it at the same time. 

#### Style and more
The MxGraph framework provides a rich set of formatting tools to help you make the diagram look however you would like. Many of these are self explanatory and are available directly in the 3 separate tabs of the **format panel**: Style, Text, and Arrange.  

The Style panel let's you apply style to whatever element is selected.  So if it is a line, the choice of line style (dash, solid), endpoint style (arrow type), thickness, color, etc.  You can also adjust whether the line is straight, curved, orthogonal jogs, etc.  Also if two lines are selected (which cross), you can set the style for the line crossing.  If the symbol is a shape then things like fill and outline color, etc are available to be changed. 

The style panel also includes an Edit Style button which provides access to the basic properties of the shape for instance the base shape type, whether it is a container, whether the shape is represented by an image (icon) - thus exposing an "edit image" control, etc. Knowledge of the "Edit Style" and the corresponding style commands are most important to be able to replace the style of one symbol with the basic style of some other symbol in the system. 

**Tip:** For instance, you might want to have your Target System represented by an image in the System Context diagram. One way to do this is copy the style from a Logical Node from an AOD IT System View and paste that into the Style for the Target System and then edit its image. This approach of identifying and applying a style from a symbol from any diagram to a different symbol in the same or different diagram type can universally be applied. 


The Text panel let's you modify the text properties for the selected item.  This includes things like positional alignment (vertical and horizontal), font family and size, bold, italics, and underline, word wrap, font color and background color.

The Arrange panel allows you to position the layering of stacked items (to front, to back), the size of symbols and the position relative to the canvas, and flip and rotate symbols. Of perhaps most value is being able to select multiple symbols and align and space them.

**Tip: Grouping** There are two separate approaches to "grouping" elements in diagrams: 1) containment (parent / child) and 2) Group.  You can define any symbol as being a container and optionally collapsible, for example Subsystem, Location, OMLocation.  This is done within the Style panel by clicking on **Edit Style** and  adding properties, "container=1;" and "collapsible=1;". Any symbol with container=1 will be highlighted when another symbol gets placed within it.  Then moving the parent (container) will move it along with all its contained children as a group.  You can also select multiple independent symbols, and then on the Arrange panel, click on **Group/Ungroup** to make them act like most drawing tool symbol groups.

#### Undo, Save, and Auto-save

Architect Assistant is a single page application (written in Angular). In this environment all of your edit operations are being handled within the Browser via the MxGraph javascript library. As you make changes, MxGraph is managing a "stack" of changes you make allowing you to "undo".  At the same time, nothing is being persisted to the back-end until a "Save" is performed.   Thus, if you were to make several changes and then close your Browser your work will be lost. The Save button, in the upper right corner of the MxGraph editor, will write-back the current state of the diagram (and underlying architecture model) to the back-end for saving. 

When a diagram is saved, the undo "stack" is cleared. Thus, undo is only available between "saves". 

In addition to the explicit save, Architect Assistant will "**auto-save**" your diagram every 5 minutes.

#### Model validation rules and Auto-save
Each diagram type has a set of validation rules associated with it to help maintain a valid architecture data model.  For example, a System Context diagram, must have 1 and exactly 1 Target System present on the diagram. In addition, all connectors must have 1 endpoint connected to the Target System and the other endpoint connected to an Actor. In other words, connectors are not allowed to connect two Actors together. Also while editing this diagram, there are some architecture-wide validation that is also being enforced, e.g., each of the Actors and Target system must be unique (unique name) within the Architecture.  Attempting to name a symbol/element with a name that already exists will generate an error. In the case of the System Context diagram, all of this validation can (and is) performed by the front-end logic, i.e., the UI. In other diagram types, there are some validation rules that can only be fully assessed by the back-end during a "save" operation. The user experience of these types of validation checks, is that you won't see the validation error message until the save happens. This is particularly odd for the user when the application "auto-saves". In this case you might not be actively doing anything in the editor, auto-save occurs, and the back-end detects a validation error and you likely get a "save failed" along with the validation error.

**Tip**: When starting to work on a new diagram type, you are advised to explicitly save after any noteworthy change to the diagram so that you can better understand any back-end validation errors that may get triggered.

#### Diagram level attributes
In any diagram in Architect Assistant, with no symbol selected, the Attributes panel will present the attributes of the diagram itself.  This is where you will see the diagram name, a diagram description (which is where you can document the intent of the diagram), and potentially one or more diagram level view controls.  One common view control is turning on/off displaying of connection names on the diagram.

### Diagram Overlay artifacts
The fourth artifact type from a user experience basis is a diagram overlay, **Usage Scenario**. The usage scenario provides a way to overlay a "story" or "flow" onto an existing Architecture Overview diagram. What is uniquely authored in a Usage Scenario instance, is this story. When a new instances is created, you must first specify the AOD diagram it is based upon (selected from a list) along with the scenario name.

In the editor for a usage scenario, there are no drawing palettes. Instead you are provided with a way to select a "connector" from the underlying AOD diagram and then associate it with one or more *steps*. A step has two attributes, name and description. Further the name must be a single token and either be all numeric or all alphabetic. (The idea is the steps have names: 1, 2, 3, ... or A, B, C, ...).  The description is used to tell the "story segment" associated with the step. When a "connector" is selected, all currently defined steps for the usage scenario are presented along with a checkbox to select or deselect each one. The usage scenario editor will place "step circles" on the selected connector for each associated step. When given the option to select the associated steps, you are also presented with the ability to create a new step.

In addition to adding and associating steps to connectors, you can also select any other (non-connector) symbols and "disable" them.  The editor then will "gray-out" these disabled symbols.

![Usage scenario](../../images/sample-usage-scenario.png)

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

## Breadcrumbs and Navigation

Navigation within the tool is managed in several ways. From a top-level landing pages you have the two-level navigation tabs presented as seen here.

![Main Navigation](../../images/main-navigation-ITAA.png)

Within an architecture there are two different navigation mechanisms depending on if you are within an artifact instance. When you are not within an artifact instance, the TOC provides the way to select an artifact type to view or edit. In or out of an artifact instance, there is a "breadcrumb" that supports navigation to all levels of the tool. If a particular level of a breadcrumb represents multiple options at that level, there is a "down arrow" that will present you with the available elements at that level to select and navigate to.

![Breadcrumb Navigation](../../images/breadcrumb-navigation.png)

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))



### Copy and Paste

With any documentation tool you want to be able to quickly reuse elements. This is logically a copy and paste operation. In some of our how-to videos, we describe both fine-grained and coarse-grained reuse support within Architect Assistant.  



### Course-Grained Reuse

The **copy** operation at an architecture level (either via the '...' menu on the asset card or via the *copy* toolbar button within any architecture) is the purest form of course-grained reuse.   Take an architecture and make a new copy that can be customize independent of the source. This is where it is critical that we build and share (either globally via As-Is or published asset or via explicit collaboration with peers) architectures that form a good foundation for starting to build new solutions.

### Fine-Grained Reuse

Contrasted with coarse-grained reuse is the desire to reuse individual architectural elements, artifact instances, and/or partial artifact instances (e.g. patterns).  These are various degrees of fine-grained reuse.  

Within each artifact type there is the ability to copy an existing artifact instance within an architecture, name it as a unique instance and then customize that new artifact instance.  The complexity of the copy depends on the underlying complexity of the artifact instance itself.  For example, copying a Functional Requirement is much less complex than copying an AOD IT System View.

What about fine-grained copying between architectures? Today there are two approaches based on the type of artifact. For "text-based" artifacts, the most streamlined copy-and-paste is actually a bulk Export / Import operation (see next section on Import and Export). You can export a set of artifact instances from one architect to an Excel Spreadsheet and then import those artifact instances (possible filtered and edited while in spreadsheet form) into another architecture.  

For diagrams, you likely will only want to copy part of a source artifact instance (diagram). To suport this,  Architect Assistant provides the **Resource** menu.  Within that menu there are three choices: Open from Private, Open from Collaboration, and Open from Bookmarks.

![Resource copy from menu](../../images/resource-copy-menu.png)

This allows you to select from 3 sets of architectures to copy from. Open from Private will list all of your private workspace architecture, Open from Collaboration will list all of the architectures in your collaboration workspace, while Open from Bookmarks allows you to access public assets that you have bookmarked. The user experience is then to select the architecture you want to copy from. Once an source architecture is selected you will be present with the list of architecture artifact instances that match the artifact type of your target diagram. (Only copying between the same artifact type instances is supported.) You then will select the artifact instance and that instance is opened read-only as an addition tab within the editor. You can then select a portion (or all) of the content of the source diagram and select copy, then click on the tab of your target diagram and select paste.

![Target diagram with read-only source diagram tabs](../../images/source-target-diagrams.png)

Note, it is critical that the paste succeeds. So the tool does not allow for name conflicts. So as the elements are copied from the source to the target, if an element's name matches an element in the target architecture, the "pasted" element will be renamed using a "Copy of" prefix. If these "copied and renamed" elements align with an element in the target architecture you can then use the "Select from existing" option to properly integrate the pasted content.  For example, you are copying a set of Logical Nodes and connections representing a ETL pattern, and one of those nodes is named "Product Data Warehouse" and a node representing that same content already exists in the target architecture, initially on paste you will have a new Logical Node named "Copy of Product Data Warehouse".  If that node didn't already appear on the target diagram you could select the "Copy of Product Data Warehouse", click the Select from existing button and locate and select "Product Data Warehouse". This now "connects" the new set of elements with the existing architecture.  It also produces an "orphaned" Logical Node (not in use) with the name Copy of Product Data Warehouse.  Note if the Product Data Warehouse node was already present on the target diagram, rather than use the Select from existing, you would move the connection endpoints from the Copy of Product Data Warehouse and connect them instead to the pre-existing Product Data Warehouse and then delete the extra "Copy of Product Data Warehouse" node from the diagram.

[In an upcoming release, you will be provided with an option of how to handle the paste operation for each element which has a name conflict with the target architecture.  This will allow you to have the current behavior (create new element with name "copy of …") or to define how the element is "merged" with the target architecture's element with the same name.]

In a mechanism very similar to the Resource menu, you can copy text-based artifact instances, e.g., an NFR or a Use Case, directly from one architecture to another. This is triggered on the "Add  <element>" dialog, in the case below, Add Non Functional Requirement.

![copy from another architecture](../../images/CopyFromTextArtifact.png)



Click on the Copy xxx from another architecture to get a selection menu equivalent to the Resource > Copy from menus found on the diagrams.

![Select from architecture type pool](../../images/text-copy2.png)



#### Copy of elements within a diagram

To support users that are used to quickly duplicating a symbol on a diagram to create a new element, a local copy-paste or "duplicate" behaves this way, namely a new architecture element of the same type is created with a new name "copy of <copied from name>". The copy will include the same direct attribute values and any "child" dependent relationship elements will also be cloned ("copy by value") as the source element to keep (duplicate) the same structure.

#### Orphan element clean-up

Through the course of authoring an architecture, various architecture elements will be created and then abandoned (orphaned) and not actually used or referenced.  These elements do not impact the architecture's integrity but can become misleading and annoying.  Most notably if you export an architecture to a MS Word document, then in sections that list all of the elements of a particular type, the orphan elements will be listed.   Also, more significant, is when you are provided with a list of available elements of a type for selection of a relationship, e.g. select from available Physical Components for an "Implemented by" relationship - then that list can become extremely long if there are many orphaned "physical components" within the architecture.   

To selectively remove orphan elements, click on the "trash can (Manage orphan elements)" icon within the architecture.  [Note, this toolbar button will only show if you have exclusive edit rights for the architecture and you are at the TOC level, i.e. not editing an artifact instance. If the architecture has multiple collaborators that are editors, then you must obtain the architecture lock (Get pen and lock).]

![Manage Orphan Element button](../../images/manage-orphans.png)

This will bring up the manage orphan elements panel.  Here you can select all, select all by type, or drill down and select individual orphan elements, and then click **Delete**.

![Manage Orphan Element panel](../../images/manage-orphan-panel.png)

## Import and Export

There is a lot of value of having everything associated with a Solution Architecture captured within a single asset that can easily be shared with collaborators. However there are many situations in which an architect would like to deliver a snapshot of the architecture in a different format, not requiring either the online or offline tool. Architect Assistant provides a set of import and export utilities to address these needs. Let's first take a look at the rich set of Export Utilities available. 

![Import/Export Toolbar button](../../images/import-export-toolbar.png)

Above you see the toolbar button to access the import and export utilities. First you select if you want to export or import.  Note there is also a link to an *import template* file to download and modify in order to be able to import from an Excel spreadsheet. Selecting Export and clicking Next will take you to a dialog where you can choose the type of export. There are three* choices presented:
- **Microsoft PowerPoint** - This produces a summary PPTX document containing the major sections of the architecture. This is a good way to quickly get content out in this format to share with others.  Clicking Next will generate the file and then prompt you with a Browser open/save dialog.
- **Microsoft Excel** - This produces a multi-worksheet Excel document (XLSX) that include everything in the model with the exception of the diagram images. In reality, when you click next you are presented with a pick list of "reports" to be included in the export.  There are three groupings of reports, Architectural elements (the key reusable elements in the model), Text-based artifact reports (FRs, NFRs, ...), and Diagram-based artifacts that describe content that appears on each diagram.
- **Microsoft Word** - Today this produces a standard all inclusive Word document.  In the future you will likely be able to select among a set of document templates. **Note**, when you open the downloaded .docx file you will be asked if you want MS Word to update external references during open.  Respond yes to this request to make sure the TOC, List of Figures and List of Tables gets populated. You will also then want to "Update table" for each of this lists after the fact to make sure all of the figure numbers and table numbers are updated correctly.

If you choose Import you are presented with one* choice:
- **Microsoft Excel** - This expects the import file to conform to a standard import template that you can download via the link. This import only supports the first two report groups from the Excel export utility. This allows you to add or modify shared architectural elements and well as all of the text-based artifacts.  This is a great way to manage working with FRs, NFRs, Use Cases, Architecture Decisions, etc. as spreadsheet data and import / update in a timely manner. 

The template includes a worksheet for each architecture element or artifact instance type. Here there are columns for all attributes of the items to be imported. There is also an extra column, *Previous Name* that can be optional used to indicate you wish to change the name of an existing element.

Import by default supports *Add*, *Update*, and *Rename*. The parser checks the "Name" and "Previous Name" columns. Typically the Previous Name entry will be blank, in which case if a row name matches an existing element, all attributes are overwritten with the values found in the import spreadsheet. If name  does not match any existing elements, a new element is created. If Previous Name matches an existing element then that element is renamed and updated.

In the future, expect to see additional functionality added to the existing import/export utilities including support for other external formats.

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))



## Collaboration

Let's take a step back and realize that Solutioning tends to be a team sport.  Even if there is a single architect working on a Solution Design, there are many stakeholders and reviewers.  It is therefore important that the platform (Architect Assistant) effectively support the wide-range of needs for a collaborating team.  Architect Assistant is hosted on a cloud instance. This permits access to all users by their userid. An architecture can be shared with a team (or virtual team) via explicitly adding Collaborators and specifying the access role for each user as well as share implicitly via the ["Share As-Is"](#as-is) making the architecture discoverable (and accessible read-only) via search.  

To explicitly share, click on the share button.

![Share an architecture](../../images/share-button.png)

Here you can see the current collaborators and their role (Admin, Editor, or Viewer).  Click Invite to locate a user or group to add as collaborators.

![Select collaborator](../../images/collab-lookup.png)



Once a user has been selected, choose the role, and click Invite. 

![Choose role and invite](../../images/select-role.png)

In each of these cases, once the sharing has occurred, the architecture shows up on the users' Workspace > Collaboration tab.

A collaborator that has Editor or higher rights has the ability to modify the architecture.  The platform implicitly "locks" the current artifact instance being worked on by an editor.  When you enter an architecture the "Overview" is locked.  Collaborators can see this lock on the (artifact instance) card view and on the architecture toolbar.

![Artifact Instance locked by peer](../../images/currently-edited-instance.png)

It is the pen icon and collaborator's name that indicates this artifact instance is currently being edited by someone else.  Note from the menu you still have the ability to open the artifact instance read-only via selecting **View**.  This same View menu item is available even when an artifact instance is not currently locked.  This allows you to view the artifact and not lock out any of your peers.

![Read only](../../images/select-viewonly.png)

It is also possible as an owner/collaborator with a minimum of Editor role to lock (for write) the entire architecture.   This is done at the architecture card level on the workspace view (either Private or Collaboration).  If currently no one is editing within the architecture you will see the "box" icon on the architecture card.   In this case you will have the ability to **get pen**. 

![Unlocked prepare to get pen](../../images/pen-in-box-get.png)

Once you have acquired the pen, then all other collaborators will only be presented with a read-only view of the architecture.   You can **release pen** to unlock the architecture returning it to default behavior.

![Holding pen option to release](../../images/hold-lock-return.png)

In addition to manipulating a shared asset directly one can author content offline via Excel spreadsheet and import (update) content in bulk. Also, although not direct, one can also edit a copy of an architecture in offline mode (single user mode) and bring that updated content back into the cloud and then use Resource > Copy from to move/copy updated content back into a  master [shared] architecture asset.

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))



## Comments

The comment feature supports architecture reviews. In an open architecture, you will find the comment tool bar button, that will open the comment panel.   

![Comments panel](../../images/comments-panel.png)

This panel let's you select an artifact type (section) within the architecture and review any comments/replies attached to that artifact type. The same panel lets the user create new comments/replies.   The comments are visible to all persons that have access to the architecture (Viewer, Editor, …).

([Back to Top and TOC](#cognitive-architect-user-guide-v24)) 

## Change Log

When collaborating with a team authoring an architecture, it is valuable to be able to understand the change history.  You can review major change events via the Change Log. This does not track the actual change data, but identifies the change action and the responsible party.  To display the Change Log, click on the corresponding toolbar button.

![Show Change Log button](../../images/change-log.png)



![Show Change Log panel](../../images/change-log-panel.png)

([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

## Co-Relationships

Most of the time, you will be reviewing an architecture from an artifact perspective, i.e., you will be using the Table of Contents as a navigation tool to locate a particular aspect or view of the architecture and then open that artifact instance.  It is however, useful to be able to navigate the architecture from a more bottom up approach.  For instance, you are looking at a diagram and find a particular Logical Component, say **Event Services** and then you want to understand what other diagrams does this Logical Component appear on and what other elements are related to (referenced by) this element?  

A new co-relationship feature allows you to explore the relationships within an architecture from the perspective of the primitive architecture elements.  Open the co-relationship panel via the Co-relationship toolbar button.

![Co-Relationship button](../../images/co-relationship.png)

The Co-Relationship Table (panel) displays the architecture elements by type. You can then select an element and drill down and see what diagrams that element appears on, and what other elements it is related to via a relationship property.

![Co-Relationship Table](../../images/co-relationship-table.png)



([Back to Top and TOC](#ibm-it-architect-assistant-user-guide))

