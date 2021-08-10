---
layout: programming_post
title: "A Better Amethyst Documentation"
date_published: 2021-07-30
updated: false
published: false
---
This documentation is for [beta Amethyst (rev. 6d0e7aaf58a4d1483b902f63920044eabb865c92)][beta-amethyst] on Rust `nightly-2021-07-29`.

1.
{:toc}

# Github Crate Structure

The Amethyst structure is very confusing. Not all components of amethyst are in the same crate, nor even the same repository, which makes the documentation hard to navigate.

In general, `amethyst::<crate>` is the crate in the subdirectory `amethyst_crate` in the main [amethyst repository].

There are many exceptions. The ECS library is a reexport of the external [Legion crate] as well as the local dispatcher module.

# Entity Component System

The entity component system documentation is way outdated, as the documentation uses the prior ECS crate [Specs] whereas the current unstable version uses [Legion][Legion crate].

Some major differences between Specs and Legion are:

## Entities and Components

### Creation

 - Entities are created with `World::push<T>(&mut self, components: T) -> Entity`[][World::push] where `components` essentially implements `IntoIter<Component>` <br/> (actually `Option<T>: IntoComponentSource`).
   - There is also the `World::extend<U>(&mut self, components_array: U) -> &[Entity]`[][World::extend] where `components_array` is an array of sets of components (actually `U: IntoComponentSource`), which may be used if all entities are **[archetypes][Archetype]** of one another (that is, they share the same components).
 - A component is *any* type (including primitives) and is identified by its type. It does not have to implement the `Component` trait, and hence the storage is decided for you.

### Access

 - Components of an entity may be accessed and modified through the `Entry`[][Entry] struct returned from `World::entry(&mut self, entity: Entity) -> Option<Entry>`[][World::Entry]. NB: This is less efficient than the next method.
   - A single component can be retrieved via `Entry::get_component<T: Component>(&self) -> Result<T>` or its [mutable][Entry::get_component_mut] or [unchecked][Entry::get_component_unchecked] counterparts. There are also consuming methods for each (`into_...` instead of `get_...`).
 - Entities of certain components may be retrieved with the `<T: IntoQuery>::query() -> Query<T, EntityFilter>`[][<>::query] where `IntoQuery` specifies the component(s) and mutability. For example
   1. `<&Position>::query()` retrieves the immutable positions of all applicable entities
   2. `<&mut Position>::query()` retrieves the mutable positions of all applicable entities
   3. `<(&Position, &Velocity)>::query()` retrieves the immutable positions and velocities of all applicable entities.
   4. `<(&mut Position, &Velocity)>::query()` retrieves the mutable positions and immutable velocities of all applicable entities
 - Queries can be filtered via `Query::filter(self, filter: T) -> Query`[][Query::filter] where the filter is `component<T: Component>()`s[][component] combined via bitwise operators (eg. `query.filter(!component::<Acceleration>())` or `query.filter(component::<Ally>() & !component::<Medic>())`). This is more versatile and presumably more efficient than querying for a value and then discarding it (eg. `for (_, pos) in <(&Player, &mut Position)>::query().iter_mut(world) {...}`)
   - There are also the `Any`[][Any] filter
 - Queries can be iterated and accessed in [many ways][query iteration], most notably through `Query::iter(&mut self, world: &World)`[][Query::iter], `Query::iter_mut(&mut self, world: &mut World)`[][Query::iter_mut], which both iterate in-order tuples of the components, and the functional `Query::for_each(&mut self, world: &World, f: FnMut)`[][Query::for_each] and `Query::for_each_mut(&mut self, world: &mut World, f: FnMut)`[][Query::for_each_mut].

### Command Buffer

 - A `CommandBuffer`[][CommandBuffer] can be used to modify the world by queueing commands like `push` or `exec`. It allows syncronization between systems.

## State

 - There are two types of state
   1. Local State, which is local to a system
   2. Global State, which can be accessed across systems and are called resources

## Systems

 - There are two ways to make systems
   1. Attributing a function with the `#[system]`[][system macro] procedure macro (This does not work with Amethyst, but rewriting the [system proc macro][system macro rewrite] fixes it). For a function `function`, the procedure macro creates the system `function_system` based on other attribute macros. The `function_system` takes in arguments for the initial state.
   2. Building a system manually with the `SystemBuilder`[][SystemBuilder] struct

### Method 1

