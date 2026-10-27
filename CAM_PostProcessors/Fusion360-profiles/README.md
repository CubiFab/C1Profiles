# CubiFab C1 Post Processor for Autodesk Fusion (Fusion 360)

This folder contains the CubiFab C1 post processor for Autodesk Fusion. Use it to generate NC files from toolpaths in the Manufacture workspace.

| Item | Value |
| --- | --- |
| Post processor file | [CubifabC1.cps](CubifabC1.cps) |
| Name displayed in Fusion | `Cubifab C1` |
| Supported configuration | Three-axis milling (X, Y, and Z). |
| Output file extension | `.nc` |

The current Fusion package supports three-axis milling only.

**Metric output only:** Select **Millimeters (mm)** when posting. Imperial (inch) output is not supported and must not be used.

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
6. Enter the program name, output filename, and destination folder. Set **Units** to **Millimeters (mm)**.
7. Apply the settings in [Configure the NC Program](#configure-the-nc-program). Before clicking **Post**, confirm **Units = Millimeters (mm)** and **Output tool number = Checked**, then generate the `.nc` file in the selected output folder.
8. Review the generated NC file, including units, work offsets, the tool and tool-change sequence, and safe retracts.
9. Simulate, inspect the code, then perform a controlled single-block check without cutting before machining.

Do not run the program if the units, tool-change sequence, or retract path are incorrect.

Dialog labels may vary with the Fusion version or interface language. Autodesk also provides a guide to [selecting a post processor in the NC Program dialog](https://help.autodesk.com/cloudhelp/ENU/Fusion-CAM/files/MFG-REF-NC-PROGRAM-POST-SELECTION.htm).

## Configure the NC Program

Use the following settings for XYZ three-axis machining. Review each group in the **Post Process / NC Program** dialog before posting.

### NC Program Settings

| Interface item | Select or enter |
| --- | --- |
| Post | **Cubifab C1** / `CubifabC1` |
| Use machine configuration | Unchecked |
| Use cascading post | Unchecked |
| Name / number | Enter the program number, e.g. `1001`. |
| File name | Enter the NC file name, e.g. `1001`. |
| Comment | Optional; leave blank if not needed. |
| Output folder | Select the folder for the generated NC file. |
| Publish to Fusion hub | Unchecked |
| NC extension | `.nc` |
| Units | **Millimeters (mm)** |
| Open NC file in editor | Checked |
| Create NC Program / Name | Checked; enter a job-specific name. |

### Preferences and Safe Retracts

| Property | Setting | Use |
| --- | --- | --- |
| Split file | **No splitting** | Generates a single NC file. **Split by tool** and **Split by toolpath** are available for workflows requiring separate files. |
| Output M6 | **Checked**, subject to the condition below. | Outputs `M6` for tool changes. |
| Output tool number | **Checked** | Outputs tool numbers (`T` codes). Keep checked when using the C1 automatic tool changer. |
| Safe Retracts | **G28**, subject to the condition below. | Uses the G28 return method for safe retracts. |

Use **M6** and **G28** only after confirming the tool-change workflow and G28 return path for your C1 configuration. If either is unconfirmed, contact technical support before running the program.

### Formats

| Interface item | Setting |
| --- | --- |
| Use sequence numbers | **No** |
| Start sequence number | `10` |
| Sequence number increment | `1` |
| Separate words with space | Checked |
| Write machine | Checked |
| Write tool list | Checked |

The start number and increment apply when sequence-number output is enabled.

### Built-in Parameters

Keep the following values unless instructed otherwise by technical support.

| Interface item | Setting |
| --- | --- |
| Allow helical moves | Checked only when both the controller and post support helical interpolation; otherwise unchecked. |
| High feedrate mapping | **Preserve rapid movement** |
| High feedrate | `5000.00 mm/min` |
| Maximum circular radius | `1000.00 mm` |
| Minimum chord length | `0.250 mm` |
| Minimum circular radius | `0.010 mm` |
| Tolerance | `0.002 mm` |

Enable **Allow helical moves** only after confirming helical-interpolation support for your controller and post.

## Update the Post Processor

When you download a newer `CubifabC1.cps`, import the updated file into your Local Post Library and select that version in your NC Program before posting again. Recheck the configuration above, especially **Units** and **Output tool number**.

## Troubleshooting

| Problem | What to check |
| --- | --- |
| Cubifab C1 does not appear in the post list. | Confirm that the file was imported into **My posts > Local**. Check any active library filters and look for the display name **Cubifab C1**. |
| Fusion uses a different post processor. | Open the NC Program settings and select **Cubifab C1** from your Local library. |
| Tool-number (`T`) commands are missing. | Check **Output tool number** in the post properties and regenerate the NC file with this option checked. |
| M6 commands are missing. | Check **Output M6** in the post properties, and confirm the tool-change workflow before enabling it. |
| Several NC files are generated. | Set **Split file** to **No splitting** if you want one output file. |
| The program uses inch units or the wrong scale. | Set **Units** to **Millimeters (mm)** and regenerate the NC file. Do not machine with inch output. |
| The retract path is incorrect or unconfirmed. | Check **Safe Retracts** and the G28 return path for your C1 configuration. Contact technical support before running the program. |

[Back to C1Profiles](../../README.md)
