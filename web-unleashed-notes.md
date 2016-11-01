WEB UNLEASHED - WORKSHOP 10/2/2016
==================================

Smart Responsive Design Patterns: Front-End & Performance
---------------------------------------------------------
*Vitaly Friedman, Editor-in-Chief, Smashing Magazine*

### How to solve language handling for 23 different countries wihtout having to generate diff CSS?
- BBC uses JSON files to indicate text direction, length, social media buttons, etc, then create mixins
- Use flexbox to manage positioning of popular components
- Published article about making responsive web design multi-lingual (*Responsive News - Where BBC News developers blog about responsive design*)

### Content Choreography
- Flexbox helps solve the problem of **source order**
- We face 2 issues:
	- **source order**: in a linearized layout, content blocks are displayed in the source order by default
		- flexbox is a solution
		- flexbox is hungry and wants to spread all the time (jabba the hut)
		- use flex to define share of screen space && order

```css
/* use flex to define share of screen */
#main { display: flex; }
nav { flex: 1; }
aside { flex: 1; }
article { flex: 2; }

/* use flex to define ordering outside of source order */
@media screen and (max-width: 20em) {
	article { order: 0; }
	aside { order: 1; }
	nav { order: 2; }
}
```

- Flexibility: JS polyfill for Flexbox *on github*
- use `margin-top: auto;` to stick something to the bottom
- **"If you read the specs, at night..."**
- custom bullets for ordered list: css counters

### Performance Strategy
- Priority lists for content and styles to define "core"
	- core content doesn't rely on JS
	- Only one main feature image considred "core"
- The Guardian
- Optimizations based on simple principle: optimize content, *defer the rest*
	- Load critical CSS inline and full CSS on load
	- Avoid JS libraries (jQuery -> JS)
	- Store Web fonts in localStorage + cookies
	- Defer advertising, tracking and all non-critical CSS/JS
	- Replaced Respond.js with IE8 stylesheet (fixed-width)
	- Optimize the critical rendering path for content delivery
	- Resource hints, dns-prefetch, preconnect, prerender, preload
		- prerender content when user reaches a certain point
- `https://www.webpagetest.org/result/161002_RY_J9Y/`, measuring speed index, should be below 1000
- employ 'scout' approach instead of loading versioned files using `<script>` tags, doesn't require reloading of all HTML

##### Image Compression
- Take images blown up 4x then save at lowest quality. Use that image at the desired (smaller) size. File size decreases significantly.
- Blurring unimportant parts of the photo brings size down significantly
- Use alternate scanning for jpg rendering, mozjpeg (run all jpgs through jpg encoder)

- pragmatist's guide to service workers *on github*
- HTML -> HTML2, estimated 2wks, took 3 months



WEB UNLEASHED - DAY ONE 10/3/2016
=================================

Thinking Outside the Little Black Box: Interaction Design in the Post-Mobile Era
--------------------------------------------------------------------------------
*Jonathan Stark, Mobile Consultant*

- Mobile phones have more power than the computer systems that sent men to the moon
- Desktop is dead - browser is a casualty
- Forcing desktop website down to mobile is a "forced march to hell"
- Using a phone requires an eyeball and a hand
- We outsource pieces of our brain to our phones - don't have to remember anything
- Think outside the browser
- screenless web browsing: google home, amazon echo, everywhere

### Horizontal Specialization: i.e. react development
- safe web skills: JS, CMS (content management system), API
- safe design skills: typography, RWD (responsive web design), UX (cross-device experiences)

### Vertical Specialization: go deep on problems for a particular audience i.e. websites for credit unions
- be able to serve your customer really well because you know them



A Cartoon Guide to Performance in React
---------------------------------------
*Lin Clark, Code Cartoonist, Senior Developer Tools Engineer, Mozilla Firefox DevTools*

**Focus on performance of the render cycle in React**

