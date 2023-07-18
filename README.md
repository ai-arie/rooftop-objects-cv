# Detection and Segmentation of Photovoltaic Installations in Germany

- 'yolov7-seg' is the custom version of the VOLOv7 segmentation model (based on https://github.com/WongKinYiu/yolov7/tree/u7/seg)
- 'yolov7-det' is the custom version of the main branch of VOLOv7 (based on https://github.com/WongKinYiu/yolov7)

- The best weights (.onnx file) for the segmentation model, which are not mandatory for the submission, can be found here: https://drive.google.com/file/d/1RYaDK6SvV30_BQ9i6MJFCut9hzHC6DuD/view?usp=share_link

- Note that due to IP constraints, the images are not published in this repository. The following information about the images would also to recreate such a dataset:
- source: GoogleMapsAPI
- image size: 400x400
- zoom: 20
- 1000 images, each centred on a rooftop in Germany were used. >90\% of the images had a rooftop object on them (e.g. PV/Thermal panel/Windows). 

- The 'coco_data.zip' file contains the annotations in the COCO format (.json file).

- The code notebooks in the 'code' folder are:
    1. convert-bbox-annotations-coco-to-yolo.ipynb :
        - converts the bounding box annotations from the COCO format to the YOLO format
        - need the coco_data.zip file in order to run.
        - need the images folder in order to run (please make sure the two 'images_' zip files are unzipped and combined into one folder).
    2. convert-segmentation-annotations-coco-to-yolo.ipynb
        - converts the segmentation annotations from the COCO format to the YOLO format
        - need the coco_data.zip file in order to run.
        - need the images folder in order to run (please make sure the two 'images_' zip files are unzipped and combined into one folder).
    3. YOLOv7-detection.ipynb
        - trains the YOLOv7 detection model
        - evaluates the YOLOv7 detection model
        - note that all the training data is still shown in the output of the training cell
        - need the output of 'convert-bbox-annotations-coco-to-yolo.ipynb' in order to run.
    4. YOLOv7_segmentation-inference.ipynb
        - evaluates the YOLOv7 segmentation model using the best weights
        - need the output of 'convert-segmentation-annotations-coco-to-yolo.ipynb' in order to run.
    5. final_YOLOv7.ipynb
        - trains the YOLOv7 segmentation model with best parameters.
        - evaluates the YOLOv7 segmentation model
        - note that all the training data is still shown in the output of the training cell
        - need the output of 'convert-segmentation-annotations-coco-to-yolo.ipynb' in order to run.
    6. inference_and_center_building_postprocessing.ipynb
        - postprocesses the YOLOv7 segmentation model output to get the final mask of objects of interest, and area prediction of the PV installations on the center building.
        - need the output of 'convert-segmentation-annotations-coco-to-yolo.ipynb' in order to run.

IMPORTANT: in all the notebooks above, one has to change the path to the directory when running to your location. All notebooks should run on Google Colab. 