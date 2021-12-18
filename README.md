
## Cal.com Submodule Concept/Proposal
While we are currently exploring the possibilities of an admin console, I wanted to explore changes to the repo structure that would allow for code sharing and closed source modules.

### Submodules
This repository would utilize git submodules to include a **closed source** repository called `console` which utilizes shared code from the open source version of Cal. This design allows more closed source submodules to exist and code share. Originally this concept would have been a monorepo, but with submodules that is not necessary. 

### Structure
To compliment the submodule setup I also propose changes to the folder structure. 

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

Currently we have `pages/api/*` and `server/router/*` for our API and tRPC resolvers respectively. API routes feel weird served up from the same pages folder as the base app, and tRPC resolvers could be confused as being the primary API. In this re-structure they live together in an `api` directory and share logic from `lib`.

### Tests
Each of these directories have their own respective `tests` folder for modularity, I believe this will help encourage tests to be written and each layer of our application isolates concerns. `api/tests`, `api/tRPC/tests`, `lib/tests`, `components/tests` etc...

### Licensing
Instead of having a dedicated folder for `ee` we can license specific areas of our application accordingly.


