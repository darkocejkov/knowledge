> https://www.darkocejkov.ca

---

> Exploring advanced React  + webdev topics to create and deliver a beautiful - but more importantly - functional and responsive portfolio.
> Complete with my personal touch with design.

<table>
	<tr>
		<td>
			<a>Figma</a>
		</td>
		<td>
			<a>Lucid</a>
		</td>
	</tr>
</table>

# Scope + Features

1. Marquee banner to display status text
2. Ability to change between views
	1. Portfolio View
	2. Note Repository view
3. Background "sketch" layer behind Hero text
4.  Component control bar
	1. Show/Hide hero text
	2. Show/Hide sketch
	3. Back/Front sketch
	4. next/previous/play/pause sketch
	5. Sketch environment controls
		1. `tweakpane`
5. Offcanvas component to display extra information
	1. GitHub commits for `darkocejkov` project
	2. GitHub global calendar view
6. Draggable components
	1. Hero text drag elastically
	2. Glass pane ability to re-order 
8. Display OR download resume
9. Composed Component Grid
		1. Re-factoring and re-branding of **REDACTED** components to include as "portfolio" ^[re-creating visuals and function from scratch, without pre-made components from packages]
10. Integrating dynamic markdown notes from `knowledge` repo.
11. Scrollspy for anchor menu
12. Scroll-based animations
	1. Scroll completion
13. Draggable card window
14. Custom tooltips
15. Responsive flex-based layout
17. Sketch Concepts
	1. Reaction-Diffusion
		1. reacts to cursor
		2. ability to upload images
		3. pre-defined pattern with integrated randomness
	2. Raining Objects
		1. Various 3D models, raining from the top
	3. Create objects from other objects
		1. Draw name using small sub-objects

## Hosting & Delivery
> the DevOps aspect of delivering and serving files is done through AWS, a more involved approach than Netlify, but much more expandable. Currently hosted through AWS Amplify, which provides:
> - WebHooks to git repo to automatically grab, build, and deploy latest version
> - Ability to create branches based on git tree structure
> - Option to include a backend server easily

## Additional Flavour
> Creating illustration-based animations (gifs) based on namesake

> [!hot] Legacy ]
> based on spacejam.com, old geocities/retro type

> [!hot] touchdesigner
> [touchdesigner + three.js](https://www.youtube.com/watch?v=lCyILpkPQ4g)

## Bugs

#### Mobile
- When using anchor buttons, label stays shown (because its not hover, its tap)
- No "close" button on offcanvas, so mobile cannot close.

# High-level Goals
1. Achieve a high-level of visual interest in terms of animations and component interaction
2. Have a performant, but also stunning visual website
3. Maintaining a small component footprint, meaning that I use almost NO component libraries
	1. bootstrap / tailwindcomponents / antd / etc.
	2. All components to be created *myself*
4. Display key traits about myself, my education, my experience, and projects
5. Build an expandable codebase that is dynamic and allows for efficient and logical abstraction of components
	1. this means that we don't need to constantly copy+paste boilerplate over and over
6. Be able to have accessible areas (pages/views/components) to play around with new concepts
	1. 2D and 3D rendering, typography, animation, state updating, etc.

