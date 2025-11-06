% --------------------------------------------------------------
% IMAGE PROCESSING OPERATIONS IN MATLAB
% Edge Detection | Histogram Equalization | Noise Reduction | Morphology
% --------------------------------------------------------------

clc; clear; close all;

% Read Input Image
img = imread('your_image.jpg');   % Change the image name if required

% Convert to Grayscale
gray = rgb2gray(img);

% -----------------------------
% 1. Histogram Equalization
% -----------------------------
hist_eq = histeq(gray);

% -----------------------------
% 2. Noise Reduction
% (Median Filtering for Salt & Pepper Noise + Gaussian Filtering)
% -----------------------------
% Add Noise for demonstration (optional)
noisy_img = imnoise(gray, 'salt & pepper', 0.02);

median_filtered = medfilt2(noisy_img, [3 3]);
gaussian_filtered = imgaussfilt(gray, 2);

% -----------------------------
% 3. Edge Detection
% Using Canny, Sobel & Prewitt
% -----------------------------
edges_canny = edge(gray, 'canny');
edges_sobel = edge(gray, 'sobel');
edges_prewitt = edge(gray, 'prewitt');

% -----------------------------
% 4. Morphological Processing
% (Dilation, Erosion, Opening, Closing)
% -----------------------------
se = strel('disk', 3);  % structuring element

dilated = imdilate(gray, se);
eroded = imerode(gray, se);
opened = imopen(gray, se);
closed = imclose(gray, se);

% ------------------------------------------------------------
% DISPLAY RESULTS
% ------------------------------------------------------------

figure('Name','Image Processing Results','NumberTitle','off');

subplot(3,4,1); imshow(img); title('Original Image');
subplot(3,4,2); imshow(gray); title('Grayscale');
subplot(3,4,3); imshow(hist_eq); title('Histogram Equalized');
subplot(3,4,4); imhist(gray); title('Original Histogram');

subplot(3,4,5); imshow(noisy_img); title('Noisy Image');
subplot(3,4,6); imshow(median_filtered); title('Median Filtered');
subplot(3,4,7); imshow(gaussian_filtered); title('Gaussian Filtered');
subplot(3,4,8); imhist(hist_eq); title('Equalized Histogram');

subplot(3,4,9); imshow(edges_canny); title('Canny Edge');
subplot(3,4,10); imshow(edges_sobel); title('Sobel Edge');
subplot(3,4,11); imshow(edges_prewitt); title('Prewitt Edge');
subplot(3,4,12); imshow(dilated); title('Morphology: Dilation');

figure('Name','Morphological Processing','NumberTitle','off');
subplot(2,2,1); imshow(eroded); title('Erosion');
subplot(2,2,2); imshow(opened); title('Opening');
subplot(2,2,3); imshow(closed); title('Closing');
subplot(2,2,4); imshow(dilated); title('Dilation');
