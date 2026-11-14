# Component architecture / composition method — how a mature Figma component library (a wireframe-kit-style system with ~Buttons, Form Elements, Text Inputs, Cards pages) decomposes UI into atoms, molecules and organisms; how it splits variant-bearing components from static ones; and its naming/namespacing conventions. (Token *values* — palette, fonts, radii — could not be resolved: the variable/context/screenshot tools require a live in-Figma selection and the page nodes expose no renderable bounds via the API. This output is the construction logic only, which is what was requested.)

_Confidence: high_

**Portable vs discard:** Portable: the whole COMPOSITION RECIPE — named base atoms, atom→'group'→organism naming ladder, variant-sets-only-where-an-axis-exists, families of specialized siblings over mega-components, states-as-axes, parallel density libraries, path+category taxonomy, and per-component usage docs. Discard: this source's concrete token values, palette, type, the 'paper/wireframe' aesthetic, and its exact component roster — those are the dish, not the recipe.

## Method principles

- **Designate explicit BASE atoms and tag them in the name (e.g. a 'Cell (Base)' marked '(Base)'). The base is a single low-level unit that higher-order structures (rows, tables, lists) instance repeatedly rather than redrawing. One edit to the base propagates everywhere.**
  - *Why:* A named, single-source base atom makes reuse visible and enforceable. Consumers and contributors can see which element is the canonical primitive, so composites stay consistent and maintenance is one-to-many instead of many-to-many.

- **Encode the composition ladder in the NAME via suffixes: an atom keeps the bare noun ('Field'), its composed molecule appends a role word ('Field group'). The group bundles the atom with its satellites (label, helper/validation text, affordances) into one placeable unit.**
  - *Why:* A naming convention that mirrors the atom→molecule→organism ladder lets anyone infer altitude from the name alone, and signals the intended unit of reuse (drop the 'group', not the raw atom) without reading structure.

- **Reserve variant SETS (multi-variant component sets) for elements that genuinely have a state or kind axis (interactive controls, cells with default/header/selectable modes); keep elements with no real axis as plain single components (a static card, a decorative/icon glyph). Do not wrap every element in a set.**
  - *Why:* Matching the container type to whether variation actually exists keeps the variant matrix meaningful. Spurious single-variant sets add property noise; genuine axes get a clean, discoverable property picker.

- **Prefer a FAMILY of specialized sibling components over one mega-component with an exploding variant matrix. A button need isn't one set with 40 combinations but a family: the generic action button, an icon-only button, a filter button, a floating action button, a selectable (radio) item — each its own component/set scoped to one job.**
  - *Why:* Splitting by job keeps each component's variant axes small and orthogonal (size × state, not size × state × shape × content-type × role). Smaller matrices are easier to test, document, and keep visually coherent, and each sibling can expose only the props it truly needs.

- **State and kind live as explicit variant AXES on the set (default / hover / disabled / error, and kind axes like header-label / selectable), never as separate ad-hoc duplicates. Interaction states are properties of one component, not forked copies.**
  - *Why:* Modeling states as axes of a single set guarantees every state shares geometry and tokens and stays in lockstep; it also makes the full state inventory inspectable in one place, so missing states (no disabled, no error) are obvious.

- **Ship PARALLEL libraries at different densities with identical component names (a full kit and a 'Mini' kit sharing the same taxonomy). Scale/density is a library-level choice, not yet another variant inside each component.**
  - *Why:* Hoisting density to the library level keeps individual components simple and lets a whole project switch scale by swapping the subscribed library, while identical names make swapping lossless and predictable.

- **Organize the library in a strict path taxonomy — design_system / <library> / components / <Name> — and sub-namespace catalog-like items with a category prefix (Finance/…, Tech & Media/…, Objects & Things/…). Group the editor PAGES by UI function with a stable marker glyph (Buttons & Actions, Form Elements, Text Inputs & Fields, Content Cards & Items).**
  - *Why:* A deterministic path plus functional page grouping makes components findable by two independent routes (browse-by-function and search-by-path), and category prefixes keep large icon/asset sets from flooding the flat namespace.

- **Attach a one-line USAGE description to every component stating what it is and when to use it ('used to represent an action…', 'allows the user to select one or more options…').**
  - *Why:* Embedded intent docs turn the library into a self-describing API: consumers pick the right component without a separate spec, and the description doubles as the contract a redesign must preserve.


## Anti-slop rules learned here

- Don't build one monolithic 'Button' (or 'Input', 'Card') component with a sprawling variant matrix trying to cover every shape, content type, and role — that's the tell of an unplanned system. Split into named siblings scoped to one job each.

- Don't fork a component per interaction state ('Button Hover', 'Button Disabled' as separate components). States are variant axes of one set; separate copies drift apart immediately.

- Don't leave the base primitive anonymous or buried. If a cell/row/item is reused everywhere, name it explicitly as the base and instance it — never copy-paste the primitive into each composite.

- Don't bake density/scale into every component as an extra variant when a parallel 'compact' library expresses it once at the library level.

- Don't dump components into a flat namespace. Use the path taxonomy and category prefixes; functional, consistently-marked pages — not a single 'Components' junk drawer.

- Don't ship components without usage descriptions. An undocumented component forces consumers to reverse-engineer intent and invites misuse.

- Don't conflate an atom with its labeled molecule. Keep the bare field separate from the 'field group' (label + field + helper) so each can be reused at the right altitude.

- Don't wrap single-state elements in a variant set for symmetry's sake — a static card or an icon glyph with no real axis should stay a plain component.
