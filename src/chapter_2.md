# Getting Started with Chunks Library

## Initial Setup

Begin by creating a new instance of the `Factory` struct in your main function:

```rust
fn main() {
    let factory = Factory::new("chunk.factory");
    // Additional configuration will go here
}
```

The factory instance serves as the foundation for managing your widgets. Next, create a closure to contain your chunks:

```rust
fn main() {
    let factory = Factory::new("chunk.factory");

    let chunks = |factory: Application| {
        // Your chunks will be defined here
    };

    factory.pollute(chunks);
}
```

## Understanding Chunks

Chunks are the fundamental building blocks of the library. Each chunk represents a widget that can display information on your screen. These widgets are:
- Highly configurable
- Independently updateable
- Positioned using a flexible anchor system
- Capable of displaying both static and dynamic text, as well as images

## Creating Your First Widget: Storage Display

Let's create a widget that shows system storage usage percentage. We'll break this down into steps:

### 1. Basic Function Structure

Create a function that takes a factory reference:

```rust
fn storage(factory: &Application) {
    // Widget configuration will go here
}
```

### 2. Core Configuration

Set up the essential variables for positioning and identifying the widget:

```rust
fn storage(factory: &Application) {
    // Create a unique identifier for the widget
    let tag = tag("storage");
    
    // Set the widget's position (top-right corner)
    let anchors = EdgeConfig::TOP_RIGHT.to_vec();
    
    // Define margins from screen edges
    let margins = vec![
        (Edge::Top, 20),     // 20 pixels from top
        (Edge::Right, 160)   // 160 pixels from right
    ];
}
```

### 3. Content Update Logic

Create a closure that generates the widget's content:

```rust
fn storage(factory: &Application) {
    // Previous configuration...
    
    let storage_closure = || {
        // Use Pango Markup for formatted text
        let text = format!(
            "<span foreground='#FFFFFF'>{:.0}%</span>",
            Internal::get_storage(),
        );
        text
    };
}
```
> It may seem redundant to use a closure for a text based widget, but this structure allows for dynamic content updates in more complex widgets.

### 4. Update Interval

Set how often the widget refreshes:

```rust
fn storage(factory: &Application) {
    // Previous configuration...
    
    // Updates every 120 seconds (default for storage widgets)
    Internal::update_storage(&tag, storage_closure);
    
    // Alternatively, you can set a custom interval:
    Internal::update_widget(&tag, storage_closure, 120);
}
```

### 5. Widget Creation

Finally, construct and initialize the widget:

```rust
fn storage(factory: &Application) {
    // Previous configuration...
    
    Chunk::new(
        factory.clone(),
        "Storage".to_string(),  // Widget title
        tag,
        margins,
        anchors,
        Layer::Bottom          // Widget layer
    )
    .build();
}
```

## Putting It All Together

In your main function, call the storage function within the chunks closure:

```rust
fn main() {
    let factory = Factory::new("chunk.factory");
    
    let chunks = |factory: Application| {
        storage(&factory);
        // Add more widgets here as needed
    };
    
    factory.pollute(chunks);
}
```

## Complete Example

Here's the complete code for reference:

```rust
fn main() {
    let factory = Factory::new("chunk.factory");
    
    let chunks = |factory: Application| {
        storage(&factory);
    };
    
    factory.pollute(chunks);
}

fn storage(factory: &Application) {
    let tag = tag("storage");
    let anchors = EdgeConfig::TOP_RIGHT.to_vec();
    let margins = vec![
        (Edge::Top, 20),
        (Edge::Right, 160)
    ];
    
    let storage_closure = || {
        let text = format!(
            "<span foreground='#FFFFFF'>{:.0}%</span>",
            Internal::get_storage(),
        );
        text
    };
    
    Internal::update_storage(&tag, storage_closure);
    
    Chunk::new(
        factory.clone(),
        "Storage".to_string(),
        tag,
        margins,
        anchors,
        Layer::Bottom
    )
    .build();
}
```

## Next Steps

You've successfully created your first widget using the Chunks library! Experiment with different Internal functions and widget configurations to build more complex displays.

Continue reading to add CSS styling to your widgets and explore advanced widget types.
