# **XSD Schema Structure and Entities**

## **Entities and Their Composition**

### **1. `Project_T` (Complex Type)**
- **Description:** Type definition of a project.
- **Base Type:** `ocx:IdBase_T` (imported from `ocx` namespace)
- **Used in:** `Project` element.

---

### **2. `Project` (Element)**
- **Description:** Represents a project that contains comments.
- **Base Type:** `cmnt:Project_T`
- **Composition:**
  - Contains **one** `cmnt:Comments` element.

#### **Attributes**
| Name                        | Type      | Required | Description |
|-----------------------------|----------|----------|-------------|
| `oid`                       | `xs:string` | Yes | Unique object ID |
| `designId`                  | `xs:string` | No | Unique vessel design ID |
| `vesselId`                  | `xs:string` | No | Unique vessel ID |
| `contractBuilderBuildNo`     | `xs:string` | No | Yard build number |
| `contractBuilderBuildName`   | `xs:string` | No | Yard name |
| `imoNumber`                 | `xs:string` | No | Vessel assigned IMO number |
| `projectId`                 | `xs:string` | No | Unique project ID |
| `projectName`               | `xs:string` | No | Project name |

---

### **3. `Comment_T` (Complex Type)**
- **Description:** Defines a comment.
- **Base Type:** `ocx:IdBase_T`
- **Composition:**
  - **Mandatory Elements:**
    - `cmnt:IssueDate`
    - `cmnt:Title`
    - `cmnt:CommentDescription`
  - **Optional Elements (`minOccurs=0`)**
    - `cmnt:ClosedDate`
    - `cmnt:Attachment`
    - `cmnt:Reference`
    - `cmnt:Note`
    - `cmnt:Replies`

#### **Attributes**
| Name          | Type      | Required | Description |
|--------------|----------|----------|-------------|
| `oid`       | `xs:string` | Yes | Unique object ID |
| `commentId` | `xs:string` | Yes | Unique comment ID |
| `status`    | Enum (`Open`, `Closed`, `Closed but disagreed`, `NA - Not applicable`) | Yes | Comment status |
| `commentType` | Enum (`Action Required`, `Important Note`) | Yes | Comment type |

---

### **4. `Comment` (Element)**
- **Description:** Represents a comment issued by a classification society.
- **Base Type:** `cmnt:Comment_T`
- **Composition:** Inherits `Comment_T`.

---

### **5. `Comments` (Element)**
- **Description:** A container for multiple comments.
- **Composition:**
  - Contains multiple occurrences (`maxOccurs="unbounded"`) of:
    - `cmnt:Comment`
    - `cmnt:MarkupComment`

---

### **6. `MarkupComment_T` (Complex Type)**
- **Description:** Defines a 3D markup comment.
- **Base Type:** `cmnt:Comment_T`
- **Composition:**
  - Contains one `cmnt:VisualizationInfo` element.

---

### **7. `MarkupComment` (Element)**
- **Description:** A 3D comment with markup of the 3D model.
- **Base Type:** `cmnt:MarkupComment_T`

---

### **8. `Reply_T` (Complex Type)**
- **Description:** Defines a reply to a comment.
- **Base Type:** `ocx:IdBase_T`
- **Composition:**
  - **Mandatory Elements:**
    - `cmnt:ReplyDescription`
    - `cmnt:IssueDate`
  - **Optional Elements:**
    - `cmnt:Attachment` (Can have multiple occurrences)

#### **Attributes**
| Name       | Type      | Required | Description |
|-----------|----------|----------|-------------|
| `oid`     | `xs:string` | Yes | Unique object ID |
| `replyId` | `xs:string` | Yes | Unique reply ID |
| `issuedBy`| `xs:string` | Yes | Name of the issuer |

---

## **External Dependencies**
- `ocx:IdBase_T`, `ocx:Point3D_T`, `ocx:Vector3D_T`, `ocx:Quantity_T` are imported from `https://3docx.org/fileadmin//ocx_schema//V300//OCX_Schema.xsd`.

---

## Class Diagram

The UML diagram is a simplified representation of the comment API and is intended to give a basic understanding of the comment exchange information.

![Class Diagram](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/OCXStandard/ocx-extension-comments/main/UML/ocx_comments.puml)

