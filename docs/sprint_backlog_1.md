## Sprint Goal
"Implement the core of the application by allowing users to securely register and log in, manage the TV show catalog (create, edit, delete), and search for specific series by name in real time."

## Definition of Done (DoD)
For any Sprint Backlog item to be considered Done:

*   The code compiles without errors or severe linter warnings in Dart/Flutter.
*   The architecture (e.g., BLoC, Riverpod, or Provider) cleanly separates the UI from the Firebase logic.
*   Firebase Auth and Firestore security rules are configured so that only authenticated users can operate the catalog.
*   Searches respond in less than 1 second and properly handle empty states (when there are no matches).
*   Gherkin scenarios defined for the user stories have been executed and approved via manual or black-box testing.

---

## Sprint Backlog (Task Breakdown)

### EPIC 6 & 7: Registration and Login
**Included Stories:** US-06 (User Registration) and US-07 (User Login).

#### Task 1: Initial Project Setup & Firebase Infrastructure
*   **Subtasks:**
    *   Create the Flutter project and configure the layered or feature-first directory structure.
    *   Link the App in the Firebase Console (Android/iOS) and install `firebase_core` and `firebase_auth`.
*   **Dependencies:** None.
*   **Impediments:** Technical delays with Android SHA-1 keys or iOS development certificates.

#### Task 2: Authentication UI (Login and Registration)
*   **Subtasks:**
    *   Design login and registration screens using Material 3 components.
    *   Implement local form validations (empty fields, email format, matching passwords).
*   **Dependencies:** Task 1.
*   **Impediments:** None.

#### Task 3: Authentication Service with Firebase Auth
*   **Subtasks:**
    *   Create login and registration methods connecting with native Firebase functions.
    *   Map Firebase error codes (e.g., `email-already-in-use`, `invalid-credential`) to display user-friendly alerts.
*   **Dependencies:** Task 2.
*   **Impediments:** Temporary IP bans by Firebase if repetitive brute-force tests are performed.

---

### EPIC 1: TV Show Management (CRUD)
**Included Stories:** US-01 (TV Show Management).

#### Task 4: Data Modeling and Database (Cloud Firestore)
*   **Subtasks:**
    *   Define the `TvShow` entity and model in Dart (`id`, `name`, `synopsis`, `imageUrl`).
    *   Create the `series` collection in Firestore and configure access rules (Read/Write allowed only for active authenticated users).
*   **Dependencies:** Task 1.
*   **Impediments:** None.

#### Task 5: Main Catalog View (Read and Delete)
*   **Subtasks:**
    *   Implement the main screen that consumes the Firestore Stream in real time.
    *   Design the TV show cards and add a button/gesture to delete, including a confirmation dialog ("Are you sure?").
*   **Dependencies:** Task 4.
*   **Impediments:** Permission errors in Firestore rules when trying to execute the `delete` method.

#### Task 6: Form to Add and Edit TV Shows (Write and Update)
*   **Subtasks:**
    *   Create a reusable form to capture the TV show's name, synopsis, and image link.
    *   Program the logic so that if it receives an existing TV show, it populates the fields automatically in "Edit" mode.
    *   Integrate Firestore `add()` and `update()` services.
*   **Dependencies:** Task 5.
*   **Impediments:** Handling text overflow in the UI if the user inputs extremely long synopses.

---

### EPIC 2: TV Show Search
**Included Stories:** US-02 (TV Show Search).

#### Task 7: Search Bar in UI and Local/Remote Filtering
*   **Subtasks:**
    *   Integrate a search component (e.g., `SearchAnchor` or a dynamic `TextField`) at the top of the main catalog.
    *   **Technical Implementation:** Since Firestore lacks native advanced full-text search (like Algolia), implement filtering using range queries (`where('name', isGreaterThanOrEqualTo: query)`) or load the initial list and filter it locally on the client using Dart if the data volume is small and controlled.
    *   Design a visual "No results found" state if the search yields no matches.
*   **Dependencies:** Task 5 (A catalog and data to search must exist).
*   **Impediments:** Firestore limitations for partial searches (case-insensitive or intermediate substrings), which will require normalizing names by saving them in lowercase in a hidden field (e.g., `name_lowercase`).

---

## Sprint Workflow and Dependencies
To prevent developers from blocking each other, the recommended execution order is:

```text
[Task 1: General Configuration]
       │
       ├──► [Task 2 & 3: Full Authentication Flow (Epics 6 and 7)]
       │
       └──► [Task 4: Database] ──► [Task 5 & 6: Series CRUD (Epic 1)] ──► [Task 7: Search (Epic 2)]
