# Personal Portfolio Feature - Deployment Guide

This repository folder contains the metadata for a reusable Salesforce Portfolio feature built with Lightning Web Components and a small Apex controller. Use this guide to deploy to any Salesforce org.

## Components Included

- LWC: `portfolioMain`, `navbar`, `heroSection`, `aboutSection`, `skillsSection`, `projectsSection`, `contactSection`, `footer`, `toastMessage`
- Apex: `ContactSectionController`
- Custom Label: `Resume_File_Title`
- Custom Object: `Enquiry__c` (for contact form submissions)
- Static Resources: `MyResume`, `prasad_profile`

## Prerequisites

- Salesforce CLI installed
- A default org set (use `sf org login web` and `sf config set target-org=<alias>`)

## Deploy using portfolio manifest

1. Pull the repo and open the project in VS Code.
2. Deploy the portfolio package:

```powershell
sf project deploy start -x manifest/portfolio-package.xml
```

## Post-deploy setup

1. Ensure Custom Label `Resume_File_Title` exists and matches the Title of your uploaded file in Files. If missing, create it or update the value.
2. Upload your resume and set Title to the value in the label (e.g., `MyResume`). Alternatively, keep `Static Resource` named `MyResume` – the hero component can download from it.
3. Create a Lightning App Page and drop `portfolioMain` onto the page. Activate as needed (App/Home/Record page or Experience site).

## Notes

- The contact form writes to `Enquiry__c`. Make sure the object and fields exist in target org. If not, you may need to migrate or recreate the fields.
- Email sending in `ContactSectionController` uses `Messaging.SingleEmailMessage` to a hard-coded address. Update as needed or externalize to Custom Metadata.
- The `toastMessage` LWC is a local utility for community compatibility.

## Troubleshooting

- Missing object/fields: Validate `Enquiry__c` exists with fields: `Email__c`, `Message__c`, `Mobile_Number__c`, `Person_Name__c`, `Subject__c`.
- Static resource not found: Ensure `MyResume` and `prasad_profile` exist under Static Resources.
- Custom label missing: Create `Resume_File_Title` via Setup > Custom Labels.
