# CleverReader Specification

## Table of Contents

1. [Introduction](#introduction)
2. [Project Background](#project-background)
3. [Requirements](#requirements)
4. [User stories](#)
5. [Use case diagram](#)
6. [Detailed use cases](#)
7. [Sequence Diagrams](#)


## Introduction

### Purpose of this document
This document aims to present in a precise and concise way the requirement that must be covered during the development phase. Moreover, principal use cases are provided, as well as user stories. In addition, the document allows the member of the development team to be on the same page with respect to the development process.

### Document Organization
The document is organized as follows:
- An introduction, that describes the content of the document
- A project background, that briefly presents the motivation of this project, the issues encountered and the solution that will be provided during the development process. Moreover, this section provides a brief overview of the principal stakeholders
- A requirement-gathering process, that briefly presents the origin of the data
- A requirement section, whose aim is to present the main requirement to meet at the end of the project
- A user history section, that describes how the users interact with the system
- A user case section, which by means of a use case diagram presents the main use case supported by the final product

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

### Functional Requirements

| Functional requirement      | Name | Description |
| ----------- | ----------- | ----------- |
| R1      | Upload PDF       | The User can upload PDF from their own device. |
| R2   | Interaction with PDF | The User can do all standard operations with the PDF, like scroll and highlight with cursor. |
| R3      | Send PDF data to Server | The System must send extracted data from PDF to dedicated analysis Servers. |
| R4   | Show reference on hover | The User can hover over any reference and the preview must open in a popup window displaying the object that is referenced. |
| R5      | Navigate to reference on click | The User can click on any reference and navigate to it. |
| R6      | Generate knowledge graph    | The System must generate knowledge graph from the list of referenced papers, usually at the last pages of academic papers. |
| R7      | Show knowledge graph | The System must show generated knowledge graph on the UI. |
| R8      | Create section summaries | The System must generate summaries from the paper. |

### Non-Functional Requirements

| Non-Functional requirement      | Name | Description |
| ----------- | ----------- | ----------- |
| NR1      | Client to server communication | Communication should be done with asynchronous type of connection. Communication via REST API. |
| NR2   | Capacity | Database cleanup after 90 days. |
| NR3      | Anonymous pdf hashing | PDF will be anonymously stored as base64 encoded hash for the purpose of building knowledge graph. |
| NR4   | Retry policy | In case of request timeout, the retry policy will be implemented so no data is lost. |
