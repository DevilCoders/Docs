# ABC_PANEL_LINK_EXISTS

Requires a link to the panel to be present in the ABC service page.

## Rationale
Used by the automatic processes for providing information during an incident
Also it helps when you find a project in ABC to quickly jump to the project's infrastructure dashboard.

## Solution
You have to follow the following instructions:
1. Go to your ABC service page - `https://abc.yandex-team.ru/services/${service-slug}/`, just replace service-slug with you service's slug.
1. Hover your pointer over the "Contacts" section in the right side panel. An pencil icon should appear. Click on it.
1. In the pop-up window choose "Monitorings. Panels" for the type. Give it a name like "Main dashboard", and enter the URL of the dashboard.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/abc/monitoring-url.test.ts#L64-89)_
