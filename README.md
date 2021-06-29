# Realtime-Vehicle-Plate-Recognition-System
This was a part of my final year project. The program uses Tesseract to perform OCR in real-time on car Images captured using a webcam. A video depicting real-time detection is availabe in the repository.

## PROBLEM STATEMENT:

Real-time end-to-end implementation of a Vehicle License Plate Recognition System, perform OCR and append the output along with the timestamp to a .CSV file.

## POST-PROCESSING:

Usually, number plates are not simple. Special Characters like ‘-’, ‘:’ between the characters corrupt the output and decrease accuracy. We also noticed that extra characters like ‘|’, ‘_’ ‘©’ etc. were detected due to shadows. These special characters were often present at the beginning or at the end of the string. To omit these characters, we put a check that the detected string should always start or end with an alphanumerical character, else the extra character should be dropped. This helped us improve the accuracy significantly. 

## OBSERVATIONS

•	Removing special characters from the recognized image in post-processing significantly improved the accuracy. 
•	The plate status, environmental conditions and the hardware used to catch pictures are deterministic important factors for the proper functioning program.
•	A good image pre-processing almost guarantees successful recognition.
•	During Real-time execution, proper lighting and an accurate camera angle are important for proper capturing and recognition.
•	OCR is most effective when characters are in a contrasting background. 


## Future Scope of Work in the problem statement:
•	Compiling a better dataset for testing
•	Calculation of %Error for each function.
•	Use of GPU to check OCR performance.
•	Accuracy comparison of OCR engines in real-time. 
•	Images needs to be captured from public places for a better dataset.
•	Adaptive filtering needs to be tested.
•	End-to-end implementation of the project using hardware with a low-resolution camera in a parking lot.
