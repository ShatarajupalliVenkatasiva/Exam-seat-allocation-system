# Exam Seating Allocation System

A comprehensive web application built to automate and optimize the process of allocating students to examination rooms. This system allows administrators to manage classrooms, students, and exams, and then uses a custom algorithm to distribute students into available seats based on configurable rules.

## Detailed Description
The Exam Seating Allocation System is designed to alleviate the manual effort of creating exam seating arrangements. It provides an intuitive interface for:
- **Classroom Management:** Define rooms, grid dimensions (rows x columns), and specify blocked or unusable seats.
- **Student Management:** Add students individually or import them in bulk.
- **Exam Management:** Schedule exams and link them to students.
- **Smart Allocation:** Automatically distribute students across classrooms according to specific rules, such as randomizing seat assignments, avoiding placing students from the same department next to each other, and balancing distribution across multiple rooms.
- **Reporting & Exporting:** View detailed seating grids and export seating plans as PDF or Excel files.

## Tech Stack
- **Framework:** Next.js (App Router)
- **Library:** React (v19)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **State Management:** React Context API
- **Icons:** Lucide React
- **Utilities:**
  - `xlsx` for parsing and exporting Excel files
  - `jspdf` & `jspdf-autotable` for generating PDF reports
  - `date-fns` for date formatting

## Program Structure
The project is built using the Next.js App Router paradigm, with the source code residing in the `src/` directory.

```
src/
├── app/                  # Next.js App Router entry points (layout, page, globals.css)
├── components/           # Reusable UI components
│   ├── Sidebar.tsx       # Main navigation sidebar
│   ├── TopHeader.tsx     # Top navigation header
│   └── views/            # Main application views/pages (Dashboard, Classrooms, Students, etc.)
├── lib/                  # Core business logic and utilities
│   ├── allocationAlgorithm.ts # Custom logic for distributing students into seats
│   └── parseFile.ts      # Utility for parsing imported Excel/CSV data
├── store/                # Global State Management
│   └── AppContext.tsx    # React Context provider holding app state (students, classrooms, exams)
└── types/                # TypeScript interfaces and type definitions
    └── index.ts          
```

## Implementation Flow
1. **Data Ingestion:** The administrator inputs or imports the basic entities: `Classrooms` (with seating capacity and blocked seats) and `Students` (including their departments).
2. **Exam Creation:** An exam is scheduled in the system.
3. **Allocation Process:**
   - The user selects the exam and triggers the allocation process.
   - The system calls `generateAllocation()` from `src/lib/allocationAlgorithm.ts`.
   - The algorithm processes the active rules:
     - **Rule 2 (Randomize):** Shuffles the student list.
     - **Rule 1 (Separate Same Department):** Interleaves students from different departments so they do not sit sequentially.
     - **Rule 4 (Distribute Evenly):** Distributes students across all available classrooms in a round-robin fashion, or fills rooms sequentially if this rule is disabled.
4. **Grid Mapping:** The algorithm maps students into 2D classroom grids (Rows x Columns), skipping blocked seats.
5. **Visualization & Reporting:** The results are saved in the global state and can be reviewed in the `ResultsView`. The `ReportsView` allows the admin to download the seating plan for offline use.

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the application.

You can start editing the main layout and pages by modifying files in `src/app/` or the views in `src/components/views/`. The page auto-updates as you edit the files.

## Learn More
To learn more about Next.js, take a look at the following resources:
- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.
