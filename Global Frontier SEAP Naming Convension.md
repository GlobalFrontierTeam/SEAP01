# Global Frontier SEAP Naming Convension

Below naming convention is expected to be followed for Monsanto Global Salesforce SE Project. If developer comes across any new types other than listed below, naming convention has to be first agreed within the team and document should be updated and circulated. All development objects should be prefixed with module name e.g SFA and suffixed by its type if required.

This will help in identifying what belongs to specific application and helps in changeset creation as well

| Type of development | Format |Example |
| ------ | ------ | ------ |
|GF_CalculateEstimate_BL | GF_<classname>_<Type> | GF_CalculateEstimate_BL |
|GF_CalculatEestimate_VFC|GF_<classname>_VFC|GF_CalculatEestimate_VFC|
|GF_CalculatEestimate_VFC_Test|GF_<classnametobetested>_<VFC>_Test|GF_CalculatEestimate_VFC_Test|
|GF_LC_CalculateEstimate|GF_LC_<lightningcomponentbundle>|GF_LC_CalculatEestimate|
|GF_LA_CalculateEstimate|GF_LA_<lightningapplication>|GF_LA_CalculatEestimate|
|GF_LE_CalculateEstimate|GF_LCE_<lightningcomponentevent>|GF_LCE_CalculatEestimate|
|GF_LE_CalculateEstimate|GF_LAE_<lightningapplicationevent>|GF_LAE_CalculatEestimate|
|GF_CalculateEstimate_VFP|GF_<pagename>_VFP|GF_CalculateEstimate_VFP|
|GF_BrandEstimate_Trigger|GF_<objectname>_Trigger|GF_BrandEstimate_Trigger|
|GF_calculatebrand_ Batch|GF_<batchname>_Batch|GF_calculatebrand_ Batch|
|GF_CalculateEstimateAnnual_ Schedule|GF_<schedulableclassname>_Schedule|GF_CalculateEstimateAnnual_ Schedule|
|GF_CMCOUsers_CS|GF_<Customsettingname>_CS|GF_CMCOUsers_CS|
|GF_HelptextonLandingPage_CL|GF_<customlabelname>_CL|GF_HelptextonLandingPage_CL|
|GF_BrandEstimate_checkfornewrecords|GF_<objectname>_<workflowname>|GF_BrandEstimate_checkfornewrecords|

