# Valentino Artisan Coffee House API

## Project Overview

This project aims to enhance the reliability and efficiency of the Valentino Artisan Coffee House API by implementing test automation using Postman, ensuring comprehensive validation of functionality, performance, and security throughout the development lifecycle.

## Installation Guide
### Prerequisites
- **JavaScript**: Proficiency in JavaScript is essential for writing and executing test scripts in Postman. Understanding JavaScript will enable you to create complex test scenarios, handle asynchronous operations, and manipulate API responses effectively.

- **Postman**: Familiarity with Postman, a powerful tool for API development and testing, is crucial. Knowledge of how to create and organize collections, set up environments, write test scripts, and use Postman’s Collection Runner and Newman command-line tool is necessary for effective test automation.

- **Chai**: Experience with Chai, a popular assertion library used in conjunction with JavaScript, is important for validating test results. Chai provides a variety of assertion styles and methods that will help ensure the API responses meet expected criteria.

- **GitHub**: Proficiency with GitHub is required for version control and collaboration. Understanding how to create repositories, manage branches, and handle pull requests will facilitate effective teamwork and maintain the integrity of test automation scripts and related documentation.
### Setup Installation for Postman
1. **Download Postman**
    
    - Visit the Postman Website: Go to the official Postman [download page](https://www.postman.com/downloads/).

    - Choose Your Platform: Select the appropriate version of Postman for your operating system (Windows, macOS, or Linux).

    - Download the Installer: Click the download link to get the installer for your platform.

2. **Install Postman**

    - Windows:

        1. Run the Installer: Double-click the downloaded .exe file to launch the installer.
        2. Follow the Setup Wizard: Click "Next" through the installation steps and then "Install" to complete the process.
        3. Launch Postman: Once the installation is complete, open Postman from the Start menu or desktop shortcut.

    - macOS:

        1. Open the Installer: Double-click the downloaded .dmg file.
        2. Drag and Drop: Drag the Postman icon into the Applications folder.
        3. Launch Postman: Open Postman from the Applications folder or using Spotlight search.

    - Linux:

        1. Extract the Archive: Use the .tar.gz file downloaded to extract it to your desired location.
        2. Install Dependencies: Ensure you have required dependencies installed, such as libgconf-2-4.
        3. Run Postman: Navigate to the extracted directory and execute ./Postman to launch the application. You might want to create a desktop shortcut or menu entry for easier access.

## Usage Instructions
### Open and Login to Postman
1. Open Postman on your computer
    - Postman Desktop Application
    - Postman Web Application
2. Login on your Postman Account

### Fork Postman Collection
1. Open this [Postman Workspace](https://www.postman.com/valentins-team/workspace/test-automation-valentino-s-artisan-coffee-house-api)
2. Create New Public Workspace on Postman
3. Fork [Valentino Artisan Coffee House API](https://www.postman.com/valentins-team/workspace/test-automation-valentino-s-artisan-coffee-house-api/collection/2354738-e6b0fbe6-5385-4751-944f-bd836b13d6e3?action=share&creator=36196810) Postman Collection to your public workspace
4. Open `status` folder, and click on `Get API status` 
5. Click `Send` and wait for respond
6. Status should be `200 OK` and Response Body should be JSON 
    ``` json title="Response Body"
    {
    "status": "API is up and running"
    }
    ```
7. Your workspace are ready


### Writing Script in Postman
1. Expand `status` folder, click on `Get API status`, select `Script` tab
2. Write your script on `pre-request` or `post-response` depend on your test plan and scenario
3. Postman only accept JavaScript ( :material-language-javascript: ) for scripting

## Project Assignment
### Assignment 1

**Task 1**

Add to the request **"Get API status"** a Postman test that verifies the status is 200.
Once you have established that the test is working as expected, duplicate the request and drag it inside the **"Assignment #1"** collection and put it in the **"API requests"** folder. Ensure the name of the request remains the same.

**Task 2**

Add to the request **"Get single product"** a script that parses the JSON response body. Log the value of the property "product-description" to the Postman console.
Once you have established that the script is working as expected, duplicate the request and drag it inside the **"Assignment #1"** collection and put it in the **"API requests"** folder. Ensure the name of the request remains the same.

**Task 3**

Add to the request **"Create a new order"** a script that parses the JSON response body and sets a Postman variable named orderId with the id of the order that was just created.
Once you have established that the script is working as expected, duplicate the request and drag it inside the **"Assignment #1"** collection and put it in the **"API requests"** folder. Ensure the name of the request remains the same.

### Assignment 2
### Assignment 3
### Assignment 4
### Assignment 5
### Claim Certification

## References and Resources

## Acknowledgements

