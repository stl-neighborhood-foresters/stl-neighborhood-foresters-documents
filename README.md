# St. Louis Neighborhood Foresters

Project brief and original volunteer and tree-care exports shared for the November 6, 2026 Code Til Dawn session.

This repository helps staff and volunteers understand what information is available, agree on reporting definitions, and prepare for future development. It contains the four original supplied files and this README. No dashboard application, dashboard source code, generated reporting dataset, or hosting configuration is included.

## Project purpose

The draft brief asks one central question:

> Where are volunteers doing tree care, how much care is being completed, and which neighborhoods need more support?

The proposed reporting should help a staff coordinator or program leader understand participation, completed tree care, and geographic gaps. The Word document is a working draft: its proposed requirements, comments, and open questions should be reviewed with the nonprofit before implementation.

## Files

The three original Excel workbooks are in the `documents/` folder. The project brief remains at the repository root.

| File | Contents | Records |
| --- | --- | ---: |
| [Wire Frame - Code Til Dawn Draft.docx](Wire%20Frame%20-%20Code%20Til%20Dawn%20Draft.docx) | Project goals, proposed screens, metric definitions, geographic rules, handoff checklist, and acceptance tests | Word document |
| [champions_20261106.xlsx](documents/champions_20261106.xlsx) | Volunteer roster, contact information, summary hours, membership information, and emergency contacts | 116 rows |
| [activities_20261106.xlsx](documents/activities_20261106.xlsx) | Recorded volunteer participation, dates, hours, activity categories, and opportunity names | 263 rows |
| [UserActivity_2024-06-23_to_2026-10-25.xlsx](documents/UserActivity_2024-06-23_to_2026-10-25.xlsx) | Tree activity history, tree identifiers, action types, locations, and inventory changes | 9,923 rows |

Counts exclude header rows. Source files are preserved without editing or removing records. Files with `.xlsx` extensions are Excel workbooks even where their worksheet names end in `.csv`.

## Open the files

Select a filename above, then download it to open in Microsoft Word or Excel, or another compatible application. GitHub may not display the contents of these binary files directly. There is no application to install or run in this repository.

## Access and personal information

Keep this repository private. The original exports contain names, email addresses, phone numbers, addresses, dates of birth, and emergency-contact information. The tree log also contains volunteer labels and precise tree locations.

Grant access only to approved project collaborators. Do not publish the original files, paste personal records into public issues, or enable public file hosting for this repository. Use a separate de-identified copy when preparing a public demo or sharing examples outside the project team. Removing a file in a later commit does not remove earlier versions from Git history.

No open-source license or permission to redistribute these records is granted by this README.

## What each dataset represents

### Volunteer roster

Worksheet: `champions_20261106.csv`.

The roster contains 116 records and 22 columns. It describes people and summary information, rather than one row per work session. Roster membership is not evidence that someone volunteered during a selected period.

Columns:

- First Name, Last Name, Email, Mobile Phone, Home Phone, Contact
- Hours, Donations, Last Activity, Groups, Address
- Emergency Contact First Name, Emergency Contact Last Name, Emergency Contact Relationship
- Emergency Contact Mobile Phone, Emergency Contact Work Phone, Emergency Contact Home Phone, Emergency Contact Email Address
- Member Since, Date of Birth, Tags, Notes

The roster Hours column totals **643.9 hours**. Its reporting scope is not documented in the file, so it should not be treated as an independently verified period total or added to the activities export.

### Volunteer participation

Worksheet: `activities_20261106.csv`.

The export contains 263 records and 21 columns. Check-In Date ranges from **May 23 through November 1, 2026**. Recorded hours sum to **644.0**, and the records contain **80 distinct normalized email addresses**. These are source summaries across the whole export, not approved tree-care-only metrics.

Columns:

- First Name, Last Name, Email, Phone Number
- Opportunity, Activity
- Check-In Date, Check-In Time, Check-Out Date, Check-Out Time, Hours
- Reflection, Rating, High-Fives, Notes
- Address, City, State, Zip, Groups, Tags

Activities include tree care, meetings, orientation, training, leadership, and outreach. Forty-eight rows have no Activity category, and 26 have no Opportunity value. Neither a stable attendance-record ID nor an explicit event ID or attendance-status column is included.

All 80 normalized activity email identities occur in the roster. Email can help reconcile these two exports internally, but shared or changed addresses can complicate identification. Use de-identified identifiers for reporting outputs, and do not assume names alone establish identity.

The meaning of the Address fields needs verification before using them as work locations. A volunteer's home address must not be used to assign the location of their volunteer work.

### Tree activity history

