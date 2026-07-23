---
if: >-
  "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product 
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

Given below are the systems supported currently by <code class="expression">space.vars.OIM</code>:

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
            <td>Aha!</td>
            <td>All</td>
            <td>Epic, Goal, Feature, Idea, Initiative, Release, Requirement, To-do, Note</td>
            <td></td>
        </tr>
        <tr>
            <td>2</td>
            <td>Aras Innovator</td>
            <td>All</td>
            <td>All System Item Types (excluding Item Types of Relationship and Core Type) and All Custom Item Types (excluding Item Types of Relationship Type)</td>
            <td></td>
        </tr>
        <tr>
            <td>3</td>
            <td>Azure DevOps Server</td>
            <td> 2010, 2012, 2013, 2015 (up to Update 3), 2017, 2017 Update 2, 2018, 2019, 2020, 2022, 2025 </td>
            <td> Work items such as Bug, Requirement, Task, Test Case, User Story, Shared Steps and All Custom Entity Types <br>Test Entities such as Test Plan, Test Result, Test Run, Test Suite <br>Iteration, Area Path, User Group, Team and User: 2010 and above <br>Git Commit Information (only read): 2016 and above<br>Dashboard, Query, Widget: 2017 and above <br>Pull Request (only read), Build Pipeline**, Release Pipeline**, Service Connection, Task Group, Variable Group : 2018 and above <br>Build* (only read): 2019 and above <br>  Agent Pool : 2020 and above</td>
            <td>Team Foundation Server (TFS)</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Azure DevOps Server Version Control</td>
            <td> 2010, 2012, 2013, 2015 (up to Update 3), 2017, 2017 Update 2, 2018, 2019, 2020, 2022, 2025 </td>
            <td> Commit Information </td>
            <td> Team Foundation Server Version Control </td>
        </tr>
        <tr>
            <td>5</td>
            <td>Azure DevOps Services</td>
            <td>All</td>
            <td> Work items such as Bug, Requirement, Task, Test Case, User Story, Shared Steps and All custom workitem types <br>Test entities such as Test Plan, Test Result, Test Run, Test Suite<br>Iteration, Area Path, Group, Team, User, Dashboard, Query, Widget, Pipeline**, Release Pipeline**, Agent Pool, Service Connection, Task Group, Variable Group  <br> Git Commit Information(only read), Pull Request(only read), Build* (only read) </td>
            <td>Visual Studio Team Services (VSTS)</td>
        </tr>
        <tr>
            <td>6</td>
            <td>Blueprint*</td>
            <td>From 5.4 to 13.0</td>
            <td>All System/Custom Entities</td>
            <td></td>
        </tr>
        <tr>
            <td>7</td>
            <td>BMC Remedy*</td>
            <td>6.3, 8.0, 8.1</td>
            <td>Request</td>
            <td>Remedy</td>
        </tr>
        <tr>
            <td>8</td>
            <td>Broadcom Clarity</td>
            <td>SaaS : 16.2.2 and above</td>
            <td>Project, Task, To Do, Custom Investment Object (Parent only)</td>
            <td>CA PPM</td>
        </tr>
        <tr>
            <td>9</td>
            <td>Broadcom Rally Software</td>
            <td>All</td>
            <td>Portfolio Items, Defect, Task, Test Case, Test Case Result, Test Set, Test Folder, User Story, Change Set [Write support only, Release, Iteration, Milestone], Risk</td>
            <td>CA Agile</td>
        </tr>
        <tr>
            <td>10</td>
            <td>Broadcom Service Desk Manager*</td>
            <td>alb-165</td>
            <td>Change Request, Incident, Problem, Issue</td>
            <td>CA Service Desk Manager</td>
        </tr>
        <tr>
            <td>11</td>
            <td>Bugzilla</td>
            <td>4.4, 4.4.1, 4.4.2, 5.0 and above<br/>Read only: 4.4.3 to 4.4.13</td>
            <td>Bug</td>
            <td></td>
        </tr>
        <tr>
            <td>12</td>
            <td>Cherwell*</td>
            <td>10.1.0</td>
            <td>Incident</td>
            <td></td>
        </tr>
        <tr>
            <td>13</td>
            <td>Codebeamer</td>
            <td>21.09-SP3, 21.09-SP9, 22.10 LTS, 2.x, 3.x</td>
            <td>All System and Custom Tracker items<br/><br/>Not Supported: SCM type entities (Working Sets, Baselines, SCM commits, repositories), timekeeping trackers (Worklogs), Non-ALM entities (Wiki pages, documents)</td>
            <td></td>
        </tr>
        <tr>
            <td>14</td>
            <td>Codebeamer X</td>
            <td>4.2.1</td>
            <td>All System and Custom Tracker items<br/><br/>Not Supported: SCM type entities (Working Sets, Baselines, SCM commits, repositories), timekeeping trackers (Worklogs), Non-ALM entities (Wiki pages, documents)</td>
            <td></td>
        </tr>
        <tr>
            <td>15</td>
            <td>Database</td>
            <td>All versions supported for MySQL, MS SQL Server/Azure SQL, Oracle, PostgreSQL, MariaDB</td>
            <td>All tables or views in the database</td>
            <td></td>
        </tr>
        <tr>
            <td>16</td>
            <td>Digital.ai Agility</td>
            <td>Cloud (All)</td>
            <td>Backlog Item, Defect, Epic, Goal, Issue, Request, Task, Test, TestSet, Theme, Project/Release, Iteration, Build Run, Changesets, Actuals</td>
            <td>VersionOne</td>
        </tr>
        <tr>
            <td>17</td>
            <td>Digital.ai TeamForge</td>
            <td>17.11 to 21.x</td>
            <td>All System/Custom Tracker Types, Planning Folders, Teams</td>
            <td></td>
        </tr>
        <tr>
            <td>18</td>
            <td>Enterprise Architect**</td>
            <td>10, 11, 13.0, 13.5, 14, 15, 16 (Build 1622 onwards), 17</td>
            <td>Element, Diagram, Package, Operation (read only), Attribute (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>19</td>
            <td>FogBugz*</td>
            <td>8.8.*, 8.9.*, 8.9.110.0H, 8.9.122.0H</td>
            <td>Case</td>
            <td></td>
        </tr>
        <tr>
            <td>20</td>
            <td>Gerrit</td>
            <td>3.6.8</td>
            <td>Change (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>21</td>
            <td>Git</td>
            <td>1.7.6, 1.8.3</td>
            <td>Commit Information (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>22</td>
            <td>GitHub</td>
            <td>GitHub Enterprise - From 2.7 to 2.20<br/>SaaS - 2.1</td>
            <td>Issue, Commit Information (read only), Pull Request (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>23</td>
            <td>GitLab</td>
            <td>SaaS<br/>On Premise: 15.x, 16.x, 17.x, 18.x</td>
            <td>Commit (read only), Epic, Issues</td>
            <td></td>
        </tr>
        <tr>
            <td>24</td>
            <td>Helix ALM</td>
            <td>2021, 2024</td>
            <td>Requirement, Issue, Test Case</td>
            <td>Testtrack</td>
        </tr>
        <tr>
            <td>25</td>
            <td>Helix Core*</td>
            <td>2009.2, 2013.1, 2015</td>
            <td>Commit Information (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>26</td>
            <td>HubSpot</td>
            <td>SaaS</td>
            <td>Deal, Ticket, Contact, Company, Orders, Notes, Emails, Tasks, Calls, Meetings</td>
            <td></td>
        </tr>
        <tr>
            <td>27</td>
            <td>IBM DevOps Code ClearCase*</td>
            <td>8.x</td>
            <td>Delivery Information</td>
            <td>Rational ClearCase</td>
        </tr>
        <tr>
            <td>28</td>
            <td>IBM Engineering Requirements Management DOORS Next</td>
            <td>6.0.x*, 7.0.1, 7.0.2 to 7.0.2 IFix25, 7.0.3</td>
            <td>All Artifacts (Text + Collection)</td>
            <td>IBM DOORS NG</td>
        </tr>
        <tr>
            <td>29</td>
            <td>IBM Engineering Test Management</td>
            <td>6.0.x*, 7.0.1 - 7.1.x</td>
            <td>Test Plan, Test Suite, Test Case, Test Script, Test Case Execution Record, Test Case Result, Keyword</td>
            <td></td>
        </tr>
        <tr>
            <td>30</td>
            <td>IBM Engineering Workflow Management</td>
            <td>5.0.2, 6.0.1, 6.0.2, 6.0.3, 7.0.1, 7.0.2</td>
            <td>Process Template/All Custom Entities</td>
            <td>Rational Team Concert</td>
        </tr>
        <tr>
            <td>31</td>
            <td>IBM Rational ClearQuest</td>
            <td>8.x*, 9.x, 10.x</td>
            <td>Defect / Any Stateful Record Type</td>
            <td></td>
        </tr>
        <tr>
            <td>32</td>
            <td>IBM Rational DOORS</td>
            <td>9.1–9.7.2</td>
            <td>Requirement, Baseline (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>33</td>
            <td>IBM Rational RequisitePro*</td>
            <td>7.0.1+</td>
            <td>Requirement [All Custom-created Requirement Types supported]</td>
            <td></td>
        </tr>
        <tr>
            <td>34</td>
            <td>Jama Connect</td>
            <td>Cloud/Self-Hosted: From 8.22+</td>
            <td>All System/Custom Item Types (Defect, Epic, Persona, Test Plan, Test Cycle, Test Run, Commit, Component, Set, Folder, Releases, etc.)<br/>Not Supported: Attachment, Core</td>
            <td></td>
        </tr>
        <tr>
            <td>35</td>
            <td>Jenkins</td>
            <td>1.617, 2.7.1</td>
            <td>Build (Read & Trigger)</td>
            <td></td>
        </tr>
        <tr>
            <td>36</td>
            <td>Jira Agile</td>
            <td>Cloud<br/>Data Center: 6.7.7 – 9.12.x</td>
            <td>Sprint, Epic, Link</td>
            <td></td>
        </tr>
        <tr>
            <td>37</td>
            <td>Jira AIO (All-In-One) Tests*</td>
            <td>Data Center: 4.4.0<br/>Cloud: 4.4.0</td>
            <td>AIO Test Case (read), AIO Test Cycle (read), AIO Test Run (read)</td>
            <td></td>
        </tr>
        <tr>
            <td>38</td>
            <td>Jira Align</td>
            <td>SaaS</td>
            <td>Capability, Customer, Defect, Epic, Initiative, Portfolio, Program, PI, Release, Sprint, Story, Task, Theme, Value Stream, Objectives</td>
            <td></td>
        </tr>
        <tr>
            <td>39</td>
            <td>Jira Cloud</td>
            <td>All</td>
            <td>All System & Custom Issue Types, Sub-Task Types, Version, Work-log</td>
            <td></td>
        </tr>
        <tr>
            <td>40</td>
            <td>Jira Data Center</td>
            <td>5.x–11.x</td>
            <td>All System & Custom Issue Types, Sub-Task Types, Version, Work-log</td>
            <td></td>
        </tr>
        <tr>
            <td>41</td>
            <td>Jira Elements Connect</td>
            <td>On-Premise: 6.13.x</td>
            <td>Live text/user/date/datetime custom fields</td>
            <td></td>
        </tr>
        <tr>
            <td>42</td>
            <td>Jira Project & Portfolio Management</td>
            <td>From Jira 8.15+ (part of Jira software)<br/>2.24.0–3.29.x</td>
            <td>Portfolio Items</td>
            <td></td>
        </tr>
        <tr>
            <td>43</td>
            <td>Jira QMetry*</td>
            <td>On Premise: QMetry 3.X, Build 4.6.1</td>
            <td>Test Case, Test Scenario, Test Run, QMetry Test Execution</td>
            <td></td>
        </tr>
        <tr>
            <td>44</td>
            <td>Jira R4J</td>
            <td>Cloud,<br/> On Premise*: 4.4.x–4.18.4</td>
            <td>Folders, R4J Relationships (Folders ↔ Jira Issues)</td>
            <td></td>
        </tr>
        <tr>
            <td>45</td>
            <td>Jira Service Management</td>
            <td>Cloud<br/>On Premise: 3.1.10–5.12.1</td>
            <td>All System & Custom Issue Types</td>
            <td>Jira Service Desk</td>
        </tr>
        <tr>
            <td>46</td>
            <td>Jira SLA Powerbox</td>
            <td>3.x–4.2.x (excl. 3.5.x)</td>
            <td>SLA Metric field (read only)</td>
            <td></td>
        </tr>
        <tr>
            <td>47</td>
            <td>Jira Stagil Assets Management*</td>
            <td>On Premise: Stagil Assets – Advanced Link 5.0.86</td>
            <td>All Entities Supported By <code class="expression">space.vars.OIM</code> In JIRA</td>
            <td></td>
        </tr>
        <tr>
            <td>48</td>
            <td>Jira Xray**</td>
            <td>On Premise: 3.6.x–6.1.3<br/>Cloud: V1.1.90-AC-4.004.000</td>
            <td>On Premise: Test, Test Plan, Test Execution, Test Set, Sub Test Execution, Pre-Condition<br/>Cloud: Xray Test, Test Plan, Test Execution, Test Set, Test Run, Precondition</td>
            <td></td>
        </tr>
        <tr>
            <td>49</td>
            <td>Jira Zephyr Essential**</td>
            <td>Data Center: 9.x, 10.x<br/>Cloud: 8.x (1.3.33-AC)</td>
            <td>Test, Test Cycle, Test Execution, Folder</td>
            <td>Zephyr Squad</td>
        </tr>
        <tr>
            <td>50</td>
            <td>Mercurial*</td>
            <td>2.0–2.0.1, 2.6.1, 2.6.2</td>
            <td>Commit Information</td>
            <td></td>
        </tr>
        <tr>
            <td>51</td>
            <td>Midas</td>
            <td>25.10.e.003</td>
            <td>Safety Mechanism</td>
            <td></td>
        </tr>
        <tr>
            <td>52</td>
            <td>Microsoft Dynamics 365</td>
            <td>9.2</td>
            <td>All Entities</td>
            <td></td>
        </tr>
        <tr>
            <td>53</td>
            <td>Modern Requirements</td>
            <td>2010–2019</td>
            <td>Test Result, Test Run, Test Suite, Work items (Bug, Requirement, Task, Test Case, User Story, etc.), Iteration, Git Commit, Custom Entities</td>
            <td></td>
        </tr>
        <tr>
            <td>54</td>
            <td>Monday.com</td>
            <td>SaaS</td>
            <td>Board items, Board sub items</td>
            <td></td>
        </tr>
        <tr>
            <td>55</td>
            <td>OpenText ALM Octane</td>
            <td>On Premise: 16.1.x to 25.x<br/>SaaS</td>
            <td>Defect, User Story, Epic, Feature, Task, Requirement, Test, Run, etc.</td>
            <td>Micro Focus ALM Octane</td>
        </tr>
        <tr>
            <td>56</td>
            <td>OpenText ALM Quality Center</td>
            <td>SaaS: 15.x*<br/>On-Prem: 10.x*, 11.x*, 12.x to 24.x</td>
            <td>Defect, Requirement, Test, Test Set, Release, Cycle, Test Run, Folders, Configurations, Execution Request</td>
            <td>Micro Focus ALM/QC, HPALM</td>
        </tr>
        <tr>
            <td>57</td>
            <td>OpenText IT Operations Cloud*</td>
            <td>2009 R3,R4, 10.1.2.1,11.0</td>
            <td>All Custom Primary Item Entities</td>
            <td>Serena Business Manager</td>
        </tr>
        <tr>
            <td>58</td>
            <td>OpenText Project & Portfolio Mgmt (PPM)*</td>
            <td>11.3, 11.5</td>
            <td>Requirement</td>
            <td>Caliber RM</td>
        </tr>
        <tr>
            <td>59</td>
            <td>PagerDuty</td>
            <td>Cloud</td>
            <td>Incident</td>
            <td></td>
        </tr>
        <tr>
            <td>60</td>
            <td>Polarion</td>
            <td>On Premise: ALM 2506<br/>SaaS*</td>
            <td>User Story, Requirement, Epic, Task, Test Case, Issue, Change Request, Release, all system-defined work items, and custom work items</td>
            <td></td>
        </tr>
        <tr>
            <td>61</td>
            <td>ReadyOne</td>
            <td>14.0.x (Release 26)</td>
            <td>All System Item Types (Core + Custom)</td>
            <td></td>
        </tr>
        <tr>
            <td>62</td>
            <td>Redmine</td>
            <td>3.1.2+</td>
            <td>Redmine Issue + Custom Issue Types</td>
            <td></td>
        </tr>
        <tr>
            <td>63</td>
            <td>Salesforce</td>
            <td>All</td>
            <td>Case, Opportunity, Feeds, Custom Objects</td>
            <td></td>
        </tr>
        <tr>
            <td>64</td>
            <td>SAP**</td>
            <td>ECC, S/4HANA</td>
            <td>Program, Transport Request, Transaction Code, Enhancement, Usage Details, Table, Function, Package, Auth Object, Class, Data Element, TADIR</td>
            <td></td>
        </tr>
        <tr>
            <td>65</td>
            <td>Selenium*</td>
            <td>All</td>
            <td>TestScripts</td>
            <td></td>
        </tr>
        <tr>
            <td>66</td>
            <td>ServiceNow</td>
            <td>San Diego - Australia</td>
            <td>All System + Custom Tables</td>
            <td></td>
        </tr>
        <tr>
            <td>67</td>
            <td>Slack*</td>
            <td>Cloud</td>
            <td>Comments, Attachments, Post (write only)</td>
            <td></td>
        </tr>
        <tr>
            <td>68</td>
            <td>Snowflake**</td>
            <td>Cloud</td>
            <td>Tables and Views</td>
            <td></td>
        </tr>
        <tr>
            <td>69</td>
            <td>SolarWinds Service Desk</td>
            <td>SaaS</td>
            <td>Catalog Items, Change Catalog, Changes, Incidents, Problems, Releases, Solutions, Tasks</td>
            <td></td>
        </tr>
        <tr>
            <td>70</td>
            <td>Subversion*</td>
            <td>1.5, 1.6.3, 1.6.17, 1.7.9</td>
            <td>Commit Information</td>
            <td></td>
        </tr>
        <tr>
            <td>71</td>
            <td>TestRail**</td>
            <td>7.2.1, 7.8.0, 8.0.1</td>
            <td>Tests, Test Cases, Test Plans, Test Results, Test Runs, Test Suites, Sections, Milestones</td>
            <td></td>
        </tr>
        <tr>
            <td>72</td>
            <td>Trac*</td>
            <td>0.12.0, 0.11.5, 1.0</td>
            <td>Trac Ticket</td>
            <td></td>
        </tr>
        <tr>
            <td>73</td>
            <td>Tricentis qTest</td>
            <td>Cloud,<br/>On Premise: 8.4.2–2023.x.x</td>
            <td>Defect, Requirement, Testcase, Testlog, Release, Test Suite, Test Run, Module, Test Cycle, Build (read only)</td>
            <td>QA Symphony</td>
        </tr>
        <tr>
            <td>74</td>
            <td>Tricentis Tosca*</td>
            <td>2023.2, 2024.2 (x64) - 2025.1 (x64)</td>
            <td>TestCase, ExecutionTestCaseLog (read), ExecutionEntry, TCFolder, Requirement, RequirementSet, Issue, Module</td>
            <td></td>
        </tr>
        <tr>
            <td>75</td>
            <td>Verisium Manager**</td>
            <td>20.x–25.x (up to 25.01)</td>
            <td>Section, Metrics Port, Reference [from 21.01+]<br/>Supported for vPlan in DB only</td>
            <td>vManager</td>
        </tr>
        <tr>
            <td>76</td>
            <td>Windchill</td>
            <td>2009–13.3</td>
            <td>Change Order, Change Request, Defect, Document, Model, Portfolio, Product, Project, Requirement, Test, Specification, Work Item, Custom Entities</td>
            <td>PTC, Windchill RV&S</td>
        </tr>
        <tr>
            <td>77</td>
            <td>Windchill PLM*</td>
            <td>13.x</td>
            <td>Issue, Part, Change Request, and Engineering Material (each with associated Soft Types and Subtypes).
            </td>
            <td>PDM Link</td>
        </tr>
        <tr>
            <td>78</td>
            <td>Zendesk</td>
            <td>Cloud</td>
            <td>Zendesk Ticket</td>
            <td></td>
        </tr>
         <tr>
            <td>78</td>
            <td>Zephyr Enterprise</td>
            <td>8.6.0</td>
            <td>Folder, Phase, Test Case, Test Execution</td>
            <td></td>
        </tr>
    </tbody>
</table>


(*) Professional services required for version specific certification. <br> (**) Professional services recommended due to modelling complexity.

`