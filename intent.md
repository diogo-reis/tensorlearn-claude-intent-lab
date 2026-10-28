# Intent

## Problem
(I-1) The clinic receives avoidable calls from patients asking whether their lab results are ready. (Source: 01-approved-prd.md — "The fictional clinic receives avoidable calls from patients checking whether results are ready.")

## Proposed outcome
(I-2) Notify the patient when a result is ready for their review in the existing authenticated portal. "Ready" means a doctor has reviewed and released the result — not merely that the lab finished uploading it. (01-approved-prd.md: "A doctor must review and release the result before any notification is eligible."; 02-current-meeting.md: "'Ready' must not mean that the laboratory upload merely finished.")

(I-3) Success will be observed as a reduction in status-only calls (calls asking only whether a result is ready, counted separately from clinical-question calls) and a reduction in delivery failures for the notification itself. (01: "Measure reduction in results-status calls and delivery failures."; 02: "count status-only calls separately from clinical questions; compare against a measured baseline.") No baseline or numeric target is approved yet — one will be agreed during discovery (01: "The baseline and numerical target will be agreed during discovery; none is approved yet.").

## Affected users and systems
(I-4) Patients receive the notification and check results in the existing authenticated portal. A doctor must review and release each result before any notification is sent. Support staff should see fewer status-only calls. Product and privacy owners decide the notification channel; clinical and privacy owners decide referring-doctor notification. Engineering builds against the existing portal result route only — no new dashboard (02-current-meeting.md: "the existing portal path is adequate. A new patient dashboard is a separate project.").

## Out of scope
(I-5) Portal redesign, a new patient dashboard, appointment scheduling, and clinical interpretation are out of scope. (01-approved-prd.md: "Portal redesign, appointment scheduling, clinical interpretation and notifying third parties are outside this approved scope.") Notifying third parties generally is out of scope; the referring-doctor case specifically is neither approved nor excluded and is tracked as an open question below, not decided by this intent.

## Constraints
(I-6) A doctor must review and release a result before any notification is eligible. (01-approved-prd.md)
(I-7) The message may only state that an update is available and direct the patient to the existing authenticated portal — no diagnosis, test result, clinical measurement, or treatment detail in the message or in notification logs. (01-approved-prd.md)
(I-8) Access is authenticated through the existing portal; do not attach results or introduce a public result link. (01-approved-prd.md)
(I-9) Avoid duplicate notifications for the same released result version, and handle delivery failures without sending duplicate patient messages. (01-approved-prd.md)

## Open questions
(OPEN-1) Channel (SMS, email, or portal push) — owners: product, privacy. To be decided after consent and delivery review. (01-approved-prd.md)
(OPEN-2) Referring-doctor notification — owners: clinical, privacy. Recipient authorization is not approved by the PRD and must not be inferred from the superseded early request. (01-approved-prd.md; 02-current-meeting.md: "do not infer approval for referring-doctor notifications from the old request.")

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
