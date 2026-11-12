# Community noticeboard

A noticeboard for one neighbourhood. Neighbours post what is happening
locally and reply underneath. Anybody can report a notice they think
should not be there, and it stays up until a person has looked at it.

The moderators are neighbours too. A moderator is a member who can
decide whether a reported notice stays up or comes down. They post,
they reply, and they fall out with people. Then they are asked to
decide whether one of those people's notices should stay up. That is
the hard part of this product, and being careful does not make it go
away. Every decision is a judgement somebody will disagree with. So
the job is to make each decision open to review, not to pretend it was
automatic.

## What finished looks like

Anyone can open the app and:

- join under a name their neighbours can see
- post a notice that the street can read within a minute
- reply to a notice, or to somebody else's reply
- report a notice or a reply, which stays up while a moderator looks

A moderator works through the reports and decides. They write down why,
and the author is shown that reason. A moderator cannot decide about a
notice they are involved in. A notice that is taken down is gone for
everybody, including anybody who already had the link, but the record
of the decision is kept. The author can appeal. A different moderator
looks, and if the decision is reversed, the notice comes back and the
record shows both decisions.

Finished means it is live on the internet, not just on your laptop. A
street full of people who have never met you can use it, and argue on
it.

## The road map

Eight sprints. Each sprint delivers one part of the list above. They
must be done in order, because each one builds on the one before.

| # | Sprint | What it delivers |
|---|---|---|
| 1 | Names on the board | Neighbours join under a name others can see, and the board can sign an account out on every device at once |
| 2 | The board | Neighbours post, edit and delete notices, and the board reads correctly while notices come and go |
| 3 | Underneath the notice | Neighbours reply to a notice and to each other, and a deleted reply leaves the conversation readable |
| 4 | Reported, and still up | Anybody can report, the notice stays up while a moderator looks, and reports arrive as a tidy queue |
| 5 | Moderators are neighbours | Several neighbours can moderate, none can decide a report they are involved in, and every decision carries a name |
| 6 | Taking it down properly | A removed notice is gone even for people with the link, and the record of what was removed is kept |
| 7 | The author's side of it | Authors appeal, a different moderator decides, reversals are visible, and a member who keeps breaking the rules can be stopped |
| 8 | In front of the street | The board is live on the internet, and a bad release can be undone without losing the record |

## The hard parts

**Removing is not deleting.** Hiding a notice from the board leaves its
address working for the fifty people who were sent the link this
morning. Deleting it completely leaves the moderator with nothing to
show the next time somebody asks why it went. Sprint 6 fixes both at
once.

**The moderator lives on your street.** The person deciding whether
your notice stays up may have argued with you last month. Sprint 5
deals with this by limiting what a moderator may decide, not by
trusting them to be fair.

## Working on it

The sprints, their briefs and their tickets are in Blacksmith
Experience. Start with sprint 1. Each sprint opens when the one before
it is finished.

Read the documents attached to a sprint before you start its first
ticket. They explain the choices you will make and the options you are
choosing between.

## What this is built with

The whole product: an API and the screens that use it.

- **Django** with **Django REST Framework** for the API.
- **SimpleJWT** for authentication, against a custom user model in `apps/users`.
- **drf-spectacular** for the OpenAPI schema, served at `/api/schema/` and browsable at `/api/docs/`.
- **React** with **Vite** for the dev server and the build.
- **Chakra UI** for components, and **React Router** for routes.
- **TanStack Query** for every call to the API, so caching and refetching are decided in one place.

## Setting it up

You need the CLI once: `npm install -g blacksmith-cli`.

```bash
blacksmith setup     # dependencies, database, migrations
blacksmith dev       # start it
```

The API answers on `http://localhost:8000`, and the app on `http://localhost:5173`.

Copy `backend/.env.example` to `backend/.env` before the first run. It is ignored by git and holds the secret key, the database URL and anything else this project should not carry in its history.

## Where the code lives

```
backend/
├── config/
│   ├── settings/        # base, development, production
│   └── urls.py          # where routes are mounted
├── apps/
│   └── users/           # the custom user model, and auth
├── utils/               # shared helpers, base model
├── manage.py
└── requirements.txt

frontend/
└── src/
    ├── api/
    │   ├── generated/   # written by `blacksmith sync` — do not edit
    │   └── hooks/       # your queries and mutations
    ├── pages/           # one folder per page
    ├── features/        # auth, and anything else that spans pages
    ├── router/          # routes and layouts
    ├── shared/          # components and hooks used across pages
    └── styles/
```

## Day to day

| Command | What it does |
| --- | --- |
| `blacksmith dev` | Run it locally. |
| `blacksmith sync` | Regenerate the frontend API types and hooks from the backend schema. Run it after changing a serializer or a route. |
| `blacksmith make:resource Post` | Scaffold a model, serializer, viewset and routes, plus the hooks and pages that use them. |
| `blacksmith backend <command>` | Run a Django management command, e.g. `blacksmith backend createsuperuser`. |
| `blacksmith frontend <command>` | Run an npm command in the frontend, e.g. `blacksmith frontend install axios`. |
| `blacksmith eject` | Remove Blacksmith and keep a plain Django and React project. Nothing here is a dependency on us. |
