General Rules 

3D Details 
When modeling 3D details, here are some basic rules to consider.

- Every model should be a MIP (model in place) object. 
- The MIP should be set to the family cathegory "Wall" even if the model object it self is not a wall. This Wall family cathegory is ideal because it allows for easy cross platform transfer into programs like Freecad. It is also suitable to use the Wall cathegory as it's the only cathegory Revit LT can read, thus increasing the workflow interoperability between software packages.
- When creating MIP Sweep or Extrustion, don't model more than it is necessary, i.e do no model the same object more than once as the madel can be copied/duplicated and tweaked at will to create other objects. 
- Since the model can be reused, it should be dissassociated from it's initial base reference plane used to create the model in first place. This makes it possible to use the model in other locations on the project. If this dissasociation is not done, it will create unepected behaviours or be practically unsable else where when duplicates and mirros of the object have been created. 
-To disassociate the MIP from it's reference plane, select the model and enter it's "Edit in Place" mode. Select the object so we can see it's properties column will show up. In the Constraints tab, go to Work Plane. If the work plane is still associated with the main base plane, the name of the plane will appear. So select the object and click on the diagonal square with lock that appears. Once the lock is clicked, the object property work plane on the properties panel will show <not associated>, thus indicating that the MIP is dissassociated and there fore can be used easily else where. 
- In the MIP edit mode, we can now assign a material from the Materials and Finishes tab on the properties panel. Assigning materials at this stage of the 3D model is very convenient as it makes creating material tag documents very expedient later on during construction document phase.




BIM Profile and BIM Object names
General rules when assigning names to newly created objects and profiles.

In the event of creating a library that is meant to grow and evolve over time, it is extremely helpful to have a naming and organisational structure to help with all the parts and pieces stored. Therefore a consistent naming template goes as this 

000000 - Element Composition - Company - Profile - Size
ex.1
074643 - Composition Siding - Fiberon - Wenge - 1x6
ex.2
074643 - Composition Siding - Fiberon - Wenge - 1in X 6in

- The number follows the Arcat numbering system (so each element must reflect Arcat classification. It is helpful to stay consistent with Arcat naming while also organising the objects in their respective folders for quick sorting.
- Element composition refers to the What the general material is made of and what it's use is i.e. metal, wood, composite, glass, cladding etc ex. Composition Cladding, Metal Roof Panels, Joint Sealant, etc etc.
- Company simply identifies the company that manufactures the material. This is helpful because the same object can be manufactured by different companies, and so in a scenario where we have a growing list of objects of the same nature and cathegory, it is easier to know and refer back to the specified company instead of re doing the research to find out the supplier anew. (which means in other words, we are loosing in efficiency)
- Profile is the name of the type of profile, for example a 2x4 is of a different profile from a 2x6 although both can be made from the same company and have the same numbering system from Arcat. We also observe this mainly with Reglets, Furrings, and most other materials which have an array of different profiles. 
-Sizes also help identify the size of an object, Ideally providing the Lenght and Width for profiles is enough since the height can be determined by the design of the object in place, meanwhile for dedicated shapes with Bim Objects such as CMU's and Bricks etc etc, can have their Heights, Lenghts, and Widths immediately identified.

Note: When writing names, it is best to use only the dash (-) symbol in between the different types of names for identification. Also avoid other symbols such as ( " ) or ( ' ) which are often used in sizes to identify feet from inches. When it is required to use ft and inches it is best to write (ft) and (in) next to the text name. 
