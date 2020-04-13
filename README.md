# Web Developer Checklist

This is (and possibly forever will be) a work in progress

## Planning
- Meaningful choice of:
  - Frontend code (javascript, typescript...)
  - Frontend framework (Vue, React...)
  - Backend code (node.js, java, php...)
  - Backend framework (express.js, springboot, laravel, Nuxt...)
  - Testing suites
  - Application type: SSR, CSR, SPA, static site...
  - Software architecture
  - Database schema (if any)
  - Deployment strategy (e.g. push code to master branch, release to staging and production from weekly release branches)
  - Code base hosting service (gitlab, github...)
  - Hosting / server provider (AWS, Heroku, DigitalOcean, Netlify, Zeit...)
  - Domain vendor
  - Useful:
    - [State of JS 2019](https://2019.stateofjs.com/)
    - [State of CSS 2019](https://2019.stateofcss.com/)

## Programming workflow
- Write new code
  - While doing so, write any comments that help understand why the code was written that way
- Write the tests that validate the use cases involved in the new code, in a per commit basis
- Debug: when finding bugs, fix them and write tests that catch these bugs
- Refactor the code if it needs refactor, or set a task to refactor it ASAP
- Have the code reviewed by someone else
- Write any necessary documentation, update the release notes for the project
- Do code reviews of someone else's code


## Basic steps to code a website:

1. Decide initial content and basic layout:
   - What pages
   - What sections per page
   - What content per section
2. Create "design-less" layout / wireframe, based on standard web elements, do mobile first, then desktop
3. Create html file without styles
4. Apply basic styles to html to create wireframe
5. Create design (branding, styles, theme) >> style guide
6. Apply theme and styles to complete design
7. Release to production
8. Optimize in terms of performance (80/20 principle)

### Create component or page:

- Sketch wireframe
- Write HTML in your choice framework (only semantic, no styles)
- Write CSS styles
- Use media queries to make component look good in different screen sizes

## Design and UX:

- https://github.com/thedaviddias/Front-End-Design-Checklist
- Refactoring-ui and my notes https://github.com/luismartinezs/web-design-ux-ui-cheatsheet
  - Feature first design
  - Design + code in small cycles
  - Use predefined spacing, sizing, font, color, shadow...
  - Design by hierarchy using color, weight, position, spacing, size, shape...
- User actions provide instant feedback
- A spinner is displayed while the server confirms an action, or result is displayed optimistically before server returns a response

## HTML and coding:

- https://frontendchecklist.io/
- Use a skeleton CSS like https://cdnjs.com/libraries/skeleton
- API error handling: https://blog.restcase.com/rest-api-error-codes-101/
- Maintain a good folder structure:
  - One folder per service
  - One folder for reusable services, e.g. common/api/, common/component/
  - [Fractal folder structure](https://hackernoon.com/fractal-a-react-app-structure-for-infinite-scale-4dab943092af) for nested components
- Tracking cookies require user permission in form of a modal
- Identification cookies (to store form-submitted data) require the user to check a checkbox before submitting a form
- `window.onbeforeunload` hook prevents form data loss on accidentally closing the tab
- Terms in different languages use the `lang` attribute
- Dates use the `<time>` element

## Performance:

- https://github.com/thedaviddias/Front-End-Performance-Checklist
- Pass chrome audit
- Any DNS-hosted fonts use:
```html
<link rel="preconnect" href="https://fonts.gstatic.com/" crossorigin />
<link rel="dns-prefetch" href="https://fonts.gstatic.com/" />
```
- Any registered event listeners are removed when the page is unloaded / destroyed

## PWA:

- https://web.dev/pwa-checklist/
  - Service workers: https://codelabs.developers.google.com/codelabs/offline/#0
  - Manifest: https://developers.google.com/web/fundamentals/web-app-manifest/
  - Requests use HTTPS

## Testing checklist:

- E2e tests test main use cases
- Integration tests test connections between services
- Unit tests test complex functions
- When a bug is caught and fixed, a test that covers it is written

## Security checklist:

- Do not trust anyone, act as if Darth Vader is everywhere in the network
- Always sanitize and validate user input
- Do not use innerHTML, use createTextNode from input
- Use libraries like knex to communicate to a database, instead of direct SQL commands
- Production accounts should not be able to execute DDL, only DML
- Always store passwords as salted hashes
- Outsource auth workflow when possible
- Take care of outdated dependencies
- Be aware of attacks as soon as they happen, (winston, morgan...)
- Never transfer any secret through HTTP (i.e. no HTTPS): [letsencrypt.org](https://letsencrypt.org/), cloudflare CDN
- Prevent XSS and XSRF: Use `Content-Security-Policy` header, `secure` and `HTTPOnly` headers for cookies
- Do not use `eval()`
- Do not use `document.write()`
- Always put any secrets in `.env` files and have git ignore them
- Secure http headers: helmet package
- Principle of least privilege
- Always have backups of any data or code
- Encrypt sensitive data in any transaction: [bcrypt](https://github.com/kelektiv/node.bcrypt.js#readme)
- Login and register forms always give an ambiguous message in the same response time to prevent [user enumeration](https://www.hacksplaining.com/prevention/user-enumeration).
- Sensitive data are never stored as such in a DB, it is stored as a salted hash ([bcrypt](https://github.com/kelektiv/node.bcrypt.js#readme))
- Any secrets required by the app are stored as environment variables in the server and never exposed in the remote code base or the client

## Dev ops:

- In development, a docker container or orchestrated set of docker containers launches all backend services with a single command
- Use a service that runs containers and takes care of managing servers and clusters automatically (e.g. AWS Fargate)
- Routing redirection points external traffic to a specific URL as needed, e.g.: HTTP to HTTPS, www domain to naked domain...
- Load balancers point traffic to specific targets inside a VPC or to different servers if traffic numbers are huge
- Services that only run occasionally or on seasonal bursts are handled by lambda functions
- A CDN caches and serves the website

## CI/CD:

- Source code is linted, formatted consistently and tested
- A precommit hook auto-formats the code and runs unit tests
- When code is pushed to the remote repo, e2e tests and integration tests are run automatically. If e2e tests fail, the push fails. resources: [circleci](https://circleci.com/)
- If working in a team, before merging a feature branch into master, a peer reviews the code
- Development environment: automatic deployment from master whenever a new commit is pushed
- Staging environment: automatic deployment from release branch tag
- Production environment: manual deployment from release branch tag
- Smoke tests are set into place to be alerted if something goes wrong on production (e.g. Sentry)
