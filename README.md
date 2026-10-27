# PRIVATE COUPLE LEDGER — SIMPLE REBUILD

Upload this project for the couple sign-in/dashboard. Do not upload it to the guest repository.

Test login email: eoseni31@gmail.com
Password: the exact test password you supplied in the conversation. It is stored only as a scrypt hash, not plaintext.

At the first database-backed request, the application creates the requested test account automatically, or sets that email's password once if it already exists. It links that account to its existing wedding or creates the Chioma & Henry wedding. The setup marker prevents resetting a changed password on later deployments. First setup revokes existing sessions for that test email. It refuses to take ownership of a Chioma & Henry wedding belonging to another account; such conflicts produce a clear error instead of silently exposing someone else's records.

This is a TEST account with a password already shared in conversation. Before storing real guest or financial information, sign in, open Wedding details, and change the password. That revokes all sessions and returns you to sign-in. There is no public self-registration, identity-provider integration, email verification or email password recovery in this rebuild.

Additional environment variable in the COUPLE Vercel project:
GUEST_SITE_ORIGIN = the exact guest website origin, for example your real https://...vercel.app address with no trailing slash.

The dashboard now includes a Create guest link form. Enter the guest name and total party allowance, then share the generated personal link privately. Its invitation record belongs to the signed-in couple's wedding. No terminal or SQL console is needed to generate invitations.

The ledger refreshes records in the background every 15 seconds while the tab is visible. Refresh records is also available manually. A database failure is reported instead of showing fake data.

## Upload: no subfolders required

All deliverable files are at the top level. The HTML, photos, fonts, videos, styles and JavaScript are embedded in server.js. There is no scripts/check.js, views folder or api folder to lose during upload.

1. Extract this ZIP and open its project folder.
2. Upload ALL files inside it to the corresponding GitHub repository. Do not upload the ZIP itself or the enclosing folder. You can now use GitHub's file picker because the project has no nested directories.
3. Keep the guest and couple repositories separate. In the Vercel project, set the framework preset to Express, install command npm ci, build command npm run build, Node 24, and remove any old public/dist Output Directory override. Leave the Root Directory at the repository root.
4. Do not mix the old files/folders with this new package. Prefer a new branch or repository for review, and replace the source in the appropriate Vercel project only when you choose to deploy. The current deliverable does not deploy itself or change your live database from this workspace.

## Database connection

Turso URL is already configured in server code as the default:
libsql://safiyahs-weddings-ella3638.aws-ap-south-1.turso.io

TURSO_AUTH_TOKEN must be set privately in Vercel's Environment Variables on BOTH projects. If already configured on the same Vercel projects, keep it there; do not put it in GitHub. The server cannot connect without a valid token. TURSO_DATABASE_URL can optionally override the default URL. Both projects must use the same database.

APP_ORIGIN should be the exact HTTPS origin of that website, without a trailing slash. If absent, the app uses Vercel's production-domain variable, then VERCEL_URL. Set APP_ORIGIN explicitly for custom domains and exact preview origins. Do not change your browser's Origin headers or add wildcard CORS rules.

The application automatically creates missing prefixed SGW tables/indexes when a database-backed API is first used. There is no manual SQL setup file to run. This is an intentional change from the earlier packages. It does not delete guest data or reassign wedding ownership. Review/back up an existing database before allowing automatic setup in production. Existing unrelated database schemas are not automatically imported.

## Payments and remaining services

The supplied Paystack link is included for monetary gifts and item contributions: https://paystack.shop/pay/bgtkmsmy8c. A contribution funds an item; it does not order or deliver it. The existing reservation flow is retained.

Automatic Paystack payment verification has NOT been implemented. A guest's notification remains unverified, not paid. Actual Paystack API/webhook integration and a secure transaction-to-wedding mapping are still required for automatic confirmed-payment syncing. No live payment or payout routing was tested or altered.

The original sample bank details remain sample details. Photo uploads, livestream, asoebi contact and external logistics are still unconfigured where they were unconfigured originally.

## Checks and limits

Run npm ci, npm run build and npm test locally. The build checks the server syntax. Tests use isolated local SQL storage, not your remote Turso database. Further checks exercised both websites against the same database with separate connections, automatic account setup, guest-link creation, RSVP/gift persistence, record isolation, logout and password-change persistence after a cold restart. Browser scripts were parsed and the guest page was compared byte-for-byte with the previous invitation.

No live Turso connection, deployed Vercel build or browser visual QA was verified here. Build success alone does not prove that your deployed environment variables, database permissions or production domain settings are correct.
