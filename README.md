# CleverReader Specification

## Table of Contents

1. [Introduction](#introduction)
2. [Project Background](#project-background)
3. [Requirements](#requirements)
4. [User Stories](#user-stories)
5. [Use Cases](#use-cases)
6. [Sequence Diagrams](#sequence-diagrams)
7. [Constraints](#constraints)
8. [Architecture](#architecture)
9. [Repositories](#repositories)

## Introduction

### Purpose of this document

This document aims to present in a precise and concise way the requirement that must be covered during the development phase. Moreover, principal use cases are provided, as well as user stories. In addition, the document allows the member of the development team to be on the same page with respect to the development process.

### Document Organization

The document is organized as follows:

- An introduction, that describes the content of the document
- A project background, that briefly presents the motivation of this project, the issues encountered and the solution that will be provided during the development process. Moreover, this section provides a brief overview of the principal stakeholders
- A requirement section, which consists of requirement-gathering process and requirements whose aim is to present the main requirement to meet at the end of the project
- A user story section, that describes how the users interact with the system
- A user case section, which by means of a use case diagram presents the main use case supported by the final product
- Constraints section, which consists of things that won't be covered in the final product
- Architecture section, which shows a high lever architecture of the product.

### Audience

This document primarily aims at:

- The Development team
- The supervisors
- The customer

### Scope

All of the functional and non-functional criteria are listed and described in the scope of this document. Use cases are used to outline the features that need to be developed, and user stories are included to describe how users will interact with the system. Additionally, usage cases are diagrammed in a use case.

## Project Background

Researchers routinely read academic papers. The goal of this project is to create by means of a web application a clever PDF reader that will enhance the reading experience for academics.
To reach that goal, these two features are essential for the PDF reader: It should first be able to parse the PDF file to extract crucial data from the document, such as figures, tables, or references. Second, it should be able to draw knowledge from the material that has been extracted in order to aid in paper interpretation and generate fresh research concepts.

## Requirements

### Requirements gathering process

All of the requirements were discusses on a couple of group meetings. After the first version of the requirements definition was created, customer was contacted and confirmed most of them and discarded a couple of requirements.

### Functional Requirements

| Functional requirement | Name                           | Description                                                                                                                            |
| ---------------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| R1                     | Upload PDF                     | The User can upload PDF from their own device.                                                                                         |
| R2                     | Preview the PDF                | A preview of the document is available for the user. Furthermore, the user can select the text with the cursor, an scroll up and down. |
| R3                     | Show reference on hover        | The User can hover over any reference and the preview must open in a popup window displaying the object that is referenced.            |
| R4                     | Navigate to reference on click | The User can click on any reference and navigate to it.                                                                                |
| R5                     | Generate knowledge graph       | The System must generate knowledge graph from the list of referenced papers, usually at the last pages of academic papers.             |
| R6                     | Show knowledge graph           | The System must show generated knowledge graph on the UI.                                                                              |
| R7                     | Create section summaries       | The System must generate summaries from the paper.                                                                                     |

### Non-Functional Requirements

| Non-Functional requirement | Name                  | Description                                                                          |
| -------------------------- | --------------------- | ------------------------------------------------------------------------------------ |
| NR1                        | Capacity              | Database cleanup after 90 days.                                                      |
| NR2                        | Anonymous pdf hashing | PDF should be stored anonymously.                                                    |
| NR3                        | Retry policy          | In case of request timeout, the retry policy will be implemented so no data is lost. |

### Requirements Validation

Requirements will be validated with unit, integration and server load tests (stress test).

## User Stories

| ID  | Name                                | Description                                                                                                                                                |
| --- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| S1  | Upload academic paper from computer | As a user, I want to upload an academic paper from my computer, so that I can preview it.                                                                  |
| S2  | Error messages                      | As a user, I want to be informed in detail if the academic paper wasn’t uploaded successfully, so that I know if something went wrong.                     |
| S3  | Try upload again                    | As a user, I want to be able to upload the academic paper if the first upload was unsuccessful, so that I can try to upload the paper again.               |
| S4  | Popups for references               | As a user, I want to see a content preview of the reference when hovering over it, so that I can see more information without navigating to the reference. |
| S5  | Reference navigation                | As a user, I want to be able to navigate to a reference by clicking on it, so that I don’t have to scroll to the reference location.                       |
| S6  | Upload another academic paper       | As a user, I want to upload another academic paper to replace the one that's currently previewed, so that I can start reading another paper.               |
| S7  | Create a knowledge graph            | As a user, I want to create a knowledge graph of the previewed paper, so that I can better see key terms and the interlocking relationships between them.  |
| S8  | Create a summary                    | As a user, I want to create a summary of the paper, so that I can get a better context of the topic.                                                       |
| S9  | Download the summary                | As a user, I want to copy the generated summary, so that I can reuse it.                                                                                   |

## Use Cases

### Use Case Diagram

<img width="50%" alt="use_case_diagram" src="https://user-images.githubusercontent.com/66385870/204817468-bda9238b-fb54-4936-8756-ee5c290fef6d.png">

### Detailed Use Cases

| Use Case Name   | Update PDF from the local device                                                                                                                                                                          |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Actor           | User                                                                                                                                                                                                      |
| Entry condition | The User has a PDF file ready to be uploaded                                                                                                                                                              |
| Event flow      | 1. The user navigates the web application's home page and clicks on the button to upload the PDF <br>2. The users choose from its local storage the PDF to upload <br>3. The user clicks the start button |
| Exit condition  | The PDF is uploaded on the web application, and a preview is available                                                                                                                                    |
| Exception       | 1. The file selected by the user has the wrong format <br>2. A communication error occurs                                                                                                                 |

<br>

| Use Case Name   | View a referred item via a pop-up                                                                                       |
| --------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Actor           | User                                                                                                                    |
| Entry condition | The user has uploaded a PDF file with cross-references                                                                  |
| Event flow      | 1. The user hovers the mouse cursor over the cross-referenced item <br>2. A window containing the referred item pops-up |
| Exit condition  | The user can view the referred item via the pop-up                                                                      |
| Exception       | A communication error occurs                                                                                            |

<br>

| Use Case Name   | Navigate to a referred item                                                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------- |
| Actor           | User                                                                                                       |
| Entry condition | The user has uploaded a PDF file with cross-references                                                     |
| Event flow      | 3. The user hovers the mouse cursor over the cross-referenced item <br>4. The user clicks on the reference |
| Exit condition  | The user can view the referred item                                                                        |
| Exception       | A communication error occurs                                                                               |

<br>

| Use Case Name   | Generate a knowledge graph                                        |
| --------------- | ----------------------------------------------------------------- |
| Actor           | User                                                              |
| Entry condition | The User has uploaded one or more PDF files with cross-references |
| Event flow      | The user clicks on the knowledge graph icon                       |
| Exit condition  | The knowledge graph is generated and a preview is available       |
| Exception       | A communication error occurs                                      |

<br>

| Use Case Name   | Generate a summary                                     |
| --------------- | ------------------------------------------------------ |
| Actor           | User                                                   |
| Entry condition | The user has uploaded a PDF file with cross-references |
| Event flow      | The user clicks on the summary icon                    |
| Exit condition  | A window with the summary of the paper pops-up         |
| Exception       | A communication error occurs                           |

## Sequence Diagrams

#### Upload PDF

<img width="70%" alt="sequence_diagram_upload_pdf" src="https://user-images.githubusercontent.com/66385870/204835065-cc1e2842-009a-49ac-9158-41b6f2cce659.png">

#### View a referred subject

<img width="50%" alt="sequence_diagram_referred_subject" src="https://user-images.githubusercontent.com/66385870/204835197-dbbc4b48-2a30-4ca4-ae16-1b1f25d449cd.png">

#### Generate summary

<img width="50%" alt="sequence_diagram_summary" src="https://user-images.githubusercontent.com/66385870/204835359-9fe922fb-0ce3-460f-b855-775afcdea9f1.png">

#### Generate knowledge graph

<img width="50%" alt="sequence_diagram_knowledge_graph" src="https://user-images.githubusercontent.com/66385870/204852103-83c95b27-1ea4-4c1c-8a4d-69d816a71972.png">

## Constraints

- No user authentication, so if multiple users connect unexpected behaviour can occur
- No mobile support because it is not convenient to have much popups and small windows on mobile screens

## Architecture

<img width="70%" alt="architecture_image" src="https://user-images.githubusercontent.com/66385870/204838387-31b93a05-00cf-42e1-b1c4-5b3813ee0219.png">

## Repositories

### List of repositories

The project development was split into 4 git repositories:

- [Frontend](https://github.com/MihaelsGit/CleverReader)
- [Middleware](https://github.com/AvendoOT/clever-reader-middleware)
- [Summary service](https://github.com/jaimetomares/CleverReaderJaime)
- [Reference service](https://github.com/AvendoOT/clever-reader-reference)

# Deployment

## Deploying a React App to Firebase

### Prerequisites

- A Firebase account and a Firebase project set up. If you don't have one, go to the [Firebase website](https://firebase.google.com/) and create a new account. Then, log in to the Firebase console and create a new project.
- The Firebase CLI (Command Line Interface) installed on your system. To install it, run `npm install -g firebase-tools` in your terminal.

### Steps

1. In your React project directory, run `firebase init`. This will set up the Firebase configuration for your project.
2. Choose the Firebase project that you want to use for this app.
3. Set up hosting for the app and configure the public directory as `build`, which is the default directory created when you run `npm run build` in a React project.
4. Build the app for production by running `npm run build` in the terminal.
5. Deploy the app to Firebase by running `firebase deploy`.
6. Your app should now be live at the URL provided in the terminal. You can also find the URL in the Firebase console under the "Hosting" section.

## Alternative way, using Firebase console website (prerequisites are the same)

### Steps

1. In the Firebase console, click on the "Hosting" card in the "Develop" section.
2. Click on the "Get started" button and follow the prompts to set up hosting for your project.
3. Click on the "Upload files" button and select the `build` directory from your React project.
4. After the files have been uploaded, click on the "Deploy" button to deploy your app.
5. Your app should now be live at the URL provided in the Firebase console under the "Hosting" section.
