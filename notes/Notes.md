# Attempt 1: Barebones
Trained a model on the dataset as is, without any changes.

![[Pasted image 20240315205644.png]]

The model is learning but is being prone to massive overfitting. This issue could arise from many places but the first thing to do is try and simplify the problem and try with a smaller set of data.

So this happens because the split was 8.7K:200 which was wrong. It felt to memorizing/overfitting.
# Attempt 2: Data Split & Class Reduction
Maybe the base model im using might be wrong. https://pyimagesearch.com/2017/03/20/imagenet-vggnet-resnet-inception-xception-keras/

Also, gonna split the dataset from 8.7K images as:

base -> 70/30 : **train**/test
**train** -> 70/30 : train/valid

And change it to only the top 10 classes, the ones containing the highest samples.

![[Pasted image 20240315203703.png]]

This shows the model is actually learning but the validation curve shows it could use some fine-tuning. This shows that dropout layer needs a bit of tuning to lower overfitting rate. 

Now that the mode is learning, we drop the validation data and split the full data in a 70/30 split for train/test. 

Final Training Accuracy: 95.74% 
Final Validation Accuracy: 86.10%
# Attempt 3: Dropout Layer Optimization
So, reducing the classes showed that the model is starting to learn and overfitting is being dealt with, even if it's a little prevalent to it. 

So we add back all the 50 classes and a range of values for dropout layer, starting with 3 values: 0.2, 0.4, 0.5 and see how each model performs.

Result:
The best dropout layer value was 0.2. 

Through classification report and confusion matrix, 

two classes that contain similarity: water pump, vacuum brake booster, gas cap  

remove top 5 worst performers and check avg performance