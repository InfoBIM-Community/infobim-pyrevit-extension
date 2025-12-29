# InfoBIM pyRevit Extension

A custom [pyRevit](https://github.com/eirannejad/pyRevit) extension designed to provide detailed insights and reports for Revit elements, views, and spatial relationships.

## 🚀 Features

- **Scope Box–Driven Context**: Reports are built from the active **Scope Box** (spatial volume), independent of view visibility.
- **Advanced Spatial Detection**: Uses geometric queries (BoundingBox intersection, ray projection) to infer relationships between elements, rooms, and levels.
- **Unit Aware**: Formats lengths/areas/volumes using the project's unit settings.
- **Link-Aware**: Inspects elements inside **RVT links**. (IFC links planned.)
- **Customizable**: Supports category filtering for reports via `categories.json`.

## 🛠️ Tools

The extension adds an **InfoBIM** tab with a **Current View** panel containing the following tools:

### 1. 📋 General Report
Analyzes the currently active view and provides a comprehensive summary:
- **View Boundaries**: Reports coordinates for Scope Box, Crop Box, and Section Box (Min/Max points).
- **View Range**: Detailed top, cut, bottom, and depth offsets for plan views.
- **Elements in Scope**: Lists model elements and Revit links intersecting the Scope Box / Crop Box / Section Box (depending on view type).
    - *Configuration*: You can filter specific categories (Include/Exclude) by editing `categories.json` inside the tool's folder.

### 2. 🔍 Element Report
Provides a deep dive into the selected element's properties:
- **Identity Data**: ID, Name, Category, Family, Type.
- **Context**: Workset, Created Phase, Level.
- **Parameter Dump**: Lists all instance parameter values, formatting numbers and IDs for readability.

### 3. 🏢 Space Report
A powerful tool for spatial context. Select an element to see:
- **Room Detection**: Identifies which Room(s) the element belongs to or intersects with.
    - *Strategies*: Uses direct properties, phase-aware lookups, location points, and **BoundingBox intersection** (useful for elements touching multiple rooms).
- **Vertical Context**: Calculates vertical distances to associated levels and detects the **Top Level** (via parameters or geometry).

## 📦 Installation

### Method 1: Local Link (For Developers)
If you have the source code on your machine:
1. Open a terminal.
2. Run the pyRevit CLI command:
   ```bash
   pyrevit extend ui InfoBIM /path/to/infobim-pyrevit-extension
   ```

### Method 2: Git Clone
1. Open a terminal.
2. Add the extension via git URL:
   ```bash
   pyrevit extend ui InfoBIM https://github.com/InfoBIM-Community/infobim-pyrevit-extension.git
   ```

## Quick Start

1. Create/activate a **Scope Box** in your view.
2. Run **General Report** to inspect everything inside that spatial volume.
3. Select an element and run **Element Report** for deep parameters.
4. Run **Room Report** to understand room + vertical context.

## ⚙️ Configuration

**General Report Filters**:
To include or exclude specific categories from the "General Report", edit the `categories.json` file located in:
`InfoBIM.tab/Current View.panel/01_General Report.pushbutton/categories.json`

**Format:**
```json
{
  "blacklist": ["Walls", "Windows"],
  "whitelist": []
}
```

## 🧩 Requirements

- Autodesk Revit (2020+ recommended)
- [pyRevit](https://github.com/eirannejad/pyRevit)

## License

This project is licensed under the **Mozilla Public License 2.0 (MPL-2.0)**.

You are free to use, study and contribute to the code.
Modifications to existing source files must remain open.
Commercial use and proprietary integrations are allowed.
