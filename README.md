# Science Centre Volunteer Desk

A responsive, browser-based **Volunteer Desk** single-page application for science centres. It streamlines volunteer check-in, check-out, asset tracking, roster management, and CSV import/export.

No backend, server, or database is required. The application runs entirely in the browser and saves its current data in `localStorage`.

## Features

### Check-in

- Search volunteers by name; only volunteers with **Scheduled** shifts are shown.
- QR-code scanning support for volunteer identification.
- Automatically handles volunteers with multiple shifts on different days.
- When a volunteer has more than one eligible shift, the app asks you to select the correct shift.
- Confirms the selected shift’s date, assignment, expected hours, and current status.
- Records the actual check-in date and time.
- Tracks issued assets:
  - Lanyard
  - Name tag
  - Meal voucher
  - T-shirt and size
  - Access card
  - Locker

### Check-out

- Search volunteers by name; only volunteers with **Checked In** shifts are shown.
- Supports multiple active shifts per volunteer.
- Requires return of issued assets before completing check-out.
- Tracks returned lanyards, T-shirts, access cards, and lockers.
- Records the actual check-out date and time.
- Updates inventory availability when assets are returned.

### Dashboard

- Displays a summary of:
  - Total unique volunteers
  - Checked-in shifts
  - Scheduled shifts
  - Completed shifts
- Provides a responsive volunteer roster:
  - Table view on desktop and larger screens
  - Card-based layout on mobile devices
- Shows shift date, assignment, scheduled hours, attendance, status, and assigned assets.
- Includes filters for:
  - Name, assignment, card, locker, and notes
  - Status
  - Assignment
  - Outstanding assets
- Allows sorting the roster by volunteer name.
- Opens a details editor for each individual shift record.

### Inventory management

The application tracks availability for:

- T-shirts by size: XS, S, M, L, XL, and 2XL
- Access cards
- Top and bottom lockers

Inventory is updated when assets are issued during check-in and returned during check-out.

### CSV import and export

- Import a volunteer roster from a CSV file.
- Export the current roster, including shift and asset details, to a CSV file.
- Supports multiple shifts for the same volunteer ID.
- Uses quote-aware CSV parsing to preserve notes and fields containing commas.

## Getting started

1. Download or clone this repository.
2. Open `index.html` in a modern web browser.
3. Start using the Volunteer Desk.

No installation, build step, or server is required.

```bash
# Optional: clone the repository
git clone <your-repository-url>
cd <repository-folder>

# Open the application
open index.html
```

On Windows, you can double-click `index.html` or open it directly in Chrome, Edge, Firefox, or Safari.

## CSV format

The application expects a CSV file with the following headers:

```csv
ID,Name,Assignment,Expected Time In,Actual Time In,Expected Time Out,Actual Time Out,Status,Lanyard Given,Lanyard Returned,Name Tag Given,Meal Voucher Given,Access Card Number,Access Card Returned,Locker Number,Locker Cleared,T-Shirt Size,T-Shirt Received,T-Shirt Returned,Gift Received,Notes
```

### Example

```csv
ID,Name,Assignment,Expected Time In,Actual Time In,Expected Time Out,Actual Time Out,Status,Lanyard Given,Lanyard Returned,Name Tag Given,Meal Voucher Given,Access Card Number,Access Card Returned,Locker Number,Locker Cleared,T-Shirt Size,T-Shirt Received,T-Shirt Returned,Gift Received,Notes
5AD07323-57E8-4C7D-9960-28EA56EF0F8E,Alex M.,The Lab,06/11/2026 08:00,,06/11/2026 12:00,,Scheduled,Yes,No,Yes,Yes,AC-001,No,L-01,No,M,Yes,No,No,Arrived early; orientation completed
5AD07323-57E8-4C7D-9960-28EA56EF0F8E,Alex M.,Kid's Playground,07/11/2026 08:00,,07/11/2026 12:00,,Scheduled,Yes,No,Yes,Yes,AC-002,No,L-02,No,S,Yes,No,No,Assigned to station lead
```

### Supported statuses

- `Scheduled`
- `Checked In`
- `Checked Out`
- `Absent`
- `Cancelled`

### Multiple shifts

A volunteer may have multiple rows in the CSV, with one row per shift. Use the same `ID` for the same volunteer, but provide a different `Expected Time In`, `Expected Time Out`, and/or `Assignment`.

For example, Alex M. can have both of the following shifts:

```csv
5AD07323-57E8-4C7D-9960-28EA56EF0F8E,Alex M.,The Lab,06/11/2026 08:00,,06/11/2026 12:00,,Scheduled,...
5AD07323-57E8-4C7D-9960-28EA56EF0F8E,Alex M.,Kid's Playground,07/11/2026 08:00,,07/11/2026 12:00,,Scheduled,...
```

The application will allow each shift to be checked in and checked out independently.

## Data storage

The application saves its current state in the browser’s `localStorage` under the key:

```text
scienceCentreVolunteerDesk.v12
```

This means that data remains available after refreshing the page, but it is stored only in the browser being used. Clearing browser data or using a different browser or device will not share the saved data.

To reset the application to its sample data, clear the site’s local storage or use the browser developer tools to remove the storage key above.

## QR scanning

QR-code scanning uses the browser camera through the `html5-qrcode` library.

- Camera access requires user permission.
- Scanning works best when the page is served over HTTPS.
- If camera access is unavailable, use the name search instead.

## Browser support

The application is designed for modern browsers, including:

- Google Chrome
- Microsoft Edge
- Mozilla Firefox
- Safari

## Project structure

```text
.
├── index.html
├── Volunteers.csv
└── README.md
```

## License

This project is provided for demonstration and internal operational use.
