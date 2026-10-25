# CubiFab C1 Post Processor for Autodesk Fusion (Fusion 360)

This folder contains the CubiFab C1 post processor for Autodesk Fusion. Use it to generate NC files from toolpaths in the Manufacture workspace.

| Item | Value |
| --- | --- |
| Post processor file | [CubifabC1.cps](CubifabC1.cps) |
| Name displayed in Fusion | `Cubifab C1` |
| Supported configuration | Three-axis milling (X, Y, and Z). |
| Output file extension | `.nc` |

The current Fusion package supports three-axis milling only.

## Install the Post Processor

1. Download or locate `CubifabC1.cps` in this folder.
2. Start Autodesk Fusion and switch to the **Manufacture** workspace.
3. Open **Manage > Post Library**.
4. Under **My posts**, select **Local**.
5. Click **Import**, select `CubifabC1.cps`, and complete the import.
6. Confirm that **Cubifab C1** appears in your Local library, then close the Post Library.

This installs the post in your personal Local library. For details about library locations and importing posts, see Autodesk's [Post Library documentation](https://help.autodesk.com/cloudhelp/ENU/Fusion-CAM/files/MFG-POSTPROCESSOR-LIBRARY-REF.htm).

## Generate an NC File

1. Open your design and switch to **Manufacture**.
2. Create or open a milling setup. Set the stock, work coordinate system, and tools for your job.
3. Generate and simulate the three-axis toolpaths you want to output.
4. Select the setup or operations, then choose **Post Process** to open the NC Program dialog.
5. In the **Post** selector, choose **Choose from Library** or click the folder icon. Open your **Local** library, select **Cubifab C1**, and click **Select**.
6. Enter the program name, output filename, and destination folder. Check the output units against your machining setup.
7. Review the post properties described below, then click **Post** to generate the `.nc` file.
8. Review the generated NC file, including work offsets, retract moves, and tool changes, before machining.

Dialog labels may vary with the Fusion version or interface language. Autodesk also provides a guide to [selecting a post processor in the NC Program dialog](https://help.autodesk.com/cloudhelp/ENU/Fusion-CAM/files/MFG-REF-NC-PROGRAM-POST-SELECTION.htm).

## Post Properties

The supplied post includes these options:

| Property | Default | Use |
| --- | --- | --- |
| Output tool number | Enabled | Outputs tool numbers (`T` codes). Keep enabled when using the C1 automatic tool changer. |
| Output M6 | Enabled | Outputs `M6` for tool changes. Keep enabled when using the C1 automatic tool changer. |
| Split file | No splitting | Generates a single NC file. Select **Split by tool** or **Split by toolpath** if your workflow requires separate files. |

Choose property values to match your machine configuration and machining workflow.

## Update the Post Processor

When you download a newer `CubifabC1.cps`, import the updated file into your Local Post Library and select that version in your NC Program before posting again.

## Troubleshooting

| Problem | What to check |
| --- | --- |
| Cubifab C1 does not appear in the post list. | Confirm that the file was imported into **My posts > Local**. Check any active library filters and look for the display name **Cubifab C1**. |
| Fusion uses a different post processor. | Open the NC Program settings and select **Cubifab C1** from your Local library. |
| Tool numbers or M6 commands are missing. | Check **Output tool number** and **Output M6** in the post properties. |
| Several NC files are generated. | Set **Split file** to **No splitting** if you want one output file. |

[Back to C1Profiles](../../README.md)
