---
layout: page
title: ImageInquiry
description: Developed a web application utilizing AWS services that allows users to upload images, automatically generate AI-based tags, and add custom tags for efficient image searching.
img: assets/img/projects/image-inquiry/thumbnail.jpg
importance: 2
category: fun
related_publications: false
---

#### 🔗Github: [Backend](https://github.com/deepjyotk/image-inquiry-backend), [Frontend](https://github.com/deepjyotk/image-inquiry-react-app)

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

### Design Decision

1. **Frontend**:

   - **Design Decision**: Use a frontend application to provide a user interface for uploading images and searching for images.
   - **Justification**: The frontend interacts with users, allowing them to upload images and search for tagged images. This provides an intuitive and user-friendly interface, improving user experience.

2. **Amazon Cognito**:

   - **Design Decision**: Utilize Amazon Cognito for user authentication and authorization.
   - **Justification**: Amazon Cognito provides secure user authentication and user management, ensuring that only authorized users can upload and search images. It also integrates well with other AWS services, providing a seamless security layer.

3. **API Gateway**:

   - **Design Decision**: Use AWS API Gateway to create, publish, maintain, monitor, and secure APIs.
   - **Justification**: API Gateway acts as a bridge between the frontend and the backend services. It provides a scalable and reliable way to handle API requests, enabling communication between the frontend and backend Lambda functions securely.

4. **S3**:

   - **Design Decision**: Store images in Amazon S3.
   - **Justification**: Amazon S3 is a highly scalable and durable storage solution. It is well-suited for storing images, providing easy access, and integrating seamlessly with other AWS services like Lambda and Rekognition.

5. **Lambda Functions**:

   - **Upload Handler**:
     - **Design Decision**: Use a Lambda function to handle the uploading of images.
     - **Justification**: The Lambda function processes image uploads, generating pre-signed URLs for secure image upload to S3 and triggering further processing.
   - **AI Label Handler**:
     - **Design Decision**: Use a Lambda function to handle AI-generated labels from Rekognition.
     - **Justification**: This function processes the labels generated by Rekognition, saving them to Elasticsearch and ensuring the data is available for search.
   - **Search Handler**:
     - **Design Decision**: Use a Lambda function to handle search queries.
     - **Justification**: This function processes search requests from the frontend, querying Elasticsearch for relevant images based on labels and returning results to the user.

6. **Amazon Rekognition**:

   - **Design Decision**: Use Amazon Rekognition for object detection in images.
   - **Justification**: Rekognition provides powerful image analysis capabilities, automatically generating labels for objects detected in images. This automates the tagging process, enhancing the searchability of images.

7. **Amazon Comprehend**:

   - **Design Decision**: Use Amazon Comprehend for analyzing entities in search queries.
   - **Justification**: Comprehend processes the search queries to understand the entities involved, improving the accuracy of search results by providing more relevant matches based on the user's intent.

8. **Amazon Elasticsearch Service**:
   - **Design Decision**: Use Amazon Elasticsearch Service for indexing and searching images.
   - **Justification**: Elasticsearch is a powerful search engine that allows for efficient indexing and querying of large datasets. It provides fast and accurate search capabilities, enabling users to quickly find images based on tags.