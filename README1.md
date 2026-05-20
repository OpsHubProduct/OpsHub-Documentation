---
if: >-
  "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product 
cover: ./docs/assets/Site_Images/OIM.png
icon: hand-wave
coverY: 0
layout:
  width: wide
  cover:
    visible: true
    size: full
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: false
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: false
---

{% if "OM4ADO" !== visitor.claims.unsigned.product && "OAM" !== visitor.claims.unsigned.product %}    

<table data-view="cards">
   <thead>
      <tr align="center">
         <th align="center"></th>
         <th data-hidden data-card-cover data-type="image">Cover image</th>
         <th data-hidden data-card-target data-type="content-ref"></th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Get Started</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Getting_Started.svg">Getting Started</a></td>
         <td><a href="docs/getting-started/getting-started.md">getting-started</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Integrate</mark></h3></td>
         <td><a href="docs/assets/Site_Images/integrate.svg">Integrate</a></td>
         <td><a href="docs/integrate/integrate.md">Integrate</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Manage</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Manage.svg">Manage</a></td>
         <td><a href="docs/manage/manage.md">Manage</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Supported Connectors</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Supported_Connectors.svg">Supported Connectors</a></td>
         <td><a href="docs/supported-connectors/systems-supported.md">Supported Connectors</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Connector Documentation</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Connector_Documentation.svg">Connector Documentation</a></td>
         <td><a href="docs/connectors/connectors.md">Connectors</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Connector SDK</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Connector_SDK.svg">Connector SDK</a></td>
         <td><a href="docs/connector-sdk/connector-sdk-index.md">Connector SDK</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Release Notes</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Release_Note.svg">Release Note</a></td>
         <td><a href="docs/release-notes/release-notes.md">Release Note</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Knowledge Resources</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Knowledge_Resources.svg">Knowledge Resources</a></td>
         <td><a href="docs/knowledge-resources/knowledge-resource-index.md">Knowledge Resource</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Help Center</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Help_Center.svg">Help Center</a></td>
         <td><a href="docs/help-center/help-center-index.md">Help Center</a></td>
      </tr>
   </tbody>
</table> 

{% endif %}   

{% if "OM4ADO" === visitor.claims.unsigned.product %}  

<table data-view="cards">
   <thead>
      <tr>
         <th align="center"></th>
         <th data-hidden data-card-cover data-type="image">Cover image</th>
         <th data-hidden data-card-target data-type="content-ref"></th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Get Started</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Getting_Started.svg">Getting Started</a></td>
         <td><a href="docs/getting-started/getting-started.md">getting-started</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Migrate</mark></h3></td>
         <td><a href="docs/assets/Site_Images/integrate.svg">Migrate</a></td>
         <td><a href="docs/integrate/integrate.md">Migrate</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Manage</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Manage.svg">Manage</a></td>
         <td><a href="docs/manage/manage.md">Manage</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Supported Connectors</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Supported_Connectors.svg">Supported Connectors</a></td>
         <td><a href="docs/supported-connectors/systems-supported.md">Supported Connectors</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Release Notes</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Release_Note.svg">Release Note</a></td>
         <td><a href="docs/release-notes/release-notes.md">Release Note</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Knowledge Resources</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Knowledge_Resources.svg">Knowledge Resources</a></td>
         <td><a href="docs/knowledge-resources/knowledge-resource-index.md">Knowledge Resource</a></td>
      </tr>
      <tr>
         <td align="center"><h3><mark style="color:#233C5D">Help Center</mark></h3></td>
         <td><a href="docs/assets/Site_Images/Help_Center.svg">Help Center</a></td>
         <td><a href="docs/help-center/help-center-index.md">Help Center</a></td>
      </tr>
   </tbody>
</table>


{% endif %}
