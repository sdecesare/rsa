# Research Support Allowance — applicant prototype

Applicant-only variant of the existing RSA prototype. Existing reviewer/committee screens and source files are untouched in the sibling `rsa-app/` directory.

Serve `dist/` with any static HTTP server. Run `npm test` for application-schema, calculation, flat-file, CSV, and ranking tests. No build step is required: the citation formatter bundle and its attribution files are reused from Publication Studio.

## Applicant flow

1. Enter details and choose allowance hours; combined PI/CI bids are capped at 120 hours, as in the existing prototype.
2. Import public ORCID works, upload BibTeX, look up a DOI, or add manual references. Only selected imports enter the application. Exact DOI duplicates are skipped.
3. Record pipeline, REF outputs, income, supervision, and conferences. REF outputs can reuse selected publication references. REF ratings are entered by the applicant; journal rankings are not treated as REF output ratings.
4. Enter plans, culture/esteem, and impact.
5. Review, confirm the declaration, and download the complete JSON application file. CSV export contains one application row with multiline evidence fields for spreadsheet viewing. Print output includes all sections.

## Storage

- Draft auto-save uses browser localStorage.
- **Save application file** downloads an editable JSON snapshot at any time.
- **Open application file** restores a JSON file saved by this app.
- **Finish & save** validates basic details and exports `Ready for review`. It is not an online submission.
- CSV values that could be interpreted as formulas are prefixed for safe spreadsheet viewing.
- There is no central submission endpoint, shared spreadsheet, authentication, or reviewer interface. Users share files using their agreed university process. Do not treat browser draft storage as a shared university record.

## Data

Allowance values and reference periods are carried over from the existing 2026/27 prototype, not newly verified policy. Existing user-supplied AJG 2024 and SJR data are reused without fetching new ranking data. Hosted access is private by default. ORCID and Crossref terms and quotas apply. BibTeX import does not send file content to these services.

## Browser-only Excel export

Finish & download Excel creates a real `.xlsx` workbook locally using the bundled ExcelJS 4.4.0 library (MIT license in dist/vendor). Nine sheets cover application details and totals, publications, submissions, work in progress, REF outputs, income and bids, conferences, culture and esteem, and statements. Long values use numbered continuation rows. User text is stored as text, never as formulas.

Save draft JSON downloads the editable application. Open application file restores it. Device draft saving is off by default; enabling it uses localStorage on that device. Disabling removes that local draft. Without device saving, closing/reloading loses edits unless a JSON copy was downloaded. Existing saved drafts can be restored explicitly.

There is no application submission API, database, analytics, or remote application storage. ORCID and Crossref requests disclose the queried identifiers to those services. GitHub Pages (or another static host) serves the app files and receives normal page requests. Applicants upload the downloaded workbook separately through the university process.

## GitHub Pages

Upload this package's contents to a separate repository for the applicant app, including the hidden `.github` directory. In repository Settings → Pages choose GitHub Actions. The included workflow tests the app and publishes `dist/`; no backend or build is required. Local preview: `python3 -m http.server 8000 --directory dist`.

The supplied rankings dataset is included as in the existing prototype. Check your permission to redistribute it before making the repository public.
