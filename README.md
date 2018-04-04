# HP SiteScope (One-way) Integration
The information provided details the instructions to configure a one-way integration to trigger a web service call to xMatters.

# Pre-Requisites
* HP SiteScope 11.32.301

# Files
* [SiteScope Communication Plan](SiteScope.zip) - The JSON mapping file for SiteScope
* [SiteScope Mapping File](xMatters) - The JSON mapping file for SiteScope

# How it works
SiteScope uses Action Alerts that are capable of performing HTTP Rest Web Service calls to xMatters to generate an xMatters alert. The Action Alerts are configured to run based on trigger conditions in SiteScope.

# Installation

### Import the Communication Plan
* Import the SiteScope Communication Plan [SiteScope Communication Plan](SiteScope.zip)
* Instructions to import a Communication Plan can be found here: [Import a Communication Plan](http://help.xmatters.com/OnDemand/xmodwelcome/communicationplanbuilder/exportcommplan.htm)

### Import Communication Plan

### Create a REST user account
* **First Name:** SiteScope
* **Last Name:** Rest Web Service
* **User ID:** sitescope
* **Roles:** REST Web Service User

### Assign permissions to the Communication Plan, Form, and Endpoint  
1. **Communication Plan**
    * From within the Developer tab, select the Edit drop-down menu for the SiteScope communication plan
    * From the Edit drop-down menu, select Access Permissions
    * From within Access Permissions, add the xMatters REST User created

2. **Form**
    * From within the Developer tab, select the Edit drop-down menu for the SiteScope communication plan
    * From the Edit drop-down menu, select Forms
    * From within Forms, select the Web Service drop-down menu for the SiteScope form
    * From within Web Service drop-down menu, select Sender Permissions
    * From within Sender Permissions, add the xMatters REST User created

3. **Endpoint**
    * From within the Developer tab, select the Edit drop-down menu for the SiteScope communication plan
    * From the Edit drop-down menu, select Integration Builder
    * From within the Integration Builder tab, select Edit Endpoints
    * From within Edit Endpoints, add the xMatters REST User created

## HP SiteScope

### Deploy the xMatters REST Mapping File

1. Navigate to the server that contains the SiteScope root directory
2. Navigate to the following directory: `<SiteScope root directory>\templates.rest`
3.From within the `\templates.rest` directory, add the [xMatters](xMatters) file.

### Configure a SiteScope Alert

This task describes the steps involved in configuring an alert definition.

#### Prerequisites

Only a SiteScope administrator user, or a user granted the appropriate alerts permissions can view, create, or edit alerts. For details on user permissions, see Permissions.

#### Create an alert

You can create a new alert or copy an existing alert into any group or monitor container in the SiteScope tree.

To create a new alert:
1. Right-click the container to which you want to associate the alert, and select New > Alert.
2. Enter a name for the alert.
3. Configure an alert action (in the Alert Actions panel, click New Alert Action to start the Alert Action wizard).
4. For Action Type select Rest.

<kbd>
  <img src="https://github.com/matthewhenry1/xm-labs-sitescope/blob/master/media/action_type.png">
</kbd>

5. Once Rest is selected, on the next window ensure that xMatters is selected for template.


<kbd>
  <img src="https://github.com/matthewhenry1/xm-labs-sitescope/blob/master/media/action_type_settings.png">
</kbd>

#### User interface elements are described below:

**Action name** The name given to the action to be done when the alert is triggered. It is not the name of the alert.

**Rest to URL form** <INSERT STEPS TO INSERT INTEGRATION BUILDER URL>

**Template** xMatters

Note: You can view the contents of the existing templates or add additional templates in the `<SiteScope root directory>\templates.rest` directory. For more details on alert templates, see [Customize Alert Templates](http://sitescope-help.saas.hpe.com/en/11.40/Online/Content/Use/cust_alert_templates.htm).

**HTTP Method** Select the HTTP method for the Rest alert action.

Default Value: POST

**Format Type**	Select the format type for the Rest alert action.

Default Value: JSON

**Additional Parameters**	Enter any parameter that REST API supports. You must enter all the additional parameters used in the template. The format for providing the parameters is <name> = <value> with multiple parameters separated by commas. The <name> specified here must match the parameter name specified in the template.

Note: If there are additional parameters specified in the template and if you do NOT specify in this field, then it results in an error. You can see the error messages in the alert.log file in the SiteScope Logs directory located at <install_dir>/Sitescope/logs .

#### Relevant tasks
[Configure SiteScope Alerts](http://sitescope-help.saas.hpe.com/en/11.40/Online/Content/Use/alert_workflow.htm)

#### See also
[Alert Action Dialog Box](http://sitescope-help.saas.hpe.com/en/11.40/Online/Content/Use/Action_Type_Settings_Panel.htm)

### Editing the Filter
This task describes how to customize SiteScope alert templates to alter the content and format of alert messages.
1. Open a text editor that has access to the alert template directories on the SiteScope machine.

For a list of the directory names containing SiteScope alert templates, see [Alert Template Directories](http://sitescope-help.saas.hpe.com/en/11.40/Online/Content/Use/cust_alert_templates.htm#Alert_Template_Directories).

2. Open an existing template file of the alert type you want to customize within a text editor.

3. Make changes to the template. Depending on the alert type, you can add or remove text, change the order of text or property variables, or add other property variables. To add specific properties, add the applicable property variable name between < > bracket pairs to the template.

For a list of specific property variables, see [Properties Available in Alerts, Templates, and Events](http://sitescope-help.saas.hpe.com/en/11.40/Online/Content/Use/alert_properties_directory.htm).

4. Save the changes to a unique filename within the directory for the applicable alert type. The new template is added to the Action Type Settings Template drop-down list.

# Testing
For testing execute the action to occur.