1. The basics of rendering in the broswer
	- main thread -> DOM Tree -> Render Tree (reflow), happens in batches of changes
	- reduce the amt of work the main thread must do
		1. reduce # of changes made to DOM
		2. batch changes together in time, so it's easier for main thread to batch to render tree
	- Your code needs to be a good PM and tech lead
	- All developers need to know about best practices
	- Elements -> Instances -> DOM -> reflow -> UI is rendered

2. Minimizing and batching DOM changes in the virtual DOM
	- Determines the smallest number of DOM changes, batches them together, so the browser can reduce the # of reflows

3. What you can do to make it faster
	- React yells at you and tells you what to do
	- Use keys to match previous instances with new ones
	- shoudlComponentUpdate
	- immutability
	- using setState() or connect() at lower levels of the tree
	- Memoization
	- Virtualization (only show things visible in the page currently)
	- Observables (a more precise way to know when data has changed)

- Article coming out in Smashing Magazine about this stuff



A Day In the Life of a Developer Bo$$
-------------------------------------
*Dyanna Zaidman (moderator, Talent Scout, Creative Niche), Wes Bos (Independent Web Dev), Robyn Larsen (FE Dev), Haris Mahmood (FE Dev, Shopify)*

### Biggest misconception about devs?
- Haris: People assume devs are born good devs, 100% false. There's SO MUCH we don't know.
- Wes: Everyone thinks you need to be good at math. Just need time and creative hunger.
- Robyn: Assume you're some dude in a basement with a massive beard.

### What does your day to day look like?
- Haris: Make myself aware of what's happening in the world via blogs, twitter, go out for a walk
- Robyn: No tech days (no phone, computer, tv, etc), no email until after 12pm
- Wes: Have as little as possible on my calendar

### System to keep track of emails, calendar?
- Wes: Follows GTD (getting things done) guide
- Haris: GSD (getting shit done)

### What are the biggest challenges in the tech industry? What are the best qualities of a tech leader?
- Wes: Being able to wait until frameworks or libraries are stable, not chasing the shiny penny

### Is business acumen important for devs?
- Wes: Yes, how does the stuff you're building making you money?
- Haris: The end user doesn't care about the frameworks/libraries you use

### How do you overcome feeling of others knowing more than you when collaborating?
- Robyn: Be humble, be open/honest about what you don't know
- Haris: Everyone has their own set of knowledge, with some minor overlaps
	Juniors, explain HOW to explain things to others. In a unique position to help others learn how to teach
- Wes: The more you learn the more you realize you don't know. Don't be afraid to share what you don't know. Don't assume that others know things you don't.
	Push past the haters.

### What excites you most about the future of development?
- Haris: It's getting to a place where it's no longer the nerds club. It's sexier and more accessible.
- Wes: CSS is getting huge (flexbox, grid, animations), dev is growing so much, future is specialization, pick your thing

### What's the best piece of professional advice?
- Robyn: You'll learn more from your peers than through blog posts
	If you can't do the shitty jobs awesome, do the great jobs awesome
- Haris: If you want to get good at something, volunteer to teach/mentor
	Having to explain things to someone else is extremely valuable
- Wes: Keep on sharing what you know - blogs, github, codepen

### How important is social media presence to your career path?
- Wes: It's how good you are as a dev, but depends on what it is you're trying to do
	Twitter is an amazing tool, connect with others to get jobs, gain community, share and gain knowledge
- Robyn: Get access to companies

### What one tool, whatever is on your radar and you're excited about?
- Robyn: ES6 & React
- Wes: GraphQL
- Haris: React, Redux, UX (non-browser)



DownTheRabbitHole.js – How to Stay Sane in an Insane Ecosystem
--------------------------------------------------------------
*Branden Hall, CEO/Maker, Automata Studios*

- 2009 node.JS
- 2011 npm --> The JavaScript Explosion
	- 329,149 JS modules as of 9/22/16
	- easy to publish to npm
	- zero gatekeeping
	- quality varies wildly
