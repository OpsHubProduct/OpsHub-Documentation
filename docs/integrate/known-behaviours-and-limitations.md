# Synchronization Limitations and Known Behaviours

## Common

There are a few limitations that are common across all connectors. The limitations are listed below:

- **User Mention Synchronization Limitations**  
  - If both the source and the target system support synchronization of User mentions and the user which is being synchronized from the source system does not exist in the target system, then that user's display name as seen in the source system will synchronize to the target system as literal text.
  - If the source system supports synchronization of User mentions but the target system does not, then there are two scenarios:  
    - If the user *exists in both the source and the target system*, then the target system's user's display name will synchronize to the target system as literal text.  
    - If the source user *does not exist in the target system*, then the source system's user's display name as seen in the source system will synchronize to the target system as literal text.
  - In both the above-mentioned cases, once the literal text for the user's display name is synchronized to the target system, and when this data is synchronized back to the other system, the actual User mention will be overwritten with the literal text as displayed in the target system.

- **Inline Image Synchronization Limitations**  
  - The inline image from an entity of the source system synchronizes as a broken image to the target system, given that the embedded inline image URL in the source system is not accessible/reachable from the machine on which <code class="expression">space.vars.OIM</code> is installed while the entity is getting synchronized. In that case, the inline image synchronizes to the target system without transformation in the URL corresponding to the target system. As a result, the synchronized image is broken.
  - Synchronization of the height and width of the inline image is performed only for HTML-supported systems.
  - If the same image is referred to more than once with a different height and width, then only the size of the last image is synchronized with all the images on the target side.

- **Attachment Synchronization Limitations**  
  - While performing reconciliation, if the source and target systems have multiple attachments with the same name and the same size, the source attachment will be synchronized as a new attachment in the target system, as mapping to any existing attachment can lead to incorrect data.  
    - **Example:** If the source entity has an attachment `About.png` (with 1 KB size) and the target entity has two attachments named `About.png` (both having 1 KB size), then during reconciliation, <code class="expression">space.vars.OIM</code> will synchronize a duplicate attachment in the target system.

- **Comment Synchronization Behaviour (Edited Comments)**
  - Consider the following scenario:
      - Initial sync of an entity:
          - Comments **C1** and **C2** are added and synchronized to the target system.
      - Later:
          - Comment **C1** is edited in the source system.

  - When the edited comment is synchronized:
      - <code class="expression">space.vars.OIM</code> detects the updated **C1** based on its modified timestamp.
      - As **editing existing comments is not supported**, the <code class="expression">space.vars.OIM</code> does not update the previously synced comment (C1).
      - Instead, a **new comment is created** with the updated content.

  - This may result in **duplicate-looking comments** in the target system (original C1 + updated C1).
      
## End System Limitations

In addition to the common limitations, each system has its own set of synchronization limitations.  
Such limitations are available in the limitations section on each connector's page under [Connectors](../connectors/connectors.md).

