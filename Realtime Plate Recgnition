import cv2
from matplotlib import pyplot as plt
import numpy as np
import imutils
import easyocr
import os
import glob
import datetime
import pytesseract
import csv

def main():
    x=int(input("Press 1 to start the program"))
    serial=1
    while x:
        cap = cv2.VideoCapture(0)
        while 1:
            ret, img = cap.read()
            cv2.imshow('Car Image', img)
            cv2.waitKey(0)
            cv2.destroyAllWindows()
            print(img.shape)
            break
        #pic=cv2.imread("Car Image.jpg")
        #plt.imshow(cv2.cvtColor(pic, cv2.COLOR_BGR2RGB))
        result=predicts_number(img)
        print(datetime.datetime.now(), result)
        if(serial==1):
            fields = ['Date', 'Time', 'Number Plate']
            filename = "Vehicle_Entry_Record.csv"
            with open(filename, 'w', newline='') as csvfile: 
                    # creating a csv writer object 
                    csvwriter = csv.writer(csvfile) 
                    csvwriter.writerow(fields)
        
        record(result, serial)
        serial+=1
        x=int(input("Press zero to terminate, any other character to capture next image"))
        cap.release()
    cv2.destroyAllWindows()
    
def predicts_number(img):
   
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    #cv2.imshow(cv2.cvtColor(gray, cv2.COLOR_BGR2RGB))
    
    bfilter = cv2.bilateralFilter(gray, 25, 60, 30)
    #cv2.imshow(cv2.cvtColor(bfilter,cv2.COLOR_BGR2RGB))
    
    edged = cv2.Canny(bfilter, 30, 60) #Edge detection
    #cv2.imshow(cv2.cvtColor(edged, cv2.COLOR_BGR2RGB))
    
    keypoints = cv2.findContours(edged.copy(), cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
    contours = imutils.grab_contours(keypoints)
    contours = sorted(contours, key=cv2.contourArea, reverse=True)[:10]
    
    location = None
    for contour in contours:
        global approx
        approx = cv2.approxPolyDP(contour, 10, True)
        if len(approx) == 4:
            location = approx
            break
    print(location)
    mask = np.zeros(gray.shape, np.uint8)
    new_image = cv2.drawContours(mask, [location], 0,255, -1)
    new_image = cv2.bitwise_and(img, img, mask=mask)
    (x,y) = np.where(mask==255)
    (x1, y1) = (np.min(x), np.min(y))
    (x2, y2) = (np.max(x), np.max(y))
    cropped_image = gray[x1:x2+1, y1:y2+1]
    
    plt.imshow(cv2.cvtColor(cropped_image, cv2.COLOR_BGR2RGB))
    
    #Numberplate reading using Tesseract
    
    result=func_tesseract(cropped_image)
    return result

def func_tesseract(cropimg):
    predicted_result = pytesseract.image_to_string(cropimg, lang ='eng', config='--psm 6')
    filter_predicted_result = "".join(predicted_result.split()).replace(" ", "").replace("-", "")
    first_char=filter_predicted_result[0]
    last_char=filter_predicted_result[-1]
    if(not((ord(first_char)>=65 and ord(first_char)<=90) or (ord(first_char)>=48 and ord(first_char)<=57))):
        filter_predicted_result= filter_predicted_result[1:]
    if(not((ord(last_char)>=65 and ord(last_char)<=90) or (ord(last_char)>=48 and ord(last_char)<=57))):
        filter_predicted_result= filter_predicted_result.rstrip(filter_predicted_result[-1])
    return filter_predicted_result

#Write Data to CSV File

# name of csv file 

def record(plate_no, serial):
        filename = "Vehicle_Entry_Record.csv"
        # writing to csv file 
        rows = str(datetime.datetime.now())+" "+ plate_no
        with open(filename, 'a', newline='') as csvfile: 
                # creating a csv writer object 
                csvwriter = csv.writer(csvfile) 
                csvwriter.writerow(rows.split())
        


if __name__ == "__main__":
    main()
