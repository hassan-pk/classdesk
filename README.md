# ClassDesk

**Students organized. Fees accounted for.**

Offline student enrollment, classes, attendance, fee dues and staff expense records for small academies and tuition centres.

An offline Windows desktop pilot for one owner on one computer. Configure your own business; no default accounts, private shop data or seeded transactions are included. Version **0.1.0**.

## Screenshots

Captured from the desktop app with a fictional business and synthetic records only.

![Business overview](docs/screenshots/overview.png)

<details>
<summary>See the workspace, record, document preview and reports</summary>

![Business workspace](docs/screenshots/workspace.png)

![Record details](docs/screenshots/record.png)

![Document preview](docs/screenshots/document.png)

![Module reports](docs/screenshots/reports.png)

</details>

## Install

Download the Windows x64 installer from [Releases](https://github.com/hassan-pk/classdesk/releases), install, and create your local owner account. The installer is unsigned; Windows may show an unrecognized-publisher warning. Test on your computer and printer before using for real business.

Start by adding the master records (contacts, catalog or resources), then create your business transactions. Use **Open** to see record details, update progress, record payments or preview/print documents. See [BUSINESS.md](BUSINESS.md) for this application's workflow and limits.

## Modules

- **Teachers**: Teacher contact and subject records.
- **Classes**: Class sections, assigned teacher and timetable notes.
- **Students**: Student enrollment, guardian contact and assigned class.
- **Fee dues**: Create one monthly due per student and record initial and later fee receipts.
- **Attendance**: Record daily attendance for a student; one entry per student/date.
- **Teacher payments**: Record salary amounts paid; this is a spending record, not a customer collection.
- **Expenses**: Record business spending independently of customer receipts.

## Common capabilities

- Business identity, local password-protected owner account and password changes.
- Searchable records, status filtering, pagination and business-specific forms.
- Initial advances and later payments with cash/card/bank event history; overpayments are rejected.
- Offline image attachments where the business form supports them.
- A4 document preview and Windows printer dialog.
- Per-module financial summaries; supplier payments are not mixed with customer revenue.
- SQLite persistence, automatic local backups, validated export/restore and recovery copies. Other apps' backups are rejected.

## Data and backups

Data is saved outside the install folder at `%APPDATA%/ClassDesk/business.sqlite`. Uninstall preserves it. Automatic copies run at startup, hourly and on exit; the latest per UTC date is retained for 30 dates. Export copies to another drive regularly. Files/backups are not encrypted; use Windows and disk security to protect them.

Restore replaces records and accounts, saves a recovery copy and signs out. Use the password stored in the restored backup. Password recovery requires a known backup; there is no default password or reset backdoor. Export a backup before upgrades, and close the app before manual database operations.

## Build and test

Use Node.js 24+ and npm on Windows.

```powershell
git clone https://github.com/hassan-pk/classdesk.git
cd classdesk
npm ci
npm start
```

- `npm run build`: type-check and compile.
- `npm test`: isolated store, print and business-configuration regressions.
- `npm run test:desktop`: actual desktop workflow test with temporary records.
- `npm run dist`: Windows installer in `release/`.

No tests use your normal data directory. `BUSINESS_DATA_DIR` can explicitly select an isolated directory. Printing is checked as HTML and simulated native calls, not actual physical output.

## Pilot limits

- Monthly fee dues are created manually; no bulk auto-generation, late-fee engine or attendance-device integration.
- Class/teacher reference fees and salaries do not automatically populate or generate financial records.
- One class reference per student; multi-course enrollment and timetable conflict checking are not implemented.
- Fee-month keys are entered as YYYY-MM; consistent entry is required for monthly duplicate prevention.
- Fee statuses Due, Part-paid and Settled are calculated from actual receipts; this pilot has no late-fee or refund automation.
- No exam marksheets, certificates, guardian portal, online payments, payroll deductions or refunds.
- One owner account; no cashier role, networking or cloud sync in this pilot.
- No partial refunds or paid cancellation. Finished records are locked; settle outstanding balances through payments.
- Reports are lifetime operations summaries, not audited accounting or profit statements.
- Physical printing, second-computer installation and a real trading-day pilot still require verification.

## Source structure and license

`business.json` defines the application modules. `src/business.json` is its compiled source copy; keep both in sync when changing configuration. `src/main/` owns storage/security and native operations, `src/renderer/` owns the interface, and `src/shared/` contains typed models and printing. The shared implementation is included here so this repository builds independently.

MIT licensed; see [LICENSE](LICENSE). Dependencies retain their upstream licenses; Electron distributions include third-party notices. Use synthetic records when reporting issues; never attach private business databases.
