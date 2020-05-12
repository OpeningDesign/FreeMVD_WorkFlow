This file lists "exercises" to be performed by a BIM application to achieve adequate round-tripping 
with IFC files. The application should successfully complete all the steps.

## 1. importing and exporting a simple extrusion

The application should be able to export and import an IFC file containing one IfcBuildingElementProxy 
entity, with one representation, which is an IfcExtrudedAreaSolid, based on an IfcArbitraryClosedProfileDef
made of an IfcPolyline, like the example below:

```
  #20= IFCBUILDINGELEMENTPROXY('0ohBfsArr3ruXYxacT4yl5',#1,'NOTDEFINED',$,$,#2,#21,$,.NOTDEFINED.);
    #21= IFCPRODUCTDEFINITIONSHAPE($,$,(#22));
      #22= IFCSHAPEREPRESENTATION(#9,'Body','SweptSolid',(#23));
        #23= IFCEXTRUDEDAREASOLID(#24,$,#25,2000.);
          #24 = IFCARBITRARYCLOSEDPROFILEDEF(.AREA., $, #26);
            #26 = IFCPOLYLINE((#27, #28, #29, #30));
              #27 = IFCCARTESIANPOINT((0., 0.));
              #28 = IFCCARTESIANPOINT((1000., 0.));
              #29 = IFCCARTESIANPOINT((1000., 1000.));
              #30 = IFCCARTESIANPOINT((0., 1000.));
          #25= IFCDIRECTION((0.,0.,1.));
```

#### Import criteria

* The extrusion can be changed after import
* The base polyline can be edited after import

#### Export criteria

* The exported IFC file contains an IfcBuildingElementProxy, with an IfcExtrudedAreaSolid as its representation
and an IfcArbitraryClosedProfileDef made of an IfcPolyline as its profile

#### Results

|                | BlenderBIM | FreeCAD                                                      | Revit | ArchiCAD | BricsCAD |
| -------------- | ---------- | ------------------------------------------------------------ | ----- | -------- | -------- |
| passed?        |            | yes                                                          |       |          |          |
| exported file: |            | [result 1.FCStd](Specifications%20test%20files/Rountrip%20Results/Roundtrip%201%20FreeCAD.FCStd) |       |          |          |
| imported file: |            | [result 1.ifc](Specifications%20test%20files/Rountrip%20Results/Roundtrip%201%20FreeCAD.ifc) |       |          |          |

