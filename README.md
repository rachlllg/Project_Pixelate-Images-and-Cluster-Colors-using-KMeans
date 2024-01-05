# Project_Pixelate-Images-and-Cluster-Colors-using-KMeans

Refer to the project page on my website for detailed discussion on the project.

Project page: https://rachlllg.github.io/project/2024-Pixelate_Images_and_Cluster_Colors_using_KMeans/

## Background:
One of my hobbies is designing and creating yarn crafts, I wanted to use C2C technique in crochet to make blankets and needed a reliable (and free) way to create pixelated images and group/cluster the colors in the image to a reasonable number (it would be awfully difficult to make a blanket with 200 different shades of each color 😆). So I figured why not write a Python code to do exactly this!

The pixelation process is written in vanilla Python, while K-Means clustering is used to group the colors. All work was done in Google Colab (Free). Notable Python packages used:
- standard: numpy, pandas
- image processing: PIL Image
- modeling: scikit-learn
- visualization: matplotlib
- parameter validation: pydantic

## Results:
Since K-Means clustering falls within the realm of unsupervised learning, no 'training' was neccessary. The class `Process` takes in below 6 parameters and calls the various supporting functions within the class to process the input image. The parameters are validated using Pydantic.
1. input_image_path (str): Path to the input image file.
2. resize_ratio (float): The ratio by which the image should be resized. 
  - Only positive values are accepted. 
  - Values between 0 and 1 decrease the image size while values > 1 increase the image size.
  - Images are sized to proportion of the original image.
3. grid_size (int): The size of the grid for pixelation.
  - Only positive values are accepted. 
  - This specifies the number of pixels in each grid.
4. do_reduce (bool): Flag indicating whether to reduce the number of colors.
5. cluster_metric (str): Method for identifying number of clusters. 
  - Ignored if do_reduce == False.
  - Acceptable inputs:
    - 'sil': [silhouette method](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html)
    - 'db': [davies bouldin method](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.davies_bouldin_score.html)
    - 'ch': [calinski harabasz method](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.calinski_harabasz_score.html)
6. num_colors (int): Maximum number of colors to reduce to.
  - Ignored if do_reduce == False.
  - Must be >= 2.
  - This specifies the maximum number of clusters for the specified cluster methic in K-Means clustering.

The Google Colab notebook pixelate_cluster_color.ipynb contains the class and example usage. The input_image_path should be updated to your image path, the other parameters can be updated as needed. It is highly recommended to resize the image to a smaller size (using the `resize_ratio` parameter) if the original image is large in size, as processing a large image could take up substantial memory.
