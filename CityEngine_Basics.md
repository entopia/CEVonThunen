# Basics of City Engine modeling

CityEngine functions as a "Procedural Modeling Application," which means it converts 2D shapes into 3D models using a sequence of steps defined by CGA rule files. The core capability of CityEngine is rooted in CGA (Computer Generated Architecture), a specialized programming language for generating 3D architectural models. When CGA rules are applied to shapes, they produce 3D structures. The level of detail in these models is dictated by the CGA rules and their specific instructions. For instance, a simple CGA file might turn a building's footprint into a basic 3D shape, while a more elaborate rule could add surface textures or subdivide the structure into more detailed parts, creating intricate 3D models.

An important strategy in writing CGA rules is to develop them progressively, incorporating features incrementally. It's more efficient to build and test the rule in stages rather than writing a large amount of code all at once. This approach allows for continuous testing and refinement to achieve the desired results.

![image](https://github.com/entopia/CEVonThunen/assets/4749503/1890af84-179f-45f1-88f0-461aef631216)

This tutorial will take you through the step-by-step process of creating 3D buildings from a basic footprint by progressively developing a CGA rule.


## Creating a New Scene

1. **Create a New Scene**:
   - Open the Navigator and locate the `scenes` folder.
   - Right-click on the `scenes` folder and select `New Scene`.
   - Name your scene appropriately, such as `MyFirstModel.cej`.

## Drawing and Adjusting Road Segments

2. **Draw the Road Segment**:
   - Click on the `Street Creation Tool` icon in the top menu.
   - Click on the starting point in the viewport where you want the road segment to begin.
   - Move the cursor to the endpoint of the road segment and click again to finalize the road segment.

3. **Adjust Road Properties**:
   - With the road segment selected, open the Inspector window.
   - Adjust properties such as width, type, and alignment to customize the road segment as needed.

![image](https://github.com/entopia/CEVonThunen/assets/4749503/0a7670f1-a7d7-4cb2-a3bb-8a3d4fd3a3de)



## Growing Streets

4. **Select the Grow Streets Tool**:
   - With your street segment selected, in the toolbar, click on the `Grow Streets` icon or navigate to `Tools > Street Creation > Grow Streets`.

5. **Configure Street Growth**:
   - In the Grow Streets tool, configure parameters for your hypothetical city.
   - Set the `Number of streets` to 1000.
   - Choose `Pattern of Streets`: Radial.
  
![image](https://github.com/entopia/CEVonThunen/assets/4749503/3b94a079-cec0-4531-b321-1f2eb331547f)

6. **Generate and Refine Streets**:
   - The tool will automatically generate a network of streets based on the parameters you set.
   - After generation, manually adjust and refine the street network by selecting and editing individual segments.

7. **Save Your Project**:
   - After making necessary adjustments, save your project to preserve the street network and scene setup.



## Creating Your First CGA Rule

1. **Create a New Rule File**:
   - Right-click the `\rules\` folder.
   - Navigate to `New > CGA Rule File`.
   - Name the rule file `MyFirstRule.cga`.

2. **Add Initial Code**:
   - Open the `MyFirstRule.cga` file.
   - Below the line of code that states the version, add the following lines:

   ```cga
   version "2024.0"

   // Hello World Example
   @StartRule
   Lot --> extrude(10)
   ```
   
3. **Assign the Rule to the Lot Shapes**
   
   **Select Lots:**
   
   In the viewport or the Scene Editor, select the lot(s) to which you want to assign the rules.
   (A common way to do this is from the Layers panel, to expand the current layer, and you ll notice that there are two sub-layers, 'streets' and 'Lots'. Right click on the Lots --> select all.)

   **Assign the Rule to the Selected Lots:**
   
   In the Navigator, locate your CGA rule file (e.g., MyFirstRule.cga).
 
   With the lots selected, go to the Inspector window.
   In the Inspector window, find the section labeled 'Rule' File.
   Click on the folder icon next to the Rule File field to browse and select your CGA rule file.
   After selecting the rule file, the Start Rule field will be populated automatically, or you may need to select the appropriate start rule from the dropdown.
   
   **Generate Models:**
   Click the Generate button (usually a green play icon) in the toolbar to apply the rules and generate the 3D models on the selected lots.

