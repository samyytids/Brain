---
tags:
  - note
  - bevy/0_14
Project:
  - "[[Map out useful bevy features]]"
Status: Finished
---
## Colour grading
### Summary 
What it says on the tin really...

## ECS hooks and observers
### Summary 
Stuff for checking whether an event has occurred or a `Entity` has been changed or added to. 

## Query joins
### Summary 
Well you have 2 queries and you want to combine them into a single query. 

### Example
```rust
fn helper_function(a: &mut Query<&A>, b: &mut Query<&B>){    
    let a_and_b: QueryLens<(Entity, &A, &B)> = a.join(b);
    assert!(a_and_b.iter().len() <= a.len());
    assert!(a_and_b.iter().len() <= b.len());
}
```

### Warning
More of a way to get yourself out of a jam rather than as a feature to actively reach for. 

## Computed states and sub states
### Summary 
The state system basically involves checking state... Shocker I know!
But previously this only let you naively always check for a specific state or only a basic state. Eg in menu, but not easily which sub menu you are in. 

#### Current implementation
```rust
#[derive(States, Clone, PartialEq, Eq, Hash, Debug, Default)]
enum GameState {
    #[default]
    Menu,
    InGame {
        paused: bool
    },
}
```
Here we have an issue where I can be in menu or in game, but maybe while I am in game I want more states to be represented. 
#### Computed states
These basically allow you to compute state based on some rules. Basically it lets you set paused more easily. 
```rust
#[derive(Clone, PartialEq, Eq, Hash, Debug)]
struct InGame;

impl ComputedStates for InGame {
    // Computed states can be calculated from one or many source states.
    type SourceStates = GameState;

    // Now, we define the rule that determines the value of our computed state.
    fn compute(sources: GameState) -> Option<InGame> {
        match sources {
            // We can use pattern matching to express the
            //"I don't care whether or not the game is paused" logic!
            GameState::InGame {..} => Some(InGame),
            _ => None,
        }
    }
}
```

#### Sub States
```rust
#[derive(SubStates, Clone, PartialEq, Eq, Hash, Debug, Default)]
// This macro means that `GamePhase` will only exist when we're in the `InGame` computed state.
// The intermediate computed state is helpful for clarity here, but isn't required:
// you can manually `impl SubStates` for more control, multiple parent states and non-default initial value!
#[source(InGame = InGame)]
enum GamePhase {
    #[default]
    Setup,
    Battle,
    Conclusion
}
```
Think of this as implementing a sub enum for your enum that requires a specific parent enum value to kick the child enum into being. 

### Example
```rust
App::new()
   .init_state::<GameState>()
   .add_computed_state::<InGame>()
   .add_sub_state::<GamePhase>()
```
States provide you access to a series of schedules based on things like entering a given state, exiting it, etc. 

## State scoped entities
### Summary 
It makes sense that if your game has states that you would have certain entities that only exist when the game is in a given state. 

### Example
```rust
#[derive(Clone, Copy, PartialEq, Eq, Hash, Debug, Default, States)]
enum GameState {
 #[default]
  Menu,
  InGame,
}

fn spawn_player(mut commands: Commands) {
    commands.spawn((
        // We mark this entity with the `StateScoped` component.
        // When the provided state is exited, the entity will be
        // deleted recursively with all children.
        StateScoped(GameState::InGame)
        SpriteBundle { ... }
    ))
}

App::new()
    .init_state::<GameState>()
    // We need to install the appropriate machinery for the cleanup code
    // to run, once for each state type.
    .enable_state_scoped_entities::<GameState>()
    .add_systems(OnEnter(GameState::InGame), spawn_player);
```
Here our player is only spawned when we enter a specific state. 

## Query sorting
### Summary
A new much nicer implementation of query sorting has been added!

### Example
```rust
// To be used as a sort key, `Attack` now implements Ord.
#[derive(Component, Copy, Clone, Deref, PartialEq, Eq, PartialOrd, Ord)]
pub struct Attack(pub usize)

fn handle_enemies(enemies: Query<(&Health, &Attack, &Defense)>) {
    // Still an allocation, but undercover.
    for enemy in enemies.iter().sort::<&Attack>() {
        work_with(enemy)
    }
}
```