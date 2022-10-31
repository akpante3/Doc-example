# Manifold

This project is a collection of tools to make creating and maintaining Gfinity digital media sites easier. It contains common used components, services, mixins, plugins, styles etc. Manifold uses lerna as a tool for managing javascript projects. It consists of 3 projects: `manifold-core`, `manifold-services`, `manifold-vue`.

[architecture](https://whimsical.com/embed/MjnJ53YWCdPKhX97vrPc9w ':include :type=iframe width=100% height=400px')

## Core principles

When writing or refactoring any code in manifold we should always keep these core principles in mind

1. **Simplicity:**
   Always try to keep code as simple as possible. Avoid any hasty abstractions. Don't try to overcomplicate code just to account for any possible future features. Go for the simplest solution possible.

2. **Communication:**
   Always strive for clear transparent communication with other dev team members and product owners. Make sure you fully understand the requirements of the task. Give regular updates, don't work in a vacuum. Ask for help, feedback and support. If something is taking too long, consult with the product owner about the importance and goals of the task before continuing.

3. **Readability:**
   Think about the readability of the code when you're writing it. The intention of the code should be obvious, variable names should make sense and avoid complicating the control flow too much. Use comments for code for clarifying the purpose or structure of the code if it's not obvious enough. The code should be easy to read and scan by other members of the team.

4. **Be curious:**
   Always be curious about any edge cases, possible problems and any hidden costs of a new feature or bug fix. You don't have to handle every possible edge case in your code but you should at least be aware of them and have a talk with other team members and the product owners.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Recommended VSCode Extensions

It is highly recommended that you use VSCode for you dev work since it is used by most of the team members. Here is a list of extensions that you should use to make working with Manifold easier

-   Bracket Pair Colorizer 2
-   Code Spell Checker
-   Conventional Commits
-   Eslint
-   Prettier
-   Headwind
-   GitLens
-   Sanity.io
-   Search node_modules
-   stylelint
-   stylelint-plus
-   tailwind css intelliSense
-   Vetur
-   vsc-nvm
-   Webhint

For the headwind plugin to work correctly, you need to add this to your VS code settings(JSON)

```
  "headwind.classRegex": {
    "css": "\\B@apply\\s+([_a-zA-Z0-9\\s\\-\\:\\/]+);",
    "postcss": "\\B@apply\\s+([_a-zA-Z0-9\\s\\-\\:\\/]+);",
    "scss": "\\B@apply\\s+([_a-zA-Z0-9\\s\\-\\:\\/]+);",
    "vue": "\\B@apply\\s+([_a-zA-Z0-9\\s\\-\\:\\/]+);"
  },
```

To automatically fix stylelint issues on save, add this to your VS code settings(JSON)

```
  "stylelint.autoFixOnSave": true,
```

### Recommended Browser Extensions

The following Chrome extensions are can be helpful while develpment and testing (they should also work on any Chromium based browser):

-   [AMP Validator](https://chrome.google.com/webstore/detail/amp-validator/nmoffdblmcmgeicmolmhobpoocbbmknc?hl=en)
-   [Browsec VPN](https://chrome.google.com/webstore/detail/browsec-vpn-free-vpn-for/omghfjlpggmjjaagoclmmobgdodcjboh?hl=en)
-   [SEOInfo](https://chrome.google.com/webstore/detail/seoinfo/ppbdklaincgliegpfolkjjfncpgobneb?hl=en)
-   [Web Vitals](https://chrome.google.com/webstore/detail/web-vitals/ahfhijdlegdabablpippeagghigmibma?hl=en)

### Prerequisites

1. First thing will be lerna, we need to install it globally

```
npm install --global lerna
```

2. Nice thing to have is nvm. This project uses node version of `14.15.3` (check out .nvmrc file). Follow instructions in this link to set it up: `https://github.com/nvm-sh/nvm`

3. Yarn installation:

```
npm install --global yarn
```

### Installing

A step by step series of examples that tell you how to get a development environment running

1. Change node to version specified in `.nvmrc`

```
nvm use
```

(If you use VS code, you can install extension for automation switching between node versions https://marketplace.visualstudio.com/items?itemName=henrynguyen5-vsc.vsc-nvm)

2. We will bootstrap all packages using lerna

```
yarn bootstrap
```

3. Build Manifold services.

```
yarn manifold-services:build
```

You can also watch the changes by running this command

```
manifold-services:start
```

4. We need to link our projects with `yarn link` so it can pick up changes locally. Command down below is going in every project folder and run yarn link. Run this command from root of this project.

```
yarn manifold-link
```

Now we need to **go into the GDM site repo** that we're working on (realsport, gfinityesports, etc).

5. Run this command in the GDM site repo to connect manifold using yarn link. **Note: You have to run this command everytime you install a new dependency from npm into the GDM site**

```
yarn manifold
```

If this script doesn't exists use this command (`yarn link @cevo/manifold-core @cevo/manifold-services @cevo/manifold-vue`)

6. In `nuxt.config.js` file add module config (**skip this step if the GDM site already has the manifold config**)

```
modules: [
  [
	'@cevo/manifold-core',
		{
			hasNewURL: false,
			hideAds: true,
			categoryTerm: 'string',
			isStaging: process.env.MANIFOLD_STAGING === 'true'
			sanity: {
				projectId: 'ncavvykf',
				// dataset: 'gfes-test',
				dataset: 'gfinityesports',
				apiHost: 'https://cdn.realsport101.com'
			},
			twitterHandle: 'Gfinity',
			seo: {
				siteName: 'Gfinity Esports',
				siteURL: 'https://www.gfinityesports.com',
				siteTagline:
					'The latest gaming news, features, and tournaments',
				defaultTitle:
					'Gfinity Esports | The latest gaming news, features, and tournaments',
				defaultDescription:
					'Welcome to the home of Esports! The fastest-growing community in competitive gaming - covering news, features and tournaments.',
				defaultImage:
					'https://www.gfinityesports.com/images/gfinity-placeholder.png',
				defaultLogo:
					'https://www.gfinityesports.com/images/gfinity-logo.png'
			},
			jsonld: {
				sameAs: [
					'https://www.facebook.com/GfinityRocketLeague',
					'https://www.facebook.com/GfinityFGC',
					'https://www.facebook.com/GfinityEsports/',
					'https://www.facebook.com/GfinityFIFA',
					'https://www.instagram.com/gfinity/',
					'https://twitter.com/Gfinity',
					'https://www.tiktok.com/@gfinity',
					'https://www.youtube.com/user/GfinityTv'
				]
			},
			instagram: {
				appId: '204596790142880',
				clientToken: '95e14bb70a7451e4068d539e6bec6182'
			},
			playspace: {
				// defaults
				storyId: '6baaf19c-1665-4546-a1fc-3fbc0657a75c',
				playerId: '8175bbba-3a5b-44f4-879d-4391862e88b9'
			},
			defaultVideoPlayer: 'aniview',
			connatixVideo: {
				// defaults
				playlistId: '08d828c6-683a-4d04-837c-64fdfa8eb008',
				playerId: 'e8dacced-b3c8-41e1-a9e2-b4c57be625f1',
			},
			aniview: {
				// defaults
				mobileTag: '60dae03fa3866e47472643b5',
				desktopTag: '60dadff0171f68029537b1e7',
				mobileCmsID: '611e592535f97e019d2eb4f2',
				desktopCmsID: '611373cb5089c408901d71d2'
			},
			ad: {
				idMap: {
					'1x1-1': '5e78f84b1c957813c16edead', // without video slider
					'1x1vs-1': '5f22d01e0db7c34a71657ec0', // with video slider
					'300x250d-1': '5e8211021c957813c16ee0ce',
					'300x250d-2': '5eba6ff033ac7c678655e414',
					'300x250d-3': '5eba701a33ac7c678655e416',
					'300x250s-1': '5e8211111c957813c16ee0d0',
					'300x250s-2': '5eba6f2433ac7c678655e410',
					'300x250s-3': '5eba6f4f33ac7c678655e412',
					'728x90d-1': '5e821127963d0e25e62b614f',

					'728x90s-1': '5e82113e9f81721e77c768df',
					'728x90s-2': '5eba70c233ac7c678655e41a',
					'728x90s-3': '5eba70da33ac7c678655e41c',
					'728x90s-4': '5eba70e033ac7c678655e41e',
					'728x90s-5': '5eba70e867200b4317949e3d',
					'728x90s-6': '5eba70f667200b4317949e3f',
					'300x50d-1': '5e821153963d0e25e62b6151', // mobile

					'300x50d-2': '5eba71a0162ee068a31bbe2c', // mobile
					'300x50d-3': '5eba71a933ac7c678655e420', // mobile

					'300x50d-4': '5eba719767200b4317949e41', // mobile
					'300x50d-5': '5eba71b8162ee068a31bbe2e', // mobile
					'728x90df-1': '5e82118b963d0e25e62b6153', // dynamic footer

					// ATF tags
					'300x50-atf': '5eba71b133ac7c678655e422', // mobile ATF
					'728x90-atf': '5eba706367200b4317949e39', // ATF
					'970x250-atf': '5eba707767200b4317949e3b' // 970x250 ATF
				},
				ampDataSlot: '/21726375739/VM_5e78f4d86a9be55c3ef22466',
				scriptOptions: {
					'data-site-id': '5e78f4d86a9be55c3ef22466'
				}
			}
		}
	]
]
```

Change the config as required for different sites.

7. In `nuxt.config.js` file add this line to build property

```
build: {
  transpile: [/@cevo\/manifold/]
}
```

8. Add the `manifold/triggerVerify` action in `nuxtServerInit` of the index.js file in the vuex store (in the GDM site). This is needed to get user and token data from cookie.

```
export const actions = {
	async nuxtServerInit({ dispatch }, context) {
		try {
			await dispatch('manifold/triggerVerify', {
				req: context.req,
				context
			})
		} catch (e) {
			// eslint-disable-next-line no-console
			console.log('nuxt server init', e)
		}
	}
}
```

9. Connect theme file with css variables to nuxt config css field

```
css: [
	'~/assets/css/manifold-theme.css'
],
```

# Common Lerna commands

We use a tool called [Lerna](https://github.com/lerna/lerna) to manage the different packages in manifold. Before starting to work with Manifold, you should be aware of a few basic commands. (You can also look up the commands in the lerna [docs](https://github.com/lerna/lerna/tree/main/commands))

## lerna bootstrap

```
yarn lerna bootstrap
```

or use the script in the main package.json

```
yarn bootstrap
```

Bootstrap the packages in the current Lerna repo. Installs all of their dependencies and links any cross-dependencies.

When run, this command will:

-   npm install all external dependencies of each package.
-   Symlink together all Lerna packages that are dependencies of each other.
-   npm run prepublish in all bootstrapped packages (unless --ignore-prepublish is passed).
-   npm run prepare in all bootstrapped packages.

## lerna add

```
yarn lerna add <package>[@version] [--dev] [--exact] [--peer]
```

Add local or remote package as dependency to packages in the current Lerna repo. Note that only a single package can be added at a time compared to yarn add or npm install.

When run, this command will:

-   Add package to each applicable package. Applicable are packages that are not package and are in scope
-   Bootstrap packages with changes to their manifest file (package.json)

If no version specifier is provided, it defaults to the latest dist-tag, just like npm install.

```
# Adds the module-1 package to the packages in the 'prefix-' prefixed folders
yarn lerna add module-1 packages/prefix-*

# Install module-1 to module-2
yarn lerna add module-1 --scope=module-2

# Install module-1 to module-2 in devDependencies
yarn lerna add module-1 --scope=module-2 --dev

# Install module-1 to module-2 in peerDependencies
yarn lerna add module-1 --scope=module-2 --peer

# Install module-1 in all modules except module-1
yarn lerna add module-1

# Install babel-core in all modules
yarn lerna add babel-core
```

# Manifold-Core

This is a nuxt module that can be configured in the nuxt.config.js file of the GDM sites. It contains the common nuxt module/plugin dependencies shared across GDM sites as well as manifold-services and manifold-vue. GDM sites should only install manifold-core to use all the sub packages within manifold. This module also registers nuxt plugins, injects global variables and copies the manifold-theme.css file to the GDM site's assets folder. Any configuration that manifold needs should be passed in through this module.

## config

Manifold-core takes in configuration for the site info used for seo, ad slots, sanity, jsonld, api keys,etc.

```
{
	hasNewURL: false,
	hideAds: true,
	categoryTerm: 'string',
	isStaging: process.env.MANIFOLD_STAGING === 'true'
	sanity: {
		projectId: 'ncavvykf',
		// dataset: 'gfes-test',
		dataset: 'gfinityesports',
		apiHost: 'https://cdn.realsport101.com'
	},
	twitterHandle: 'Gfinity',
	seo: {
		siteName: 'Gfinity Esports',
		siteURL: 'https://www.gfinityesports.com',
		siteTagline:
			'The latest gaming news, features, and tournaments',
		defaultTitle:
			'Gfinity Esports | The latest gaming news, features, and tournaments',
		defaultDescription:
			'Welcome to the home of Esports! The fastest-growing community in competitive gaming - covering news, features and tournaments.',
		defaultImage:
			'https://www.gfinityesports.com/images/gfinity-placeholder.png',
		defaultLogo:
			'https://www.gfinityesports.com/images/gfinity-logo.png'
	},
	jsonld: {
		sameAs: [
			'https://www.facebook.com/GfinityRocketLeague',
			'https://www.facebook.com/GfinityFGC',
			'https://www.facebook.com/GfinityEsports/',
			'https://www.facebook.com/GfinityFIFA',
			'https://www.instagram.com/gfinity/',
			'https://twitter.com/Gfinity',
			'https://www.tiktok.com/@gfinity',
			'https://www.youtube.com/user/GfinityTv'
		]
	},
	instagram: {
		appId: '204596790142880',
		clientToken: '95e14bb70a7451e4068d539e6bec6182'
	},
	playspace: {
		// defaults
		storyId: '6baaf19c-1665-4546-a1fc-3fbc0657a75c',
		playerId: '8175bbba-3a5b-44f4-879d-4391862e88b9'
	},
	defaultVideoPlayer: 'aniview',
	connatixVideo: {
		// defaults
		playlistId: '08d828c6-683a-4d04-837c-64fdfa8eb008',
		playerId: 'e8dacced-b3c8-41e1-a9e2-b4c57be625f1'
	},
	aniview: {
		// defaults

		mobileTag: '60dae03fa3866e47472643b5',
		desktopTag: '60dadff0171f68029537b1e7',
		mobileCmsID: '611e592535f97e019d2eb4f2',
		desktopCmsID: '611373cb5089c408901d71d2'
	},
	ad: {
		idMap: {
			'1x1-1': '5e78f84b1c957813c16edead', // without video slider
			'1x1vs-1': '5f22d01e0db7c34a71657ec0', // with video slider
			'300x250d-1': '5e8211021c957813c16ee0ce',
			'300x250d-2': '5eba6ff033ac7c678655e414',
			'300x250d-3': '5eba701a33ac7c678655e416',
			'300x250s-1': '5e8211111c957813c16ee0d0',
			'300x250s-2': '5eba6f2433ac7c678655e410',
			'300x250s-3': '5eba6f4f33ac7c678655e412',
			'728x90d-1': '5e821127963d0e25e62b614f',

			'728x90s-1': '5e82113e9f81721e77c768df',
			'728x90s-2': '5eba70c233ac7c678655e41a',
			'728x90s-3': '5eba70da33ac7c678655e41c',
			'728x90s-4': '5eba70e033ac7c678655e41e',
			'728x90s-5': '5eba70e867200b4317949e3d',
			'728x90s-6': '5eba70f667200b4317949e3f',
			'300x50d-1': '5e821153963d0e25e62b6151', // mobile

			'300x50d-2': '5eba71a0162ee068a31bbe2c', // mobile
			'300x50d-3': '5eba71a933ac7c678655e420', // mobile

			'300x50d-4': '5eba719767200b4317949e41', // mobile
			'300x50d-5': '5eba71b8162ee068a31bbe2e', // mobile
			'728x90df-1': '5e82118b963d0e25e62b6153', // dynamic footer

			// ATF tags
			'300x50-atf': '5eba71b133ac7c678655e422', // mobile ATF
			'728x90-atf': '5eba706367200b4317949e39', // ATF
			'970x250-atf': '5eba707767200b4317949e3b' // 970x250 ATF
		},
		ampDataSlot: '/21726375739/VM_5e78f4d86a9be55c3ef22466',
		scriptOptions: {
			'data-site-id': '5e78f4d86a9be55c3ef22466'
		}
	}
}
```

The config options should be defined in the manifoldConfigOption variable in the index.js file

```
const manifoldConfigOptions = [
  // sanity object props
  //   "projectId",
  //   "dataset",
  //   "apiHost",
  "sanity",

  // seo object props
  //   "siteName",
  //   "siteTagline",
  //   "defaultTitle",
  //   "defaultDescription",
  //   "defaultImage",
  //   "siteURL",
  "seo",

  // JSONLD object props
  //   "sameAs",
  "jsonld",

  // instagram onject props
  //   "appId",
  //   "clientToken",
  "instagram",

  // connatix playspace defaults
  // { storyId, playerId }
  "playspace",

  // connatix video defaults
  // { playlistId, playerId }
  "connatixVideo",

  // aniview video defaults
  // { mobileTag, desktopTag, mobileCmsID, desktopCmsID }
  "aniview",

  // ad object props
  //   idMap
  // ampDataSlot:
  // scriptOptions
  "ad",
  // connatix or aniview
  "defaultVideoPlayer",
  ...moduleDependencies,
];
```

## Nuxt Module Dependencies

Manifold Core adds adds a few shared nuxt modules used across the GDM sites. To add a new nuxt dependency using manifold-core, you need to install the dependency into manifold-core and then add it to the moduleDependencies variable in the index.js file.

```
const moduleDependencies = [
  "@nuxtjs/amp",
  "@nuxtjs/device",
  "@nuxtjs/feed",
  "@nuxtjs/gtm",
  "@nuxtjs/redirect-module",
  "@nuxtjs/sitemap",
  "nuxt-basic-auth-module",
  "vue-scrollto/nuxt",
  "@nuxtjs/dayjs",
  "@nuxtjs/speedcurve",
];
```

## Folder Structure

```
📦 manifold-core
 ┣ 📂 plugins - here we keep all the nuxt.js plugins
 ┃ ┣ 📜 ad-plugin-setup.js
 ┃ ┣ 📜 filters.js
 ┃ ┣ 📜 jsonld.js
 ┃ ┣ 📜 localStorageWithExpiry.js
 ┃ ┣ 📜 manifold.js
 ┃ ┣ 📜 sanity-block-content.js
 ┃ ┣ 📜 vue-notification.js
 ┃ ┣ 📜 vue-observe-visibility.js
 ┃ ┗ 📜 vuelidate.js
 ┣ 📜 .gitignore
 ┣ 📜 CHANGELOG.md - here you can read about versions and changes
 ┣ 📜 index.js - main Nuxt Module file
 ┗ 📜 package.json
```

# Manifold-Services

This package is created to manage the services used by the GDM sites. It consists of sanity services which fetch data from sanity, the models for the sanity documents, the sanity queries and an authentication service. It's built using TypeScript and scaffolded using [tsdx](https://tsdx.io/).

## Folder Structure

```
📦manifold-services
 ┣ 📂src
 ┃ ┣ 📂api
 ┃ ┃ ┣ 📂interceptors
 ┃ ┃ ┃ ┣ 📜bearer-token-interceptor.ts
 ┃ ┃ ┃ ┣ 📜error-interceptor.ts
 ┃ ┃ ┃ ┗ 📜json-api-type-cast-interceptor.ts
 ┃ ┃ ┣ 📂modules
 ┃ ┃ ┃ ┗ 📜Authentication.ts
 ┃ ┃ ┣ 📜ApiError.ts
 ┃ ┃ ┣ 📜ApiService.ts
 ┃ ┃ ┣ 📜ApiTypes.ts
 ┃ ┃ ┣ 📜Payload.ts
 ┃ ┃ ┣ 📜axios.ts
 ┃ ┃ ┗ 📜type.ts
 ┃ ┣ 📂models
 ┃ ┃ ┣ 📜Article.ts
 ┃ ┃ ┣ 📜Author.ts
 ┃ ┃ ┣ 📜Category.ts
 ┃ ┃ ┣ 📜FeaturedArticle.ts
 ┃ ┃ ┣ 📜Page.ts
 ┃ ┃ ┣ 📜PageLink.ts
 ┃ ┃ ┣ 📜PromotedArticle.ts
 ┃ ┃ ┣ 📜Schema.ts
 ┃ ┃ ┣ 📜SeoTools.ts
 ┃ ┃ ┗ 📜Settings.ts
 ┃ ┣ 📂utils
 ┃ ┃ ┣ 📜DeferredPromise.ts
 ┃ ┃ ┗ 📜helpers.ts
 ┃ ┣ 📜ArticleService.ts
 ┃ ┣ 📜CategoryService.ts
 ┃ ┣ 📜ImageService.ts
 ┃ ┣ 📜PageService.ts
 ┃ ┣ 📜SanityService.ts
 ┃ ┣ 📜SettingsService.ts
 ┃ ┗ 📜index.ts - main file which exports all services
 ┣ 📂test
 ┃ ┗ 📜blah.test.ts
 ┣ 📜.gitignore
 ┣ 📜CHANGELOG.md
 ┣ 📜LICENSE
 ┣ 📜README.md
 ┣ 📜message.js
 ┣ 📜package.json
 ┣ 📜sanity-codegen.config.ts
 ┣ 📜tsconfig.json
 ┗ 📜yarn-error.log
```

## Organizing queries

We're in the process from migrating away from a query builder and query director approach for handling the sanity queries. Depending on the size of the queries it should either be include inline like this

```
	async getTeamMembers() {
		const teamMembersQuery = groq`
		*[_type=='siteSettings'
				&& !(id in path('drafts.**'))]
				{
					teamMembers[]->
				}[0]
		`
		const teamMembers = await this.sanityService.fetch<{
			teamMembers: AuthorSchema[]
		}>(teamMembersQuery)

		return teamMembers
	}
```

or be imported from a .groq.ts file like the articleQueries.groq.ts file. We're using the groq package which provides syntax highlighting and the ability to try out the queries from inside vs code using the sanity.io extension. You just need to temporarily replace any variables inside the queries with hardcoded values for testing and click on the execute button that's shown on top of the query.

## Data Models

We're using the [sanity-codegen](https://github.com/ricokahler/sanity-codegen) package to generate typescript definitions from our sanity schema. We use those generated types as the interface for our data models and then add extra fields to make accessing data easier.

```
import { Article as ArticleSchema, Category as CategorySchema } from './Schema'
import { ImageService } from './../ImageService'
const imageService: ImageService = new ImageService()

export class Article implements ArticleSchema {
	_id = ''
	disableIndexing = false
	enableAMP = false
	disableEcommerce = false
	category: CategorySchema
	categories: CategorySchema[] = []
	excerpt = ''
	publishedAt = ''
	author = {}
	featuredImage = {}
	updatedAt = ''
	clickbaitTitle = ''
	articleTitle = ''
	seoDescription = ''
	categoryID = ''
	canonicalUrl = ''
	tags = ''
	sections: string[] = []
	thumbnail = ''

	title: string
	slugUrl: string

	_createdAt: string = ''
	_rev: string = ''
	_updatedAt: string = ''
	_type: 'article' = 'article'
	data: any

	constructor(article: ArticleSchema) {
		const allCategories = <CategorySchema[]>(
			(<unknown>article?.data?.category)
		)
		this.slugUrl = article.data?.slug?.current || ''
		this.title = article.data?.title || article.data?.seo?.seo_title || ''

		this._id = article._id
		this.categories = <CategorySchema[]>(<unknown>article?.data?.category)
		this.category = <CategorySchema>(<unknown>article?.data?.category?.[0])
		this.disableIndexing =
			article?.data?.disableIndexing || this.disableIndexing
		this.enableAMP = article?.data?.enableAMP || this.enableAMP
		this.disableEcommerce =
			article?.data?.disableEcommerce || this.disableEcommerce
		this.excerpt = article?.data?.excerpt || this.excerpt
		this.publishedAt = article?.data?.publishedAt || this.publishedAt
		this.author = article?.data?.author || this.author
		this.featuredImage = article?.data?.featuredImage || this.featuredImage
		this.updatedAt = article?._updatedAt || this.updatedAt
		this._type = article?._type || this._type
		this._createdAt = article?._createdAt || this._createdAt
		this._updatedAt = article?._updatedAt || this._updatedAt
		this._rev = article?._rev || this._rev
		this.clickbaitTitle =
			article?.data?.clickbaitTitle ||
			article?.data?.title ||
			this.clickbaitTitle
		this.articleTitle =
			article?.data?.seo?.seo_title ||
			article?.data?.title ||
			this.articleTitle
		this.seoDescription =
			article?.data?.seo?.meta_description || this.excerpt
		this.categoryID = allCategories?.[0]?._id || this.categoryID
		this.canonicalUrl = `${allCategories?.[0]?.data?.slug?.current ||
			'misc'}/${article?.data?.slug?.current}/`

		const parentSlug = (this.category?.data?.category as any)?.data?.slug
			?.current

		if (parentSlug) {
			this.canonicalUrl = `${parentSlug}/${this.canonicalUrl}`
		}

		this.tags = article?.data?.tags?.length
			? article.data.tags.join(',')
			: this.tags
		this.sections = allCategories?.length
			? allCategories.map(
					(item: CategorySchema) => item?.data?.title || ''
			  )
			: this.sections

		this._id = article._id
		this._createdAt = article._createdAt
		this._updatedAt = article._updatedAt
		this._rev = article._rev
		this._type = article._type
		this.data = article.data

		if (imageService) {
			this.thumbnail =
				imageService
					.getImageBuilder(this.featuredImage)!
					.width(700)
					.height(394)
					.url() || this.thumbnail
		}
	}
}
```

### Object.assign hack

You'll notice that whenever we're creating a new instance of a data model, we're using Object.assign to create a new copy. This is to avoid warnings from NUXT regarding object serialization during SSR.

```
return Object.assign(
	{},
	new Article(result.mainPromotedArticle)
)
```

## Scripts

-   `start` : watch change in package
-   `build` : build services
-   `test` : test
-   `lint` : run eslint test
-   `prepare` : build services
-   `size` : calculate size
-   `analyze` : analyze size
-   `generate:types` : generate types from sanity

To work with Manifold services, you can use commands to rebuild the package after changes to the services:

```
$ yarn manifold-services:start
$ yarn manifold-services:build
```

## GfinityAPI

To interact with `GfinityAPI` we created `ApiService`. It built using singletone pattern and in constructor sets interceptors and modules. For now we have only `Authentication` module. It manage everything related user requests (login, registration, password reset, user preferences). Basically this is a copy of `GfinityAPI` but forged to use in data-components. Plans for future is to integrate `GfinityAPI` more closely with `Manifold`.

# Manifold-Vue

Manifold-Vue contains all the UI components, data loader components, mixins, vuex store and vue plugins. We also use [storybook](https://storybook.js.org/) for documenting of our components (more details in section about `StoryBook`) and [Chromatic](https://www.chromatic.com) for UI regression testing.

## Folder Structure

```
📦manifold-vue
 ┣ 📂config
 ┃ ┗ 📂storybook
 ┃ ┃ ┣ 📂fonts
 ┃ ┃ ┃ ┗ 📂fort-awesome
 ┃ ┃ ┃ ┃ ┣ 📂scss
 ┃ ┃ ┃ ┃ ┃ ┣ 📜mixins.scss
 ┃ ┃ ┃ ┃ ┃ ┗ 📜variables.scss
 ┃ ┃ ┃ ┃ ┗ 📜embedded-woff2.css
 ┃ ┃ ┣ 📂scss
 ┃ ┃ ┃ ┣ 📂base
 ┃ ┃ ┃ ┣ 📂components
 ┃ ┃ ┃ ┣ 📂settings
 ┃ ┃ ┃ ┣ 📂tools
 ┃ ┃ ┃ ┣ 📂utils
 ┃ ┃ ┃ ┣ 📜style.amp.scss
 ┃ ┃ ┃ ┗ 📜style.scss
 ┃ ┃ ┣ 📜main.js
 ┃ ┃ ┣ 📜preview-head.html
 ┃ ┃ ┗ 📜preview.js
 ┣ 📂src
 ┃ ┣ 📂assets
 ┃ ┃ ┣ 📜manifold-theme.css
 ┃ ┃ ┗ 📜tailwind.css
 ┃ ┣ 📂components
 ┃ ┃ ┣ 📂account
 ┃ ┃ ┣ 📂ad-components
 ┃ ┃ ┣ 📂app-footer
 ┃ ┃ ┣ 📂app-header
 ┃ ┃ ┣ 📂app-header-bar
 ┃ ┃ ┣ 📂app-menu
 ┃ ┃ ┣ 📂article-author
 ┃ ┃ ┣ 📂article-featured-list
 ┃ ┃ ┣ 📂article-full
 ┃ ┃ ┣ 📂article-info
 ┃ ┃ ┣ 📂article-jumper
 ┃ ┃ ┣ 📂article-network
 ┃ ┃ ┣ 📂avatar
 ┃ ┃ ┣ 📂avatar-editor
 ┃ ┃ ┣ 📂base-modal
 ┃ ┃ ┣ 📂base-switcher
 ┃ ┃ ┣ 📂dropdown
 ┃ ┃ ┣ 📂form
 ┃ ┃ ┃ ┣ 📂vue-select
 ┃ ┃ ┃ ┃ ┣ 📂global
 ┃ ┃ ┃ ┃ ┣ 📂modules
 ┃ ┃ ┣ 📂grid-layout
 ┃ ┃ ┣ 📂hamburger
 ┃ ┃ ┣ 📂header-dropdown
 ┃ ┃ ┣ 📂icons
 ┃ ┃ ┣ 📂image-gallery
 ┃ ┃ ┣ 📂image-gallery-modal
 ┃ ┃ ┣ 📂img-container
 ┃ ┃ ┣ 📂infinite-loader
 ┃ ┃ ┣ 📂language-switcher
 ┃ ┃ ┣ 📂loader
 ┃ ┃ ┣ 📂manifold-notifications
 ┃ ┃ ┣ 📂menu-button
 ┃ ┃ ┣ 📂menu-button-text
 ┃ ┃ ┣ 📂menu-logo
 ┃ ┃ ┣ 📂overlay
 ┃ ┃ ┣ 📂profile
 ┃ ┃ ┣ 📂sanity-image
 ┃ ┃ ┣ 📂serializers
 ┃ ┃ ┣ 📂site-badge
 ┃ ┃ ┣ 📂skeleton
 ┃ ┃ ┣ 📂spinner
 ┃ ┃ ┗ 📂title-text
 ┃ ┣ 📂data-components
 ┃ ┣ 📂mixins
 ┃ ┣ 📂mocs
 ┃ ┣ 📂plugins
 ┃ ┣ 📂store
 ┃ ┃ ┣ 📂modules
 ┃ ┃ ┃ ┗ 📜user.js
 ┃ ┃ ┗ 📜index.js
 ┃ ┗ 📜index.js
 ┣ 📂static
 ┃ ┣ 📂images
 ┣ 📜.browserslistrc
 ┣ 📜.eslintignore
 ┣ 📜.eslintrc.js
 ┣ 📜.gitignore
 ┣ 📜.prettierrc
 ┣ 📜CHANGELOG.md
 ┣ 📜README.md
 ┣ 📜babel.config.js
 ┣ 📜build-storybook.log
 ┣ 📜jsconfig.json
 ┣ 📜package.json
 ┣ 📜postcss.config.js
 ┗ 📜tailwind.config.js
```

## Dumb Components

All the dumb UI components should be in the components folder of manifold-vue inside their own folder that has the vue, scss and stories file. We shouldn't call out to any APIs here, the logic should be simple as possible with the UI component just receiving some props and displaying a template with a few methods/computed props if necessary.

## Data components

Data components are wrappers to provide data and methods to other components. They follow the [renderless components pattern](https://adamwathan.me/renderless-components-in-vuejs/). We use them as a simple vuex replacement for some shared state in a component tree and to load data from the manifold-services.

## Links

We should use nuxt-links for all page links. We also need to ensure that all the links **don't have duplicates** so that there are no duplicate page links that google has to crawl. For example, google treats these URLs as different URLs

-   https://www.gfinityesports.com/fortnite/fortnite-updates
-   https://www.gfinityesports.com/fortnite/fortnite-updates/

For Realsport & Gfinityesports were opting for a trailing slash approach but this will be changed to a non-trailing slash approach soon because it makes writing redirects simpler.

We use non-trailing slash URLs on Epicstream.

**Note:** Whenever you create or render a URL, you should use the linkMixin and then use the mixin's linkFormatter method, this will ensure the link uses the correct format so you don't have to worry about the format yourself

## Serializers and Injection

We're using the [sanity-blocks-vue-component](https://www.sanity.io/plugins/portable-text-to-vue) package to render sanity embeds as vue components. All the components inside the serializers folder represent the embeds that are used in the sanity cms.

We are also using the `injector-mixin` in manifold-vue to inject custom components/markup into the sanity block components.
How does this works ? In `injector-mixin` we have access to all data because mixin is attached to `article-full` component. From there the `block-content` component gets `filteredBody` computed property which filters based on `injectedBody` computed property. `InjectedBody` is body which we get from sanity + our injections into it. We manually adding or removing blocks into body based on algorithms. Easiest example is `injectCTAMobileEmbed` function, which basically just injects block in middle of 2nd article in Infinite Scroll.

```
{
	index: Math.floor(this.article.data.body.length / 2),
	_type: 'fetchCTAEmbed',
	excludeId: this.article._id,
	categoryId
}
```

This is how injection looks like. First we specify index where block will be injected (the `inject` function is taking care of it) then very important is `_type`. Setting type to `fetchCTAEmbed` means what when `block-content` going to render body and meet this type of block it will go to serializers and pick specific component for it. This way we can manage rendering part of block from sanity or out manual injection. Other properties is just data which will be visible in rendering component as props. You can check `lazy-load-serializer.vue` file to see which component is assigned to which type of block.

Then let's talk about more complex injection algorithm, function called `injectAds`. This is default parameters of the function:

-   starOffset (default: 0) - how much block should algorithm skip from start before placing ads.
-   endOffset (default: 0) - the same as `startOffset` but count blocks from end.
-   threshold (default: 0) - how much blocks should be skipped between ads injections.
-   fluid (default: false) - If true will pass fluid property to `ad` component.

Algorithm will loop throw body and start counting `valid` block (of type `title` and `p`). If all blocks are valid it will place `text ad` as soon as it satisfy all conditions (all condition you can check in functions like `isValidLongAd`, `isValidTextAd`, etc). If check for text ad is not passed and previous element is listItem it will try to inject long ad. When it finds not valid block it will try to place `long ad` if it satisfy all conditions. After injecting any ad, all counters will be reset. Also algorithm counts media blocks (function `isValidMedia`) and places ad every 2 media blocks in row. Main idea is:

-   place text ad after 3 blocks (not list and not after titles).
-   place long ad after long lists, and not valid blocks.
-   place text ad between many pictures in a row or video.

This algorithm should inject ads evenly throw the article so every screen or two should have ad in it. The main problem is what articles don't have templates and can be very different from one another. Article may have many embeds, video players, other ads.

### `Warning !`

Changing something in injector-mixin should be done carefully since this is global for every article and may cause bugs (which is very hard to debug) and performance issues.

## Auth

For authentication we use vuex store with user module, on server side method `triggerVerify` is triggered which sets user and token data from token. For this to work we need to fire this action in `nuxtServerInit` hook in project where we are using the `manifold-core` package (described in installation chapter)

## Storybook

-   For previewing `manifold-vue` components we use [storybook](https://storybook.js.org/).

Storybook helps us to develop reusable components and test them easily by passing hardcoded props. We can test edge cases and see how they will behave in production. We also have a design tab where we can connect the figma designs for the components to the stories file. You can learn how to connect the designs [here](https://pocka.github.io/storybook-addon-designs/?path=/docs/docs-figma-examples--embed-file). We also have an accessibility tab that does some basic accessibility tests. You should make sure all the tests in that tab are passing.

To launch the storybook sever use:

```
yarn manifold-vue:storybook
```

## Styling and Theming

### styling

For styling we use scss and [tailwind](https://tailwindcss.com/). We use [BEM](http://getbem.com/introduction/) for naming our classes and then use the `@apply` tailwind directive in the scss file to use the tailwind style. If a tailwind class is available for a property then we should use that, otherwise we use regular css declarations. We also use [stylelint](https://stylelint.io/) for linting the styles and the [prettier extenstion](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) with the [headwind extenstion](https://marketplace.visualstudio.com/items?itemName=heybourn.headwind) for auto-formatting the styles.

### theming

When manifold-core is used by a GDM site, it copies a file with the manifold theme (list of CSS variables) to the assets folder. There you can find all css variables for theming. For overwriting it you can change variables in a scss file named `manifold-overrides.scss` in the GDM site. Example:

```css
// manifold-overrides.scss
:root {
	--manifold-color-brand-primary: #e62932;
}
```

Too use the Manifold tailwind config with GDM projects, we need to import it in the site's `tailwind.config.js` file.

```js
cconst manifoldTailwindConfig = require('@cevo/manifold-vue/tailwind.config')

module.exports = manifoldTailwindConfig
```

To add a new manifold theme variable, you need to edit the `manifold-theme.css` file inside manifold-vue. Make sure to also add the variable to the `tailwind.config.js` file in manifold-vue.

## scripts

-   `serve`: launch server
-   `build`: builds manifold-vue into `manifold-components`
-   `lint`: check project with linter
-   `storybook-build`: building storybook
-   `storybook:serve`: launch storybook dev server

# Committing to Manifold

For committing we use `Conventional commits` (https://www.conventionalcommits.org/en/v1.0.0/). For ease of use, you can install the [extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits). All the data from conventional commits are picked up for automating the package releases and generating the changelog.

# Publishing packages

Publishing packages is automated after merging to master. Normally we send PRs to a release branch, for example `release/3.5` and then once all the PRs are reviewed and tested, we merge the PRs into the release branch and then merge the release branch into master.

Lerna only bumps the packages that have been changed and does a patch/minor/major release depending on the conventional commits for the release.

# Related Docs

We're using a bunch of technology to power manifold so these docs should be helpful in working with them

-   [Sanity](https://www.sanity.io/docs/getting-started)
-   [Sanity Queries Cheat Sheet](https://www.sanity.io/docs/query-cheat-sheet)
-   [Storybook](https://storybook.js.org/docs/vue/get-started/introduction)
-   [Lerna](https://github.com/lerna/lerna)
-   [Yarn workspaces](https://classic.yarnpkg.com/en/docs/workspaces/)
-   [Tsdx](https://tsdx.io/)
-   [Nuxt](https://nuxtjs.org/docs/2.x/get-started/installation)
-   [Tailwind](https://tailwindcss.com/)
-   [Typescript](https://www.typescriptlang.org/docs/)
-   [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/)
-   [Docsify](https://docsify.js.org)
-   [Stylelint](https://stylelint.io/)
-   [Eslint](https://eslint.org/)
-   [Prettier](https://prettier.io/)
