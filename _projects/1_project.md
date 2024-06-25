---
layout: page
title: ImageInquiry
description: Developed a web application utilizing AWS services that allows users to upload images, automatically generate AI-based tags, and add custom tags for efficient image searching.
img: assets/img/12.jpg
importance: 1
category: work
related_publications: false
--- 
#### Github: [Backend](https://github.com/deepjyotk/lf1-image-indexing), [Frontend](https://github.com/deepjyotk/image-inquiry-react-app)
    Technologies Used: React, AWS(Lambda, ElasticSearch, Cognito, S3, DynamoDB, AWS CDK, Github Actions)

### Features
1. Users can upload images to the platform.
2. The application uses AWS Rekognition for object detection, which automatically generates labels for uploaded images.
3. Users can also add custom tags to enhance searchability.
4. Images and tags are indexed and stored using AWS services, facilitating efficient and quick searches based on specific queries (e.g., "show me images of apples and grapes").
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/image-inquiry/upload.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/image-inquiry/and_query.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/image-inquiry/or_query.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
   On the left, an image of the upload page features AI-generated labels and custom labels. In the middle, a user performs searches using an AND query. On the right, a user conducts searches using an OR query.
</div>
### Architecture
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/image-inquiry/architecture.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    ImageInquiry HLD Architecture
</div>

### Motivation
Designed to help users effortlessly locate photos based on context or content, enhancing the retrieval of memory-specific images like recalling a beach visit where pineapple was enjoyed.

### Usecases

1. Event Planners and Photographers: Quickly locate event-specific images by searching for tags like "Smith Wedding June 2024."
2. Travel Enthusiasts: Easily find travel photos by querying specific locations or activities, such as "Eiffel Tower night."
3. Academic Researchers and Students: Manage and retrieve academic images efficiently by tagging them with relevant study terms.
4. Marketing Professionals: Sort and access marketing materials by campaign or brand tags, such as "2023 Q3 Campaign."
5. Home Organizers and Interior Designers: Organize and compare interior designs by searching images tagged by room type or style.

<!-- The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
``` -->

{% endraw %}
