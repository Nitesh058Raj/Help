# PCF Component Creation Guild:

Install Pac & NodeJS
Install MSBuild (VS)

Create Component to Edit
pac pcf init --namespace SampleNamespace --name SamplePCFControl --template field

```
npm install 
```

code edit 

```
npm run start
npm run build

mkdir Solutions
pac solution init --publisher-name "YourPublisherName" --publisher-prefix "prefix"

pac solution add-reference --path "path_to_your_pcf_project"


msbuild /t:build /restore
```

The generated solution files(.zip) are located inside the \bin\debug\ folder after the build is successful.

Import the Solution into Dynamics 365

Settings > Customizations > Publish All Customizations 

Add the PCF Control to a Form or View

Go to old solution editor, go in entity -> form -> edit form 
Double click field that you want to add custom control, Control tab -> Add control 

Publish 
