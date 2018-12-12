# Deploy Descriptor examples

Control-M Automation API enables you to use **Deploy Descriptor** to change job definition properties in JSON format before building, deploying, or running the JSON file. Using the Deploy Descriptor enables you to streamline your code across different environments (for example, between Development, Test or Production). Since each Control-M environment has different properties, the Deploy Descriptor enables you to programmatically manipulate them.

This page contains several Deploy Descriptor examples. For more information, please check the [Control-M Automation API Code Reference](https://docs.bmc.com/docs/display/public/workloadautomation/Control-M+Automation+API+-+Code+Reference), make sure you have your product version selected, and click on "*Deploy Descriptor*" on the left side of the page.

You can use the following Automation API service to test how a Deploy Descriptor applies on a workflow without performing any action on the Control-M environment:
```
ctm deploy transform <definitionsFile> <deployDescriptorFile>
```
Once tested, you can build, deploy or run workflows on Control-M applying a Deploy Descriptor - e.g. for the "deploy" operation:
```
ctm deploy <definitionsFile> [deployDescriptorFile]   
```

Here are additional examples of commands to invoke the Control-M Automation API. These have been created and configured for **Notepad++**, but could potentially be adapted for other IDE tools or code/text editors.
   
To integrate them in Notepad++ you have two options:

   1. Do it manually for each operation, following the instructions in [**Integration with Notepad++**](/601-integration-with-ides-and-code-editors/integration-with-notepad++.md). 
   
      * make sure the NppExec plugin is installed (as explained in [Integration with Notepad++](/601-integration-with-ides-and-code-editors/integration-with-notepad++.md)) and then close Notepad++
      * unzip the file and copy (overwrite) the existing “contextMenu.xml” in your “%APPDATA%\Notepad++” folder
      * copy the other two files to “%APPDATA%\Notepad++\plugins\config”

<br>

### Run workflow
```
NPP_CONSOLE 0
set local TMP_FILE="$(CURRENT_DIRECTORY)\$(NAME_PART)_runid.tmp"
cmd /c ctm run "$(FULL_CURRENT_PATH)" > $(TMP_FILE) 2>&1
NPP_OPEN $(TMP_FILE)
cmd /c del $(TMP_FILE)
```
* It will open a temp file containing the command output (which includes the **runId**)
