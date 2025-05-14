# PushOrderToSAP (Salesforce Apex Integration)

This repository contains a Salesforce Apex class `PushOrderToSAP` that integrates with SAP via SOAP web services. It sends sales order data from Salesforce to SAP and processes the response to update Salesforce order records accordingly.

---

## 🚀 Features

- Sends approved Salesforce orders to SAP via a SOAP request
- Dynamically builds XML structure for order data
- Securely sends authentication using base64-encoded credentials
- Processes XML response from SAP to:
  - Update order SAP ID
  - Update message and status
- Supports previewing order data
- Clean modular design following Apex best practices

---

## 🧩 Components

### Main Class
- `PushOrderToSAP.cls` – Apex controller class that:
  - Sends order data to SAP
  - Processes the XML response
  - Updates Salesforce objects accordingly

### Apex Methods
- `@AuraEnabled static String pushOrder(Id orderId)`
- `@AuraEnabled static List<Order> orderPreview(Id sales)`
- `@AuraEnabled static String userprof()`

---

## 🛡️ Security

- Endpoint and credentials are dynamically fetched from a custom metadata/config object (`GetApidetail__c`)
- All sensitive operations are handled securely
- **Recommended**: Migrate authentication to [Named Credentials](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_callouts_named_credentials.htm) for enhanced security and maintainability

---

## 🧪 Testing

- The class is structured to allow unit testing via mock responses and dependency injection patterns
- A separate test class should be written to cover:
  - Valid SOAP response handling
  - Error handling and rejection logic
  - Various order scenarios (ZSUG, ZDSO)

---

## 📂 Folder Structure


src/
├── classes/
│   ├── PushOrderToSAP.cls
│   └── PushOrderToSAP.cls-meta.xml
├── README.md


 Prerequisites
Salesforce DX or Developer Org

Order object with custom fields like SAP_ID__c, Order_Typelookup__r.code__c

Custom metadata or custom setting: GetApidetail__c with Username__c, Password__c, Endpoint__c

Connected SAP endpoint ready to receive SOAP messages


Deployment
Use Salesforce DX, Workbench, or Metadata API to deploy:

sfdx force:source:deploy -p force-app/main/default/classes/PushOrderToSAP.cls
Or use Change Sets in a sandbox-to-prod deployment.


📌 Notes
This solution assumes that the SAP system adheres to a strict XML structure.

All SOAP headers, nodes, and namespace bindings are handled according to SAP integration specs.

