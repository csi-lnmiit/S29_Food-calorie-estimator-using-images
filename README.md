# S29_Food-calorie-estimator-using-images

Due to the advance in people’s standards of living, fat rates square measure increasing at associate forbidding speed, and this can be reflective to the risks in people’s health. individuals ought to management their daily calorie intake by consumption healthier foods, that is that the most elementary technique to avoid fat. However, though food packaging comes with nutrition (and calorie) labels, it’s still not terribly convenient for individuals to reference. Thus, scientists began to use machine learning algorithms in laptop vision to assist individuals verify the caloric worth within the food they eat. throughout the 2015 work Deep Learning Summit in capital of Massachusetts, Google human Kevin white potato conferred a deep learning algorithmic rule that was wont to analyze static food image. By analyzing the composition of the food in image, the algorithmic rule will calculate what quantity calories the dish has.

This paper is attempting to produce a a lot of economical approach of estimating calories. First, it desires the highest read and aspect pictures of the food being analyzed. Then, it'll use quicker R-CNN to sight the food and standardisation object, once that, a GrabCur algorithmic rule is employed to work out the food’s contour. once estimating the amount of food, the authors will finally estimate the number of calories.

INTRODUCTION

When people’s Body Mass Index (BMI) is over thirty (kg/m2), they're usually thought-about to be corpulent. High BMI will increase the chance of diseases like cardiopathy [1]. the most reason of fat is attributable to the imbalance between the number of caloric intake (consumption) and energy output (expenditure). due to disposition to record and track, lack of connected nutritionary info or alternative reasons, patients typically expertise hassle in dominant the number of calories they consume. There square measure countless projected strategies to estimate calories supported laptop vision [2, 3, 4, 5], however once the authors’ analysis, the accuracy of detection and volume estimation still ought to be improved. during this paper, the most distinction from alternative similar approaches is that it needs associate input of 2 pictures, and also the use quicker R-CNN to sight the item and GrabCut algorithmic rule to get every food’s contour. After that, the authors will estimate every food’s volume and calories.

Material and strategies

A. Calorie Estimation technique supported Deep Learning

This technique is shown in Figure one. As mentioned before, the method of estimating calories needs 2 pictures from prime and facet, and every image ought to embrace the standardisation object. Here, the authors select quicker Region-based Convolutional Neural Networks (Faster R-CNN) [5] to sight objects, and GrabCut algorithmic rule [6] because the segmentation algorithmic rule.

B. Deep Learning based mostly Objection Detection

The authors selected quicker R-CNN rather than victimisation linguistics segmentation technique like absolutely Convolutional Networks (FCN). Here, once the pictures square measure inputted as RGB channels, the authors will get a series of bounding boxes, which implies the category if judged.

C. Image Segmentation

This method uses a picture process approach to section every bounding box. As mentioned on top of, the bounding boxes round the object that GrabCut desires are often provided by quicker R-CNN. once segmentation, we will get a series of food pictures keep in matrix, however with the the values of the background pixels being replaced by zeros. this can leave solely the foreground pixels.

D. Volume Estimation

To estimate the amount, the authors calculate the dimensions factors supported standardisation objects. The authors use a one CNY coin to indicate the particular method of conniving the amount. The diameter of the coin is two.5 cm, and also the facet view’s multiplier factor was calculated with Equation one.

(alpha)s=5/(Ws+Hs)

In this equation, Ws is that the breadth of the bounding box, Hs is that the height of the bounding box. Similarly, the highest view’s scale are often calculated with Equation two.

(alpha)t=5/(Wt+Ht)

After, the authors divide the foods into 3 classes supported shape: ellipsoid, column, irregular. completely different volume estimation formula are elect for various forms of food, in keeping with Equation three. HS is that the height of aspect notation and LkS is that the variety of foreground pixels in row k (k ∈ one,2,…,HS). LMAX = max(Lk ,…,Lk ), it records the utmost variety of foreground pixels in notation. ß could be a compensation issue (default worth = one.0). After that, for every food kind there'll be a singular worth.

E. Calorie Estimation

After estimating the amount, consecutive step is to estimate every food’s mass. It are often calculated in Equation four, wherever v (cm^3) represents the amount of current food, and ρ (g/cm^3) represents its density worth
m=p*v
Then the calorie of the food are often obtained with Equation five.
C=c*m
Where m(g) represents the mass of current food and c(Kcal/g) represents its calories per gram.

Conclusion


Since the pictures square measure taken from smartphones, and also the image process strategies used here square measure well-developed, this projected technique are often simply integrated into health apps as associate engineering resolution. however, from a look perspective, i feel this paper has 2 limitations. First, there's no comparison with previous work. The authors did offer a literature review within the introduction, however i feel they must have compared their results with the leads to those previous work. If this approach can do a higher performance, then we will say that this paper provides a simpler approach. sadly we tend to cant’s say that, as a result of the author didn’t offer a series of comparison experiment. Secondly, i'm unsure if the dataset is correct or large enough. The authors simply say that they take the pictures from a smartphone, however they didn’t tell whether or not there's a regular to gather the pictures. just like the strength, and also the variety of pixels. Besides, in Table two we will see that the mean error remains massive, that indicates that there's some area to create the mean error a lot of smaller.
