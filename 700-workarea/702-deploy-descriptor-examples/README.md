# Deploy Descriptor examples

Control-M Automation API enables you to use **Deploy Descriptor** to change job definition properties in JSON format before building, deploying, or running the JSON file. Using the Deploy Descriptor you can streamline your code across different environments (for example, between Development, Test or Production). Since each Control-M environment has different properties, the Deploy Descriptor enables you to programmatically manipulate them.

This page contains several Deploy Descriptor examples. For more information, please check the [Control-M Automation API Code Reference](https://docs.bmc.com/docs/display/public/workloadautomation/Control-M+Automation+API+-+Code+Reference), make sure you have your product version selected, and click on "*Deploy Descriptor*" on the left side of the page.

You can use the following Automation API service to test how a Deploy Descriptor applies on a workflow without performing any action on the Control-M environment:
```
ctm deploy transform MyWorkflow.json DeployDescriptor.json
```

To verify that the Deploy Descriptor is valid, you can use the "build" service:
```
ctm build DeployDescriptor.json
```

Once tested, you can build, deploy or run workflows on Control-M applying a Deploy Descriptor - e.g. for the "deploy" service:
```
ctm deploy MyWorkflow.json DeployDescriptor.json   
```
<br>

### Assign Control-M/Server
```
{ "Property" : "ControlmServer",
  "Assign"   : "my_ctm_server"
}
```

### Assign Host depending on Application
```
{ "Property" : "Host",
  "Source"   : "Application",
  "Replace"  : [ { "Test" : "test_server" },
                 { "HHRR" : "hhrr_server" },
                 { "Finance" : "finan_server" } ]
}
```

### Change RunAs user when Application starts with "Test"
```
{ "Property" : "RunAs",
  "Source"   : "Application",
  "Replace"  : [ { "Test.*" : "myuser" } ]
}
```

### Remove prefix "TST_" from Job name
```
{ "ApplyOn"  : { "Type" : "Job", "@" : ".*" },
  "Property" : "@",
  "Replace"  : [ { "TST_(.*)" : "$1" } ]
}
```

### Remove prefix "PRE_" from Folder name
```
{ "ApplyOn"  : { "Type" : "Folder", "@" : ".*" },
  "Property" : "@",
  "Replace"  : [ { "PRE_(.*)" : "$1" } ]
}
```

### Replace scripts path for production server
```
{ "ApplyOn"  : { "Type" : "Job:Script", "@" : ".*" },
  "Property" : "@.FilePath",
  "Assign"   : "/opt/bin/myapp01/scripts"
}
```
