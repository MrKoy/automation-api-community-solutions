# Notepad++ additional examples

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

<br>

> Note that all operations are performed by default on the current Automation API environment (as displayed via "**ctm env show**"). If you want to create operations for multiple environments, you can use the "**-e \<environment>**" option.

ctm_test_run.sh

-	This one will run in Control-M all folders & jobs defined in a JSON file, and check that they have all completed with OK status.
-	This is the script I am using in my Jenkins demo to show how we can invoke the API for automatic testing of workflows – together with the rest of testing Jenkins can perform for applications code.
-	This one uses the commands from the AAPI DevKit, so it has to be installed and configured for the user running the script (with the proper CTM environment defined etc).
-	Read the script contents for the parameters needed.
-	It will check the statuses of all folders/jobs every <timeout> seconds for a max of <retries>. It completes when all jobs/folders are in OK status.
-	If any of the jobs/folders is not in OK status (this is, in any other status), it will keep looping for a max of <retries> x <timeout> seconds.
-	Take that in mind – if all your jobs in your JSON file take e.g. 120 secs to complete and you define 5 retries every 10 seconds, you will never get the script to complete ok. Same if one of your jobs is not executed due to conditions or whatever.
-	To show the progress, you can uncomment the line “echo $jobs_stats”, and you will see one line per iteration with the statuses of all folders/jobs.
-	Also needs “jq” installed.
  
  -	Needs “jq” installed in your Linux system to work (easy to install, check https://stedolan.github.io/jq/). “jq” is very useful to parse, filter and format JSON in a script.
