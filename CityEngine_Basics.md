# Basics of City Engine modeling

CityEngine functions as a "Procedural Modeling Application," which means it converts 2D shapes into 3D models using a sequence of steps defined by CGA rule files. The core capability of CityEngine is rooted in CGA (Computer Generated Architecture), a specialized programming language for generating 3D architectural models. When CGA rules are applied to shapes, they produce 3D structures. The level of detail in these models is dictated by the CGA rules and their specific instructions. For instance, a simple CGA file might turn a building's footprint into a basic 3D shape, while a more elaborate rule could add surface textures or subdivide the structure into more detailed parts, creating intricate 3D models.
![image](https://github.com/entopia/CEVonThunen/assets/4749503/1890af84-179f-45f1-88f0-461aef631216)


An important strategy in writing CGA rules is to develop them progressively, incorporating features incrementally. It's more efficient to build and test the rule in stages rather than writing a large amount of code all at once. This approach allows for continuous testing and refinement to achieve the desired results.

This tutorial will take you through the step-by-step process of creating 3D buildings from a basic footprint by progressively developing a CGA rule.


## Create a new scene





## Creating Your First CGA Rule

1. **Create a New Rule File**:
   - Right-click the `\rules\` folder.
   - Navigate to `New > CGA Rule File`.
   - Name the rule file `MyFirstModel.cga`.

2. **Add Initial Code**:
   - Open the `MyFirstModel.cga` file.
   - Below the line of code that states the version, add the following lines:

   ```cga
   version "2024.0"

   // Hello World Example
   @StartRule
   Lot --> extrude(10)

