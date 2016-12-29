# BIM Specifications

Originally elaborated by [OpeningDesign](http://www.openingdesign.com) / Ryan Schultz / Yorik van Havre and licensed under [CreativeCommons](http://creativecommons.org/licenses/by/4.0/). Feel free to use, distribute or contribute to improve the process.

### Foreword

This BIM specification, unlike most other BIM specifications available, is based on real-life, tested methods to get the job done and guarantee as much as possible the primary aim of BIM--real collaboration between the different actors of a building project.

This specification consists of simple rules to guarantee a maximum of fidelity in data transfers using the [IFC](https://en.wikipedia.org/wiki/Industry_Foundation_Classes) file format. The following rules work with any version of the IFC schema.

The correct implementation of these rules implies a good understanding of the [IFC format](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/), and ways to verify the contents of IFC files others than in the software where it was authored. Several [free](http://www.ifcwiki.org/index.php/Open_Source) or [open-source](http://www.ifcwiki.org/index.php/Open_Source) applications allow to open, visualize and inspect IFC files and make sure that the rules below were correctly implemented.

---

## Rules

---

### **Model Lines:** Lines in 3-dimensional space



| Platform                 |Native Functionality| Import | Export |
| --- | --- | --- | --- |
| FreeCAD                  |Any [Part-based](http://www.freecadweb.org/wiki/index.php?title=Part_Module) object which contains edges and no faces, such as [Draft](http://www.freecadweb.org/wiki/index.php?title=Draft_Module) or [Sketch](http://www.freecadweb.org/wiki/index.php?title=Sketcher_Module) objects| [IfcAnnotation](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcproductextension/lexical/ifcannotation.htm) objects are imported as simple, non-parametric Part objects. Color and line style currently not supported. | Part-based objects with edges and no faces are exported as [IfcAnnotation](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcproductextension/lexical/ifcannotation.htm) |
| Revit                    |[Model Lines](https://knowledge.autodesk.com/support/revit-products/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Revit-Model/files/GUID-24A8763F-D8DD-4579-9CF3-BBC02EF3A314-htm.html)|PASSES -  Name, Color, & Pattern, FAILS - Weight|Had to use an MVD that supports the export of lines (Coordination View 2.0 does not)|
| ArchiCAD 					| x | x | x |


Test folder: [Model Lines](Specifications test files/Model Lines)

---

### **Walls**


| Platform                 |Native Functionality| Import | Export |
| --- | --- | --- | --- |
| FreeCAD                  |[Walls](http://www.freecadweb.org/wiki/index.php?title=Arch_Wall)|[IfcWall](https://encrypted.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiekN3amJrRAhVFHZAKHVaZBrQQFgghMAE&url=http%3A%2F%2Fwww.buildingsmart-tech.org%2Fifc%2FIFC4%2Ffinal%2Fhtml%2Fschema%2Fifcsharedbldgelements%2Flexical%2Fifcwall.htm&usg=AFQjCNFehG4I0NTWy_EHVqfUV9skODan5w&sig2=qdyLzXHB0uERtQ2MUO-NBg) and IfcStandardWall are imported as [wall](http://www.freecadweb.org/wiki/index.php?title=Arch_Wall) objects | all [walls](http://www.freecadweb.org/wiki/index.php?title=Arch_Wall) and any other [Arch](http://www.freecadweb.org/wiki/index.php?title=Arch_Module)-based object which Role property is set as Wall, is exported as an [IfcWall](https://encrypted.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiekN3amJrRAhVFHZAKHVaZBrQQFgghMAE&url=http%3A%2F%2Fwww.buildingsmart-tech.org%2Fifc%2FIFC4%2Ffinal%2Fhtml%2Fschema%2Fifcsharedbldgelements%2Flexical%2Fifcwall.htm&usg=AFQjCNFehG4I0NTWy_EHVqfUV9skODan5w&sig2=qdyLzXHB0uERtQ2MUO-NBg).|
| Revit                    |[Walls](https://knowledge.autodesk.com/support/revit-products/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Revit-Model/files/GUID-9A9F7D00-A6A1-4E17-8C74-0965FDA5E007-htm.html)|from FreeCAD, the wall imports as a in-place family, that is, not an intelligent wall|Yes|
| ArchiCAD 					| x | x | x |

Test folder: [Wall](Specifications test files/Wall)

**To do:**

* Check if there is any possibility to recreate a working family from an IFC file

---

### Materials

The notion of material in IFC is spread over different types: objects can have a [IfcStyledItem](http://www.buildingsmart-tech.org/ifc/IFC2x4/rc1/html/ifcpresentationappearanceresource/lexical/ifcstyleditem.htm) applied directly to them, that allows to set for example a color, an [IfcMaterial](http://www.buildingsmart-tech.org/ifc/IFC2x4/alpha/html/ifcmaterialresource/lexical/ifcmaterial.htm), that actually contains little more (it also contains an IfcStyledItem), and different [IfcProperties](http://www.buildingsmart-tech.org/ifc/IFC2x4/rc1/html/ifcpropertyresource/lexical/ifcpropertysinglevalue.htm) that is where the physical properties of a material can be stored.

Any Ifc object can have any of the above. For the material to work in Revit, it must have a IfcStyledItem directly applied on the object,and an IfcMaterial. Both the IfcStyledItem and the IfcMaterial contain an [IfcSurfaceStyle](http://www.buildingsmart-tech.org/ifc/IFC2x3/TC1/html/ifcpresentationappearanceresource/lexical/ifcsurfacestyle.htm). It is important that both these IfcSurfaceStyle have the same name as the material. So for any given object with a material, you need three IFC entities with the same name.

| Platform                 |Native Functionality| Import | Export |
| --- | --- | --- | --- |
| FreeCAD                  |[Material](http://www.freecadweb.org/wiki/index.php?title=Arch_SetMaterial)| For objects with an associated IfcMaterial, a FreeCAD material is created and linked to the object. For objects that only have a Surface Style directly applied, no material is created in FreeCAD, but the object takes the color of the Surface Style.| If FreeCAD objects have a material, it is exported as an IfcMaterial with corresponding Surface Style. Otherwise, only the shape color is exported as Surface Style. |
| Revit                    |x|x|x|
| ArchiCAD 					| x | x | x |


---

### **Name and Description:** All objects and materials should have a human-readable name or description


Objects should have a name that allows a human being to understand what it is, in case the software that reads the IFC file fails to recognize or categorize it appropriately. For example, bad names are "Object00014", "Material43". Good names are "Kitchen chair", "Grey concrete", "East living room wall"

All [IFC objects](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifckernel/lexical/ifcroot.htm) have a **Name** and a **Description**. Any of them can be used for this purpose.

This rule mainly applies to [IfcProduct](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifckernel/lexical/ifcproduct.htm) entities in IFC: They are the final, individual objects that compose a building. For example, a wall, a column, a chair, a window. It doesn't consider objects that are part of a final product, when they are composed of multiple objects, for example a leg of a chair or a brick of a wall. It is sufficient to have the chair correctly named, not necessarily each component of the chair.

| Platform                 |Native Functionality| Import | Export |
| ------------------------ | ------ | ------ | ------ |
| FreeCAD                  |[Label property](http://www.freecadweb.org/wiki/index.php?title=Property_editor) (all FreeCAD objects), Description property (only [Arch objects](http://www.freecadweb.org/wiki/index.php?title=Arch_Module))| IFC name translated to FreeCAD object **label** ```('My test wall')```, IFC **description** ```('This is a test wall to check rule number one')``` imported into FreeCAD object description if available | FreeCAD object label exported as IFC name, FreeCAD object description, if present, exported as IFC description |
| Revit                    |???|Upon import, **name** and **description** is not accessible to modify from Revit UI. see Screenshots [1](Specifications test files/wall_with_name_and_description/Revit Properties_1.png) & [2](Specifications test files/wall_with_name_and_description/Revit Properties_2.png)      |  **Name** and **description** exports out correctly.      |
| ArchiCAD | ??? | ??? | ??? |

Test folder: [Name and Description](Specifications test files/Name and Description)

**To do:**

* Check where name and description are stored in Revit, maybe that could be accessed by dynamo or something. See if Revit doesn't provide any alternative (different ways to "label" objects)

---

### **Nested Groups:** All objects should be grouped in meaningful ways


Grouping objects using [IfcGroups](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifckernel/lexical/ifcgroup.htm) allows a human being to clearly recognize objects as being part of a same area, funcion or category. Groups can be nested inside other groups. A same object cannot be part of several groups.

| Platform                  |Native Functionality| Import | Export |
| ------------------------ | ------ | ------ | ------ |
| FreeCAD                  |[Groups](http://www.freecadweb.org/wiki/index.php?title=Group)| IFC groups translated to FreeCAD groups. Nesting is respected. | FreeCAD groups are exported to IFC groups, but groups are not part of IfcBuildingStoreys (**Problem**: IfcGroups cannot be nested into IfcBuildingStoreys) |
| Revit                    |[Groups of Elements](https://knowledge.autodesk.com/support/revit-products/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Revit-Model/files/GUID-52612B0F-43AA-47AF-A76C-BB0E3DD24E34-htm.html)|   Does not import IFCgroups into Revit Groups     |  Yes, exports ```#253= IFCGROUP('2wfBgyl9H71872FVeaZPs0',#41,'Model Group:Test Revit Group:149951',$,'Model Group:Test Revit Group');``` |
| ArchiCAD | ??? | ??? | ??? |

Test folder: [Nested Groups](Specifications test files/Nested Groups)

**To do:**

* IFC offers two different "structures" to group and organize contents: [space-related](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifcproductextension/lexical/ifcrelcontainedinspatialstructure.htm) (Building->BuildingStorey->Zone->Space) and non-space-related ([Group](http://www.buildingsmart-tech.org/ifc/IFC4x1/html/schema/ifckernel/lexical/ifcgroup.htm) ). These two structures are fully independent and cannot be combined (you cannot add a group to a spatial structure element). Check if using IFC Groups is the most adequate form, and if it wouldn't be better to switch to a full space-related system.

---


### Duplicatable components


A way to be able to group a series of objects into a same structure, let's call it a component, and duplicate that component in the model. If one object is changed, added or removed from/to the base component, all instances of that component should update automatically. This is typically how "blocks" work in AutoCAD, or "components" in SketchUp, or "compounds" in FreeCAD. An example would be a restroom stall, with all its parts and accessories: door, wc basin, paper hanger, sink, etc.

| Platform                 |Native Functionality| Import | Export |
| --- | --- | --- | --- |
| FreeCAD                  |[Compound](http://www.freecadweb.org/wiki/index.php?title=Part_MakeCompound)| x| x |
| Revit                    |x|x|x|
| ArchiCAD 					| x | x | x |

---

## Tools


Use free/open-source IFC applications to validate the data inside IFC files.

It is fundamental for the author of an IFC file to be fully aware of what has been included in that file. Therefore, it is essential to be able to vertify the contents of the file in a neutral manner (independent of the application that exported it). It should also be possible for other people to easily open that file, and verify its contents, independently of the application used to import it.

**Items that should be checked on opening an IFC file for verification**:

* The application used for verification reports no error on opening the file
* The total number of objects informed by the application used for verification matches the number of objects informed by the application used for exporting
* All the geometry is there when inspecting the 3D model in the application used for verification
* All the geometry is at its correct location when inspecting the 3D model in the application used for verification

**To be developed:**

* For now the only reliable one I know that is open-source and cross-platform is [IfcPlusPlus](http://www.ifcplusplus.com/) which does a fairly good job. If it prints no error, and all objects appear in place, it generally means the data is of very good quality. [BimServer](http://bimserver.org/) might become a perfect option once it has good data validation plugins. IfcPlusPlus doesn't support IfcAdvancedBrep (Still not checked with BimServer).

### 04. Use geometry types that makes objects editable in all applications

**To be developed:**

* Some geometry types, although they import correctly in all applications, are sometimes not editable (the concept of what editable means needs to be developed as well). This item should identify the geometry types that are "safe".

**To be tested:**

* Vertical (Z-axis) [extrusions](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcgeometricmodelresource/lexical/ifcextrudedareasolid.htm) of any profile (straight/only lines, complex/curved, and predefined types)
* Arbitrary (any direction) extrusions of any profile
* [Booleans](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcgeometricmodelresource/lexical/ifcbooleanresult.htm) (unions, differences, intersections)
* [Faceted Brep](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcgeometricmodelresource/lexical/ifcfacetedbrep.htm) shapes
* [Advanced Brep](http://www.buildingsmart-tech.org/ifc/IFC4/final/html/schema/ifcgeometricmodelresource/lexical/ifcadvancedbrep.htm) shapes


<!-- Table Template

| Platform                 |Native Functionality| Import | Export |
| --- | --- | --- | --- |
| FreeCAD                  |x| x| x |
| Revit                    |x|x|x|
| ArchiCAD 					| x | x | x |

-->

