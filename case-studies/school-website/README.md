# Full-Stack School Website & Publishing Automation

**Organisation:** St. Alphonsa Public School & Junior College, Kerala  
**Live website:** [sapsjc.in](https://sapsjc.in)  
**Source code:** Private

## Context

The school needed a modern website covering admissions, campus facilities, faculty, galleries, fee-payment information, and mandatory public disclosure documents. Its existing visual editing workflow introduced layout problems and made maintenance difficult.

The project also had practical constraints: a 2 MB server upload limit, inconsistent staff photographs received over WhatsApp, and office staff who needed to update notices without developer assistance.

## My contribution

- Built a full-stack school website using Laravel, HTML, and CSS, combining a responsive frontend with staff admin workflows.
- Created a Python publishing script to submit prepared page content to the existing server workflow.
- Developed an OpenCV pipeline to locate faces, remove unwanted image borders, and produce consistent square faculty portraits.
- Automated video cutting and compression with FFmpeg to fit the server's upload limit.
- Built checks for broken links, selected design conventions, and required disclosure document references.
- Supported notice and calendar updates through the existing staff admin portal.

## Engineering decisions

### Repeatable page publishing

Preparing page markup outside the visual editor and publishing it through a script made the layout easier to control and reduced repetitive editing work.

### Face-aware image preparation

Simple centre crops could cut off faces in photographs with different framing. Face detection provided a useful reference for consistent portrait crops across the faculty directory.

### Media processing under a hard upload limit

The FFmpeg workflow shortened and compressed clips to fit a 2 MB upload limit. Clip duration, resolution, and compression settings were practical tradeoffs between file size and visual quality.

### Checks before publication

Automated checks helped identify missing document links and selected content or styling problems before publishing. These checks support maintenance; they do not constitute a formal regulatory compliance audit.

### Staff ownership of routine updates

The admin portal let staff maintain notices and dates while the scripted workflow handled the more structured pages and media preparation.

## Delivered work

- A full-stack website covering the school's main information needs, with responsive pages and staff-managed updates.
- Standardized portraits for a 46-member faculty directory.
- Repeatable workflows for page publishing and media preparation.
- Staff-managed notices and calendar updates.
- Automated checks for public disclosure document links.

## Technology

Laravel, HTML5, CSS, Python, OpenCV, FFmpeg, and Python Requests.

## Relevance to my career direction

This project demonstrates operational automation and applied computer vision in a real institutional workflow. It gave me experience adapting software to hosting constraints and making maintenance easier for non-technical users.