- No language support for modules
- Scaffold: Yeoman, Slush, etc.
- Transpile: Coffeescript, TypeScript, Dart, Babel, Clojurescript, Elm
- Build: Grunt, Gulp, Webpack, Brunch
- On the horizon: asm.js, ES6 (Modules!)
- One size does not fit all
	- What are you building? (single page application)
	- How big will the codebase be?
	- Who is your audience? (accessibility)
	- What does your team know? (understanding the people and what they've worked with)
	- When is the project due? (do you have time to learn, implement)
	- How long will your code last? (is this a product or a project? don't want future you to hate current you)
- Affects hiring, employee morale, internal training

### Transpiled Languages
- Pros: just the 'good parts', strong typing, improved syntax, domain specificity
- Cons: need to know JS too, matters less than discipline, more complex tooling, longer ramp-up

### Invest in great tooling and REALLY understanding it
- The best setups have the tightest feedback loops - faster from going to writing code to seeing it work
- Automate all the things! Bootstrapping, building (including sourcemaps), testing, deploying
- Document tools like crazy

Choice now: Webpack, Future: Brunch
Why the switch to Brunch?

### Philosophy
- What's the core idea that this library is trying to solve?
- Can **THEY** explain it?
- What is their inspiration?
- Are they solving YOUR problem?
- Does it play well with otheres?

### Small vs. Big
- Monolithic = consistency
- Reduced flexibility

### Documentation
- Bad docs = bad software
- Unit tests
- Code coverage
- Read the docs (Yes, all of them)

Choice for SPAs: lodash, react, redux

### Options Diff from the "Big Boys"
- vue.js: view layer
- zepto: jQuery
- riot: react
- meteor: full stack!

### Other great libraries
- d3: data viz
- rxjs: reactive programming
- jest: testing made easy
- moment: dates & times
- superagent: ajax (w/o jquery)

### You cannot stop swimming
- always going to have to learn new things
- picking a "winner" is a bad idea
- find what works for you, but never stop searching for better



Start Using ES6 Today
---------------------
*Wes Bos, Full Stack Web Developer and Designer*

### Life Makers - features That Make Life SOOO Much Better
- `let` and `const`: never have to use var again
	- `let` and `const` block scoped
	- `var` function scoped
- template strings: backticks!
	- `Your total is ${calculate(11.95)}.`
	- can be infinitely nested
	- ternaries can be used
	- use render functions
- default function arguments

```js
function calculateBill(total, tax = 0.13) {
	// stuff here
}
```
- arrow functions
	- replace `function` w/ `=>`
	- single argument, lose the parens (if you prefer)
	- implicit return, no more using `return`
	- `this` equals what the parent it was bound to, if nested

```js
// single argument
name => {

}

// no arguments
() => {

}

// multiple arguments
(name, height) => {

}
```
- object literals
	- `{ name, age, breed }` instead of `{ name: name, breed: breed, age: age }`

### Tooling
- Transpiling: converting ES6 -> ES5
	- Babel

### New Features
- Promises, Sets, Maps: `babel-polyfill`

### Deep End - New Concepts
- Destructuring: allows us to create and assign multiple variables in a single line of code. Works with both objects and arrays.
	- `const { first, twitter, city } = person` instead of `const first = person.first`, `const twitter = person.twitter`, etc.
	- Works for nexted objects `const { twitter: tweet, facebook: fb } = west.social.links`
	- Works for arrays as well, based on index
	- Swap values: `[current, benched] = [benched, current]`


### Sets
- Kind of like arrays you have always wanted
- a unique array iwth a nice API for adding/removing/checking items that live inside a set

```js
const students = new Set();

students.add('Wes');
students.add('Cait');
students.add('Anita');

students.size; //3
students.add('Wes');
students.size //3 because Wes was already there

students.delete('Wes');
students.clear; //empty the set

for (const student of students) {
	console.log(student);
}

const badApple = { first: 'Wes', id: 123 };
students.add(badApple);
students.has(badApple); // true
```

- ES7 has `array.include('x');` and exponents `x**2`



Rebuilding Facebook Comments Plugin w/ React
--------------------------------------------
*Stoyan Stefanov, Engineer, Facebook*

- How do you approach redesigning your code base with React? Where do you start?
- Implementing a Component
	- Small
	- Small surface (not too many properties or too configurable)
	- State as needed, Or not.
- `create-react-app` sets up base react app
	- npm i -g `create-react-app`
- escape latches



Building Node Microservices With Docker & Swarm
-----------------------------------------------
*Rami Sayar, Developer Evangelist, Microsoft*

- The problem with monolithic apps
	- with every new feature you add, you web app becomes more complex
		- increasing costs of maintaining app
		- raising difficulty in tracking bugs/issues
		- increase cost of scaling
		- deployment takes longer as shipping increasingly bigger packages
		- morale costs increase
		- marketing can't promot new features on time
		- sales fails to deliver on promises
- What are microservices?
	- a small fairly indepedent code package that fulfills a specific task
	- building block of a modular service
- Why Node.js suited for microservices
	- follows unix philosophy: write programs that do one thing and do it well
	- NPM makes package management and deployment easy
	- Straight-forward networking API

### Pros anc Cons of Microservice Architecture

#####Pros
- Loosely coupled: each microservice is independent
	- separate teams can work at diff paces
	- easier upgrade path for each microservice
- Smaller code bases make for easier deployments
	- easier for new team members to onboard
	- refactoring no longer halts development
- Easy to scale heavily used microservices without scaling the entire app
- You can use the best language/framework/platform for the job
	- even easier with Docker containers

##### Cons
- Outsourcing in-process communication to the network stack
- Heavier devops requirements on the dev team
	- need to monitor more moving parts and manage more complex infrastructure
	- networking, service discovery, etc...
- Data sharing and data modeling is hard
	- Ideally, each microservice should have per-service db

- React - The Definitive Guide
- Express-Microservice-Starter

### Patterns to Handle Networking FE and BE
- Service registration & Discovery
- Automatic Routing & Configuration
- Also want: Security, Authorization, Load Balancing
- API Gateway Pattern (preferred)
	- Implementing with several diff technologies: Docker & Swarm Mode, nginx, HAProxy, Kong, Skipper, Traefik, Tyk
- DNS Pattern
	- Each microservice has its own publically addressable URL
	- No single point of failure and easy to setup and scale
	- Doesn't follow the DRY principle
		- Individual handling of common concerns like security, authentication, etc.
		- Tempting to treat each microservice as its own project
	- Forces you to use CORS



Need for Speed: Tips to Optimize Your Website
---------------------------------------------
*Anne Thomas, Lead Developer, Out of the Sandbox*

### Business, business, business
- Selling all the things - conversion
- Instantaneous response time
- Bounce rates
- Google likes fast sites

### Simple rules to keep in mind
- Do no harm to data plans
- Embrace the new and progressive
- Listen to your townsfolk (and stats)
- Always keep optimizing

### Culprits
- Huge, full-width images
	- Conversion rates are 98% higher with images, it's a balance
	- Set a performance budget, how many bytes will your site be?
	- Use SVGs, responsive images when possible
- Webfonts
- Multiple server requests/large files
	- switch to HTTP2
	- https
	- combine CSS and JS files
	- CSS sprites?
- Third-party JS
- Uncached files
	- Don't leverage new storage systems
	- Get CDN
	- BE AGGRESSIVE with caching
- Render-blocking JS/CSS
	- Want to load first
	- Leverage the onload event
	- Minify CSS and use less CSS overall
- Crummy webhost - look for under 200ms server response time
- Page reloads
	- try to use AJAX
	- JS frameworks can handle state and refresh only things that change (but come with other caveats)
	- make calls on hover so the page preloads

### Responsive Images
- Minimize the pain of srcset by using variables
- Lazy sizes JS (more weight but can help)

### Lazy loading and dynamic content
- Lazy sizes includes lazy loading
	- triggers loading of images when scroll reaches a certain point
	- implemented for quick view (preview)

### AJAX adds some fancy
- use for infinite scolling
- preloading clicks

### Future
- HTTP/2
- Client hints - get info about the image from the server before it's loaded
- Service workers
- AMP pages (Accelerated Mobile Pages)

### Tools
- Web page test
- Google apge speed
- Varvy
- GTMetrix
- Chrome Dev tools

### Terms to know
- speed index (ms)
- time to first byte (TTFB)
- response time vs. load time
	- server side, end user, html, TTLB (response time)
	- load time is a more reliable metric
- perception of loading: get people to test it out



Increasing Effectiveness As A Technical Candidate/Interviewer
-------------------------------------------------------------
*Scott Biggart (Senior SE, Uber), Haris Mahmood (FE Dev, Shopify), Stacey Mulcahy (Senior PM, MS Garage), Kyle Simpson (Open Web Evangelist, Getify Solutions, moderator)*

### Screening Process - why is this process so formulaic? Matching buzzwords, etc.
- Terrible to match certain words for tools/frameworks
- Sometimes necessary to weed out batch applications, lazy applications
- Doesn't happen everywhere, especially small startups, it's a luxury to have to do that
- When you get really large you have to have some mechanism to narrow down applicants
- Recruiting events, meeting in person instead, but limited resources
- Arms race, if you're applying to a job you're 100% qualified for, you're applying to the wrong job
- How do we dig deeper?
	- Big difference b/w resumes in SF and NY -- buzz words vary
	- Look at problems solved rather than technologies used
	- Mention impact of the work done in their job

### Were you properly identified as a candidate in a phone screen in your early career?
- They didn't really answer the question

### What's the one thing that is done poorly in the technical interview process?
- Completely qualified but don't understand the job. It was sold to you as something else.
	- Ask, what are things I'm going to hate about this job?
- Focus on getting specific, correct answers for algorithms
- Force someone into a position of conflict to see if they work well on a team
- Make questions extremely clear to let the candidate know you're not trying to trick them, if it's unclear, you've failed

### Is the white board a net positive or negative?
- I love it. Design Uber. Supposed to ask what are the product requirements? Dive into specific things.
- Are misused heavily, when people ask for specific function where they test memory rather than using it as a tool of explanation

### Top Mistakes
- Spend too much time focusing on what you don't know when preparing for the interview
- Have opinions and be vocal about them
- Humility to say 'I don't know', over-confidence
- Giving your team credit for your team's work
- Name dropping

### What do you like to see?
- Ask questions that show you care about the work environment
	- What's the relationship like between a designer, PM, and engineer on your team
	- How are the teams structured?
- Excitement about specific aspects of the company beyond code (diversity, culture, products)
- Passion, side projects


Creating Beautiful, Accessible and User-Friendly Forms
------------------------------------------------------
*AClarissa Peterson, UX Analyst, ICE Health Systems*


Dirty Little Tricks from the Dark Corners of Front-End
------------------------------------------------------
*Vitaly Friedman, Editor-in-Chief, Smashing Magazine*

### Fluid Typography w/o Media Queries
- combine calc() function in CSS
- get perfectly fluid type with `html{font-size: calc(16px + (24 - 16) * (10vw - 400px)/(800-400));}`
- 16px = min font size
- 24-16 = max - min font size
- 400px - min screen size
- 800 - 400 = max - min screen size
- line height can be done the same way
- read about CSS locks

### Easiest way to implement the baseline rythym in CSS for type and buttons?
- Align baseline so that text sits on the same gridline
- vertical-rhythm.scss
- implementing baseline rhytym in CSS


RANDOM NOTES
============
- Teachers are better speakers
- Canadians do say 'eh?', 'aboot', 'sorery'
