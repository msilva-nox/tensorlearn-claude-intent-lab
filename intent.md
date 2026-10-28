# Intent: Results-ready notification

Sources: `inputs/01-approved-prd.md` (PRD N-17, approved 2026-09-18), `inputs/02-current-meeting.md` (discovery notes, 2026-09-20). `inputs/03-superseded-request.md` is superseded history and approves nothing here.

## Problem

- **I-1** The fictional clinic receives avoidable calls from patients checking whether their results are ready (PRD N-17).
- **I-2** Patients have no prompt signal that a result is ready for their review, so they phone the clinic to ask.

## Proposed outcome

- **I-3** The patient is notified when a result is ready for their review in the existing authenticated portal.
- **I-4** "Ready" means a doctor has reviewed and released the result. A finished laboratory upload alone is not "ready" and never makes a notification eligible.
- **I-5** The notification only says that an update is available and directs the patient to the existing authenticated portal.
- **I-6** Success will be observed by:
  - a reduction in results-status calls, counted separately from clinical questions and compared against a measured baseline;
  - the number of delivery failures.
- **I-7** The baseline and any numerical target will be agreed during discovery. No target is approved, so none is set here.

## Affected users and systems

- **I-8** Patients, who receive the notification and view results in the portal.
- **I-9** Doctors, who review and release results before any notification is eligible.
- **I-10** Clinic support staff, who take the status calls and report the baseline.
- **I-11** The existing authenticated portal and its existing result route.
- **I-12** The patient is the only approved recipient. Any other recipient is not approved.

## Out of scope

- **I-13** Portal redesign.
- **I-14** Appointment scheduling.
- **I-15** Clinical interpretation.
- **I-16** Notifying third parties. Notifying the referring doctor is not approved and is tracked only as OPEN-2.
- **I-17** A new patient dashboard, which is a separate project.
- **I-18** Everything in the superseded early request: sending every result as soon as the lab uploads it, putting the test result in an SMS, copying the referring doctor, rebuilding the dashboard, and the 90% call-reduction aim.

## Constraints

- **I-19** A doctor must review and release the result before any notification is eligible.
- **I-20** The message and the notification logs must not contain any diagnosis, test result, clinical measurement or treatment detail.
- **I-21** Access is authenticated in the existing portal. Results are never attached, and there is no public result link.
- **I-22** No duplicate notification is sent for the same released result version.
- **I-23** Delivery failures are handled without sending duplicate patient messages.
- **I-24** No sensitive content appears in messages or operational logs (privacy owner).

## Open questions

- **OPEN-1 Channel.** SMS, email or portal push is undecided. Owners: product owner and privacy owner, after the consent and delivery review. Nothing in this intent assumes a channel.
- **OPEN-2 Referring-doctor notification.** Whether and how the referring doctor is notified is undecided. Owners: clinical owner and privacy owner, who must decide recipient authorization. Approval must not be inferred from the old request.
- **OPEN-3 Baseline and target.** The baseline and any numeric target are to be agreed during discovery. Support lead and product owner are named in the sources for measurement and the PRD, but the PRD names no formal owner for this item.

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
