# Styling Chunks with CSS

### Setting Up Your Styles

First, create a constant in your program to hold your CSS definitions:

```plaintext
const STYLE: &str = "
    /* Base window styles */
    window {
        background-color: transparent;
    }

    /* Storage widget styles */
    #storage {
        font-size: 34px;
        background-color: #000000;
        color: #FFFFFF;
    }
";
```

### Notes

1. **Window Transparency**
   - The `window` selector isn't necessary but should be included in your CSS
   - Setting `background-color: transparent` is crucial to ensure that only the Layer Shell remains visible

2. **Widget Selectors**
   - Use ID selectors (#) that match your widget tags
   - Example: `#storage` corresponds to a widget created with `tag("storage")`

### Applying the Styles

Load your CSS within the chunks closure:

```rust
fn main() {
    let factory = Factory::new("chunk.factory");
    
    let chunks = |factory: Application| {
        storage(&factory);
        load_css(STYLE);    // Apply the CSS styles
    };
    
    factory.pollute(chunks);
}
```
