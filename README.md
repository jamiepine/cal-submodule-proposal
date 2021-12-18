
## Cal.com Monorepo Concept/Proposal
A monorepo brings many advantages to us the more we branch off with additions such as the Console, which would benefit greatly from code-sharing ui and backend logic.

This repository would utilize git submodules to include a **closed source** repository called `console` which utilizes shared code from the open source version of Cal. This design allows more closed source submodules to exist and code share.

The file structure in this project illustrates at a bare minimum what the layout could look like.

At the top level we have: 
| Folder        | Purpose                                   |
|------------|----------------------------------------------|
| `app`        | The user facing app           |
| `console`    | The admin dashboard                        |
| `api`        | Both REST API endpoints and tRPC resolvers |
| `components` | Shared UI components                       |
| `lib`        | Shared logic and database CRUD                              |
| `prisma`     | Database schema                            |

`app`, `console` and `api` all have their own `pages` directory which we can use "Multi Zones" from Next.js to serve three separate deployments.

Each of these directories have their own respective `tests` folder, again for clear modular association.

I think the layout of the existing repository is a little confusing, its not immediately clear where API endpoints live, `pages/api/*` and `server/router/*` for example. API routes feel weird served up from the same pages folder as the base app, and tRPC resolvers could be confused as being the primary API. Both of them respectively are a form of API and if we are to maintain both it would be nice for them to live together, with respective `tests` directories and share logic from `lib`.

Instead of having a dedicated folder for `ee` we can license specific areas of our application accordingly.
