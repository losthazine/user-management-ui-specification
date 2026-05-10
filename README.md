# User Management UI Specification

## UI Specification: User Management Screen
### 1. Overview
The User Management Screen utilizes a classic Master-Detail layout. It allows administrators to view a list of system users, filter and sort the user list, create new users, and edit existing user details.

### 2. Initial State (Page Load)
+ Data Grid: Populated with the current list of users fetched from the database.

+ "Hide Disabled User" Checkbox: Checked by default. The grid should only display active/enabled users upon initial load.

+ Form Panel: Empty and disabled, or displaying a prompt to "Select a user or create a new one."

+ Action Buttons: "+ New User" is enabled. "Save User" is disabled until a form is active and modified.

### 3. UI Components & Behavior

##### 3.1 Top Action Bar
+ + New User Button

    + Type: Primary Button.

    + Behavior: Clicking this button clears the "User Details Form" on the right, sets the form title to "New User", and focuses the cursor on the "Username" field. Deselects any currently highlighted row in the User Grid.

+ Hide Disabled User Checkbox

    + Type: Checkbox control.

    + Default: Checked.

    + Behavior: When checked, the User Grid filters out any user where Enabled is false. When unchecked, all users (both enabled and disabled) are displayed in the grid.

+ Save User Button

    + Type: Primary/Action Button (Aligned Right).

    + Behavior: Submits the data currently populated in the "User Details Form". It should be disabled unless the form is dirty (data has been entered or changed) and all required validation rules are met.

##### 3.2 Master View: User Data Grid
+ Type: Interactive Data Table.

+ Columns: * ID (Numeric)

    + User Name (Alphanumeric)

    + Email (Alphanumeric)

    + Enabled (Boolean: true/false)

+ Column Features: Every column header includes contextual controls for Sorting (Up/Down carets) and Filtering (Funnel icon).

    + Sorting: Clicking the sort arrows toggles between ascending, descending, and default sorting for that specific column.

    + Filtering: Clicking the filter icon opens a small contextual popover to enter filter criteria (e.g., text match for names/emails, boolean toggle for Enabled).

+ Row Interaction (Selection): Clicking a row highlights it (e.g., light blue background) and populates the User Details Form on the right with that user's data.

##### 3.3 Detail View: User Form Panel
+ Title: Dynamic. Displays "New User" when creating a record, or "Edit User" (or the specific Username) when a grid row is selected.

+ Form Fields:

    + Username: Text input. (Required, Alphanumeric, unique).

    + Display Name: Text input. (Required).

    + Phone: Text input. (Optional, numeric/symbol formatting allowed).

    + Email: Text input. (Required, must pass standard email regex validation).

    + User Roles: Multi-select dropdown menu.

        + Options: Guest, Admin, SuperAdmin.

        + Behavior: Clicking the input opens the dropdown. Multiple roles can be selected. Selected roles should appear as tokens/chips in the input box or as a comma-separated list.

    + Enabled: Checkbox. Determines if the user account is active.

### 4. Key Workflows
##### 4.1 Creating a New User
1. User clicks "+ New User".

2. Form clears and title updates to "New User".

3. User fills out mandatory fields (Username, Display Name, Email, Role).

4. User clicks "Save User".

5. System: Validates input. If successful, saves to backend, displays a success toast/message, adds the new user to the Data Grid, and highlights the newly created row.

##### 4.2 Editing an Existing User
1. User clicks a row in the Data Grid (e.g., ID 1, AdminUser).

2. The row becomes highlighted.

3. The form populates with AdminUser's data.

4. User modifies a field (e.g., changes Phone number).

5. "Save User" button becomes active.

6. User clicks "Save User".

7. System: Validates input, saves changes to backend, displays a success message, and refreshes the Data Grid to reflect updated values.
