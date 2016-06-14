# BIM Specifications

Originally elaborated by [OpeningDesign](http://www.openingdesign.com) / Ryan Schultz / Yorik van Havre and licensed under [CreativeCommons](http://creativecommons.org/licenses/by/4.0/). Feel free tu use, distribute or contribute to make it better.

### Foreword

This BIM specification, unlike most other BIM specifications available, is based on real-life, tested methods to get the job done and guarantee as much as possible the primary aim of BIM, real collaboration between the different actors of a building project.

This specification consists of simple rules to guarantee a maximum of fidelity in data transfers using the [IFC](https://en.wikipedia.org/wiki/Industry_Foundation_Classes) file format. The following rules work with any version of the IFC schema.

The correct implementation of these rules implies a good understanding of the [IFC format](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/), and ways to verify the contents of IFC files others than in the software where it was authored. Several [free](http://www.ifcwiki.org/index.php/Open_Source) or [open-source](http://www.ifcwiki.org/index.php/Open_Source) applications allow to open, visualize and inspect IFC files and make sure that the rules below were correctly implemented.

### Rules

### 01. All objects and materials must have a human-readable name or description

Objects should have a name that allows a human being to understand what it is, in case the software that reads the IFC file fails to recognize or categorize it appropriately. For example, bad names are "Object00014", "Material43", "Wall034". Good names are "Kitchen chair", "Grey concrete", "East living room wall"

All IFC objects have a **Name** and a **Description**. Any of them can be used for this purpose.

This rules mainly applies to [IfcProduct](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifckernel/lexical/ifcproduct.htm) entities in IFC: They are the final, individual objects that compose a building. For example, a wall, a column, a chair, a window. It doesn't consider objects that are part of a final product, when they are composed of multiple objects, for example a leg of a chair or a brick of a wall. It is sufficient to have the chair correctly named, not necessarily each component of the chair.

| Support                  | Import | Export |
| ------------------------ | ------ | ------ |
| FreeCAD                  | IFC name translated to FreeCAD object name, IFC description not imported into FreeCAD | FreeCAD object name exported as IFC name, FreeCAD object description, if present, exported as IFC description |
| Revit                    |        |        |

Test file: [wall_with_name_and_description.ifc](Specifications test files/wall_with_name_and_description.ifc)

### 02. All objects should be grouped in meaningful ways

Grouping objects using [IfcGroups](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifckernel/lexical/ifcgroup.htm) allows a human being to clearly recognize objects as being part of a same area, funcion or category. Groups can be nested inside other groups. A same object cannot be part of several groups.

| Support                  | Import | Export |
| ------------------------ | ------ | ------ |
| FreeCAD                  | IFC groups translated to FreeCAD groups. Nesting is respected. | FreeCAD groups are exported to IFC groups, but groups are not part of IfcBuildingStoreys. |
| Revit                    |        |        |

Test file: [wall_in_nested_groups.ifc](Specifications test files/wall_in_nested_groups.ifc)
