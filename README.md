# ARSOCIAL

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)

## Overview
### Description
Creates an AR image with a virtual product so the user can see what it would look like in real life. Could be a shareable gallery with others with editable features

### App Evaluation
- **Category:** AR imaging/camera app (marketing, consumer goods, social)
- **Mobile:** This app would be primarily developed for mobile, uses camera
- **Story:** Creates AR imaging and a platform to share the images The user can then decide to message this person and befriend them if wanted.
- **Market:** Any individual could choose to use this app for image sharing and creation
- **Habit:** This app could be used as frequently or infrequently as the user wanted depending on needs, and what exactly they're looking for before buying a product. Major incentive for businesses to participate in order to make product seem more available
- **Scope:** First we would prompt the user to give AR permissions on the app and to take pictures. Then the user would choose the type of product(s) they want to try and is modelled onto themselves with AR. Then, the user has the option to save the picture in their gallery and share it with others for input.






## Product Spec
### 1. User Stories (Required and Optional)

**Required Must-have Stories**
* User logs in 
* User has and marks their favorite products
* User can take images and place AR item
* User can post images
* User can follow others
* Profile pages for each user 
* User can message images to others 
* Settings (Accessibility, Notification, General, etc.)

**Optional Nice-to-have Stories**
* User can comments on others’ posts
* Rating and/or thumbs up/thumbs down

### 2. Screen Archetypes
* Login
* Register - User signs up or logs into their account (social media connection)
  * Upon Download/Reopening of the application, the user is prompted to log in to gain access to their profile information to be properly matched with another person.
* Profile - displays user profile picture, bio, and saved products
* Create - user is prompted to create post based on products they’ve tried via AR
* Stream - user’s homepage is a discover streaming page that displays products they would most likely be interested in
* AR - user can choose product to test out in AR screen and then save/share

### 3. Navigation

**Tab Navigation** (Tab to Screen)

**Flow Navigation** (Screen to Screen)
* Discover feed
* Friends feed 
* Camera AR placement view
* Forced Log-in -> Account creation if no login is available
* Product Selection -> Try-on (AR)
* Profile -> Text field to be modified. 
* Settings -> Toggle settings

Optional:

* Discover (Top Choices)
* Messaging Screen - Chat for users to communicate (direct 1-on-1)
* Settings Screen
   * Lets people change language, and app notification settings, etc

## Wireframes

### [BONUS] Digital Wireframes & Mockups
<img src="https://i.imgur.com/z8Vdoyz.png">

## Schema 
### Models
#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User| image author |
   | image         | File     | image that user posts |
   | caption       | String   | image caption by author |
   | commentsCount | Number   | number of comments that has been posted to an image |
   | ratingAvg    | Number   | average rating for post |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         ```
      - (Create/POST) Create a new rating on a post
      - (Delete) Delete a rating on a post
      - (Create/POST) Create a new comment on a post
      - (Delete) Delete existing comment
   - Create Post Screen
      - (Create/POST) Create a new post object
   - Profile Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile image
      - (Update/PUT) Update user interests, description and following
