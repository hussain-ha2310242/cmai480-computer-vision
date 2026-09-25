# IMAGE PROCESSING

## Color channels
```matlab
I0 = imread("images/pengu.jpg");
imshow(I0)
```

![figure_0.png](img_basics_media/figure_0.png)

```matlab
size(I0)
```

```matlabTextOutput
ans = 1x3
        1800        2880           3


```

```matlab
max(max(I0))
```

```matlabTextOutput
ans = 1x1x3 uint8 array
ans(:,:,1) =


   242


ans(:,:,2) =


   248


ans(:,:,3) =


   255


```

```matlab
I = I0/255;
I_col = zeros(size(I));


for i = 1:3
    I_col(:, :, i) = I(:, :, i);
    figure
    imshow(I_col);
end
```

![figure_1.png](img_basics_media/figure_1.png)

![figure_2.png](img_basics_media/figure_2.png)

![figure_3.png](img_basics_media/figure_3.png)

```matlab


figure
```

## Image Conversion
```matlab


I1 = imread("images/honey-comb.jpg");
imshow(rgb2gray(I1))
```

![figure_4.png](img_basics_media/figure_4.png)

```matlab
for i = [2 5 50]
    [X, map] = rgb2ind(I1, i);
    figure; imshow(X, map)
end
```

![figure_5.png](img_basics_media/figure_5.png)

![figure_6.png](img_basics_media/figure_6.png)

![figure_7.png](img_basics_media/figure_7.png)

## Sampling
```matlab
[r, c, s] = size(I1);
N = 2;
I1s = I1/255;
y = zeros(size(I1s));
y(1:N:r, 1:N:c, :) = I1s(1:N:r, 1:N:c, :);
imshow(y)
```

![figure_8.png](img_basics_media/figure_8.png)

## Noisy Image
```matlab
imshow(imnoise(I1s, "gaussian", 0, 1));
```

![figure_9.png](img_basics_media/figure_9.png)

```matlab
imshow(imnoise(I1s, "salt & pepper", 0.19));
```

![figure_10.png](img_basics_media/figure_10.png)

## Bit Resolution
```matlab


b = [7 6 5];
for i = 1 : length(b)
    d = 2^b(i);
    z = round(I1/d);
    figure
    imshow(z*d)
end
```

![figure_11.png](img_basics_media/figure_11.png)

![figure_12.png](img_basics_media/figure_12.png)

![figure_13.png](img_basics_media/figure_13.png)

## Image Operations
```matlab
I2 = imread("images/zebra.jpg");
imshow(I2, []);
```

![figure_14.png](img_basics_media/figure_14.png)

```matlab


I1c = I1(1:627, 1:1200, :);


imshow(0.3 * I2);
```

![figure_15.png](img_basics_media/figure_15.png)

```matlab


imshow(0.7 * I2 + 0.3 * I1c);
```

![figure_16.png](img_basics_media/figure_16.png)

```matlab
imshow(0.7 * I1c + 0.3 * I2);
```

![figure_17.png](img_basics_media/figure_17.png)

```matlab


% imadd()
imshow(imadd(I2, I1c));
```

![figure_18.png](img_basics_media/figure_18.png)

```matlab
imshow(imsubtract(I2, I1c));
```

![figure_19.png](img_basics_media/figure_19.png)

```matlab
imshow(I2 - I1c);
```

![figure_20.png](img_basics_media/figure_20.png)

```matlab
imshow(I1c - I2);
```

![figure_21.png](img_basics_media/figure_21.png)

```matlab
imshow(imabsdiff(I2, I1c));
```

![figure_22.png](img_basics_media/figure_22.png)

```matlab
%image subtraction is useful for scene change detection
imshow(imdivide(I1c, I2));
```

![figure_23.png](img_basics_media/figure_23.png)

## Ex: Double the columns to have mirror image
```matlab
I2s = im2double(I2);
[r, c, s] = size(I2s);
res = zeros(r, c*2, s);
I2m = flip(I2s, 2);
res(:,1:2:size(res, 2)-1,:) = I2s(:,:,:);
res(:,2:2:size(res, 2),:) = I2m(:,:,:);
imshow(res);
```

![figure_24.png](img_basics_media/figure_24.png)