Main worksheet: `UserActivity_2024-06-23_to_2026`.

The export contains 9,923 rows and 14 columns. Recorded timestamps range from **June 23, 2024 through October 25, 2026**. There are **3,771 distinct MTLC ID values** across all action types. This is not a complete city inventory or a count of trees that received completed care.

Columns:

- Date Time, Volunteer, Alias
- Action, Field, From, To
- MTLC ID, Address, Common Name, City GUID, Condition, Latitude, Longitude

The workbook also contains a `Year_Action_Summary` worksheet that is empty.

| Recorded action | Rows | Initial interpretation |
| --- | ---: | --- |
| Watering | 4,614 | Completed care candidate |
| Datachange | 1,762 | Inventory edit |
| Addedphotos | 1,093 | Documentation |
| Pruned | 881 | Completed care candidate |
| Mulched | 701 | Completed care candidate |
| Treeadded | 369 | Tree record added; does not establish planting |
| Wateringclaim | 188 | Claim or commitment; not completed watering |
| Request | 174 | Request; meaning needs review |
| Mulching not needed | 76 | Assessment |
| Releasedwateringclaim | 33 | Claim released |
| Deletedphotos | 21 | Documentation change |
| Pruning not needed | 11 | Assessment |

Counting only Watering, Pruned, and Mulched gives **6,196 raw action records across 2,773 distinct MTLC tree IDs**. The program team should approve this definition before using it in formal reporting.

## Data quality findings

- **Potential duplicate tree records:** 125 extra rows are identical to earlier rows across all source columns. Ninety-nine of those are among Watering, Pruned, and Mulched. Do not remove them automatically without understanding the export. Excluding these identical extra care rows would give 6,097 care records; the distinct-tree count remains 2,773.
- **Missing tree coordinates:** 83 tree-log rows lack latitude or longitude. Retain them as unassigned rather than silently dropping them from totals.
- **Different reporting periods:** the shared source period is May 23 through October 25, 2026. Comparisons should use a common date range and indicate where a source has no coverage.
- **No shared event key:** these exports do not contain a verified event/work-session identifier connecting volunteer participation with tree actions.
- **No stable action-record identifier:** the tree log contains tree identifiers, but no explicit unique ID for each action. A safe repeated-import strategy needs to be agreed before building an importer.
- **No complete inventory denominator:** the files do not establish the full number of eligible city trees, tree ages, or a comprehensive care-needs register.
- **Roster hours differ slightly:** the roster totals 643.9 hours while activity rows total 644.0. The reason has not been established; do not assume the files have identical scope or rounding rules.

## Proposed reporting definitions

| Measure | Proposed definition |
| --- | --- |
| Active volunteers | Distinct volunteer identities with qualifying recorded participation in the selected period |
| Volunteer hours | Sum of Hours for qualifying participation records |
| Trees cared for | Distinct stable tree IDs with at least one qualifying completed care action |
| Care actions | Count of qualifying care-action records, broken out by type |
| Hours per active volunteer | Qualifying hours divided by distinct active volunteers |
| Tree-care coverage | Distinct eligible trees receiving care divided by the full eligible-tree inventory for the same area |

“Qualifying” participation and care require program approval. Keep all recorded participation separate from tree-care-only participation.

A person attending three sessions counts as one active volunteer and three attendance records. A tree watered three times counts as one tree cared for and three watering actions. Recalculate citywide distinct counts instead of adding neighborhood distinct counts.

Coverage is unavailable until a reliable inventory denominator is supplied. Missing data must not be displayed as zero, and an absence of records should be described as **no recorded activity** rather than proof that no work happened.

## Geographic rules

- Assign tree care using the tree's work location.
- Assign volunteer participation using the event or work-session location, not the volunteer's home neighborhood.
- Treat neighborhood and ward as separate attributes. A neighborhood may intersect multiple wards.
- Use official city boundary data and document the boundary version.
- Retain missing locations and multi-area work as explicit unassigned categories when reliable allocation is unavailable.
- Event names may help staff review possible neighborhood assignments, but do not establish verified locations or direct event-to-care links.

## Questions to resolve with the nonprofit

1. Which activities count as tree-care volunteering, and should meetings, training, and outreach appear separately?
2. Do the original systems have stable volunteer, attendance, action, and event identifiers that can be added to a later export?
3. Where are event work locations recorded, and what do the activity Address fields represent?
4. What causes identical tree-log rows, and how should repeat imports be handled?
5. How should individual tree care outside organized work sessions be reported?
6. Where can the team obtain the full tree inventory, tree age information, and recorded care needs?
7. Who will approve definitions and review results before they are used externally?
