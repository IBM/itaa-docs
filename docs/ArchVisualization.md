# Architecture Visualization Best Practices

An AoT Initiative in 2020-2021 has produced a set of recommendations for architecture visualization (see [draft document](./IT-Architecture-Visualisation.pdf)). These visualization standards are being rolled out for a number of different tools, including draw.io, Cognitive Architect, Visio, PowerPoint and others.

In Cognitive Architect which shares the diagramming engine with draw.io, MxGraph framework, the core set of architecture element styles have been added to the corresponding diagram palettes.  This  document presents the current and future user experience of this vizualization "library" within Cognitive Architect and provides some best practice guidance in its use.

If you look at the referenced diagram above, the foundation of the visualization approach is to standardize on such things as:

- Shape = architecture element type
- Fixed color palette (for accessibility) - an typically used to note technology domain
- Shape details (e.g. collapsed, expanded, multiplicity) all managed via limited controls
- ...

Most of what you can and should alter for these "IBM stencil" drawing elements, can be found in a set of "Shape Style attributes".   Below you see an IT System View (AOD) in Cognitive Architect with nested - Location, Subsystem and Logical Node being placed on the diagram.  The Logical Node is currently selected and in the format panel, the Style tab is presented and the Shape Style attribute section is highlighted.

<img src="../images/ibm-style-properties.png" alt="Style Attributes" height="543px"/>

Unlike the document referenced earlier, that presents the draw.io shape properties, Cognitive Architect generally hides the "Shape" property, which is used to select an element type shape style. In Cognitive Architect, the element type was selected from the palette and carries along the architecture model's meta-data properties and so the shape selection is enforced.

The **Shape (Layout)** property has the two primary options Collapsed and Expanded.  The referenced "Nested" value is just the Expanded style resized. The other entries are used to create Legend entries.

The **Shape (Style)** property refers to the use of shape outline, strikethrough etc.  The specific available values are Solid (default), Strikethrough, Double, and Dashed.

**Multiplicity** is an on/off checkbox, which will automatically create the stacked lines to visually signify multiplicity.

**Color**, **Color (Corner)**, and **Color (Background)** - sets the shapes color from a drop-down list of colors from the standard color palette.  **Corner** adjusts the vertical bar in the upper left corner (see SubSystem above), and **Background** handles the "fill color". Note these override the basic Fill and Line color in the main part of the Style panel!

**Icon** determines how the icon is selected. For many this is extremely important and yet is among the most challenging thing to control from a UX perspective. As such this is where Cognitive Architect has introduced an approach (current and future features) in improve usability. Note there are two diffenent kind of "icons": so called stencil **icons** and **image** icons.  Stencil icons come from a community supported repository, currently, the IBM Design organization (see [UI Icons](https://www.ibm.com/design/language/iconography/ui-icons/library/)). These get specified by having the Icon property set to the value **Yes** and providing the icon "name" in a special data property, Icon-Name. [**Note**: you can click <Ctrl-m> to bring up the data property dialog and edit the properties.] Of  course, remembering icon names, and manually editing the data property is not very user friendly. In a drawing tool like draw.io, this is handled by loading very large "icon palettes" and dragging the corresponding shape+icon onto the canvas. Further in this case, you can change the base shape as this is not tied to any architecture element. 

Cognitive Architect has set out to accomplish a similar approach, but one that is subtly different. First, the tool chooses not to impose a large set of icon palettes on the architecture diagrams, as navigating them becomes difficult. However, a particular user may have a set (or sets) of icons they like to use and apply to different architectural elements. So with release 3.5, Cognitive Architect let's you define custom palettes, populating them from the "community-wide" superset of stencil icons. These custom palette(s) are then added to the diagram - and presumably much easier to navigate. Important to **note** these palettes are  not used to add drawing elements to the canvas, they are instead used to "set/replace" the icon that appears on a drawing element already on the canvas. The gesture is to drag an icon from your custom palette onto an existing drawing element, and the result is replacement of the displayed icon.

So what about **image** icons? This is a way to use any image (.png, .svg, ...) as the 32px icon. In Cognitive Architect this requires 3 magic values to be set. First, the Icon property should still have the value **Yes**; second, the image must be loaded, this is done via the Edit Image button; and third, the value of the Icon-Name data property must be empty (no text). How is this UX to be improved in Cognitive Architect? In a post v3.5 release, images can also be added to the custom palettes. And the same gesture will be used to drag an image icon from a custom palette onto a drawing element to update the displayed icon. The tool will manage the loading of the image and clearing the Icon-Name property.

What happens when Icon property value is **No**? This removes the icon from the corresponding place in the drawing element. This is used when you don't want an icon displayed.

The **Tag**, **Tag (Color)**, and **Tag (Fill)** properties are used to control the "Badge" referenced in the visualization standard document. 

### Custom Icon Palettes

As noted earlier, Cognitive Architect has an evolving approach to make it much easier to manage and manipulate icons on diagram. The approach is to make it easy for users to manage and share icon palettes that deliver easy to apply icons.

Today, on any diagram in the tool, you will find a '+' sign at the top of the drawing palettes.

<img src="../images/add-custom-palette.png" alt="Add Custom Palette" width="211px"/>

Clicking on this allows a user to create a new custom palette. You will give the palette a **name**, so that you can easily distinguish between multiple custom palettes. A custom palette today is defined at the architecture level and will be available on every single diagram within that architeture. 

<img src="../images/set-palette-name.png" alt="Create new palette, set name" width="400px"/>

[In a subsequent release, these palettes will be defined at the user-level, and you will have the opportunity to load custom palettes (already defined) into an architecture. At that time you will also be able to export these palettes to share with others.]

Once an empty custom palette has been created you then want to be able to quickly add icons to the palette. Eventually, these palettes will support managing both "stencil icons" and "image icons". Also eventually you will be able to import from a file to exchange palettes.

<img src="../images/select-icon-source.png" alt="Select to add from IBM stencils" width="400px"/>

Stencil icons are managed within the tool itself and are sourced from IBM Design UI Icons. Image icons can be any standard image (.jpg, .png, .svg).  For release 3.5, only "stencil icons" are supported. Thus the UX is to be able to add icons to your palette from the large list of built-in icons. [Note, the built-in icon set will grow significantly and soon will have the icons grouped into categories.]

<img src="../images/pick-icons.png" alt="Select icons to include" width="400px"/>

Select from the list and click Add, then review before saving.

<img src="../images/review-icons.png" alt="Select icons to include" width="400px"/>





The newly created palette will show up as a new diagram palette.   

<img src="../images/palette-on-left.png" alt="Review icons and save" width="200px"/>

Note these custom palettes can not be used to add drawing elements to a diagram, they are only used to alter the applied icon to existing elements on the canvas.

To use, drag an icon onto an element.

<img src="../images/drag-icon.png" alt="Create new palette, set name" width="400px"/>

The result will be to apply that icon to the element.

<img src="../images/applied-icon.png" alt="Create new palette, set name" width="400px"/>

### Current caveats

These icons from custom palettes can only be applied to the new, IBM architecture visualization standard elements on the canvas. Eventually you will be able to drag both stencil and image icons onto these "styled" drawing elements. Also, in the future, you will be able to drag "image icons" onto the old style elements for a similar effect.