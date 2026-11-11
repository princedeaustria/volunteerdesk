# Science Centre Volunteer Desk

A responsive, browser-based **Volunteer Desk** single-page application for a science centre. It streamlines volunteer check-in, check-out, asset issuance and return, roster management, and CSV import/export.

The application is built with **HTML, JavaScript, and Tailwind CSS** and stores data locally in the browser using `localStorage`. No backend, database, or installation is required.

## Features

### Home

The home screen provides three primary actions:

- **Check-in** — register a volunteer’s arrival and issue assets
- **Check-out** — return assets, distribute gifts, and complete the shift
- **Dashboard** — review the roster, attendance, assets, and inventory

### Check-in workflow

The check-in process is a guided, step-by-step workflow:

1. Find the volunteer by scanning or entering their ID, or searching by name.
2. Review the volunteer’s shift assignment and expected time in/out.
3. Check in the volunteer and record the actual arrival time.
4. Issue and track volunteer assets.
5. Add handover or special-instruction notes.
6. Complete check-in and return to Home.

If a volunteer cannot be found, the application displays a clear “Volunteer not found” message. Volunteers who are already checked in cannot be checked in again.

### Asset management

During check-in, the following assets can be issued:

| Asset | Required | Tracked |
|---|---:|---|
| Lanyard | Yes | `Lanyard Given`, `Lanyard Returned` |
| Name tag | Yes | `Name Tag Given` |
| Meal voucher | Yes | `Meal Voucher Given` |
| T-shirt | Yes | `T-Shirt Size`, `T-Shirt Received`, `T-Shirt Returned` |
| Access card | Optional | `Access Card Number`, `Access Card Returned` |
| Locker | Optional | `Locker Number`, `Locker Cleared` |

#### T-shirt inventory

T-shirt sizes and available quantities are maintained in the application inventory. When a T-shirt is issued, the available quantity for that size decreases. When it is returned during check-out, the quantity increases again.

Supported sizes:

- XS
- S
- M
- L
- XL
- 2XL

#### Access cards

Access cards are uniquely assigned. A card cannot be assigned to another volunteer until it has been returned and marked as available.

#### Lockers

Volunteers may optionally be assigned a locker. The application supports locker preference and availability tracking.

Available lockers:

- **Top lockers:** 21, 23, 25, 27, 29, 31, 33, 35, 37, 39
- **Bottom lockers:** 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40

When a locker is released during check-out, it becomes available for another volunteer.

## Check-out workflow

The check-out process includes:

1. Find the volunteer by ID or name.
2. Confirm that the volunteer is currently checked in.
3. Review the shift assignment, expected time in/out, and actual time in.
4. Return applicable assets.
5. Record that the volunteer received a gift.
6. Add check-out notes.
7. Complete check-out and record the actual time out.

A volunteer cannot be checked out unless they are currently in a **Checked In** status.

### Asset returns

| Asset | Return required | Behaviour |
|---|---:|---|
| Lanyard | Yes | Must be returned if it was issued |
| Name tag | No | Not shown during check-out |
| Meal voucher | No | Not shown during check-out |
| T-shirt | Optional | Can be returned; inventory is updated |
| Access card | Yes | Must be returned if it was issued |
| Locker | Yes | Must be released if it was assigned |
| Gift | Yes | Must be marked as handed to the volunteer |

## Dashboard

The Dashboard provides an operational view of volunteer activity and asset status.

### Summary cards

- Total volunteers
- Checked-in volunteers
- Scheduled shifts
- Completed shifts

### Roster table

The roster displays:

- Volunteer name
- Assignment
- Scheduled hours
- Actual attendance
- Status
- Assets at a glance
- Link to volunteer details

### Search and filters

You can search across:

- Volunteer name
- Volunteer ID
- Assignment
- Access card number
- Locker number
- Notes
- Other record details

Filters can be combined to narrow the roster:

- Volunteer status
- Assignment
- Outstanding assets

The **Outstanding assets** filter shows volunteers with any of the following:

- Lanyard not returned
- T-shirt not returned
- Access card not returned
- Locker not cleared

A single **Clear filters** button resets all search and filter fields.

### Volunteer details

The Volunteer Details dialog allows staff to edit and review:

- Volunteer name
- Assignment
- Lanyard status
- Name tag status
- Meal voucher status
- T-shirt size
- T-shirt received status
- T-shirt returned status
- Access card assignment
- Locker assignment
- Gift distribution
- Notes for handovers and special instructions

## CSV support

The application supports both CSV import and export.

### Export

Click **Export CSV** on the Dashboard to download the current volunteer roster as `volunteers.csv`.

### Import

Click **Import CSV** to load a CSV file into the application. The imported data replaces the current volunteer roster and is saved in browser storage.

### CSV columns

The application uses the following columns:

```text
ID
Name
Assignment
Expected Time In
Actual Time In
Expected Time Out
Actual Time Out
Status
Lanyard Given
Lanyard Returned
Name Tag Given
Meal Voucher Given
Access Card Number
Access Card Returned
Locker Number
Locker Cleared
T-Shirt Size
T-Shirt Received
T-Shirt Returned
Gift Received
Notes
```

