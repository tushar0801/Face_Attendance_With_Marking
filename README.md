# Face_Attendance_With_Marking
The system excels in accurate face recognition, achieving a perfect F1 Score of 1.0 and an impressive F2 Score of 1.25. Its robust performance and precise attendance marking underscore its effectiveness and reliability.
1. Imports
2. The required libraries are imported:
face_recognition: Enables face detection and recognition.
datetime: Facilitates timestamping of attendance records.
cv2 (OpenCV): Provides tools for image and video processing.
sklearn.metrics: Used for calculating metrics such as F1 scores and confusion matrices.
numpy: Supports numerical operations.
DeepFace: Offers functionality for face verification and liveness detection.
os: Allows interaction with the operating system.
deepface.commons.functions: Provides common functions for the DeepFace library.
3. Loading Known Faces and Names
Known individuals' images are loaded, and their facial encodings are computed using face_recognition.face_encodings. These encodings uniquely represent each face for comparison.
The computed encodings are stored in the known_faces list, and corresponding names are stored in the known_names list.
4. Initializing Webcam
The script initializes the webcam using cv2.VideoCapture(0) to capture real-time frames.
5. Initializing Liveness Detection Model
Haarcascade classifier XML files are loaded. These classifiers are essential for liveness detection.
6. Processing Frames from Webcam
A continuous loop captures frames from the webcam.
Each frame is saved as an image named frame.jpg using cv2.imwrite.
The Haarcascade classifier is applied to the grayscale version of the frame to detect faces.
For each detected face:
Liveness detection is performed using the DeepFace.verify function. This function compares the current frame with a reference image to confirm if the detected face is real.
If the liveness detection passes:
face_recognition is used to identify face locations and compute face encodings in the current frame.
Distances between the detected face encodings and known faces' encodings are calculated using face_recognition.face_distance.
If the minimum distance is below a threshold (0.6), the script identifies the known person with the closest face encoding and adds their name to the matched_names list. If the distance is above the threshold, the person is labeled as "Unknown."
7. Marking Attendance
A flag named attendance_marked keeps track of whether attendance has been marked.
The matched_names list stores the recognized names for each processed frame.
8. Exiting the Loop
The loop continues until the 'q' key is pressed or attendance is marked.
If all detected faces are matched to known faces and attendance has been marked, the loop breaks.
9. Calculating Metrics and Saving Attendance
If attendance was marked (attendance_marked is True):
F1 scores and F2 scores are calculated using f1_score from sklearn.metrics.
A confusion matrix is computed using confusion_matrix from sklearn.metrics.
Attendance data is written to a CSV file, including the current date and time.
The marked attendance is printed on the console.
10. Releasing Resources
After the loop completes, the webcam is released, and OpenCV windows are closed.
11. Final Steps and Outputs
If attendance was marked, the calculated metrics (F1, F2 scores, confusion matrix) and attendance details are printed to the console.
If attendance was not marked, a message indicating this is printed.
