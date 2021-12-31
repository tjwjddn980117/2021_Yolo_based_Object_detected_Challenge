# 2021_Yolo_based_Object_detected_Challenge

Team Name:
- 코딩몽키


Team Member: 
- 서정우 2019253009 (Leader)
- 유진경 2019253013
- 이채연 2019253003
- 강현영 2018272026
            

## Intro
Paper YOLO v4: https://arxiv.org/abs/2004.10934

Paper Scaled YOLO v4: * **[CVPR 2021](https://openaccess.thecvf.com/content/CVPR2021/html/Wang_Scaled-YOLOv4_Scaling_Cross_Stage_Partial_Network_CVPR_2021_paper.html)**: use to reproduce results: [ScaledYOLOv4](https://github.com/WongKinYiu/ScaledYOLOv4)

More details in articles on medium:

- [Scaled_YOLOv4](https://alexeyab84.medium.com/scaled-yolo-v4-is-the-best-neural-network-for-object-detection-on-ms-coco-dataset-39dfa22fa982?source=friends_link&sk=c8553bfed861b1a7932f739d26f487c8)
- [YOLOv4](https://medium.com/@alexeyab84/yolov4-the-most-accurate-real-time-neural-network-on-ms-coco-dataset-73adfd3602fe?source=friends_link&sk=6039748846bbcf1d960c3061542591d7)

Manual: https://github.com/AlexeyAB/darknet/wiki

This git code is entirely 'https://github.com/AlexeyAB/darknet' modified git code.

Our goal is to recognize the buildings of the Mirae Campus of Yonsei University using the yolo model.

Here is the Context
- Develop Environment
- Data
- Setting
- Popup
- How To Run
- Conclusion

Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon
              
## Develop Environment

Hardware

- CPU: AMD Ryzen 5 5600X

- GPU: ZOTAC Gaming GeForce RTX™ 3070Ti AMP Holo

- SSD: Western Digital WD BLUE SN550 M.2 NVMe 1TB

- RAM: Samsung DDR4-2666 32GB (16GB*2)


Software

- OS: Windows 10 pro

- Version:

  -  python: 3.7.11
  
  -  tensorflow-gpu: 2.7.0
  
  -  openCV: 3.4.2
  
  -  Nvidia Driver: 471.68
  
  -  Cuda: 11.4
  
  -  CUDNN: 8.2.1


Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon
  
  
## Data
You can download our dataset with this URL
dataset: https://drive.google.com/file/d/1V0TsN6g2lwNEwdx8xcUIipz8JCs3jn5F/view?usp=sharing

Please set up the datasets 'data' file in to ./darknet-master

then, this is the screen of path './darknet-master/data'

<img width="693" alt="스크린샷 2021-12-30 오후 7 55 55" src="https://user-images.githubusercontent.com/51360338/147796995-eb786813-f50a-44fe-84c9-1203cecf0917.png">

'obj' file has our labeled datas


'popup' file has our popup datas witch contain explanation about the Building.


We have 13 classes, and these are the list and number of class 'class(number of class)'
- university_headquarters (151)
- justice_hall (187)
- cheongsong_hall (53)
- creation_hall (75)
- baekwoon_hall (148)
- future_hall (144)
- central_library (364)
- student_union_building (116)
- creation_hall_back (44)
- central_library_back (138)
- student_union_building_back (123)
- eagle (79)
- future_hall_side (53)

so, total number of labels are 1,675

The side and back sides were added for labeling focusing on the distinctive features of each building.

creation_hall_back (behind the creation hall): Labeling mainly on the entrance to the rear of the creation hall (see photo below)

<img width="351" alt="스크린샷 2021-12-30 오후 8 41 47" src="https://user-images.githubusercontent.com/51360338/147798134-377451f7-2f54-4905-b45c-51b8fa9d6535.png">

In creation_hall or cheongsong_hall, if the profile and entrance are taken together as shown below,
Labeling mainly on the entrance side, which is the main characteristic for recognizing the Creation Hall.

<img width="393" alt="스크린샷 2021-12-30 오후 8 42 55" src="https://user-images.githubusercontent.com/51360338/147798188-1a0c4ca0-47ed-4384-b6ed-183a84bc4acd.png">

## Setting

edit 'cfg/yolov4-tiny-custom_testing.cfg' file.

<img width="868" alt="스크린샷 2021-12-30 오후 9 58 36" src="https://user-images.githubusercontent.com/51360338/147800504-09bb8b89-dc56-42cf-bc91-de8d43fea155.png">

'[yolo] classes' has to be 13, and '[convolutional] filters' has to be 256

edit 'data/obj.names' file.

<img width="614" alt="스크린샷 2021-12-30 오후 10 02 54" src="https://user-images.githubusercontent.com/51360338/147800644-47b8bf04-34de-41f7-ad75-e46add2ce599.png">

edit 'data/obj.data' file.

<img width="571" alt="스크린샷 2021-12-30 오후 10 04 15" src="https://user-images.githubusercontent.com/51360338/147800687-33013e22-c503-46ec-94d5-16b3dd112972.png">         

'classes' has to be 13.


Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon

## Popup

we edit '/src/image_opencv.cpp' file.

<img width="824" alt="스크린샷 2021-12-30 오후 9 01 14" src="https://user-images.githubusercontent.com/51360338/147798745-d53215ee-e352-4691-a232-e3cccb129bb5.png">

When the object is recognized, a pop-up appears. 

The program pauses for a moment while the popup is floating. 

When you close the pop-up, the program runs again.

If the detected object is a building with information of 'back' or 'side', the code is coded to display the same popup as that of a building without 'back' or 'side'.

Popup data is in the path '/data/popup'

here is the example

<img width="1301" alt="스크린샷 2021-12-30 오후 10 15 36" src="https://user-images.githubusercontent.com/51360338/147801060-47cba5fe-08dd-46b7-a06d-b82134ae919f.png">



Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon

## How To Run

If you don't have cfg file, you can download in this URL https://drive.google.com/file/d/1USA2HumLUOiQjn_obyGM3blM9BGUPc2P/view?usp=sharing

Please set up the 'cfg' file in to ./darknet-master

<img width="623" alt="스크린샷 2021-12-30 오후 10 54 41" src="https://user-images.githubusercontent.com/51360338/147802362-c593b610-78d7-4dfd-8fa0-8466cc90808e.png">

Training
- train

            darknet.exe detector train data/obj.data cfg/yolov4-tiny-custom.cfg yolov4-tiny.conv.29 -dont_show -map

- Transfer Learning

            darknet.exe detector train data/obj.data cfg/yolov4-tiny-custom.cfg /content/darknet/backup/custom-yolov4-detector_last.weights
            
            

Test

            darknet.exe detector demo data/obj.data cfg/yolov4-tiny-custom_testing.cfg ../training/yolov4-tiny-custom_best.weights -thresh 0.5

If you want to recognize objects with a webcam while running on a computer with a built-in camera,

            darknet.exe detector demo data/obj.data cfg/yolov4-tiny-custom_testing.cfg ../training/yolov4-tiny-custom_best.weights -thresh 0.5 -c 1

Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon

## Conclustion

Our training time was 10.12521 hours until 6000 epoches learning.

This is our results of test

- class_id = 0, name = university_headquarters, ap = 89.94% (TP:15, FP:3)
- class_id = 1, name = justice_hall, ap = 100.00% (TP:16, FP:1)
- class_id = 2, name = cheongsong_hall, ap = 88.69% (TP:7, FP:2)
- class_id = 3, name = creation_hall, ap = 100.00% (TP:6, FP:1)
- class_id = 4, name = baekwoon_hall, ap = 100.00% (TP:12, FP:0)
- class_id = 5, name = future_hall, ap = 99.74% (TP:18, FP:4)
- class_id = 6, name = central_liberty, ap = 100.00% (TP:35, FP:0)
- class_id = 7, name = student_union_building, ap = 100.00% (TP:12, FP:1)
- class_id = 8, name = creation_hall_back, ap = 100.00% (TP:1, FP:0)
- class_id = 9, name = central_library_back, ap = 95.56% (TP:8, FP:1)
- class_id = 10, name = student_union_building_back, ap = 100.00% (TP:11, FP:2)
- class_id = 11, name = eagle, ap = 100.00% (TP:11, FP:0)
- class_id = 12, name = future_hall_side, ap = 100.00% (TP:7, FP:1)

for conf_thresh = 0.25, precision = 0.91, recall = 0.95, F1-score = 0.93

for conf_thresh = 0.25, TP = 159, FP = 16, FN = 9, average IoU = 75.28%

IoU threshold = 50%, used AUC for each unique Recall,
mean average precision (mAP@50) = 0.979943, or 97.99%

This is the object detection about each class

0: university_headquarters
![147714278-6bf27d02-2511-42ae-9064-ca01d918afa6](https://user-images.githubusercontent.com/50481107/147714810-a3e2edb3-e922-4409-84ed-fff184b26548.png)

1: justice_hall
![147713993-0aeb54ca-1d85-4f72-968e-b7310176f732](https://user-images.githubusercontent.com/50481107/147714823-71e20e21-49ad-43ee-b1f7-1da839ff1518.png)

2: cheongsong_hall
![147714134-52f38718-fb2a-439b-954d-b6236bde8abe](https://user-images.githubusercontent.com/50481107/147714833-397a6276-d645-4842-b5f1-ca6b8df6b4d9.png)

3: creation_hall
![147714187-16218480-889b-4420-83bd-1f8c921c40fb](https://user-images.githubusercontent.com/50481107/147714840-d3bc5ca1-042c-4de3-ac09-51a9bd069a1f.png)

4: baekwoon_hall
![147714325-0b8075c4-7228-44ee-a2d6-225c701862cc](https://user-images.githubusercontent.com/50481107/147714849-17f37e2d-c643-4e08-9e8f-cf06d3f9452d.png)

5: future_hall
![147713854-e3117fcf-ccb3-4ec8-8bb7-28d4fb37c314](https://user-images.githubusercontent.com/50481107/147714919-844d692a-79d6-4f6b-98c0-06fa52ef45d9.png)

6: central_library
![147714390-f49e516d-c352-4098-8547-1050a55ca9f6](https://user-images.githubusercontent.com/50481107/147714873-ef735816-72e9-4e11-bbff-edf4e8db77d6.png)

7: student_union_building
![147714075-bbb3706d-1137-4cde-becf-fcacc15f442d](https://user-images.githubusercontent.com/50481107/147714875-3924d2ef-0f2c-4088-9ea0-e33eb27f29d3.png)

8: creation_hall_back
![147713732-d067dead-9092-45d8-b77e-4d87753e1ad4](https://user-images.githubusercontent.com/50481107/147714882-aab28006-b899-470b-8a2e-0183f912738e.png)

9: central_library_back
![147714462-c5e8f538-af3b-4772-8823-4266d7146399](https://user-images.githubusercontent.com/50481107/147714889-1130b24f-074d-4181-b265-9e06bc8e7339.png)


10: student_union_building_back
![147714025-fb6ada77-4b85-4625-b82d-38f20ca83626](https://user-images.githubusercontent.com/50481107/147714896-4c3dff36-5bf7-4edc-ab57-fbe4a05bbbbf.png)

11: eagle
![147713812-10e1651f-cbbd-49f5-86b7-84a5af594563](https://user-images.githubusercontent.com/50481107/147714912-551d9c32-1d03-4976-aff4-03a7d7372eda.png)

12: future_hall_side
![147713921-706e1e70-6dd0-45ec-9091-6482fc87f726](https://user-images.githubusercontent.com/50481107/147714867-a241a15c-62b1-47d1-8309-88409b21d63e.png)



Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon
