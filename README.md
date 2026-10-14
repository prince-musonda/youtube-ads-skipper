# YouTube Ads Skipper

YouTube Ads Skipper uses a YOLO object-detection model to find the YouTube
**Skip ad** button on the screen and click it automatically. It also opens an
animated interface when it starts.

## Run the Program

1. Open a terminal in the project folder (the folder containing `skipper.py`,
   `best.pt`, and `interface.html`).
2. Install the dependencies:

   ```sh
   python3 -m venv .venv
   source .venv/bin/activate
   python -m pip install -r requirements.txt
   ```

3. Start the program:

   ```sh
   python skipper.py
   ```

The interface opens first; the detector starts about 10 seconds later. On
macOS, allow screen recording and accessibility access for the terminal or
Python if prompted. Press Ctrl+C in the terminal to stop the program.

## Improve Detection with Labeled Data

Add more representative screenshots and matching YOLO label files to the
dataset folders:

- Images: `dataset/images/train/` or `dataset/images/val/`
- Labels: `dataset/labels/train/` or `dataset/labels/val/`

Each image needs a `.txt` label file with the same base filename. For each
Skip ad button, label one bounding box using this format:
`class_id x_center y_center width height`. Coordinates are normalized from 0
to 1, and the class ID for `skip_button` is `0`. Include varied examples of the
button's appearance, position, and surrounding screen so the model can learn
from different cases. Keep validation examples in the `val` folders rather
than training on them.

After adding labels, run `python skipper_trainer.py` to train. The training
script starts from `runs/detect/skipper/skipper_detector-2/weights/last.pt`;
make sure that checkpoint exists or update the path in `skipper_trainer.py` to
the weights you want to continue training from.
