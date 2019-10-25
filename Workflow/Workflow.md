


## 3D Details Workflow
When modeling 3D details, here are some basic approaches to consider.

### Details that will be roundtripped between Revit/FreeCAD

- Every model should be a MIP (model in place) family.
- The MIP family should be set to the 'Wall' category even if the model object itself is not a wall. The only reason being is that Revit LT only allows you to create a MIP family in the wall category--the other categories are restricted.  This assures that the entire team doesn't need full blown Revit, to help model these details.
- All MIP families should be **disassociated** from a working plane.  The reason being is that when a MIP family is associated with a working plane, it does not mirror or rotate property.  Also, the association would not survive a roundtrip either.
	- To disassociate the MIP from it's working plane, select the model and enter it's "Edit in Place" mode. Select the object so we can see it's properties column will show up. In the Constraints tab, go to Work Plane. If the work plane is still associated with the main base plane, the name of the plane will appear. So select the object and click on the diagonal square with lock that appears. Once the lock is clicked, the object property work plane on the properties panel will show <not associated>, thus indicating that the MIP is disassociated and therefore can be used easily else where. 
- Only model Extrusions
	- Don't model the following, as they do not holdup during a Revit/FreeCAD rountrip
		- The following MIP familes
			- Sweeps
			- Voids
			- Blend
			- Revolve
			- Swept Blend
		- 'Loadable' or Standard Families.
- Assign Revit Materials to the individual MIP families.  We then use Revit's 'Material Tag' to annotate the detail.


### Revit Only Approaches
If only modeling in Revit, and don't plan on roundtipping with FreeCAD via IFC, the following approaches are suggested.  They will not hold up, however, if you roundtrip the model in the future.

- Use Sweeps with Profile Families
	- If you use a sweep, only associate it with a Profile Family. 
		- Only create a profile family if you envision using the profile again in another project. If it doesn't pass this test, use an Extrusion.
		- Save the profile here: https://github.com/OpeningDesign/BIM_Profiles
			- See below, for naming conventions of profiles.
- 	Do not use the following however. The reason being, is that hopefully in the near future, we can get Sweeps with Profile Families to work via IFC, but the other modeling approaches below, are further out in the roadmap.
	- Voids
	- Blend
	- Revolve
	- Swept Blend
- Objects of repetitive nature such as objects O.C. i.e studs/furrings etc should be made into a group, and this group can be duplicated in an array or desired repetitiveness into another 'over all encompassing group'. This is an efficient way of managing these repetitive instances of the same object in an area especially when a modification is needed. Only one object of the instance within the main group can be modified and thus modifies all the remaining objects in the group at once.




---

### Profile Naming Conventions


In the event of creating a library that is meant to grow and evolve over time, it is extremely helpful to have a naming and organisational structure to help with all the parts and pieces stored. Therefore a consistent naming template goes as this 
- Examples
	- **074690 - Wood Siding** - Thermally Modified Wood - Thermory - 1 x 4 (.79in x 3.7in) - Ash Cladding.rfa
	- **051200 - Structural Steel Framing** - W-Section - W14x61.rfa
	- **086000 - Roof Windows and Skylights** - Wasco - P600 - Purlin.rfa
- The (1st) number and (2nd) name, in **bold** above, follows the MasterFormat numbering system
	- Suggest using Arcat.com to finding the MasterFormat number of a product
- The names following the MasterFormat number/name, should give the profile further description.  As a general approach, go from more general to more specific.  A few descriptive suggestions...
	- Company simply identifies the company that manufactures the material. This is helpful because the same object can be manufactured by different companies, and so in a scenario where we have a growing list of objects of the same nature and category, it is easier to know and refer back to the specified company instead of re-doing the research to find out the supplier anew.
	- Profile is the name of the type of profile, for example a 2x4 is of a different profile from a 2x6 although both can be made from the same company and have the same numbering system from MasterFormat. We also observe this mainly with Reglets, Furrings, and most other materials which have an array of different profiles. 
	- Sizes also help identify the size of an object, ideally providing the Length and Width for profiles is enough since the height can be determined by the design of the object in place, meanwhile for dedicated shapes with BIM Objects such as CMU's and Bricks etc etc, can have their Heights, Lengths, and Widths immediately identified.
	- Also avoid other symbols such as ( " ) or ( ' ) which are often used in sizes to identify feet from inches.--as they these symbols don't play nicely with Window's path names.  When it is required to use ft and inches it is best to write (ft) and (in) next to the text name. 
	
### Example Projects that have used this workflow
- https://github.com/OpeningDETAIL/Newport_Beach_CA_Residence
- https://github.com/OpeningDETAIL/Laguna_Beach_Residence
- https://github.com/OpeningDesign/FreeMVD_WorkFlow/tree/master/Example%20Projects/Restaurant
- https://github.com/OpeningDesign/OD_Library/blob/master/BIM/OD_Revit_Template.rte



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxMTg5NzEyNCw5Mzk2NjM0MzMsODc4Nz
Y1ODksLTIwNzUxMTgyMywtNzk1MDUzNjIxXX0=
-->
