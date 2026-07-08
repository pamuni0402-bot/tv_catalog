# Software Requirements Specification (SRS)
## Project: TV Catalog

---

## 1. Introduction
This document details the functional and non-functional requirements, as well as the technological stack for the development of the **TV Catalog** mobile application. The application is designed to allow users to explore, search, organize, and track their favorite television series, offering a smooth and interactive real-time experience.

---

## 2. Tech Stack

The application architecture will be based on a modern, cross-platform, and serverless solution, optimized for multimedia performance and constant data synchronization.

| Component | Technology | Rationale |
| :--- | :--- | :--- |
| **Mobile Frontend** | Dart / Flutter | Enables cross-platform development (iOS and Android) with a single codebase, guaranteeing fluid animations (60/120 fps) ideal for navigating visual catalogs. |
| **Database** | Firebase Cloud Firestore | NoSQL database that allows storing information about series, seasons, episodes, and user progress with instant synchronization. |
| **Authentication** | Firebase Authentication | Secure session management (Email, Google, Apple) so users can keep their favorites list synchronized across any device. |
| **Storage** | Firebase Cloud Storage | Optimized storage for user profile pictures and multimedia assets if required. |
| **Data Integration** | External API (Optional, e.g., TMDB) | REST service consumption to feed the catalog with thousands of updated series, connecting through Flutter (using `http` or `dio` packages). |

---

## 3. Functional Requirements (FR)

### FR01: User Management and Profiles
* **FR01.1:** The system must allow user registration and login via email/password and Google/Apple accounts.
* **FR01.2:** The system must allow users to customize their profile (name, photo, and favorite series genres).
* **FR01.3:** User customization data must be persistently stored in Firestore.

### FR02: Catalog and Series Exploration
* **FR02.1:** The application must display a main screen with organized sections: "Trending Series", "New Releases", "Most Popular", and "Recommended by Genre".
* **FR02.2:** The system must allow viewing the details of each series, including: synopsis, poster, release year, rating, cast, and a list of seasons/episodes.
* **FR02.3:** The system must allow the playback of series trailers (using embedded players in Flutter).

### FR03: Search Engine and Filters
* **FR03.1:** Users must be able to search for series by title in real time through a search bar.
* **FR03.2:** The system must offer advanced filters by genre, broadcast year, series status (Airing / Ended), and original streaming platform.

### FR04: Favorites Management and Tracking ("My List")
* **FR04.1:** Users must be able to mark series as "Favorites" or add them to a "Watchlist".
* **FR04.2:** The system must allow users to mark individual episodes as "Watched" to keep track of season progress.
* **FR04.3:** The watchlist and episode progress must automatically synchronize with the user's Firebase account.

### FR05: Push Notifications
* **FR05.1:** The system must send automatic push notifications (via Firebase Cloud Messaging) when a new episode of a series that the user has in their favorites list is released.

---

## 4. Non-Functional Requirements (NFR)

### NFR01: Performance and User Experience (UX)
* **NFR01.1:** The image catalog (posters and banners) must implement a lazy loading strategy and local image caching (using `cached_network_image` in Flutter) to avoid excessive mobile data consumption.
* **NFR01.2:** Navigation between screens and scrolling through series lists must maintain a constant frame rate of 60fps.

### NFR02: Security and Access Rules
* **NFR02.1:** Read and write access to favorite lists and viewing history in Firestore must be strictly restricted to the owner user via **Firebase Security Rules**.
* **NFR02.2:** External API keys (if used) must remain protected and not be exposed directly in public source code.

### NFR03: Availability and Offline Support
* **NFR03.1:** The application must allow access to "My List" and saved series progress even if the device has no internet connection, automatically syncing pending changes with Firestore as soon as connectivity is restored.

### NFR04: Compatibility
* **NFR04.1:** The mobile application must be fully responsive and compatible with Android smartphones (version 8.0 or later) and iOS devices (version 15 or later).

---

## 5. Project Structure (Flutter)

To ensure the scalability of **TV Catalog**, the frontend will be structured using a feature-oriented layered architecture (Feature-First) along with an efficient state manager (*Bloc* or *Riverpod*):

```text
lib/
│
├── core/                  # Global configurations, themes, router, and Firebase services
│
├── features/              # Application functionalities (Features)
│   ├── auth/              # User authentication
│   ├── catalog/           # Exploration, search, and series details
│   └── user_list/         # Favorites, history, and episode tracking
│
└── main.dart              # Application entry point
