# Fast R-CNN
The paper is about Fast Region-based Convolutional Network method (Fast R-CNN) for object detection. Using deep convolutional networks, Fast R-CNN improves over previous work to efficiently classify object proposals.<br/>
The first thought is, it proposed a model that is significantly faster than R-CNN model. This model is 9 times faster than cnn model during training and the model runs 213 times faster during inference. 
## What is R-CNN model and its limitations:
R-CNN model used in CV and image processing. This model specially designed for object detection. It uses a deep Convolutional Network to classify object proposals and achieves excellent object detection accuracy. But there is some limitation. In Fast R-CNN paper author mension three drawback:
1. The training process with R-CNN is multi-stage: The modules used in the R-CNN model are train separately. First it fine-tune ConvNet on object proposals like extract image features. Then it fits SVMs to extracted features. Lastly it train box regrassion module separately.
2. Expensive to train: The multi-stage training process is time consuming and requred more gygabytes to store the features.
3. Object detection is slow: VGG16 detection requires 47 seconds per image (on a GPU). And also features are extracted from each object proposal in each test image.
## Fast R-CNN model:
Fast R-CNN, a model for object detection, is different from R-CNN, which it replaced, in several ways. Instead of extracting CNN features separately for each region of interest, Fast R-CNN aggregates them into a single forward pass over the image. As a result, it consumes less computational power, time, and memory.<br/>
Fast R-CNN model solve the R-CNN models’ problems.<br/>
An input image only used CNN once, as alternative to applying ConvNet to each object proposal. The ROI layer feature extrantion is applied to the conv feature map using the object region proposal after image features have been extracted. Once all feature vectors have been extracted for each object region proposal, the vectors are fed into a series of fully connected layers, with two proposed outputs are proposed. In this case, softmax is used in a single branch to output an object, and a different branch is used to provide four-dimensional output.<br/>
## The result of Fast R-CNN model:
Performance measured based on the mean average of precision score.<br/>
VOC-2007: The result shows 70% for Fast R-CNN which is 4% greater than R-CNN. <br/>
VOC-2010: Fast R-CNN is 6% greater than R-CNN.<br/>
VOC-2012: Fast R-CNN is 5% greater than R-CNN.<br/>
