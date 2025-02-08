---
layout: page
title: Mock Mate
description: Mock Mate is a peer-to-peer mock interview platform where users can book slots, get matched with peers, and practice both behavioral and software engineering interviews. It offers an interactive, real-time interview experience with features such as video conferencing, peer feedback, and a comprehensive review of past interviews. The platform is designed to help users prepare for technical and behavioral interviews, enhancing their confidence and readiness for real-world interviews.
img: assets/img/projects/mockmate/thumbnail1.jpg
importance: 1
category: fun
related_publications: false
# giscus_comments: true
---


<!-- #### 🔗Github: [Backend](https://github.com/deepjyotk/image-inquiry-backend), [Frontend](https://github.com/deepjyotk/image-inquiry-react-app) -->


   Technologies Used: Spring Boot, PostgreSQL, Docker, AWS (ECS), Next.JS


## Features


### **Authentication**


- **Login**: Secure user login with email and password.
- **Registration**: Simple registration process to onboard new users.
- **Forgot Password?**: Password recovery functionality for users who forget their credentials.


### **Slot Booking**


- Users can book slots for mock interviews.
- Options for interview type:
 - **Behavioral Interview**
 - **Software Engineering Interview**
- Select difficulty level:
 - **Easy**
 - **Medium**
 - **Hard**


### **Peer Matching**


- Users can join a waiting room for a specific slot.
- A **cron job** periodically pairs users in the waiting room based on the **Peer Matching Algorithm** (explained below).


### **Video Interview Integration**


- **Short Polling**: Ensures real-time updates for peer matching.
- **3rd Party Video Toolkit Integration**: Zego UI Toolkit used to support smooth video conferencing between matched peers.


### **Interactive Interview Experience**


- **Question Distribution**: Once peers are matched, both users receive an interview question to ask each other. Questions are tailored to the user's difficulty choice.
- **Real-time Video Call**: Users can discuss the question and interview each other in real time.
- **Post-Interview Feedback**: After the session, users can provide feedback on their peer's performance.


### **Past Interview Review**


- Users can access a history of their past interviews.
- View feedback received from past peers to track improvement over time.


<div class="row">
   <div class="col-sm mt-3 mt-md-0">
       {% include figure.liquid loading="eager" path="assets/img/projects/mockmate/image1.png" title="example image" class="img-fluid rounded z-depth-1" %}
   </div>
   <div class="col-sm mt-3 mt-md-0">
       {% include figure.liquid loading="eager" path="assets/img/projects/mockmate/image2.png" title="example image" class="img-fluid rounded z-depth-1" %}
   </div>
   <div class="col-sm mt-3 mt-md-0">
       {% include figure.liquid loading="eager" path="assets/img/projects/mockmate/image3.png" title="example image" class="img-fluid rounded z-depth-1" %}
   </div>
</div>
<!-- <div class="caption">
  On the left, an image of the upload page features AI-generated labels and custom labels. In the middle, a user performs searches using an AND query. On the right, a user conducts searches using an OR query.
</div> -->


## Architecture


The platform follows a **microservices-based architecture** with the following key components:


- **Authentication Service**: Manages user login, registration, and password recovery.
- **Peer Matching Service**: Handles the waiting room, peer matching, and cron job logic.
- **Interview Service**: Manages the interview process, video call integration, and question distribution.
- **Frontend UI**: Built using Next.js to provide an interactive user experience.
- **Database**: PostgreSQL database for persisting user information, bookings, and feedback.


                    ┌──────────────┐
                     │  User (UI)   │
                     └──────────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │  Next.js Frontend    │
                └─────────────────────┘
                           │
                           ▼
           ┌────────────────────────────┐
           │  Backend API (Spring Boot)  │
           └────────────────────────────┘
               │       │          │
               ▼       ▼          ▼
        Authentication   Interview    Peer Matching
             Service       Service       Service
                           │
                           ▼
                      PostgreSQL DB


## **Peer Matching Algorithm**


The Peer Matching Algorithm aims to create interview pairs from users in the same room with minimal waiting time.


### **Matching Criteria**


1. **Difficulty Preference**: Users are grouped into Easy (E), Medium (M), and Hard (H) based on the difficulty of the interview.
2. **Pairing Logic**:
  - Users with the same difficulty are paired together.
  - If no user with the same difficulty is available, the next best option is chosen, as demonstrated below.


#### **Example**


If the interview room has:


E1, E2, E3, M1, M2, H3


Where:


- **E** \= Easy difficulty users
- **M** \= Medium difficulty users
- **H** \= Hard difficulty users


The pairs are created as:


- Pair 1: **{E1, E2}** (Easy with Easy)
- Pair 2: **{E3, M1}** (Easy with Medium)
- Pair 3: **{M2, H3}** (Medium with Hard)


If there are no available users to pair, the user waits until the next cron job cycle to be paired.


### Motivation


Motivated by the lack of collaborative interview preparation platforms, Mock Mate aims to provide an interactive, peer-driven experience for both behavioral and technical interviews.


## **Usage**


1. **Register** as a new user or **login** to your existing account.
2. **Book a Slot** for your interview by selecting the date, time, interview type, and difficulty.
3. **Join the Waiting Room** at the selected slot time.
4. **Get Matched** with a peer based on your preferences.
5. **Start the Interview** using the video interview functionality.
6. **Review Feedback** from your peer and access a history of past interviews.


## **Future Scope**


1. **WebSockets for Real-Time Updates**
  - Replace short polling with **WebSocket** connections for real-time updates, significantly improving performance and responsiveness.
2. **Custom Interview Questions**


  - Allow users to select the company they are preparing for (like Google, Amazon, etc.), and generate interview questions related to that company.


3. **Collaborative Code Editor**
  - Add a **collaborative editor** where users can write, compile, and debug code together during technical interviews.
  - Plan to use a 3rd party API for collaborative editing.
4. **In-App Notifications**
  - Notify users about interview slot availability, peer matching status, and feedback reminders.
5. **Feedback Analytics**
  - Show analytics to users based on past feedback and interview performance.



