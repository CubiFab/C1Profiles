# CubiFab C1 Post Processors for Siemens NX (UG)

This folder contains Siemens NX CAM post processors for the CubiFab C1 CNC machine. Follow the steps below to install a post processor, add it to the NX post processor list, and generate an NC file from your CAM toolpaths.

## Available Post Processors

| Post processor | Source folder | Use |
| --- | --- | --- |
| `CubifabC1-3axis` | `CubifabC1-NX-3axis` | Three-axis milling (X, Y, and Z). |
| `CubifabC1-A-4axis` | `CubifabC1-NX-4axis` | Four-axis milling with an A-axis rotary table rotating about X. |

Each post processor consists of three files with the same base name:

- `.tcl`: Post-processing logic.
- `.def`: NC output definitions and formats.
- `.pui`: Post Builder configuration for editing the post processor.

Both supplied posts use millimeters by default and specify `NC` as the output file extension.

## Install the Post Processor

### 1. Locate the NX postprocessor folder

Close NX, then open the `MACH\resource\postprocessor` folder inside your NX installation directory. For example, the NX 10.0 path shown in the reference guide is:

```text
C:\Program Files\Siemens\NX 10.0\MACH\resource\postprocessor
```

Replace `NX 10.0` with your installed version and use your actual installation location. If your organization uses a customized NX configuration, use its configured postprocessor folder.

### 2. Copy the post processor files

Copy all three files from the package you want to install directly into the NX `postprocessor` folder.

For **three-axis milling**, copy these files from `CubifabC1-NX-3axis`:

```text
CubifabC1-3axis.tcl
CubifabC1-3axis.def
CubifabC1-3axis.pui
```

For **four-axis milling**, copy these files from `CubifabC1-NX-4axis`:

```text
CubifabC1-A-4axis.tcl
CubifabC1-A-4axis.def
CubifabC1-A-4axis.pui
```

You can install both packages. Keep the filenames unchanged, and place the files directly alongside `template_post.dat` so that the entries below resolve correctly.

### 3. Add the posts to template_post.dat

In the same NX `postprocessor` folder:

1. Make a backup copy of `template_post.dat`.
2. Open `template_post.dat` in a plain-text editor, such as Notepad.
3. Add the following entries, one per line, alongside the existing post processor entries. If you installed only one package, add only its matching line.

```text
CubifabC1-3axis,${UGII_CAM_POST_DIR}CubifabC1-3axis.tcl,${UGII_CAM_POST_DIR}CubifabC1-3axis.def
CubifabC1-A-4axis,${UGII_CAM_POST_DIR}CubifabC1-A-4axis.tcl,${UGII_CAM_POST_DIR}CubifabC1-A-4axis.def
```

Each line contains the name displayed in NX, the `.tcl` path, and the `.def` path, separated by commas. Keep `${UGII_CAM_POST_DIR}` exactly as written; NX uses it to locate the postprocessor folder. The `.pui` file is not included in this registration line.

Save the file as `template_post.dat`, retaining the existing entries and file encoding. Make sure the editor does not add a `.txt` extension. Writing to an installation under `Program Files` may require administrator permissions.

### 4. Restart NX

Start NX and open the **Postprocess** dialog in Manufacturing. The post processor list should now include `CubifabC1-3axis`, `CubifabC1-A-4axis`, or both, depending on which entries you added.

## Generate an NC File

1. Open your CAM part in NX and switch to **Manufacturing**.
2. Configure the machining coordinate system, tools, and operations, then generate the required toolpaths.
3. Right-click the program or operation you want to output and select **Postprocess**.
4. Select **CubifabC1-3axis** for three-axis machining, or **CubifabC1-A-4axis** for machining with the A-axis rotary table.
5. Under **Output File**, choose the destination folder and enter the output filename. Use `NC` as the file extension.
6. Leave **Units** set to **Post Defined** to use the post's default millimeter output. Other dialog labels may vary with your NX version or interface language.
7. Click **OK** to generate the NC file.
8. Review the generated code and verify the toolpaths before machining. For four-axis work, check that the rotary axis setup and A-axis direction match the physical machine.

## Troubleshooting

| Problem | What to check |
| --- | --- |
| The post does not appear in the list. | Confirm that you edited the `template_post.dat` used by your NX installation, added the matching entry, saved the file, and restarted NX. |
| NX cannot find a `.tcl` or `.def` file. | Check that both files are directly in the configured postprocessor folder and that their filenames match the registration entry exactly. |
| You cannot save files in the NX installation folder. | Use an editor with the required administrator permissions, or ask your NX administrator to install the files. |


