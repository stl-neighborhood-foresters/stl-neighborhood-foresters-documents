# St. Louis Neighborhood Foresters

Project documentation and source data for volunteer participation and tree-care reporting in Google Looker Studio.

This repository contains the original project brief and three Excel exports provided for the November 6, 2026 Code Til Dawn session, together with a curated reporting workbook. It supports requirements review, data preparation, and agreement on reporting definitions. Application source code and dashboard assets are outside the scope of this repository.

## Reporting objectives

The project aims to help program staff understand:

- Volunteer participation and recorded service hours.
- Trees receiving care and completed care actions by type.
- Activity across neighborhoods and wards.
- Geographic gaps and limitations in the available records.

The Word document provides the draft requirements and proposed reporting layout. Metric definitions and geographic assignments require program review before formal reporting.

## Repository contents

| Document | Description |
| --- | --- |
| [Project brief](Wire%20Frame%20-%20Code%20Til%20Dawn%20Draft.docx) | Draft requirements, wireframes, reporting definitions, and acceptance criteria. |
| [Volunteer roster](documents/champions_20261106.xlsx) | Volunteer profiles, membership information, and summary hours. |
| [Volunteer activities](documents/activities_20261106.xlsx) | Participation records, service dates, hours, activity categories, and opportunity names. |
| [Tree activity history](documents/UserActivity_2024-06-23_to_2026-10-25.xlsx) | Tree identifiers, care actions, inventory changes, and recorded locations. |
| [Curated Looker Studio dataset](transformed-data/transformed%20data.xlsx) | De-identified reporting tables with standardized dates, geographic assignments, species labels, and review flags. |

The original Excel workbooks are stored in `documents/`. The curated workbook is stored separately in `transformed-data/`. All four source files are retained in their original form.

## Curated reporting dataset

The [curated workbook](transformed-data/transformed%20data.xlsx) contains three worksheets:

| Worksheet | Contents |
| --- | --- |
| Volunteer participation | 263 participation records with anonymous volunteer IDs, recorded hours, activity categories, and provisional neighborhood assignments. |
| Tree activity | 9,923 action records with tree IDs, dates, recorded species, neighborhood and ward assignments, completed-care indicators, and potential-duplicate flags. |
| Field guide | Field definitions, source references, transformation rules, reporting limitations, and reference totals. |

Connect the two reporting worksheets as separate Looker Studio data sources. The Field guide is reference documentation, not a chart data source.

Personal contact details, birth dates, emergency contacts, volunteer names and aliases, home addresses, and exact tree coordinates are excluded from the curated workbook. Potentially duplicated records are flagged and retained. Completed-care categories and event-name-based volunteer neighborhood assignments remain provisional. Species labels reflect the recorded Common Name values and have not been reconciled to a botanical taxonomy.

The workbook is a static reporting snapshot. It does not establish live synchronization with the original systems. Record IDs identify source rows within this snapshot and are not verified persistent identifiers from those systems.

## Dataset overview

| Dataset | Records | Available period | Reporting role |
| --- | ---: | --- | --- |
| Volunteer roster | 116 | Summary scope not specified | Supporting reference for volunteer records. |
| Volunteer activities | 263 | May 23–November 1, 2026 | Primary source for recorded participation and hours. |
| Tree activity history | 9,923 | June 23, 2024–October 25, 2026 | Primary source for tree actions and work locations. |

Record counts exclude headers. The overlapping activity period is **May 23–October 25, 2026**.

The volunteer activities export contains 644.0 recorded hours across 80 distinct normalized email addresses. It includes meetings, training, and outreach as well as tree care. The tree activity export contains 3,771 distinct MTLC tree IDs across all action types; this is not a complete tree inventory or a completed-care total.

## Looker Studio reporting approach

The planned reporting model uses separate tables for volunteer participation and tree activity. The roster provides supporting reference information; its summary hours must not be added to activity hours.

Prepare reporting copies with consistent date fields, de-identified volunteer identifiers, approved activity categories, and documented geographic assignments. Preserve the source records separately from reporting transformations.

The two activity exports do not contain a verified shared event identifier. Any combined area comparison requires a documented aggregation and join strategy to prevent duplicated totals. Direct attribution of tree care to individual events is not established by these files.

## Proposed metrics

| Metric | Definition |
| --- | --- |
| Active volunteers | Distinct volunteer identities with qualifying recorded participation during the selected period. |
| Volunteer hours | Sum of recorded hours for qualifying participation. |
| Trees cared for | Distinct tree IDs with at least one qualifying completed care action. |
| Care actions | Number of qualifying completed care records, reported by action type. |
| Hours per active volunteer | Qualifying volunteer hours divided by distinct active volunteers. |
| Tree-care coverage | Distinct eligible trees receiving care divided by the eligible tree inventory for the same area. |

Watering, pruning, and mulching are the initial proposed completed-care categories. Watering claims, photo uploads, inventory edits, and requests should be reported separately. The program team must approve qualifying participation and care categories.

Count each volunteer and tree once within the selected reporting scope. Recalculate distinct counts for citywide totals rather than summing neighborhood counts. Coverage remains unavailable until a complete eligible-tree inventory is supplied.

## Data quality and limitations

| Finding | Reporting implication |
| --- | --- |
| 125 potentially duplicated tree-log rows | Confirm the export behavior before removing identical records. No unique action-record ID is provided. |
| 83 tree-log rows without coordinates | Retain unassigned records and disclose their effect on geographic reporting. |
| 48 participation records without an Activity category; 26 without an Opportunity value | Review classification and work-session information before applying activity filters. |
| No verified shared event identifier | Compare sources at an agreed reporting level; avoid unsupported event-level attribution. |
| Different source periods | Apply a common comparison period and disclose dates without source coverage. |
| Roster hours total 643.9; activity hours total 644.0 | Reconcile source scope and rounding before treating the totals as equivalent. |
| No complete eligible-tree inventory, tree ages, or care-needs register | Coverage, young-tree reporting, and verified unmet-need measures require additional data. |

Using the proposed care categories gives 6,196 raw care records across 2,773 distinct MTLC tree IDs. Ninety-nine potentially duplicated rows occur within those categories. These figures describe the supplied export before duplicate resolution and program approval.

An absence of records should be labeled **no recorded activity**. Missing data must remain distinguishable from a confirmed zero.

## Geographic assignment

Assign tree care using the tree's work location and volunteer participation using the event or work-session location. Volunteer home addresses are not work locations.

Neighborhoods and wards are separate geographic attributes. Use official city boundaries, document the boundary version, and retain unassigned or multi-area records when reliable allocation is unavailable. Event names can support review but do not establish verified work locations.

## Access and confidentiality

This is a private repository containing personal volunteer and emergency-contact information, dates of birth, and precise tree locations. Access is intended for authorized project collaborators.

Use de-identified reporting copies for analysis and external demonstrations. Keep personal records out of public reports, issues, and screenshots. This repository does not grant permission to redistribute the source data.

## Decisions requiring program review

- Activities that qualify as tree-care participation and completed care.
- Availability of stable volunteer, attendance, action, and event identifiers.
- Verified event locations and the meaning of address fields in the exports.
- Treatment of potential duplicates and repeated imports.
- Reporting of individual tree care outside organized work sessions.
- Sources for eligible tree inventory, tree ages, and recorded care needs.
- Responsibility for approving metric definitions and reporting results.