#### Entity and Component Access and Modification

 - Systems can access a SubWorld as an optional argument: `fn system(world: &mut SubWorld, ...)`
 - Systems can access components in multiple ways
   1. Systems can specify components to be added to the SubWorld with the `#[read_component(component)]`[][read_component] and `#[write_component(component)]`[][write_component] attributes and then query the SubWorld.
   2. Systems can specify a query as a parameter: `fn system(world: &mut SubWorld, query: &mut Query<(&mut Position, &Velocity)>, ...)`.
   3. Systems can use the `#[system(for_each)]` attribute and specify the components as arguments (eg. `fn system(pos: &mut Position, vel: &Velocity)`) (`&Entity` can also be an argument). The query can be filtered with the `#[filter(filter)]` attribute macro.
 - Systems can add components using a command buffer specified as an argument: `fn system(cmd: &mut CommandBuffer)`

#### State Access

 - Systems can access a local state by adding a reference argument with the `#[state]` decorator. Note that the output `<function>_system`'s signature changes, with arguments added for initial state values.
 - Systems can access a global state by adding a mutable or immutable reference argument with the `#[resource]` decorator. The resource must have been initialized in the `Schedule::execute(&mut self, world: &mut World, resources: &mut Resources)`[][Schedule::execute], or, in the case of Amethyst, in the `ApplicationBuilder::with_resource`[][ApplicationBuilder::with_resource] function.

### Method 2

#### Entity and Component Access and Modification

#### State Access

### Resources

 - Resources are a global state.

[beta-amethyst]: https://github.com/amethyst/amethyst/commit/6d0e7aaf58a4d1483b902f63920044eabb865c92
[or pattern feature]: https://github.com/rust-lang/rust/issues/54883
[amethyst repository]: https://github.com/amethyst/amethyst
[Legion crate]: https://github.com/amethyst/legion
[Specs]: https://github.com/amethyst/specs

[World::push]: https://docs.rs/legion/0.4.0/legion/world/struct.World.html#method.push
[World::extend]: https://docs.rs/legion/0.4.0/legion/world/struct.World.html#method.extend
[Archetype]: https://docs.rs/legion/0.4.0/legion/storage/struct.Archetype.html

[Entry]: https://docs.rs/legion/0.4.0/legion/world/struct.Entry.html
[World::entry]: https://docs.rs/legion/0.4.0/legion/world/struct.World.html#method.entry
[Entry::get_component]: https://docs.rs/legion/0.4.0/legion/world/struct.Entry.html#method.get_component
[Entry::get_component_mut]: https://docs.rs/legion/0.4.0/legion/world/struct.Entry.html#method.get_component_mut
[Entry::get_component_unchecked]: https://docs.rs/legion/0.4.0/legion/world/struct.Entry.html#method.get_component_unchecked

[<>::query]: https://docs.rs/legion/0.4.0/legion/trait.IntoQuery.html#tymethod.query
[Query::filter]: https://docs.rs/legion/0.4.0/legion/query/struct.Query.html#method.filter
[component]: https://docs.rs/legion/0.4.0/legion/fn.component.html
[Any]: https://docs.rs/legion/0.4.0/legion/query/struct.Any.html
[Query::iter]: https://docs.rs/legion/0.4.0/legion/query/struct.Query.html#method.iter
[Query::iter_mut]: https://docs.rs/legion/0.4.0/legion/query/struct.Query.html#method.iter_mut
[Query::for_each]: https://docs.rs/legion/0.4.0/legion/query/struct.Query.html#method.for_each
[Query::for_each_mut]: https://docs.rs/legion/0.4.0/legion/query/struct.Query.html#method.for_each_mut
[query iteration]: https://docs.rs/legion/0.4.0/legion/query/struct.Query.html#implementations

[system macro]: https://docs.rs/legion/0.4.0/legion/attr.system.html
[system macro rewrite]: https://github.com/ketexon/amethyst_system_proc_macro
[SystemBuilder]: https://docs.rs/legion/0.4.0/legion/struct.SystemBuilder.html
[read_component]: https://docs.rs/legion/0.4.0/legion/systems/struct.SystemBuilder.html#method.read_component
[write_component]: https://docs.rs/legion/0.4.0/legion/systems/struct.SystemBuilder.html#method.write_component

[CommandBuffer]: https://docs.rs/legion/0.4.0/legion/systems/struct.CommandBuffer.html

[Schedule::execute]: https://docs.rs/legion/0.4.0/legion/struct.Schedule.html#method.execute
[ApplicationBuilder::with_resource]: https://docs.amethyst.rs/api/stable/amethyst/prelude/struct.applicationbuilder#method.with_resource