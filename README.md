PCB Component Placement System

## Overview

This project implements a **2D rectangular packing algorithm** for placing electronic components on a 50×50 unit PCB board. The solution is designed to satisfy strict placement constraints (hard constraints) and optimize layout efficiency (soft constraints). The final output includes a visualization of the placed components, their labels, and constraint zones.

## Problem Definition

We are tasked with placing five components on a rectangular PCB:

* **USB\_CONNECTOR (5×5)** – must touch the board edge.
* **MICROCONTROLLER (5×5)** – can be placed anywhere.
* **MIKROBUS\_CONNECTOR\_1 (5×15)** – must touch the board edge.
* **MIKROBUS\_CONNECTOR\_2 (5×15)** – must touch the opposite edge, parallel to MB1.
* **CRYSTAL (5×5)** – must be within 10 units of the microcontroller.

Constraints include:

* **Edge placement** for certain components.
* **Parallel placement** of MikroBus connectors on opposite sides.
* **Proximity constraint** between Crystal and Microcontroller.
* **Non-overlapping and boundary compliance**.
* **Center of mass alignment** within 2 units of board center.
* **Keep-out zone restriction** to avoid USB interference.

Soft constraints:

* Minimize wasted space.
* Prefer central placement when possible.

## Algorithmic Approach

1. **Pre-placement phase**:

   * Place USB connector and MikroBus connectors on board edges, ensuring MB1 and MB2 are opposite and parallel.

2. **Microcontroller placement**:

   * Place near the center of the board, adjusting position to balance mass and satisfy other constraints.

3. **Crystal placement**:

   * Select a location within 10 units of the microcontroller center.
   * Ensure the crystal–microcontroller path does not intersect the USB keep-out zone.

4. **Constraint Validation**:

   * After placing each component, verify constraints (edge, proximity, overlap, keep-out, and center of mass).

5. **Optimization**:

   * Evaluate placement candidates using a scoring function for compactness and balance.
   * Choose the best candidate under the 2-second runtime constraint.

## Technical Implementation

* **Language**: Python
* **Visualization**: Matplotlib (for board, components, labels, and keep-out zone)
* **Placement Strategy**: Greedy heuristic + constraint validation
* **Execution Time**: Under 2 seconds

## Input

* Component list and board size are predefined in the script.

## Output

* A plot showing:

  * Board boundaries
  * All component rectangles with labels
  * Proximity circle (for crystal)
  * USB keep-out zone rectangle

## File Structure

```
├── pcb_placement.ipynb   # Main notebook with algorithm and visualization
├── README.md             # Documentation (this file)
```

## How to Run

1. Open the notebook `pcb_placement.ipynb` in Jupyter or VSCode.
2. Run all cells.
3. The final output will display the PCB layout visualization.

## Example Visualization

* Board (50×50 grid)
* Components placed respecting edge, proximity, and mass balance
* Crystal proximity circle
* USB keep-out zone

## Future Improvements

* Replace heuristic approach with **metaheuristics** (simulated annealing, genetic algorithms) for better optimization.
* Add support for variable-sized boards.
* Extend to handle arbitrary number of components with different constraints.
