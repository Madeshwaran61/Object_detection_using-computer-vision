# Motion Detection System

This project implements a simple motion detection system using Python, OpenCV, and sound alerts. It captures video from the webcam, detects motion in the video frames, and triggers an audible alert when significant movement is detected.

## Features

- **Real-Time Motion Detection**: Continuously monitors the webcam feed for motion.
- **Contour Detection**: Detects areas of movement and highlights them with a bounding box.
- **Audible Alerts**: Plays a sound alert when motion exceeding a certain threshold is detected.
- **Customizable Thresholds**: Easily modify the motion detection sensitivity.

## Requirements

- Python 3.x
- OpenCV
- winsound (available by default on Windows)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/motion-detection-system.git
   cd motion-detection-system
   ```

2. Install the required libraries:
   ```bash
   pip install opencv-python
   ```

3. Add your alert sound:
   - Place an audio file named `alert.wav` in the project directory.

## Usage

1. Run the script:
   ```bash
   python motion_detection.py
   ```

2. The program will:
   - Open the webcam.
   - Detect motion.
   - Play a beep and sound an alert (`alert.wav`) when significant motion is detected.

3. To exit the program, press `q`.

## Code Explanation

### Key Components

1. **Video Capture**: Captures frames from the webcam using OpenCV:
   ```python
   cam = cv2.VideoCapture(0)
   ```

2. **Motion Detection**: Uses frame differencing, grayscale conversion, Gaussian blur, and thresholding to identify changes:
   ```python
   diff = cv2.absdiff(frame1, frame2)
   gray = cv2.cvtColor(diff, cv2.COLOR_RGB2GRAY)
   blur = cv2.GaussianBlur(gray, (5, 5), 0)
   _, thresh = cv2.threshold(blur, 20, 255, cv2.THRESH_BINARY)
   dilated = cv2.dilate(thresh, None, iterations=3)
   ```

3. **Contours and Bounding Boxes**: Detects motion areas and highlights them:
   ```python
   for c in contours:
       if cv2.contourArea(c) < 5000:
           continue
       x, y, w, h = cv2.boundingRect(c)
       cv2.rectangle(frame1, (x, y), (x + w, y + h), (0, 255, 0), 2)
   ```

4. **Sound Alerts**: Uses `winsound` for beeping and playing an alert:
   ```python
   winsound.Beep(500, 200)
   winsound.PlaySound('alert.wav', winsound.SND_ASYNC)
   ```

5. **Exit Condition**: Stops the program when `q` is pressed:
   ```python
   if cv2.waitKey(10) == ord('q'):
       break
   ```

## Customization

- **Sensitivity**:
  Adjust the `cv2.contourArea(c)` threshold to change the motion detection sensitivity.

- **Bounding Box**:
  Modify the color or thickness of the rectangle drawn around motion areas:
  ```python
  cv2.rectangle(frame1, (x, y), (x + w, y + h), (0, 255, 0), 2)
  ```

- **Sound Alert**:
  Replace `alert.wav` with your custom alert sound.

## Limitations

- Designed for Windows (due to `winsound` module).
- Motion detection sensitivity might need tuning for different environments.
- Background changes (e.g., lighting) can trigger false positives.

## Contributing

Feel free to fork the repository and submit pull requests for new features or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [OpenCV Documentation](https://docs.opencv.org/)
- Python `winsound` module for audio alerts.

---

Happy Coding! 🎉

