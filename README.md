Download Link: https://assignmentchef.com/product/solved-comp6341-programming-assignment-2
<br>
<h1>DESCRIPTION</h1>

In this assignment, you will write code to detect discriminating features in an image and find the best matching features in other images. Because features should be reasonably invariant to translation, rotation (plus illumination and scale if you do the extra credit), you’ll use a feature descriptor discussed during lecture and you’ll evaluate its performance on a suite of benchmark images. As part of the extra credit you’ll have the option of creating your own feature descriptors.

<em>In the Project</em>, you will apply your features to automatically stitch images into a panorama.

<strong>DESIGN A FEATURE DETECTOR</strong>

This involves three steps: feature detection, feature description, and feature matching.

<h1>Feature detection</h1>

In this step, you will identify points of interest in the image using the Harris corner detection method. The steps are as follows (see the lecture slides/readings for more details):

<ol>

 <li>For each point in the image, consider a window of pixels around that point.</li>

 <li>Compute the Harris matrix H for that point, defined as:</li>

</ol>

where the summation is over all pixels <em>(u,v)</em> in the window. The weights <em>w(.,.)</em> should be chosen to be circularly symmetric (for rotation invariance). A common choice is to use a <a href="http://homepages.inf.ed.ac.uk/rbf/HIPR2/gsmooth.htm">3×3 or 5×5 </a><a href="http://homepages.inf.ed.ac.uk/rbf/HIPR2/gsmooth.htm">Gaussian mask</a>. Note that H is a 2×2 matrix. To find interest points, first compute the corner strength function (the “Harris operator”).

Once you’ve computed <strong><em>c</em></strong> for every point in the image, choose only the points for which their <strong><em>c</em></strong> is above a userdefined threshold. You also want <strong><em>c</em> </strong>to be a local maximum in at least a 3×3 neighborhood.

<h1>Feature description</h1>

Now that you’ve identified points of interest, the next step is to come up with a descriptor for the feature centered at each interest point [rotational invariance should be taken into account in this step]. This descriptor will be the representation you’ll use to compare features in different images to see if they match.

<h1>Feature matching</h1>

Now that you’ve detected and described your features, the next step is to write code to match them, i.e., given a feature in one image, find the best matching feature in one or more other images. This part of the feature detection and matching component is mainly designed to help you test out your feature descriptor. The simplest approach is the following: write a procedure that compares two features and outputs a distance between them. For example, you could simply sum the absolute value of differences between the descriptor elements. You could then use this distance to compute the best match between a feature in one image and the set of features in another image by finding the one with the smallest distance.

Two distance measures you should implement are:

<ol>

 <li>A threshold on the match score. This is called the SSD distance.</li>

 <li>(score of the best feature match)/(score of the second best feature match). This is called the “ratio test”.</li>

</ol>

<h1>Testing</h1>

Using the OpenCV API you can load in a set of images, view the detected features using cv::drawKeypoints(…), and visualize the feature matches that your algorithm computes using cv::drawMatches(…).

We are providing a set of benchmark images to be used to test the performance of your algorithm as a function of different types of controlled variation (i.e., rotation, scale, illumination, perspective, blurring).

Here is a list of suggestions for extending the program for extra credit. You are encouraged to come up with your own extensions as well. Feature detection and matching is an active area in computer vision – there are many interesting techniques you can attempt here based on techniques on the literature and on your own ideas.

<ol>

 <li>Make your feature more contrast invariant. This was discussed in lecture.</li>

 <li>Implement adaptive non-maximum suppression (<a href="https://www.google.ca/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=2&amp;cad=rja&amp;uact=8&amp;ved=0ahUKEwjH3-vrpezKAhVFdT4KHUD8B2AQFggpMAE&amp;url=http%3A%2F%2Fresearch.microsoft.com%2Fpubs%2F70120%2Ftr-2004-133.pdf&amp;usg=AFQjCNFCqGlqZEQlPE-OF-Ehwvhlx3Yjxw&amp;sig2=62aRLm6E_oyaEuJ2kGhYEg">MOPS paper</a>).</li>

 <li>Make your feature detector scale invariant.</li>

 <li>Implement a method that outperforms the SSD ratio test for deciding if a feature is a valid match.</li>

 <li>Use a fast search algorithm to speed up the matching process. You can use code from the web or write your own (with extra credit proportional to effort). Some possibilities in, rough order of difficulty: k-d trees (<a href="http://www.cs.umd.edu/~mount/ANN/">code available here</a>), wavelet indexing, <a href="http://web.mit.edu/andoni/www/LSH/index.html">locality</a><a href="http://web.mit.edu/andoni/www/LSH/index.html">sensitive hashing.</a></li>

</ol>


