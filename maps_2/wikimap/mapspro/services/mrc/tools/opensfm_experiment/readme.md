# OpenSfM tests

Tools for testing opensfm positioning accuracy on rides with ground truth positions and headings collected by selfdriving. The structure is:

- `upload` -- Prepare selfdriving data.
- `view` -- Visualize positions with easyview.
- `preprocess` -- Preprocessing positions and headings.

## Example

Create tables from selfdriving data: add missing columns, format heading and pos (with ground truth).

    ./upload/create-tables --input //path/to/table --outut //path/to/output

Match points to road graph, refine headings and run segmentation

    ./preprocess/preprocess \
    --table //path/to/input
    --min-interval 1s
    --min-distance 2
    --match
    --headings
    --segment

