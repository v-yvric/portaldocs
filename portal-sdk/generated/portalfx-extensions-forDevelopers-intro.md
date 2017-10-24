<a name="portalfxExtensionsForDevelopersIntro"></a>
<!-- link to this document is [portalfx-extensions-forDevelopers-intro.md]()
-->

## Introduction

The Azure Portal UI team supports Ibiza and the Portal Framework, and can help you with onboarding a service into the Management UI in the Azure portal.

Onboarding a service, or developing a portal extension, has three phases: private preview, public preview, and GA.  The development of a portal can stop at any one of those steps, depending on content.  A portal can also proceed to the next step when it meets the exit criteria for the current step. These phases are discussed in the sections named Private Preview, Public Preview, and GA. 

Most services that onboard Azure need to use the following three components:
*	Marketing content on the Azure Web site or other websites
*	Management APIs that are exposed via Azure Resource Manager (ARM) or Microsoft Graph
*	Management UI in the Azure portal and/or other tools/websites, like Visual Studio

The Azure onboarding process is streamlined to optimize the delivery of high quality experiences based on hundreds of hours of usability testing that meet Microsoft Common Engineering Criteria (CEC) and compliance requirements. Do not start designing UI or management APIs until after you've started the onboarding process to ensure you're following the latest patterns and practices. This will better optimize your time and reduce re-working due to anti-patterns and inconsistencies that block usability, performance, and other factors.

The Azure Fundamentals are a set of Tenets each Azure service is expected to adhere to. The Azure Fundamentals program is described in this document Azure Fundamentals. The document also identifies the Stakeholders and contacts for each of the Tenets.

The Azure Fundamentals document is located at [https://microsoft.sharepoint.com/teams/WAG/EngSys/Shared%20Documents/Argon/Azure%20Fundamentals%20Proposal/Azure%20Fundamentals%20Proposal.docx?d=wf5b821bc31c44042adb55ebf4d8b408d](https://microsoft.sharepoint.com/teams/WAG/EngSys/Shared%20Documents/Argon/Azure%20Fundamentals%20Proposal/Azure%20Fundamentals%20Proposal.docx?d=wf5b821bc31c44042adb55ebf4d8b408d).

Compliance criteria and practices are defined in Quality Essentials throughout our development cycle. These ensure services meet the Trusted Cloud commitments outlined in the Microsoft Azure Trust Center for our customers. These are mandatory procedures as Preview and GA requirement, and to be revisited for every release cycle. 

The Microsoft Azure Trust Center is located at [http://azure.microsoft.com/en-us/support/trust-center/](http://azure.microsoft.com/en-us/support/trust-center/).

To meet customer expectations and continue to increase customer satisfaction, several quality metrics are tracked for every extension. An overview of Quality Essentials is in the section named Quality Essentials. 

The Quality Essentials document is located at [https://microsoft.sharepoint.com/teams/QualityEssentials/SitePages/GettingStarted.aspx](https://microsoft.sharepoint.com/teams/QualityEssentials/SitePages/GettingStarted.aspx).

Nearly 70% of Azure users are from outside of the United States. Therefore, it is important to make Azure a globalized product. There are a few Internationalization requirements that your service is required to support. This is the same set of languages that are supported by Azure Portal for GA. For more information about internationalization requirements, see [http://aka.ms/azureintlrequirements](http://aka.ms/azureintlrequirements). 