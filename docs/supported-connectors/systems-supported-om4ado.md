---
if: >-
  "OM4ADO" === visitor.claims.unsigned.product
layout:
  width: wide
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: false
---

# Supported Systems

Given below are the systems currently supported by <code class="expression">space.vars.OM4ADO</code>:

<table>
    <thead>
        <tr>
            <th width="50" data-type="number">No.</th>
            <th width="180">System</th>
            <th width="250">Versions Supported</th>
            <th>Entities Supported</th>
            <th width="160">Formerly Known as</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>Azure DevOps Server</td>
            <td> 2010, 2012, 2013, 2015 (up to Update 3), 2017, 2017 Update 2, 2018, 2019, 2020, 2022, 2025 </td>
            <td> Work items such as Bug, Requirement, Task, Test Case, User Story, Shared Steps and All Custom Entity Types <br>Test Entities such as Test Plan, Test Result, Test Run, Test Suite <br>Iteration, Area Path, User Group, Team and User: 2010 and above <br>Delivery Plan: 2018 and above<br>Git Commit Information (only read): 2016 and above<br>Dashboard, Query, Widget: 2017 and above <br>Pull Request (only read), Build Pipeline**, Release Pipeline**, Service Connection, Task Group, Variable Group : 2018 and above <br>Build* (only read): 2019 and above <br>  Agent Pool : 2020 and above</td>
            <td>Team Foundation Server (TFS)</td>
        </tr>
        <tr>
            <td>2</td>
            <td>Azure DevOps Server Version Control</td>
            <td> 2010, 2012, 2013, 2015 (up to Update 3), 2017, 2017 Update 2, 2018, 2019, 2020, 2022, 2025 </td>
            <td> Commit Information </td>
            <td> Team Foundation Server Version Control </td>
        </tr>
        <tr>
            <td>3</td>
            <td>Azure DevOps Services</td>
            <td>All</td>
            <td> Work items such as Bug, Requirement, Task, Test Case, User Story, Shared Steps and All custom workitem types <br>Test entities such as Test Plan, Test Result, Test Run, Test Suite<br>Iteration, Area Path, Group, Team, User, Delivery Plan, Dashboard, Query, Widget, Pipeline**, Release Pipeline**, Agent Pool, Service Connection, Task Group, Variable Group  <br> Git Commit Information(only read), Pull Request(only read), Build* (only read) </td>
            <td>Visual Studio Team Services (VSTS)</td>
        </tr>
    </tbody>
</table>

(*) Professional services required for version specific certification. <br> (**) Professional services recommended due to modelling complexity.

`