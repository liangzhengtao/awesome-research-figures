# Technical Diagrams with draw.io

## When to Use

- Creating system architecture diagrams, flowcharts, ER diagrams
- Building UML diagrams (class, sequence, use case)
- Designing network topology or infrastructure diagrams
- Collaborating on diagrams with team members
- Exporting diagrams to SVG/PDF for LaTeX papers or presentations

## Tools and Libraries

- [draw.io](https://www.drawio.com/) (desktop or web app)
- Alternative: `draw.io-export` CLI for batch export
- Mermaid integration for code-generated diagrams

## Step-by-Step Instructions

### 1. Create a Publication-Ready Template

Open draw.io and configure the following settings before starting:

1. **Page setup**: Extras → Edit Diagram → Set page size to journal specs
2. **Grid**: View → Grid (toggle on for alignment)
3. **Export settings**: File → Export as → PDF with 300 DPI minimum
4. **Font**: Set default font to match your journal (Times New Roman or Arial)

### 2. Color Palette for Publications

Add these as custom colors in draw.io (Format → Edit Style):

```
Blue:     #0072B2
Orange:   #D55E00
Green:    #009E73
Pink:     #CC79A7
Yellow:   #E69F00
Lt Blue:  #56B4E9
```

### 3. XML Template for Consistent Styling

```xml
<!-- draw.io style string for a publication block -->
<mxCell id="1" value="Component" style="
  rounded=1;
  whiteSpace=wrap;
  html=1;
  fillColor=#dae8fc;
  strokeColor=#6c8ebf;
  strokeWidth=1;
  fontFamily=Times New Roman;
  fontSize=11;
  fontColor=#333333;
  shadow=0;
" vertex="1"/>
```

## Code Templates

### Template 1: System Architecture Diagram

```xml
<!-- System architecture with layered components -->
<mxGraphModel>
  <root>
    <mxCell id="0"/>
    <mxCell id="1" parent="0"/>

    <!-- Presentation Layer -->
    <mxCell id="2" value="Presentation Layer" style="
      swimlane;startSize=23;fillColor=#dae8fc;
      strokeColor=#6c8ebf;fontSize=12;
      fontFamily=Helvetica;fontStyle=1;
    " vertex="1" parent="1">
      <mxGeometry x="20" y="20" width="560" height="100" as="geometry"/>
    </mxCell>
    <mxCell id="3" value="Web UI" style="
      rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;
      fontSize=10;fontFamily=Helvetica;
    " vertex="1" parent="2">
      <mxGeometry x="30" y="35" width="100" height="50" as="geometry"/>
    </mxCell>
    <mxCell id="4" value="Mobile App" style="
      rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;
      fontSize=10;fontFamily=Helvetica;
    " vertex="1" parent="2">
      <mxGeometry x="160" y="35" width="100" height="50" as="geometry"/>
    </mxCell>
    <mxCell id="5" value="API Client" style="
      rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;
      fontSize=10;fontFamily=Helvetica;
    " vertex="1" parent="2">
      <mxGeometry x="290" y="35" width="100" height="50" as="geometry"/>
    </mxCell>

    <!-- Application Layer -->
    <mxCell id="6" value="Application Layer" style="
      swimlane;startSize=23;fillColor=#d5e8d4;
      strokeColor=#82b366;fontSize=12;
      fontFamily=Helvetica;fontStyle=1;
    " vertex="1" parent="1">
      <mxGeometry x="20" y="150" width="560" height="100" as="geometry"/>
    </mxCell>
    <mxCell id="7" value="API Gateway" style="
      rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;
      fontSize=10;fontFamily=Helvetica;
    " vertex="1" parent="6">
      <mxGeometry x="30" y="35" width="100" height="50" as="geometry"/>
    </mxCell>
    <mxCell id="8" value="Auth Service" style="
      rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;
      fontSize=10;fontFamily=Helvetica;
    " vertex="1" parent="6">
      <mxGeometry x="160" y="35" width="100" height="50" as="geometry"/>
    </mxCell>
    <mxCell id="9" value="ML Service" style="
      rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;
      fontSize=10;fontFamily=Helvetica;
    " vertex="1" parent="6">
      <mxGeometry x="290" y="35" width="100" height="50" as="geometry"/>
    </mxCell>

    <!-- Data Layer -->
    <mxCell id="10" value="Data Layer" style="
      swimlane;startSize=23;fillColor=#e1d5e7;
      strokeColor=#9673a6;fontSize=12;
      fontFamily=Helvetica;fontStyle=1;
    " vertex="1" parent="1">
      <mxGeometry x="20" y="280" width="560" height="100" as="geometry"/>
    </mxCell>
    <mxCell id="11" value="PostgreSQL" style="
      shape=cylinder3;size=10;fillColor=#e1d5e7;
      strokeColor=#9673a6;fontSize=10;
      fontFamily=Helvetica;whiteSpace=wrap;
    " vertex="1" parent="10">
      <mxGeometry x="30" y="30" width="80" height="60" as="geometry"/>
    </mxCell>
    <mxCell id="12" value="Redis" style="
      shape=cylinder3;size=10;fillColor=#e1d5e7;
      strokeColor=#9673a6;fontSize=10;
      fontFamily=Helvetica;whiteSpace=wrap;
    " vertex="1" parent="10">
      <mxGeometry x="160" y="30" width="80" height="60" as="geometry"/>
    </mxCell>
    <mxCell id="13" value="Model Store" style="
      shape=cylinder3;size=10;fillColor=#e1d5e7;
      strokeColor=#9673a6;fontSize=10;
      fontFamily=Helvetica;whiteSpace=wrap;
    " vertex="1" parent="10">
      <mxGeometry x="290" y="30" width="80" height="60" as="geometry"/>
    </mxCell>
  </root>
</mxGraphModel>
```

### Template 2: Database ER Diagram

```
ER Diagram Layout (use draw.io ER diagram template):

[User] ||--o{ [Post] : "writes"
[User] ||--o{ [Comment] : "writes"
[Post] ||--o{ [Comment] : "has"
[Post] }o--o{ [Tag] : "tagged with"

Entities:
  User (id: INT PK, name: VARCHAR, email: VARCHAR)
  Post (id: INT PK, title: VARCHAR, body: TEXT, user_id: FK)
  Comment (id: INT PK, body: TEXT, post_id: FK, user_id: FK)
  Tag (id: INT PK, name: VARCHAR)
```

**draw.io tips for ER diagrams:**
- Use the Entity Relation shape library
- Set relationship lines with proper crow's foot notation
- Add a table-style layout for attribute listing

### Template 3: Algorithm Flowchart

```
Flowchart elements (draw.io):

Start → Initialize Parameters → Check Condition →
  ├─ Yes: Compute Result → Output → End
  └─ No: Update State → Loop back to Check

draw.io shapes:
  - Rounded rectangle for Start/End (fillColor=#d5e8d4)
  - Rectangle for Process (fillColor=#dae8fc)
  - Diamond for Decision (fillColor=#fff2cc)
  - Parallelogram for I/O (fillColor=#f8cecc)
```

## Export Settings for Publications

### PDF Export
```
File → Export as → PDF
  - Zoom: 100%
  - Border Width: 10 (for margin)
  - Size: Page
  - Crop: checked
```

### SVG Export (for LaTeX)
```
File → Export as → SVG
  - Embed Images: checked
  - Links: unchecked
  - Size: Page
```

### PNG Export
```
File → Export as → PNG
  - DPI: 600 (for print quality)
  - Transparent Background: unchecked
  - Border: 10
```

## Style Specifications

| Element | Property | Value |
|---------|----------|-------|
| Default font | fontFamily | Helvetica or Times New Roman |
| Font size | fontSize | 10–12 pt |
| Stroke width | strokeWidth | 1 pt |
| Rounded corners | rounded | 1 (or rounded=3 for larger) |
| Shadow | shadow | 0 (no shadow for print) |
| Page border | border | 10 px |
| Grid | gridSize | 10 px |

## Common Pitfalls

1. **Export at wrong zoom**: Always export at 100% zoom for print
2. **Font not embedded in SVG/PDF**: Install fonts locally or convert text to paths
3. **Misaligned elements**: Use grid snapping and alignment guides
4. **File size too large**: Flatten embedded images; use vector shapes instead of bitmaps
5. **Colors not matching**: Use hex color codes consistently
6. **Layer ordering issues**: Right-click → "To Front" / "To Back" for z-order control
7. **Export cut off**: Check page bounds; resize canvas to fit content

## Journal-Specific Tips

- **IEEE**: Export as PDF or EPS; embed in LaTeX with `\includegraphics`
- **Nature**: SVG preferred; ensure text is selectable (not rasterized)
- **Springer**: PDF with embedded fonts; match system architecture style across paper
- **ACM**: Use ACM template colors if specified; otherwise standard palette
- **General**: Provide editable source (.drawio) as supplementary material when possible
