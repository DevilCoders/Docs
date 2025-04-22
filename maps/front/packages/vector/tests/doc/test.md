# Testing

## Testing visualizable data

Some functionality that is visualizable by its nature is easier to test by comparing its result with a reference image.
For example curved labels layouting, glyphs positions are computed by a pretty complex rules and it is much easier and
less error prone to verify the result by looking at an image then to manually repeat the calculations in test code.
This image can be saved as a reference one to automate regression testing. So the following approach is recommended
to deal with similar cases:
 1. Implement a canvas renderer: extend CanvasRenderer and implement onRender() method by drawing all the staff
    required for your particular case.
 2. Verify the output:
     * you can console.log(rendere.getImageDataUrl()) and put in into a browser's address bar or
     * use browser_code/runner/test/canvas_renderer.js that will display the image for you or
     * use openImageWindow(rendere.getImageDataUrl()) from tests/util/window, don't forget to switch to
       a non-headless browser in karma config
 3. Create a reference image: the image produced at the previous step could be saved by "Save as..." or
    similar command in browser.
 4. Write a regression test: in unit test import the image above and use previously written implementation of
    CanvasRenderer, CanvasImageRenderer and compareRendererOutputs() util to test for regression automatically.

See [layout_straight_text.test.ts](../src/vector_render_engine/font/layout_straight_text.test.ts) for usage example
