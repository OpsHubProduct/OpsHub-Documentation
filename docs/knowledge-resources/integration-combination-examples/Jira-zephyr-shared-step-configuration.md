---
if: >-
  visitor.claims.unsigned.product !== "OM4ADO" && visitor.claims.unsigned.product !== "OAM"
---

# Synchronization of Jira Zephyr Shared Step from Test Cases

## What is a Shared Steps

In the context of ALM (Application Lifecycle Management), particularly in test management systems like OpenText ALM Quality Center, Jira Zephyr, IBM Engineering Test Management , Azure DevOps. A shared step refers to a reusable, predefined step or set of actions that can be utilized across multiple test cases. This is a way to streamline the creation and execution of tests by allowing testers to reuse common testing actions without having to redefine them for each individual test case.

Different test management systems often use different terminology for similar concepts like shared steps.

## Behavior of Shared Step in different systems.

### Jira Zephyr – Shared Steps
In Zephyr (the Jira-based test management tool), the concept is also referred to as Shared Steps.
Explain of shared step creation in jira
In **Jira Zephyr**, one test case can include steps that are *linked* from another test case.  
By this link, the base entity will also contain the steps from the linked test case.

### IBM Engineering Test Management - Keywords

In IBM Engineering Test Management (formerly known as IBM Rational Quality Manager or RQM), shared steps are known as "Keywords".
In **ETM**, a *Keyword* can be linked within a test step of a *Test Script* entity.  
Thus, steps existing in a keyword become part of the test script’s steps.

## Synchronization of Shared Steps Across Two Systems with Shared Step Support

To synchronize shared steps between two shared-step-supported systems, a **customized workflow** will be used.

## Example: Zephyr and ETM Integration

Let's take an example of two system shared step supported system.

### Zephyr as Source System and ETM as Target

To synchronize linked test case steps from **Zephyr Scale** to **ETM**, follow these steps:

1. First, synchronize all Zephyr test cases to **ETM Keywords**.
    * The purpose of the above step is to ensure that all test cases are synchronized to ETM as keywords.  
    However, <code class="expression">space.vars.OIM</code> does not know which test case is linked with another test case in Zephyr.  
    Therefore, while synchronizing a test case to a Test Script, if <code class="expression">space.vars.OIM</code> finds a linked test case, it can be replaced with a keyword.
2. Download the customized workflow from below  
{% file src="../../assets/Files/Custom Integration Workflow For Shared Step.xml" %}
Custom Integration Workflow For Shared Step
{% endfile %}  


   > **Note:**  
   > The attached workflow can be directly used as-is in this case. The parameters of the function `EaiUtility.handleStepFromSharedStepToSharedStep` are described as follows:
   > - **steps** → All the steps are set in this field.
   > - **testcase-zephyr** → Source linked entity type from which the shared step is imported in the source.
   > - **keyword** → Target linked entity type from which the shared step is imported in the target.
   > - **description** → Source system field in which the linked test case ID is appended.
   >> For integration with systems other than Zephyr to ETM, modify the above-mentioned parameters according to the end systems.  
   This method is responsible for replacing source linked entity steps with target linked entity steps.

3. Upload the above modified workflow and set it in the integration configuration of the Zephyr test case to ETM test script.
4. Then, synchronize all Zephyr test cases to **ETM Test Steps** using the customized workflow mentioned above.


### ETM as Source and Zephyr as Target System

When **Zephyr** is the target system, all the above-mentioned steps will remain the same except for step 2.

Download the customized workflow from the above link and modify the workflow as follows:

Replace:

```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,"testcase-zephyr",workflowInstanceId,"keyword");
```

With:

```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"OH_Test_Steps","description","OH_KY_DO_NOT_EDIT:",null,"keyword",workflowInstanceId,"testcase-zephyr");
```


## Synchronization of Shared steps from Shared Step Supported Systems to Non-Shared Step Systems

Consider the example of **Zephyr → Zephyr Squad** integration.  
Here, **Zephyr Squad** does **not** support shared steps.

1. Create an integration between **Zephyr Test Case** and **Zephyr Squad Test Case**.
2. Download the customized workflow from the above link and modify the workflow as follows:
    ```java
    EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,"testcase-zephyr",workflowInstanceId,"keyword");
    ```
   With:
    ```java
    EaiUtility.handleStepsWithSharedStepToNonSharedStep(mappedProperties, destinationClient,"OH_Test_Steps","description","[OH_KY_DO_NOT_EDIT:");
    ```
3. Set the modified workflow in the integration mentioned in step 1.

## Zephyr Enterprise Configuration for Shared Step Synchronization

1. Create an integration between **Zephyr Enterprise test case** and **desired entity**.
2. Download the customized workflow from the given link and modify as per your use case mentioned below.

{% file src="../../assets/Files/Custom Integration Workflow For Shared Step.xml" %}
Custom Integration Workflow For Shared Step
{% endfile %}
> **Note:**
>> You will not require workflow is Zephyr Enterprise is target and source system does not support shared step

### Zephyr Enterprise as Source and Target supports Shared Step 
Replace:
```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,"testcase-zephyr",workflowInstanceId,"keyword");
```

With
```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,"testcase",workflowInstanceId,<target-entity-type>);
```

### Zephyr Enterprise as Target and Source supports Shared Step
Replace:
```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,"testcase-zephyr",workflowInstanceId,"keyword");
```

With:
```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,<source-entity-type>,workflowInstanceId,"testcase");
```
### Zephyr Enterprise as Source and Target does not support Shared Step
Replace:
```java
EaiUtility.handleStepFromSharedStepToSharedStep(mappedProperties, sourceSystemClient, destinationClient,"steps","description","OH_KY_DO_NOT_EDIT:",null,"testcase-zephyr",workflowInstanceId,"keyword");
```

With
```java
EaiUtility.handleStepsWithSharedStepToNonSharedStep(mappedProperties, destinationClient,"steps","description","[OH_KY_DO_NOT_EDIT:");
```
### Zephyr Enterprise as Target and Source does not support Shared Step
Does not require to upload any specific workflow as all steps from source will be normal steps and synchronize to Zephyr Enterprise testcase as normal steps. 

## Behavior of Shared step Synchronization

### Both system supports Shared steps
- Regular steps will be synchronized as-is.
- If a new shared step is added, the corresponding linked entity will be added to the target.

### Shared step supported system to non-shared step supported system
- Regular steps are synchronized as-is.
- If a linked test case is found, all its steps are synchronized to the target, with the linked test case ID appended in the description field.  
  Example: `[OH_KY_DO_NOT_EDIT:<TEST CASE ID>]`


### Non Shared Step supported system to shared supported system
- Creation, update, and deletion of regular steps are synchronized as-is.
- Creation, update, and deletion of shared steps are synchronized **after** the linked test case itself has been synchronized.  
  Once the linked test case is synced, these changes are reflected in the base test case.
