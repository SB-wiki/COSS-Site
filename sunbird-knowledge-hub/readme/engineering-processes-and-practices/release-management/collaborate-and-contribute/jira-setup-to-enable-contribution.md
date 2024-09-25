# JIRA Setup for Latest Contribution Process

### JIRA Setup Details <a href="#id-1xx3tiqxobbs" id="id-1xx3tiqxobbs"></a>

### for the <a href="#qs4cq48g4utq" id="qs4cq48g4utq"></a>

### Community Contribution Practice Template <a href="#n4bvkg5cyubf" id="n4bvkg5cyubf"></a>

**Table of Contents**

**1.0 Introduction 2**

**2.0 Project Details 2**

**3.0 Template Configurations 3**

3.1 Issue Types 3

3.2 Workflow 4

3.3 Screens 4

3.3 Fields 6

3.4 Automations 6

**4.0 Revision History 7**

### 1.0 Introduction <a href="#uzsymfdawvik" id="uzsymfdawvik"></a>

To support the Community Contribution Practice, a new project template has been created in JIRA. This template includes predefined issue types and workflows aligned with the [contribution practice](https://docs.google.com/document/d/1zPDg6hlVm5rewU6dDh3CdOq6d6hdG\_hRLhnKJdoSjKU/edit?usp=drive\_link), enabling the rapid creation of JIRA projects for new building blocks.

This document provides a comprehensive overview of all the components within the template project. It serves as a reference for JIRA administrators to facilitate maintenance, enhancements, and a thorough understanding of the setup for future changes.

### 2.0 Template Details <a href="#j4r389v6p28p" id="j4r389v6p28p"></a>

**Project Name:** Building Block Template Project\
**Project Key:** BBT

**Components:**

* Dummy Component (Note: A specific component should be created for each new project derived from this template)

**Administrators:**

* Project-Sunbird Administrators
* ashok.reddy@ilimi.in

**Template Overview:**

* Total Issue Types: 9
* Total Workflows: 6
* Total Screens: 25
* Template-Specific Fields: 3

### 3.0 Template Configurations <a href="#ldpagpm0y5uy" id="ldpagpm0y5uy"></a>

#### 3.1 Issue Types <a href="#id-1cyh06760jdu" id="id-1cyh06760jdu"></a>

This template project includes the below mentioned issue types, as detailed in the [contribution practice document](https://docs.google.com/document/d/1zPDg6hlVm5rewU6dDh3CdOq6d6hdG\_hRLhnKJdoSjKU/edit?usp=drive\_link). The issue type are assigned to the project using the scheme:- **BBT: Scrum Issue Type Scheme**

Level-1

* Epic

Level-2

* Bug
* Minor-Enhancement
* Documentation-Issue
* Installation-Issues
* RFC

Issue Type- Subtask

* Checklist-Item (for checklist tasks related to the mail issue)
* Sub-task (for activities required for the development of the main issue)
* Defect

#### 3.2 Workflow <a href="#hbm133d687gh" id="hbm133d687gh"></a>

| **Issue Type**                           | **Workflow Name**                                |
| ---------------------------------------- | ------------------------------------------------ |
| Minor-Enhancement,RFC,Bug                | Building Block RFC Bug and ME Workflow V2.0      |
| Epic                                     | Building Block EPIC Workflow                     |
| Documentation-Issue, Installation-Issues | Building Block Doc and Inst Issues Workflow V2.0 |
| Sub-task                                 | Building Block Sub-Task Workflow V2.0            |
| Defect                                   | Building Block Defect Workflow                   |
| Checklist-Item                           | Building Block Checklist-Item Workflow           |

#### &#x20;<a href="#m6iife4kj8rg" id="m6iife4kj8rg"></a>

#### 3.3 Screens <a href="#rnycsjcg78ns" id="rnycsjcg78ns"></a>

| **Details**                                                                                                                                                                                                                                                         | **Screen**                                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Issue Type = Bug                                                                                                                                                                                                                                                    | <p><em>Create Issue:</em>- BBT: Scrum Create Bug Screen</p><p><em>Edit Issue:</em>- BBT: Scrum Bug Screen</p><p><em>View Issue:</em>- BBT: Scrum Bug Screen</p>                                                 |
| Issue Type = Checklist Item                                                                                                                                                                                                                                         | <p><em>Create Issue:</em>- BBT: Scrum Checklist Item Screen</p><p><em>Edit Issue:</em>- BBT: Scrum Checklist Item Screen</p><p><em>View Issue:</em>- BBT: Scrum Checklist Item Screen</p>                       |
| Issue Type = Documentation Issue                                                                                                                                                                                                                                    | <p><em>Create Issue:</em>- BBT: Scrum Create Documentation Issue Screen</p><p><em>Edit Issue:</em>- BBT: Scrum Documentation Issue Screen</p><p><em>View Issue:</em>- BBT: Scrum Documentation Issue Screen</p> |
| Issue Type = EPIC                                                                                                                                                                                                                                                   | <p><em>Create Issue:</em>- BBT: Scrum EPIC Screen</p><p><em>Edit Issue:</em>- BBT: Scrum EPIC Screen</p><p><em>View Issue:</em>- BBT: Scrum EPIC Screen</p>                                                     |
| Issue Type = Installation Issue                                                                                                                                                                                                                                     | <p><em>Create Issue:</em>- BBT: Scrum Create Installation Issue Screen</p><p><em>Edit Issue:</em>- BBT: Scrum Installation Issue Screen</p><p><em>View Issue:</em>- BBT: Scrum Installation Issue Screen</p>    |
| Issue Type = Minor Enhancement                                                                                                                                                                                                                                      | <p><em>Create Issue:</em>- BBT: Scrum Create Minor Enhancement Screen</p><p><em>Edit Issue:</em>- BBT: Scrum Minor Enhancement Screen</p><p><em>View Issue:</em>- BBT: Scrum Minor Enhancement Screen</p>       |
| Issue Type = RFC                                                                                                                                                                                                                                                    | <p><em>Create Issue:</em>- BBT: Scrum Create RFC Screen</p><p><em>Edit Issue:</em>- BBT: Scrum RFC Screen</p><p><em>View Issue:</em>- BBT: Scrum RFC Screen</p>                                                 |
| Issue Type = Sub-task                                                                                                                                                                                                                                               | <p><em>Create Issue:</em>- BBT: Scrum Create Sub-task Screen</p><p><em>Edit Issue:</em>- BBT: Scrum Sub-task Screen</p><p><em>View Issue:</em>- BBT: Scrum Sub-task Screen</p>                                  |
| <p><strong>Workflow TransitionScreen</strong> for Transition from Open to Selected for Contribution</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow V2.0</p>                                                         | BBT: Status Transition Screen-1                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition from Selected for contribution to In-Development</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow</p><p>Building Block RFC Bug and ME Workflow V2.0</p> | BBT: Status Transition Screen-2                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition from In-Development to In-Validation status</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow V2.0</p><p>Building Block RFC Bug and ME Workflow V2.0</p> | BBT: Status Transition Screen-3                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition from In-Validation to Fixed status</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow V2.0</p><p>Building Block RFC Bug and ME Workflow V2.0</p>          | BBT: Status Transition Screen-4                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition from Open to Invalid</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow V2.0</p><p>Building Block RFC Bug and ME Workflow V2.0</p>                        | BBT: Status Transition Screen-5                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition from Any Status to Open Status</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow V2.0</p><p>Building Block RFC Bug and ME Workflow V2.0</p>              | BBT: Status Transition Screen-6                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition to Failed Validation Status</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Doc and Inst Issues Workflow V2.0</p><p>Building Block RFC Bug and ME Workflow V2.0</p>                 | BBT: Status Transition Screen-7                                                                                                                                                                                 |
| <p><strong>Workflow Transition Screen</strong> for Transition Defect from Assigned to Fixed</p><p><strong>Applicable Workflow</strong>:-</p><p>Building Block Defect Workflow</p>                                                                                   | BBT: Status Transition Screen-8                                                                                                                                                                                 |
| Default Screens                                                                                                                                                                                                                                                     | <p><em>Create Issue:-</em> BBT: Scrum Create Defect Screen</p><p><em>Edit Issue:-</em> BBT: Scrum Defect Screen</p><p><em>View Issue:-</em> BBT: Scrum Defect Screen</p>                                        |

#### 3.3 Fields <a href="#id-7t2llbdk88mo" id="id-7t2llbdk88mo"></a>

Below are the fields created for the template

1. “All Sub-Tasks Completed ?”
2. “All Checklist Items Completed ?”
3. “Discussion Link”

#### 3.4 Automations <a href="#igkjzon6vfpw" id="igkjzon6vfpw"></a>

Below automations are available for projects to leverage. The names self explains automation

1. When epic is completed → then close all the stories present
2. When all stories are completed → then close epic,
3. When issue type RFC is created -> add checklist items to the RFC issue

### 4.0 Revision History <a href="#r7akf1c8zzna" id="r7akf1c8zzna"></a>

| Version | Details                         | Author            |
| ------- | ------------------------------- | ----------------- |
| 1.0     | Initial Version of the document | Chitranshu Keshav |
