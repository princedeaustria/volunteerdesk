# Volunteer Desk

### A simpler way to manage volunteers, shifts, and event-day check-ins.

Volunteer Desk is a responsive, browser-based dashboard for coordinating volunteer attendance, assignments, and equipment. Built with HTML, Tailwind CSS, and vanilla JavaScript, it brings essential event-day information into one workspace.

Search the roster, record arrivals and departures, update volunteer details, and export filtered records—without setting up a backend.

## Features

### Dashboard & Roster
- View summary cards for total volunteers, checked-in volunteers, scheduled shifts, and completed shifts.
- Review assignments, scheduled hours, actual attendance, status, and equipment at a glance.
- Sort volunteers by name.
- Start with 17 prepopulated sample records.

### Search & Filters
- Search across names, assignments, access cards, lockers, notes, and other record details.
- Filter by volunteer status or assignment.
- Show only volunteers with outstanding access cards or uncleared lockers.
- Combine search and filters to narrow the roster.
- Clear all filters with one click.

### Check-In & Check-Out
- Check in scheduled volunteers and record their arrival time.
- Check out active volunteers and record their departure time.
- Review and adjust attendance details in the volunteer editor.
- Display times in 24-hour format.

### Volunteer Details
- Edit volunteer information in a dedicated dialog.
- Track access card assignments and returns.
- Track locker assignments and clearance.
- Record T-shirt sizes, T-shirt distribution, and gift distribution.
- Maintain notes for handovers and special instructions.

### Local Storage & Export
- Save changes in the current browser using localStorage.
- Export the currently filtered roster as CSV.
- Restore the original sample data when needed.

## Technology Stack

| Technology | Purpose |
| --- | --- |
| HTML5 | Page structure and forms |
| Tailwind CSS | Responsive layout and styling |
| Vanilla JavaScript | Search, filtering, editing, and attendance actions |
| Browser localStorage | Local persistence |
| Blob and URL APIs | Downloadable CSV exports |

No JavaScript framework, package installation, or build step is required.

## Getting Started

### Requirements

- A modern web browser.
- An internet connection to load Tailwind CSS from its CDN.

### Run Locally

1. Clone the repository:

   ```bash
   git clone https://github.com/princedeaustria/volunteer-desk.git
   cd volunteer-desk
   ```

2. Open the HTML file in your browser.

   If using the original generated file, open:

   ```text
   volunteer-desk.html
   ```

3. Begin searching, filtering, or updating volunteer records.

> If your repository uses a different name, update the clone URL accordingly.

## How to Use

### Find a Volunteer

Enter a name, assignment, card number, locker number, or keyword in the search field.

Use the status and assignment filters to narrow the results further.

### Check In a Volunteer

1. Find a volunteer with the `Scheduled` status.
2. Select `Check in`.
3. The status changes to `Checked In`, and the current local time is recorded as the actual time in.

### Check Out a Volunteer

1. Find a volunteer with the `Checked In` status.
2. Select `Check out` and confirm.
3. The status changes to `Checked Out`, and the current local time is recorded as the actual time out.
4. Review the details dialog to confirm equipment returns and other outstanding items.

> Checking out does not automatically mark an access card as returned or a locker as cleared.

### Edit Volunteer Details

1. Select a volunteer’s name or `View details`.
2. Update the relevant fields.
3. Select `Save changes`.

### Export Records

1. Apply any search terms or filters.
2. Select `Export filtered CSV`.
3. The downloaded file contains all fields for the matching volunteers.

Clear filters before exporting if you want the full roster.

### Reset Sample Data

Select `Reset sample data` and confirm to restore the original records.

This replaces changes saved in the current browser.

## Volunteer Record Fields

| Category | Fields |
| --- | --- |
| Identification | ID, Name |
| Assignment | Assignment |
| Shift Schedule | Expected Time In, Expected Time Out |
| Attendance | Actual Time In, Actual Time Out, Status |
| Access Cards | Access Card Number, Access Card Returned |
| Lockers | Locker Number, Locker Cleared |
| Merchandise | T-Shirt Size, T-Shirt Received, Gift Received |
| Additional Information | Notes |

A dash (`—`) represents a value that is not recorded or not applicable.

## Statuses

| Status | Meaning |
| --- | --- |
| Scheduled | Assigned to a shift and awaiting check-in |
| Checked In | Arrival recorded; currently on shift |
| Checked Out | Departure recorded; shift completed |
| Absent | Did not attend the scheduled shift |
| Cancelled | Participation or shift was cancelled |

## Equipment Tracking

The outstanding-equipment filter includes volunteers who have either:
