# Questions for Quiz 3

There is no summary or questions for the theory. I didn't feel good enough to do it. I'm sorry.

# Quiz 2021/2022

### 1:

**Consider the set of pixels represented in the image, and assume as similarity criterion for pixels
to be considered neighbors that their values belong to the subset V = {1,3}.
Determine the shortest length of the (i) 4-, (ii) 8- and (iii) m-, paths between (p) and (q)**

![img](https://i.imgur.com/4Nos8TZ.png)

Ok, knowing that the values of the pixels are considered neighbors if they belong to the subset V = {1,3}.

(i) 4-path:

|   | 1 |   |
|---|---|---|
| 1 | x | 1 |
|   | 1 |   |

And since there is no 1 or 3 in the pixels for the 4-path, **no path exists.**

(ii) 8-path: Since for the 8-path we consider something like:

| 1 | 1 | 1 |
|---|---|---|
| 1 | x | 1 |
| 1 | 1 | 1 |

We can go diagonally, and since there are positions in which pixels are 1 or 3, the path is of length : **4**

(iii) m-path: The m-path is strange. You have to take the neighbors of the pixel and check if they are in the subset V, then check if the neighbor you want to go is in the 4-neighborhood of the neighbor you are in. If it is, you can go there. If not, you can't. Moreover, if nothing is possible, take the diagonal.

So, the path is:

1 -> 1 -> 1 -> 1 -> 1 -> 3 -> 1 -> 1

![img](https://i.imgur.com/X8C9j4G.png)

I think it's like this.

### 2:

**Consider the following image and its histogram.
Suggest a set of image processing operations that
could be used to enhance the image quality.
When possible, indicate values of relevant
parameters of the proposed techniques.
Explain what aspects of the image quality will be
improved, and why they will be improved**

![tremendo](https://i.imgur.com/K72Kj4k.png)

In my opinion, there is the need of a **histogram equalization**. The image is too much focused on te middle values, and the contrast is not good. The histogram is not well distributed, and the image is too dark.
Ok since in the histogram there is a little bit of noise, is goot to apply some thresholding and remove everything under the 90 value. This will remove the noise and make the image more clear.

### 3:

**Specify a 3x3 filtering mask that could be used to detect vertical edges in an image.**

The mask is:

| -1 | 0 | 1 |
|----|---|---|
| -1 | 0 | 1 |
| -1 | 0 | 1 |

Explanation: We put a **-1** in the first column, a **0** in the middle and a **1** in the last column. This works because the mask is looking for a change in the pixel values in the vertical direction. If the pixel values change, the mask will give a high value, otherwise, it will give a low value.


If we wanted an horizontal edge, we would have to change the mask to:

| -1 | -1 | -1 |
|----|----|----|
| 0  |  0 |  0 |
| 1  |  1 |  1 |

### 4:

**The image on the left was processed with the help of morphological operations, to get the result
on the right. Explain what processing operations may have been applied**

![img](https://i.imgur.com/D1JuEid.png)

The answer is: 
- Original – morphological erosion with 3x3 square structuring element
- Alternative: morphological dilation – original

The image on the left is a white figure on a black background. On the right we have only the borders.

The explanation is that the morphological erosion with a 3x3 square structuring element will remove the borders of the figure, and the dilation will remove the background, leaving only the borders.

### 5:

**Consider an image of size 100 x 100 pixels, with each pixel taking values in: {0, 1, 2, 3}.**

The image histogram (rk) is as specified in the table below.

![](https://i.imgur.com/AUW8PyQ.png)
a) Compute the new histogram after performing histogram equalization of the image (sk = T(rk)) and the values conversion table (sk(rk)).

table is the following:

| rk | nk|
|----|---|
0 | 3000
1 | 1000
2 | 2000    
3 | 4000 

We want to calculate:

|rk | sk|
|---|---|
|0  | ? |
|1  | ? |
|2  | ? |
|3  | ? |

How to do it?

Knowing that the result is:

| rk | sk |
|----|----|
| 0  | 1  |
| 1  | 1  |
| 2  | 2  |
| 3  | 3  |

We can calculate the sk values by doing:

$$sk = (L-1) * \sum_{j=0}^{k} \frac{nj}{N}$$

Where L is the number of different values in the image, N is the total number of pixels and nk is the number of pixels with value k.

So:

0. $$sk = (4-1) * \frac{3000}{10000} = 1$$
1. $$sk = (4-1) * \frac{4000}{10000} = 1$$
2. $$sk = (4-1) * \frac{6000}{10000} = 2$$
3. $$sk = (4-1) * \frac{10000}{10000} = 3$$


So at the end the nk pixels are:

|sk | nk|
|---|---|
|0|0|
|1|4000|
|2|2000|
|3|4000|


b) Was a uniform distribution obtained? Why?
No, is not uniform. To be uniform, the histogram should have the same number of pixels for each value. In this case, the number of pixels is not the same for each value. For discrete values is not always possible to have a uniform distribution.

c) What would happen if applying the histogram equalization a second time?
The histogram would be the same. The histogram equalization is a one-time operation. If you apply it again, the histogram will not change.

# Quiz 2022/2023

### 1:

![](https://i.imgur.com/cB4Yp27.png)

Consider the following image and its histogram.
Suggest a pointwise intensity transformation
operation that could be used to enhance the
image quality.
Discuss the merit of your proposal vs. using
histogram equalization

In this case, contrast stretching is a good idea. The image is too dark and the contrast is not good. The histogram is not well distributed. To do it, take the minimum and maximum values of the image and apply the following formula:

$$s = \frac{s - min}{max - min} * L$$

Where s is the pixel value, min is the minimum value of the image, max is the maximum value of the image and L is the number of different values in the image.

The image with the histogram equalization would look less natural, and the contrast stretching is more natural. Instead, constrast stretching is based on the actual maximum and minimum values of the image, resulting in a more natural image.

### 2:

Consider the technique known as Inverse Filtering.
a) In what does this technique consist of and for what purpose is it used?

Inverse filtering is a technique used restaurate the image. Some images can be blurried or distorted by a filter. The inverse filtering is used to remove the filter and restore the original image.

b) What needs to be known for this technique to be applicable, and what are its main
limitations?

You need to know the degradation model, like blur or distortion. The main limitation is that the inverse filtering is very sensitive to noise. If the image is noisy, the inverse filtering will not work.

### 3:

Consider an image of size 100x100 pixels, with the possible pixel values of: {0, 1, 2, 3}.
The image histogram (rk) is as specified in the table below.

![](https://i.imgur.com/cFM1a8B.png)

- a) Compute the new histogram after performing histogram equalization of the image (sk = T(rk)) and the values conversion table (sk(rk)).
Knowing the table is:

|rk|nk|
|--|--|
|0|1000|
|1|500|
|2|5000|
|3|3500|

We need to use the formula:

$$ (L-1) * \sum_{j=0}^{k} \frac{nj}{N} $$

Where L is the number of different values in the image, N is the total number of pixels and nk is the number of pixels with value k.

So, let's go:

0. $$sk = (4-1) * \frac{1000}{10000} = 0.3$$
1. $$sk = (4-1) * \frac{1500}{10000} = 0.45$$
2. $$sk = (4-1) * \frac{6500}{10000} = 1.95$$
3. $$sk = (4-1) * \frac{10000}{10000} = 3$$


So the new histogram is:

|rk|sk|
|--|--|
|0|0|
|1|0|
|2|2|
|3|3|

- b) Was a uniform distribution obtained? Why?

|sk|nk|
|--|--|
|0|1500|
|1|0|
|2|5000|
|3|3500|

No, the distribution is not uniform. To be uniform, the histogram should have the same number of pixels for each value. In this case, the number of pixels is not the same for each value. For discrete values is not always possible to have a uniform distribution.

### 4:

What is the minimum number of monochromatic light sources needed to produce white light?
Justify your answer

To produce white you can use 3 colors like red green and blue.
Another way is to use 2 complementary colors like red and cyan, green and magenta, blue and yellow. This will produce white light.

### 5:

The image on the left (A) was processed, with the help of morphological operations using a 3x3
square structural element (S), to get the result on the right (B). Identify, justifying your option,
the applied operations:

![](https://i.imgur.com/aFmwGEe.png)

a) $$B = (A \circleddash  S) \cap A^C$$
b) $$B = (A \bigoplus  S)^C \cap A$$
c) $$B = (A \circleddash  S)^C \cap A$$

In this case, the *c* operation is the correct one. It is an erosion followed with the intersection of the main image.