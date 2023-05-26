# VueConf 2023

### Action Items -- Project

- **Remove Vetur, install Volar** as IDE plugin
  - Official recommendation is that Vetur is outdated, deprecated
  - [CoC-Volar](https://github.com/yaegassy/coc-volar)
- **Prettier/formatting on save** -- document and force team to do this
- **Typescript** -- can we add this to our current Vue2/Vite4 pipelines?
  - Wait until Vue 3 upgrade?
  - Investigate a single TS file and go from there
- **Component Testing**
  - Demonstration shows that with our setup, it should be simple/painless
  - Create very basic component test based on a single little component
  - Better understand `cy.validate` and re-using Component test code in an E2E
test suite
- **VueUse** -- research how to integrate
  - [https://vueuse.org/](https://vueuse.org/)
  - Probably after Vue 3
  - Seems *extremely* useful

### Action Items -- Personal

- Check to see if I use Vue Devtools
- CSS `@scope` block -- investigate this new feature proposal
- Nuxt presenter was using the Arc browser. I've seen this before -- look into again

### Parking lot for generic thoughts

- Need to prioritize Vue 3 upgrade so we can take advantage of all this stuff
- We should investigate using TypeScript (TS)
  - How big of a lift?
  - When we upgrade to Vue 3, do it then?
- HighCharts highlighted as having "great" Vue integration by Alex Harding
  - Keep in mind if site needs data visualizations
- Cypress-Cucumber -- tests in "human readable" code
  - See slack convo in #coi-testing for discussion about this
- Histoire -- Vue-specific Storybook alternative (also supports Svelte)
  - Do we even care about Storybook at all at this point?
  - Depending on LOE, this might be a better alternative
- Live coding exercise from Nuxt CEO
  - demonstrated used TailwindCSS, which has incredible utility for rapid prototyping.
    - makes it clear why people like TailwindCSS
  - Nuxt CEO uses CoPilot, as shown and mentioned during his live demo
- `pre` tag once again shown as being very useful for debugging raw text/JSON/etc

### Vue/web dev/etc thoughts/reminders/etc

- `computed` properties -- main use is to cache expensive properties.
Good to remember/be reminded of that.
- `composables`
  - encapsulate and re-use stateful logic
  - We don't use these -- keep in mind moving forward
  - Examples of places where these could be useful:
    - Shared logic between Resources/Search pages
- Destructuring assignment for props/etc in Vue ecosystem still very fragile
  - Vue 3.3 allows destructured props to maintain reactivity, **BUT**
  - Pinia and other libraries still do not allow it
- "phrasing context"
  - [MDN Link](https://developer.mozilla.org/en-US/docs/Web/HTML/Content_categories#phrasing_content)
  - `divs` can't be in `p` tags, for example.  Browser "fixes" that for you and
  swaps them if you make this mistake
  - upcoming improvements for SSR hydration will better warn people about this
- "Tangibility Principle" -- once users get their hands on it, they can tell
you what's wrong with it
  - This was why we had interactive prototypes back in the day

### eRegs-specific thoughts

- Vue 3 upgrade sooner rather than later
  - Vuetify seems ready
  - I wanna use all these cool tools that were demonstrated, and best to get to Vue 3 first
    - VueUse seems especially helpful
  - Want to upgrade to Vue 3 before adding complexity
  - We're well positioned now
  - the longer we wait, the harder it will be
- Cypress Component Tests -- *We can do them now*
  - Demo made them seem extremely easy to enable if you're on latest version of Cypress
    - We're on the latest Major Version, and should upgrade to latest Minor Version
    - See notes below -- can be extremely useful

## Notes -- Day One

### Opening remarks/business/housekeeping

- The venue has a warm-up comic/MC.  Doing well warming up the crowd
- Wifi not working well; sound cutting in and out
- Conference Reception -- tonight, Howlin' Wolf
  - Open bar and "alligator bites" and other food
  - ...we'll see
- Music Room - lunch space for people flying solo (i.e. me)
- Raffle at end of conference -- must be present to win
  - surprise grand prize to encourage attendance

### State of the Vuenion -- Evan You

- NOLA is where the first VueConf was held
- Volar -- IDE experience
  - nvim/vim?
- Vue 3.3 released
  - TS improvements in core
    - import Props into `defineProps`
    - `generic` types in `script setup`
    - Types slots with `defineSlots`
    - Props destructuring
      - Now stays reactive
    - `toValue`/`toRef`
  - we do not use JSX
- VitePress
  - Static Site Generator
  - Successor to VuePress, but lighter and faster
- Vue 3.x upcoming plans
  - stabilizing `Suspense`
    - nice
- Vapor Mode
  - new compilation strategy -- more performant
  - large undertaking, multiple stages to complete, not soon
    - ETA: End of 2023/start of 2024
  - will be able to "opt in" at component level, or more holistically
    - This is a VDOM-free feature; things like Vuetify will still need VDOM
      - Which is why it is opt in at the component level
      - Still free to use VDOM if/when needed

### Rendering What/Where/When/Why -- Phil Hawksworth

- HTML/DOM -- letting the browser paint the view for you
- "The Rule of Least Power" -- choose the least powerful language for any purpose
  - fundamental to web being sustainable (his opinion)
- Build > Server > Edge > Client
  - Compute happening at all steps -- or can happen?
  - Where is the best place?  When is the best time to render?
- SSG -- Static Site Generation
  - Rendering happens on: Build
  - CI/CD (GitHub Pages, Netlify) re-invigorated this pattern via automation
- CSR -- Client Side Rendering
  - Larger onus on dev to make sure JS error handling works well
  - Rendering happens on: Client
    - When?  When the assets arrive
    - Must handle edge cases
- SSR -- Server Side Rendering
  - Rendering happens on: Server
    - ... Or does it?
    - yes
- ESR -- Edge Side Rendering
  - Rendering happens on: Edge
  - Abilities:
    - Geolocation
- "Which one is the best, Phil?"
  - Answer: "It depends."
  - Question: "It depends on what?"
  - Answer: returning to "The Rule of Least Power"
    - Do we need the biggest, most complex solutions?
  - "If I can do things in advance, I will."
- Increments
  - Incremental rendering
  - Netlify/Gatsby definitions
  - Some names/concepts/acronyms about this concept:
    - On Demand Builders (ODB)
    - Deferred Static Generation (DSG)
  - **Don't generate in build**. Wait until the first time it's requested
    - (His opinion)
- "Deciding demands questions."
- *Demonstration*
  - Nuxt -- route-based rendering configuration.  Pretty cool
    - Can we use this?  
      - Can't imagine we have time/buy-in to implement
      - Site works fine as it is

### Building Data-Intensive Visualization Applications to Vue -- Alex Harding

- Data Storytelling -- a "soft skill"
  - A process for understanding data, users/ narratives, and needs
- Telling stories...
  - ... Enhanced with charts, visualizations, tabular output, etc
  - Allow users to build their own stories vs having a short story collection
- Reports vs Query Tools
  - static report vs interactive app
    - Is interaction needed, or does it overcomplicate?
- APPR Dashboard tool -- example of interactive visualization
  - Query Builder type tool -- have access to all data, let users can tell their
   own story
  - has a Static Report feature for a "curated" view for people with less data
  literacy (or time, etc)
- Having many filters becomes a spiderweb of event broadcasting and **required
good state management**
  - Likely through a `store`
  - Resources page probably could have benefited -- URL params got unwieldy
    - Think about this for any further enhancements to Search Page
  - This person's solution: `Harness-Vue` library
    - [Harnessjs.org](https://harnessjs.org/)
    - Developer patterns can become libraries

### Vue to the Edge (Nuxt) -- Sebastian Chopin

- Nuxt is a web framework for creating Vue applications
  - SSR, CSR, SSG, ESR, Hooks, File System Router, Auto Imports, Data fetching
    - Very fully featured, endless features.  Overkill for us.
- The "Edge"
  - a limited JS environment running on CDN nodes
  - code replicated to many nodes (Cloudflare, etc)
  - renders quickly and is cheap to host
    - ms from end users
    - 0ms cold starts
    - automatic scaling
  - Providers: several
  - Limitations
    - different from Node/Browser (V8 isolates)
      - Although Nuxt has polyfills etc
    - Total size limit: 5MB
  - DBs are coming to the Edge
- *Live coding demonstration*
  - creating a table in a sqlite DB with Drizzle looked easy and fun
  - Migrations happen automatically with Nuxt
  - Nuxt devtools looks very cool
  - Nuxt 3 -- HMR on the server if only server is updated
- Very cool demo, Coffee or Tea app with GitHub authentication

### Patterns for Large Scale Vue.js applications -- Daniel Kelly (VueSchool)

- What is the best way to structure a Vue.js application?
- Heavy dose of opinion incoming, but from experience

#### Seven tips

1. **Standards are key**
    - The modern world works because of standards
    - Vue.js styleguide is a good place to start
    - When you use standards, new and existing team members have to think less
    - Component Standards:
        - SFCs should be PascalCase
        - Prefix base components (App/Base/etc)
    - Use Recommended Tooling
        - Custom tools are tempting but lots of overhead that will sap your time
        - Nuxt3 highlighted as best of breed option
2. **Take full advantage of IDE**
    - Remove Vetur, install Volar
    - Formatting -- set up to format automatically on save
        - It's 2023, let your IDE and libraries (like Prettier) make the
        bikeshedding decisions
    - Use TS
3. **File Structure**
    - "Use Nuxt"
    - group page-specific components with pages
4. **Route Naming Convention**
    - CRUD
5. **Wrap third party code** (sometimes)
    - decreases chance of third party lock-in
    - Allows you to replace deps in ONE PLACE
    - You can extend functionality easily
    - Example: `axios` (except don't actually wrap `axios`, it's just an example)
        - Wrap `axios` in HTTP class
        - If you wanna use another HTTP request library, you only replace it here
    - (This all works for components, too)
6. **Interact with Backends with an SDK**
7. **Prefer the Composition API**
    - Mainly it is easier to spot opportunities for abstraction and code re-use
    - See abstractions more clearly

### Testing Vue Components with Cypress -- Mark Noonan

- Starting off with fixing failing Component tests
- First failing component: failing paragraph component
- Component testing looks very straightforward.  Test suite looks identical to
a normal e2e test
  - Difference: use `cy.mount()` to render a component by itself, in a real browser
    - use props/slots etc to set up initial state
  - Component tests are "driven by user interactions in the browser, not unit
  testing the implementation"
  - An example for testing CSS issues was shown.  Nice.
    - Another one: asserting that `font-size` should be greater than a value (16)
    - Asserting against computed styles is an intended use
    - Asserted that an `aria-label` was present in another test
  - Can expect that a component will throw an error
  - An example of a test suite that contains a test against a live API and the
   same test
  being intercepted with mock data.  Interesting
  - Component tests can be re-used in e2e tests using `cy.validate()`
  - Some exciting reasons to component test sooner rather than later:
    - Encourages better isolated components
    - Allows for frond end workflow for developing single components without
    spinning up the entire site -- built in live reloading.  Much like Storybook
    - **E2E tests can focus on user flows**.  All the component correctness testing
    can be offloaded to Component tests

## Notes -- Day Two

### What you'll love about Vue in 2023 -- Alex Kyriakidis

- Vue usage tripled in 2023
- How many sites have been built with Vue.js?
  - 4,000,000 (four million)
- Do I use Vue Devtools?
  - I don't know.  See Action Items
- Vue Ecosystem:
  - Matured
  - Stabilized
    - Big players (Nuxt, Vuetify) have caught up to Vue 3
- Library spotlight
  - Pinia -- store, new standard that has replaced Vuex
  - Quasar -- cross platform apps.  Was not a fan when we researched component libraries
    - Nuxt, Vuetify, Ionic all in one framework
  - Formkit -- Build forms better, easier, nicer
    - build forms "10x faster"
  - VueUse -- "essential" Vue composition utilities
    - 200 functions (`onClickOutside`, `useDraggable`, `useLocalStorage`, `useGeolocation`)
  - Naive UI -- UI Library (Vue3)
  - Vue Macros -- syntactic sugar
    - new shorthand -- cognitive overload for devs not in Vue every day (or even
    every week)?
  - StorefrontUI -- Popular in Europe
    - eCommerce UI platform
  - Capacitor -- "the new Cordova"
    1. Drop in existing app
    2. Install native platforms
    3. Compile for iOS/Android
  - Vitest -- see Thomas's Spike/PR
    - "Jest replacement" for Vue3
  - TresJS -- 3D using ThreeJS
    - Cool but not relevant to me
- Vue.js Forge -- what is it?
  - a "hands-on coding conference"
- VueJobs -- the leading job board for the Vue.js ecosystem
- Would you like the composition API in any non-Vue app?
  - **Handlebars** templating engine + Vue for ref, watch, etc
  - Seems like unnecessary overhead: *But Why?*
    - You can use the framework you know on legacy apps
    - Helps you copy/paste code/functions/composables/etc for legacy apps
    - You can bring the Vue ecosystem with you
    - Helps you **begin the migration** from legacy app to modern (Vue) app
    - Helps keep the same mindset between apps
    - Build faster (and have fun)
- Presenter is pushing official Vue.js Certification program
  - I'm ambivalent about this.
  - Value proposition (time + money) -- not sure it makes sense
  - Do front end technologies and libraries still move too fast for this to be valuable?
    - React has been monolithic for years now... So perhaps not
    - Will Vue be widely used enough for this to be valuable, though?

### Proven Pinia Patterns -- Adam Jahr

- "Next evolution of State Management"
  - Specifically Global State
- Why Pinia?
  - more "freeing"
    - but with more freedom comes more responsibility
    - Patterns become important to prevent freedom from accidentally creating anti-patterns
- Couldn't we just use the Composition API?
  - Example: we could create a reactive object that could behave as our store
  - Why use Pinia instead?
    - Patterns for collaborative organization
    - Clear actions to mutate state
    - Fully featured Pinia devtools
    - Better developer experience
- Different ways to compose stores
  - Options stores
  - Setup stores
- "Store-ganization"
- Unidirectional Data Flow still a best practice
- `$patch` -- multiple changes at once
  - single entry in devtools
  - if we always use `$patch`, would be easy to find all instances when state is
  updated in code
  - can take an object of function as argument
- Can be used in router
  - example: when user navigates home, clear state with `$reset`

### Build and Deploy Mobile Apps with Nuxt Ionic -- Cecelia Martinez

- Nuxt Ionic Module
- Benefits of Nuxt, brought to mobile
- Not super relevant since we don't use Nuxt and don't have a need for an app
store app
- Live coding demonstration
  - Looks pretty nice and straight forward -- native elements

### Conquering Forms in Vue -- Justin Schroeder

- [Formkit.com](https://www.formkit.com)
- Forms dominate the effort of lots of front end devs
- Form complexity is at an all-time high and it is very painful
  - Think back to introduction of AJAX -- the expectations became high then
  - And expectations are way, way, way higher now
  - Absurd amounts of HTML needed for even modest forms
- Component libraries still do not solve 75% of form complexity and pain
- These remaining issues: Structural Domain and Structural Problems
- Solution?
  - Global store?
    - Vue Formulate 1
    - Store models data but does not model errors/validation well (Vuex)
  - Components? With Provide/Inject?
    - Vue Formulate 2
    - Components also did not model errors/validation well
- Not everything in our component tree is in our form tree
- Forms are their own *distinct* trees
  - Forms have always been distinct trees
  - Distinct from the DOM tree
- Sales pitch for FormKit begins now
  - A "form building framework"
  - (not a UI library)
  - a ton of features
  - Part of it is Open Source
    - With some more niche/complicated components behind a paywall
  - Looks really nice.

### The Next Vuetify -- John Leider

- Version 3.0
  - We need to get on this
  - Seems mature
  - The more that is shown as new/improved in V3, the more nervous I'm getting
  about upgrading
  - What's new and improved?
    - Global Defaults
      - Boolean props on their way out, maybe removed entirely compared to V2
      - "Making it easy" to apply global styles, simplified maintenance, reduced
      duplication
    - Dynamic defaults based on context
    - Overriding defaults at DEeach level
    - Versatile theming with nested defaults
      - granular control is the goal here. Buuuut is this too granular
    - Aliases
      - Create virtual components from core Vuetify
    - "Massive" theme system
    - Snappier animations
    - Layout system
      - `v-layout-item`
      - "unlimited" custom layout combinations
- Version 3.1 "Valkyrie"
  - Introducing Vuetify Labs
    - Channel for components that are not yet at feature parity with V2, but can
    still be used
- Version 3.2 "Orion"
  - Vuetify Play REPL moving to replace Codepen (eventually)
- Version 3.3 "Icarus"
  - Form validation improvements
  - Skeleton loader hits lab channel (good to know)
- Version 2.7 Nirvana
  - Will be LTS -- 18 months of bug/security fixes
  - **WILL FINALLY HAVE A VUETIFY 2 to VUETIFY 3 UPGRADE GUIDE**
    - This is what we have been missing
  - End of June 2023 release date
- Version 3.4 "Blackguard"
  - 90% Feature parity with V2
  - Composition API documentation examples
  - October 31, 2023 release date
