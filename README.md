# Paddleocr

# Image Table Extraction and OCR
This repository contains a comprehensive pipeline for extracting tabular data from images using object detection models and OCR (Optical Character Recognition). The project leverages LayoutParser for detecting layout elements and PaddleOCR for text recognition, ensuring accurate extraction and representation of tabular data.

# Features
Object Detection with LayoutParser:
Utilizes the Detectron2LayoutModel from LayoutParser, trained on the PubLayNet dataset, to identify and classify layout elements such as text, titles, lists, tables, and figures.
Configured to detect tables with high accuracy using a pre-trained Faster R-CNN model.

#Image Preprocessing:
Reads and processes input images to fit the expected input format for the detection model.
Crops the detected table region from the original image for further text extraction.

#Text Extraction with PaddleOCR:
Applies PaddleOCR to the cropped table images to extract text with bounding box coordinates.
Annotates detected text in the image and overlays bounding boxes for visualization.


# Copy code
!pip install layoutparser torchvision && pip install "git+https://github.com/facebookresearch/detectron2.git@v0.5#egg=detectron2"

# Running the Script
1. Load the Image:
   Ensure your image is accessible and specify the path in the script:
# pythonCopy code
image = cv2.imread("/path/to/your/image.jpg")

2.Detect Layout and Extract Table:
The script will process the image to detect layout elements and extract tables.

3. Run OCR:
PaddleOCR will extract text from the cropped table image.

# Output to CSV:
The extracted table data will be saved in a CSV file named sample.csv.

# Example python
# Load and preprocess image
image = cv2.imread("/content/drive/MyDrive/imageocr/image00016.jpg")

image = image[..., ::-1]

# Load detection model
model = lp.Detectron2LayoutModel('lp://PubLayNet/faster_rcnn_R_50_FPN_3x/config',

                                 extra_config=["MODEL.ROI_HEADS.SCORE_THRESH_TEST", 0.8],
                                 
                                 label_map={0: "Text", 1: "Title", 2: "List", 3:"Table", 4:"Figure"})

# Detect layout
layout = model.detect(image)

# Extract table and apply OCR



![detections](https://github.com/Shikha409/paddleocr/assets/124184032/f3c8af39-8771-4b90-8500-6aec30954e25)




# Save extracted data to CSV 

pd.DataFrame(out_array).to_csv('sample.csv')



![excelsheet](https://github.com/Shikha409/paddleocr/assets/124184032/5ed78de7-b58b-410a-951f-82a7c1aa9e06)