## Sample CSV

Save the following as `Volunteers-Volunteers.csv`:

```csv
ID,Name,Assignment,Expected Time In,Actual Time In,Expected Time Out,Actual Time Out,Status,Lanyard Given,Lanyard Returned,Name Tag Given,Meal Voucher Given,Access Card Number,Access Card Returned,Locker Number,Locker Cleared,T-Shirt Size,T-Shirt Received,T-Shirt Returned,Gift Received,Notes
1,Alex M.,Steven's Lab,8:00,7:55,12:00,—,Checked In,Yes,No,Yes,Yes,AC-001,No,L-01,No,M,Yes,No,No,Arrived early; orientation completed
2,Jamie C.,CKM,8:00,8:03,12:00,—,Checked In,Yes,No,Yes,Yes,AC-002,No,L-02,No,S,Yes,No,No,Assigned to station lead
3,Taylor B.,Front of the House,8:00,7:58,12:00,—,Checked In,Yes,No,Yes,Yes,AC-003,No,L-03,No,L,Yes,No,No,Supporting guest welcome and directions
4,Jordan P.,Registration,7:00,6:55,9:00,9:05,Checked Out,Yes,Yes,Yes,Yes,AC-004,Yes,L-04,Yes,M,Yes,Yes,Yes,Shift completed; handover finished
5,Casey N.,Event Setup,7:00,—,9:00,—,Absent,No,—,No,No,—,—,—,—,—,XL,No,No,No,Did not attend; coordinator notified
6,Riley T.,Eatery,8:00,—,12:00,—,Cancelled,No,—,No,No,—,—,—,—,—,S,No,No,No,Cancelled before shift; replacement requested
7,Morgan L.,Steven's Lab,10:00,—,14:00,—,Scheduled,No,—,No,No,—,—,—,—,—,M,No,No,No,Assist with activity preparation
8,Avery W.,CKM,10:00,—,14:00,—,Scheduled,No,—,No,No,—,—,—,—,—,L,No,No,No,Report to station lead on arrival
9,Quinn G.,Front of the House,10:00,—,14:00,—,Scheduled,No,—,No,No,—,—,—,—,—,XS,No,No,No,Support guest arrivals and wayfinding
10,Cameron D.,Registration,10:00,—,14:00,—,Scheduled,No,—,No,No,—,—,—,—,—,XL,No,No,No,Assist with attendee check-in
11,Reese M.,Volunteer Support,11:00,—,15:00,—,Scheduled,No,—,No,No,—,—,—,—,—,M,No,No,No,Provide break coverage
12,Skyler A.,Eatery,11:00,—,15:00,—,Scheduled,No,—,No,No,—,—,—,—,—,S,No,No,No,Assist with serving and restocking
13,Parker L.,Steven's Lab,12:00,—,16:00,—,Scheduled,No,—,No,No,—,—,—,—,—,L,No,No,No,Afternoon shift; receive handover
14,Rowan C.,CKM,12:00,—,16:00,—,Scheduled,No,—,No,No,—,—,—,—,—,M,No,No,No,Afternoon station support
15,Emerson H.,Front of the House,12:00,—,16:00,—,Scheduled,No,—,No,No,—,—,—,—,—,2XL,No,No,No,Support guest departures and directions
16,Finley Y.,Event Cleanup,14:00,—,18:00,—,Scheduled,No,—,No,No,—,—,—,—,—,L,No,No,No,Assist with packing and cleanup
17,Dakota K.,Volunteer Support,14:00,—,18:00,—,Scheduled,No,—,No,No,—,—,—,—,—,S,No,No,No,Support closing tasks and equipment returns
```

## Getting started

### Run locally

1. Download or clone this repository.
2. Open `index.html` in a modern web browser.
3. Use the Home screen to begin a check-in, check-out, or open the Dashboard.

No build step, server, or database is required.

### Project structure

```text
.
├── index.html
├── Volunteers-Volunteers.csv
└── README.md
```

## Browser storage

The application saves volunteer records, asset assignments, and inventory changes in the browser using `localStorage`.

Data remains available after refreshing or closing the browser, provided the same browser and browser profile are used.

To reset the application to its sample data, clear the site’s local storage or use the browser developer tools to remove the `scienceCentreVolunteerDesk.v5` key.

## Technology

- HTML5
- CSS3
- JavaScript
- Tailwind CSS
- Browser `localStorage`
- CSV import/export

## Intended use

This application is designed for front-desk volunteers, volunteer coordinators, and event staff who need a simple, reliable way to manage:

- Volunteer arrivals and departures
- Shift assignments
- Physical asset distribution
- Asset returns
- Locker and access-card control
- Roster visibility
- CSV-based record keeping

## License

This project is provided for internal science-centre volunteer operations. Add your preferred license before publishing publicly.
