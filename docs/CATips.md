# Tips for success with IT Architect Assistant

This part of the User's Guide is intended to highlight common questions and challenges new users to IT Architect Assistant tend to run into along with supporting guidance.

## Common Topic Areas

### Unique Shared Architecture Elements within an Asset

Within each IT Architect Assistant asset / architecture there is a set of shared/reused elements. Not all element types are reused across the architecture but most are, including:

- Actors
- Logical Components
- Deployment Units
- Physical Components
- Logical Nodes
- Physical Nodes
- OMLocations
- Entity
- Relationship

What does it mean for an element type to be shared across the architecture? For one, any element of such a shared type must have a **unique name** within the architecture itself.  Thus if you attempt to "create" a new element within an architecture whose name is a duplicate of a same type element already present within the architecture, you are presented with an **Error** (duplicate name).  Note: This most often occurs when adding a new element using a default icon on a diagram (from the diagram specific palette). In this scenario the element is assigned an initial default name.  

If you know you are going to reuse an existing element, **use  the list available in the [appropriate "Existing <element type>" palette](./enterprise/Overview-ITAA#existing-element-palettes) instead**. Explicitly grabbing an existing element will directly reuse that element within the current artifact instance. Should you set the name field resulting in a duplicate name error and you determine your intent is to reuse an existing element by that name, click on the corresponding [**"Select from existing"** button  or link](./enterprise/Overview-ITAA#bind-to-existing-element) to get the opportunity to bind to an existing element.

The other impact is starting to reuse an element on a different diagram and then reverting to a mindset of think this is a drawing tool.   For instance, you make a copy of a diagram within the same architecture.  Note at the start there are two separate diagram but each contain the same set of base architecture elements. Then you decide to rename one more more elements in the copied diagram, starting to reuse the look-and-feel, but intending to capture different content. Renaming an element in the second diagram ALSO renames the element in the original diagram.   The name is part of the architectural element (not an artifact of the drawing icon).   So quickly you could start to mess up the original diagram thinking you are saving time!

#### Shared elements, back-end/model save and orphans

When explicitly creating elements or when implicitly creating as part of a cross-diagram "paste" operation (e.g. when using Resource > copy from menu), initially the newly name item is only known in the front-end (Browser Javascript). Thus, correcting names such as reusing shared elements in the editor prior to saving, will prevent temporary named elements from being added to the architecture model. However, anytime a save occurs (either explicit or auto-save) and named element present in the current editor will be saved to the back-end model.  

So what does this mean and how does it impact your architecture/solution model? Let's take a concrete example. In a AOD IT System View instance, you create a new Logical Node and name it **Messaging Hub**. Later (after a save) you realize that this node really should reuse an already existing Logical Node named **Messaging Engine**.  To fix this, you select the Messaging Hub element on the diagram, click **Select from existing** from the bottom of the Attributes panel and then select **Messaging Engine** from the selection list. Then you click **Save**.   You have fixed this diagram so it, like other artifacts instances are all referencing the **Messaging Engine** Logical Node.  But the back-end/model still has a [now] unused Logical Node named **Messaging Hub**.  This is what is known as an **ophaned element**.

What is the implication of this orphaned element? For one thing it will appear in all lists and menus within the architecture as an available Logical Node for reuse. If you have lots of orphans that you don't ever intend to actually reuse within the architecture, then those lists become cumbersome and confusing.  Also, if you export to a Word document, these "unused" elements will show up as Architecture-wide elements. You can remove these orphan elements via the [**Manage orphans** panel](./enterprise/Overview-ITAA#orphan-element-clean-up) (you will have to have explicit write-access to the architecture to actually delete orphans). Note, there are scenarios when you don't want to do this "clean-up" such as when you import a set of elements via Excel import that you intend (eventually) to use within your architecture. Even so, you will likely want to at least review the list of orphaned elements prior to an Export (at least either MS Word or MS Excel).

#### Model Reviews and Not quite orphans

Many times, particular in a pre-sales setting, our architectures are very lean and focused on just a couple of artifact instances. And in those settings, model consistency (same named elements, i.e. shared/reused elements, where appropriate) is easily eye-balled and you probably don't care about orphans unless you are sharing an export document. However, in most other settings, it can be hard to make sure you are consistently representing the architecture across all of the artifact instances. 

A best practice is to create a [**full MS Excel export**](./enterprise/Overview-ITAA#export) of the model and **review** the contents. Here you may discover that you have multiple names for what is intended to be a common element, e.g. two Logical Components, one named **DataLake** and another named **Data Lake**.   (Note that space makes a difference!)  Such a review can point out the need to reconcile names across the architecture.  To correct this, you can use the [**Co-relationship** button](./enterprise/Overview-ITAA#co-relationships) to locate the artifact instances where the incorrect name(s) is/are used and then you can change them using the **"Select from existing"** button/link within those artifact instances.  Note, after you reconcile the elements, you will have created an orphan.  Prior to reconciling, each of the name variants would have been referenced in the architecture and thus wouldn't have shown up as an orphan!

### Diagram Icons and Style manipulation

For most, the user experience in creating diagrams and the ease by which one can create compelling and conforming* visuals greatly determines how one perceives how productive you can be within a tool. A key design principle for IT Architect Assistant is to deliver an intuitive and productive drawing experience while managing a simplified meta-model. This balance of delivering a modeling tool with most of the beneficial experiences of a drawing tool is one we continually strive for.  

With that in mind, it is important to understand the underlying drawing engine (MxGraph framework) and how and where we can and will deliver ease of use. MxGraph (and the derived tool, **Draw.io**) provide a simple drawing tool. Beyond foundation tooling to adjust and manage style, productivity comes from delivering a rich set of standard element styles (icons), through a number of drawing palettes.

In IT Architect Assistant, we need to be able to associate an icon with an architectural element. Note that an icon or shape manifests itself on the drawing as a *drawing element* and that drawing element's look and feel can be completely altered via the tools available in the format panel. Most notable are the edit style and edit image buttons. In most cases (with the exception of AOD IT System View), IT Architect Assistant provides a default (vanilla) icon for each architecture element type. When you add such an element to the diagram you are manipulating two elements: a UI element (drawing element) and an *architectural element*. From the discussion above, note that you can change the binding between a visible UI element and the associated architectural element via the ["Select from existing" button](./enterprise/Overview-ITAA#bind-to-existing-element). At the same time, the default behavior is to create an architectural element each time you add a new UI/drawing element onto a diagram.

So how do you provide easy access to a rich set of shapes and icons while keeping the palette structure simple? This trade-off continues to be a work in progress in IT Architect Assistant.  Today, as of version 3.0, the AOD IT System View, is unique and contains a set of, now legacy palettes representing a snapshot in time of many of the standard icons used in reference architectures in the IBM Cloud Architecture Center. 

![IT System View specialized palettes](../images/ITsystem-palettes.png)

We have run into 2 problems with this approach: First, this set of icons is ever changing and ever growing and organizing them so that it is easy to find the icon you are interested in proved to be quite challenging; Second, given this is a modeling tool, the value of standardizing around a set of published Reference Architectures is to reuse much more than just the iconification, but also where possible reuse names, descriptions and other attributes of the underlying architectural element.  Thus the tool's move away from delivering customized palettes.

#### Building and working with Reusable Element Libraries

 So how does a user today optimize workflow without a rich set of palettes on every single diagram? First understand what approaches are available to you, how to optimize each of these approaches, and then establish a workflow best suited for your preferences.

##### Simple use of local images for icons

One strategy is to use the "Edit Image" button on any* icon (drawing element) and load an image from local filesystem. Obviously you can also collect your own icons. When you select an image file via the "Edit Image" finder dialog, the image is uploaded into the system (IT Architect Assistant) and added to the Cloud Filesystem and a file path to this uploaded file is then added into the UI element's (on your diagram) style.

A second strategy is to copy style from known graphics. For example, the Annotation palette is provided both to create non-architectural content on a diagram, but also is available to copy the style to be applied to the UI element associated with an architectural element. Select the "Edit Style" on a *drawing element* and copy the contents of the Style, then select the "Edit Style" for the *drawing element* you wish to change and paste the copied style contents.  In a similar way you can also copy the style from other palettes available other places.

The third strategy is to build and maintain or just reuse content from one or more assets established primarily as a reusable element library. The intent here it to capture reusable "packages" that include architectural element (type), Name, Description, icon/visualization, and possibly additional attributes. An excellent example of this is the **Icon Library- IBM Cloud Architecture Center** that you can find via Search in Cognitive Architect. Here 1 or more AOD IT System View instances provide access to reusable content that one can copy from using the ["Resource > Copy from xxx" approach](./enterprise/Overview-ITAA#fine-grained-reuse).  Note this approach is powerful beyond delivering a set of reusable elements for your diagrams.  It can also be used to capture a reference set of other elements, such as typically used Architectural Decisions, Non-Functional Requirements, perhaps even Use Cases. Managing a reuse library help you and your team to consistently use the same artifacts across multiple architectures!

### Dependent and Linked Diagrams

Currently, there are a couple of places where multiple diagrams are dependent on other diagrams, beyond just potentially sharing reused/common architecture elements. One of these linkages is the Usage Scenarios. Currently all Usage Scenarios are tied to an underlying AOD. Further, within the Usage Scenario, the scenario "steps" are bound to one or more connectors.  (Note, a backlog item will allow steps to be tied to any architecture element in the future.)  Typically, updates to these now dependent diagrams are handled iteratively. But, note that removal of a connector (even if another is redrawn between the same elements) in the base AOD, means that the association of any steps within a Usage Scenario based on the AOD will now be removed. Thus beware the changes you make in your AODs may impact any dependent Usage Scenario Diagrams.

Another, linkage, is supported in the Operational Model. Here when you create a Prescribed Operational Model view, you can choose to link it to an existing Logical Operational Model view. [There are restrictions to this and only one such linked pair is supported per architecture.]  The linkage triggers a number of synchronization and validation checks which will automatically retain any changes to placement of Prescribed Nodes and Actors within OMLocations consistent across the two diagrams.  There will be times, however, you will find you are fighting the synchronization functionality and therefore want to unlink the diagrams.   The way to do this is make a copy of either the LOM or POM (not both).  Then delete the original copy. The two remaining diagrams will no longer be linked together.

