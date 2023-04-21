# RIDAGOP toolkit ProcessPage-Schema

*A process-page description file for the RIDAGOP toolkit*

## Properties

- **`title`** *(string)*: The title of the process page.
- **`process`** *(object)* **(required)** : The process to be used. Either the full instance or a uri to the process description.
  - **`$comment`** *(string)*
  - **`uri`** *(string/format: uri)*: The uri to the process description.
  - **`instance`**: The full process instance, which needs to be a valid Process. Refer to *[process](/Schema/process)*.
- **`services`** *(object)* **(required)** : Process-page description for the services to be used in the process. The services here must match the services in the process.
  - **Additional Properties**: Refer to *[PP-Service](#pp-service)*.
- **`uri`** *(string)*
- **`view`** *(object)*: The type property of the view defines if the page view should be generated (build) or if specified ui elements should be mapped to existing ui elements in the html page.
  - **`type`** *(string)*: Must be one of: `['build', 'map']`.
- **`scriptUri`** *(string/format: uri-reference)*: Absolute or relative url to the process-page module. this module will be merged with the process module. Activities can use the module function when they specify a 'moduleFunction' instead of 'bridgeCapability'.
- **`common`** *(object)*: Settings for the common part. Common activities can reference to all services.
  - **`ui`**: Settings of the common UI part. Refer to *[PP-UISettings](#pp-uisettings)*.
- **`schemaUri`** *(string)* **(required)** : The uri to the RIDAGOP schema to be used. The uri of this file.
- **`local_prefix_path`** *(string)*
## Definitions

<h2 id="pp-service">PP-Service</h2>
- **`PP-Service`** *(object)*: A service as it is defined in the ProcessPage. Compared to Services defined in the Process, these cannot define activities.
  - **`title`** *(string)*: The title of the service.
  - **`ui`**: Settings of the service UI part. Refer to *[PP-UISettings](#pp-uisettings)*. Default: `{}`.
  - **`parameters`** *(object)*: Parameters that are available to all activities of the service.
    - **Additional Properties**: Refer to *[process#P-Parameter](/Schema/process#p-parameter)*.
  - **`autostart`**: List of activities (names/keys in the the activities objects) that should be started automatically on startup (either a string or a list of strings).
  - **`bridge`**: The bridge definition for the service. Refer to *[process#P-BridgeDefinition](/Schema/process#p-bridgedefinition)*.
<h2 id="pp-uisettings">PP-UISettings</h2>
- **`PP-UISettings`** *(object)*: UI settings.
  - **`sections`** *(object)*: Each service has three sections: input, output and status.
    - **`input`** *(object)*: The input section of the UI. This section is used to specify all the UI input elements (inputFields, buttons, checkboxes, ...)for the service.
      - **`display`** *(boolean)*: Whether to display the input section. Note that the service UI is more elaborate in the process description. Default: `True`.
      - **`inputFields`** *(object)*: The input fields (textfields) of the service.
        - **Additional Properties** *(object)*
          - **`default`** *(string)*: Overwrite the default parameter of the process.
          - **`display`** *(boolean)*: Whether to display the input field. Default: `True`.
      - **`buttons`** *(object)*
      - **`checkBoxes`** *(object)*
      - **`blocks`** *(array)*
        - **Items** *(object)*
          - **`name`** *(string)* **(required)** 
          - **`title`** *(string)*
          - **`description`** *(string)*
          - **`items`** *(array)* **(required)** 
            - **Items** *(string)*
    - **`output`** *(object)*: Settings for the output section. This can be used to display results of an activity.
      - **`display`** *(boolean)*: Whether to display the output section. Default: `True`.
    - **`status`** *(object)*
      - **`display`** *(boolean)*: Default: `True`.
  - **`display`** *(boolean)*: Whether for the display of the page. This is only relevant when the page is generated (build). Default: `True`.