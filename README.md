# S29_Food-calorie-estimator-using-images

Due to the improvement in people’s standards of living, obesity rates are increasing at an alarming speed, and this is reflective to the risks in people’s health. People need to control their daily calorie intake by eating healthier foods, which is the most basic method to avoid obesity. However, although food packaging comes with nutrition (and calorie) labels, it’s still not very convenient for people to reference. Thus, scientists started to use machine learning algorithms in computer vision to help people determine the caloric value in the food they eat. During the 2015 Rework Deep Learning Summit in Boston, Google scientist Kevin Murphy presented a deep learning algorithm that was used to analyze static food image. By analyzing the composition of the food in picture, the algorithm can calculate how much calories the dish has.

This paper is trying to provide a more efficient way of estimating calories. First, it needs the top view and side view images of the food being analyzed. Then, it will use Faster R-CNN to detect the food and calibration object, after which, a GrabCur algorithm is used to determine the food’s contour. After estimating the volume of food, the authors can finally estimate the amount of calories.

INTRODUCTION

When people’s Body Mass Index (BMI) is over 30 (kg/m2), they are generally considered to be obese. High BMI can increase the risk of illnesses like heart disease [1]. The main reason of obesity is due to the imbalance between the amount of caloric intake (consumption) and energy output (expenditure). Because of unwillingness to record and track, lack of related nutritional information or other reasons, patients often experience trouble in controlling the amount of calories they consume. There are lots of proposed methods to estimate calories based on computer vision [2, 3, 4, 5], but after the authors’ analysis, the accuracy of detection and volume estimation still need to be improved. In this paper, the main difference from other similar approaches is that it requires an input of two images, and the use Faster R-CNN to detect the object and GrabCut algorithm to obtain each food’s contour. After that, the authors can estimate each food’s volume and calories.

Material and Methods

A. Calorie Estimation Method Based On Deep Learning

This method is shown in Figure 1. As mentioned before, the process of estimating calories requires two images from top and side, and each image should include the calibration object. Here, the authors choose Faster Region-based Convolutional Neural Networks (Faster R-CNN) [5] to detect objects, and GrabCut algorithm [6] as the segmentation algorithm.

B. Deep Learning Based Objection Detection

The authors chose Faster R-CNN instead of using semantic segmentation method such as Fully Convolutional Networks (FCN). Here, after the images are inputted as RGB channels, the authors can get a series of bounding boxes, which means the class if judged.

C. Image Segmentation

This process uses an image processing approach to segment each bounding box. As mentioned above, the bounding boxes around the object that GrabCut needs can be provided by Faster R-CNN. After segmentation, we can get a series of food images stored in matrix, but with the the values of the background pixels being replaced by zeros. This will leave only the foreground pixels.

D. Volume Estimation

To estimate the volume, the authors calculate the scale factors based on calibration objects. The authors use a 1 CNY coin to show the specific process of calculating the volume. The diameter of the coin is 2.5 cm, and the side view’s scale factor was calculated with Equation 1.

(alpha)s=5/(Ws+Hs)

In this equation, Ws is the width of the bounding box, Hs is the height of the bounding box. Similarly, the top view’s scale can be calculated with Equation 2.

(alpha)t=5/(Wt+Ht)

After, the authors divide the foods into three categories based on shape: ellipsoid, column, irregular. Different volume estimation formula will be selected for different types of food, according to Equation 3. HS is the height of side view PS and LkS is the number of foreground pixels in row k (k ∈ 1,2,…,HS). LMAX = max(Lk ,…,Lk ), it records the maximum number of foreground pixels in PS. ß is a compensation factor (default value = 1.0). After that, for each food type there will be a unique value.
