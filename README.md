
# Von Thunen Model in CityEngine

This repository contains a CityEngine CGA rule file (`vonthunen.cga`) that implements a simple model based on Johann Heinrich von Thünen's theory of agricultural land use. This model calculates and visualizes agricultural rent zones based on yield, market price, production cost, and transportation cost.

## Von Thunen Model

The Von Thunen model explains how agricultural land use is determined by a series of concentric rings around a central market, with different crops occupying different rings based on their transportation costs and market prices.

## Code Breakdown

### 1. Setting Up Variables and Constants

This section defines the main attributes and constants for the model. The attributes include yield (`Y1`, `Y2`, `Y3`), market prices (`PriceMarket1`, `PriceMarket2`, `PriceMarket3`), and transportation costs (`TransportCost1`, `TransportCost2`, `TransportCost3`). The production cost (`C`) is a constant.

```cga
version "2010.3"

# Set variables and constants
attr Y1 = 300 // Yield (t/sqkm)
attr Y2 = 200 // Yield (t/sqkm)
attr Y3 = 100 // Yield (t/sqkm)

@Range(min=6, max=9, stepsize=0.2, restricted=false)
attr PriceMarket1 = 7 // Market price of the crop (in DM/t)
@Range(min=6, max=9, stepsize=0.2, restricted=false)
attr PriceMarket2 = 7 // Market price of the crop (in DM/t)
@Range(min=6, max=9, stepsize=0.2, restricted=false)
attr PriceMarket3 = 7 // Market price of the crop (in DM/t)

const C = 5 // Production cost of the crop (in DM/t)

@Range(min=1, max=6, stepsize=0.2, restricted=false)
attr TransportCost1 = 4 // Transport cost (in DM/t/km)
@Range(min=1, max=6, stepsize=0.2, restricted=false)
attr TransportCost2 = 3 // Transport cost (in DM/t/km)
@Range(min=1, max=6, stepsize=0.2, restricted=false)
attr TransportCost3 = 2 // Transport cost (in DM/t/km)

# Boolean to toggle between 3D "Rent" graph and simplified visualization
attr _ShowRent = false
```

### 2. Calculating Distance to Center

This section calculates the distance from the center of the market to each block using the Pythagorean theorem.

```cga
# Calculates distance from the center
distanceToCenter = sqrt((initialShape.origin.px)*(initialShape.origin.px)+(initialShape.origin.pz)*(initialShape.origin.pz))
```

### 3. Creating Rent Zones

The rent for each zone is calculated based on the Von Thunen model equation, taking into account yield, market price, production cost, and transportation cost.

```cga
# Creates rent zones
const L1 = Y1 * (PriceMarket1 - C) - Y1 * (distanceToCenter / 1000) * TransportCost1
const L2 = Y2 * (PriceMarket2 - C) - Y2 * (distanceToCenter / 1000) * TransportCost2
const L3 = Y3 * (PriceMarket3 - C) - Y3 * (distanceToCenter / 1000) * TransportCost3
```

### 4. Generating 3D Geometries

This section defines how to generate the 3D geometries for the lots and parcels based on the rent values. It uses conditional statements to extrude the parcels differently depending on whether `_ShowRent` is true or false.

```cga
# Generates 3D geometries
attr shapeType = "Lot"

Lot -->
case shapeType == "Lot":
    Parcel
else:
    color("#8C8C8C")

Parcel -->
case _ShowRent == false:
    # Extrudes lots based on Von Thunen zones
    case L1 > L2 && L1 > L3 && L1 > 0:
        extrude(rand(100, 300)) color("#4D87B3")
    case L1 < L2 && L2 > L3 && L2 > 0:
        extrude(rand(50, 150)) color("#C64F39")
    case L1 < L3 && L2 < L3 && L3 > 0:
        extrude(rand(5, 50)) color("#CFB549")
    else:
        color("#D3D3D3")
else:
    # Extrudes lots based on Von Thunen zones using Rent values
    case L1 > L2 && L1 > L3 && L1 > 0:
        extrude(L1) color("#4D87B3")
    case L1 < L2 && L2 > L3 && L2 > 0:
        extrude(L2) color("#C64F39")
    case L1 < L3 && L2 < L3 && L3 > 0:
        extrude(L3) color("#CFB549")
    else:
        color("#D3D3D3")
```

## Usage

1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/von-thunen-model.git
   cd von-thunen-model
   ```

2. **Open the project in CityEngine**: 
   - Import the `vonthunen.cga` rule file into your CityEngine project.

3. **Adjust parameters**:
   - Modify the attribute values for yield, market prices, and transportation costs as needed.

4. **Toggle visualization**:
   - Use the `_ShowRent` attribute to switch between the simplified model and the 3D rent graph.

## License

This project is licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt the material for any purpose, even commercially, as long as you provide appropriate credit, a link to the license, and indicate if changes were made.
```

This README provides a detailed explanation of the `vonthunen.cga` script, including its purpose, a breakdown of the code, and instructions for usage and licensing.
