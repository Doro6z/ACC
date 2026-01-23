# Proto Ready Pack — Plugin Template Guide

**Created**: 2026-01-22  
**Type**: Template Documentation

---

## Template Location

`Templates/PR_Module_Template/`

---

## How to Use This Template

### Step 1: Copy Template

```powershell
# Copy entire template folder
Copy-Item -Path "Templates/PR_Module_Template" -Destination "Plugins/PR_YourModule" -Recurse
```

### Step 2: Rename Files

**Replace `PR_Module_Template` with `PR_YourModule`** :

- `PR_Module_Template.uplugin` → `PR_YourModule.uplugin`
- `Source/PR_Module_Template/` → `Source/PR_YourModule/`
- All `.h` and `.cpp` files with `ModuleTemplate` → `YourModule`

### Step 3: Update .uplugin

Edit `PR_YourModule.uplugin` :

```json
{
    "FriendlyName": "Your Module Name",
    "Description": "Proto Ready Pack - Your module description",
    "Modules": [
        {
            "Name": "PR_YourModule",
            ...
        }
    ]
}
```

### Step 4: Update Build.cs

Rename `Source/PR_YourModule/PR_Module_Template.Build.cs` → `PR_YourModule.Build.cs`

Update class name :
```csharp
public class PR_YourModule : ModuleRules
{
    public PR_YourModule(ReadOnlyTargetRules Target) : base(Target)
    {
        // ... dependencies
    }
}
```

### Step 5: Customize Component/Data

Replace example files :
- `Public/Components/PR_ExampleComponent.h`
- `Public/Data/PR_ExampleData.h`

With your module's classes.

### Step 6: Test Compilation

1. Open project in UE5
2. Reload project (it will detect new plugin)
3. Compile (Development Editor)
4. Verify 0 errors, 0 warnings

---

## Template Structure

```
PR_Module_Template/
├── PR_Module_Template.uplugin
├── Resources/
│   └── Icon128.png
├── Source/
│   └── PR_Module_Template/
│       ├── Public/
│       │   ├── Components/
│       │   │   └── PR_ExampleComponent.h
│       │   └── Data/
│       │       └── PR_ExampleData.h
│       ├── Private/
│       │   ├── Components/
│       │   │   └── PR_ExampleComponent.cpp
│       │   ├── Data/
│       │   │   └── PR_ExampleData.cpp
│       │   └── PR_Module_TemplateModule.cpp
│       └── PR_Module_Template.Build.cs
├── Content/
│   ├── Demo/
│   │   └── DM_Example_Showcase.umap
│   └── Data/
│       └── DA_Example_Default.uasset
└── Documentation/
    └── README.md
```

---

*Template guide — Proto Ready Pack*
