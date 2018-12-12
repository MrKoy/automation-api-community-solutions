# Deploy Descriptor samples

For any of these sample integrations to work, the **Control-M Automation Command Line Interface (CLI)** must be installed on the same computer as the IDE tool or code/text editor, and configured for the required Control-M endpoint(s). For more details, please check the [Control-M Automation API Installation](https://docs.bmc.com/docs/display/public/workloadautomation/Control-M+Automation+API+-+Installation) documentation and look for "*Installing the Control-M Automation CLI*".


Following lines need "jq" installed - https://stedolan.github.io/jq/
To install on Linux 64b:
wget -O jq https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64
chmod 755 ./jq
mv ./jq /usr/bin

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
