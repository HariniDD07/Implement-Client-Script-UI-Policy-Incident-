# Implement Client Script & UI Policy (Incident)

## Problem Statement
Incident records often require consistent and accurate data entry to ensure effective triage, routing, and resolution. Relying solely on user awareness and manual checks can lead to incomplete or incorrect data. Conditional field behavior and validation are required directly at the user interface level to ensure data integrity.

## Objective
To demonstrate how ServiceNow client-side controls (UI Policies and Client Scripts) enforce data integrity, auto-populate values, dynamically control field behavior, and prevent record submission when required conditions are not met.

## Features & Implementation
- **UI Policy (High Impact Control):** Automatically sets the `Assignment Group` field to mandatory and `Urgency` field to read-only when `Impact` is set to '1 - High'.
- **onChange Client Script:** Auto-populates `Urgency` to High when `Impact` is changed to High.
- **onSubmit Client Script:** Validates that `Assigned To` is not empty when submitting a High-impact incident.
- **onCellEdit Client Script:** Restricts users from directly editing the `State` field from the Incident list view.

## Project Structure
- `docs/` : Contains detailed project documentation (PDF).
- `screenshots/` : Configuration and testing screenshots taken from the documentation.
- `scripts/` : Contains all ServiceNow Client Script JavaScript files.
- `xml/` : Contains exported ServiceNow Update Set (XML).

## How to Setup / Install in ServiceNow
1. Log in to your ServiceNow Developer Instance.
2. Navigate to **System Update Sets** -> **Retrieved Update Sets**.
3. Click **Import Update Set from XML** and upload the file from the `xml/` folder.
4. Open the imported Update Set, click **Preview Update Set**, and resolve any problems.
5. Click **Commit Update Set**.

## Testing
| Scenario | Steps | Expected Result |
|---|---|---|
| High impact UI Policy | Open an Incident, set Impact = 1 - High | Assignment Group becomes mandatory, Urgency becomes read-only |
| Auto-set urgency | Change Impact to 1 - High | Urgency is set to 1 - High and an info message appears |
| Prevent save | Set Impact = High, leave Assigned To empty, Submit | Error shown: "Assigned To is mandatory for High impact incidents." |
| Prevent list edit | In the Incident list, double-click the State cell | Alert shown and the edit is cancelled |

## Client Scripts
| File | Type | Field |
|---|---|---|
| `auto_set_urgency.js` | onChange | Impact |
| `prevent_save_assigned_to.js` | onSubmit | - |
| `prevent_list_edit_state.js` | onCellEdit | State |

## Demo Video
[Add your demo video link here]
