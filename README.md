# Calculate Client Security Hash - UiPath Automation Process

## 1. Project Description

This UiPath robot automates the process of calculating and recording a unique Security Hash for clients within ACME Systems Inc. It interacts with the ACME System 1 web application and the SHA1 Online tool to generate these hashes based on client-specific information (ClientID, ClientName, ClientCountry). The automation aims to deliver faster processing, reduce redundant activities, and improve overall performance and reliability. The process is designed for 100% automation.

## 2. Process Overview (How it Works)

The robot performs the following key steps:

1.  **Login to ACME System 1:** Securely logs into the ACME System 1 web application using preconfigured credentials.
2.  **Navigate and Retrieve Work Items:** Accesses the "Work Items" section to view all available tasks.
3.  **Filter WI5 Items:** Identifies and filters for work items of type "WI5".
4.  **Process Each WI5 Item:** For each identified WI5 item, the robot:
    * **Opens Item Details:** Navigates to the specific work item's details page, using a direct URL constructed with the Work Item ID (e.g., `https://acme-test.uipath.com/work-items/{WIID}`) for robustness.
    * **Extracts Client Data:** Retrieves the ClientID, ClientName, and ClientCountry from the details page.
    * **Generates SHA1 Hash:**
        * Opens the SHA1 Online website (http://www.sha1-online.com/).
        * Inputs the client data in the format: `[ClientID]-[ClientName]-[ClientCountry]`.
        * Retrieves the generated SHA1 hash value.
    * **Updates Work Item in ACME System 1:**
        * Navigates back to the ACME System 1 application and opens the "Update Work Item" page for the current item.
        * Sets the work item's status to "Completed".
        * Adds the retrieved Security Hash as a comment.
        * Saves the changes.
5.  **Continues:** Proceeds to the next WI5 item until all are processed.

## 3. Prerequisites and Setup

### Software:
* UiPath Studio (e.g., version 2022.10 or later).
* Supported Web Browser (e.g. Microsoft Edge) with the corresponding UiPath Web Automation extension installed and enabled.
* Access to the ACME System 1 web application.
* Access to the SHA1 Online website (http://www.sha1-online.com/).

### Orchestrator Configuration:
* **Assets:** The following assets configured in UiPath Orchestrator:
    * `ACME_System1_Credentials` (Credential): Securely stored username and password for ACME System 1.

## 4. Input to the Process

* Work Items of type "WI5" available in the ACME System 1 application, in an "Open" status.

## 5. Output of the Process

* Updated Work Items in ACME System 1: Status changed to "Completed" with the generated Client Security Hash added as a comment.


## 6. Error Handling and Logging
### Logging:
* The robot generates detailed logs for its actions, including:
    * Start and end of the process.
    * Key steps and decisions made
    * Successful updates to work items.
    * Any errors or exceptions encountered.

## 8. Project Structure

* `Main.xaml`: The main workflow that orchestrates the entire process.

