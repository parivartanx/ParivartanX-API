# UIDMT API Documentation

Base URL: https://uidmt-backend.vercel.app/api/1.0/

## Table of Contents
- [Authentication & User Routes](#authentication--user-routes)
- [Course Routes](#course-routes)
- [Offline Course Routes](#offline-course-routes)
- [Order Routes](#order-routes)
- [Layout Routes](#layout-routes)
- [Analytics Routes](#analytics-routes)
- [Notification Routes](#notification-routes)

## Authentication & User Routes

### Register User
- **POST** `/users/signup`
- **Description**: Register a new user
- **Body Validation**: Required
- **Auth**: Not required
- **Request Body Example**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "avatar": "optional-avatar-url"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Registration successful. Please check your email for verification."
  }
  ```

### Login User
- **POST** `/users/login`
- **Description**: Login existing user
- **Body Validation**: Required
- **Auth**: Not required
- **Request Body Example**:
  ```json
  {
    "email": "john@example.com",
    "password": "password123"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "accessToken": "jwt_access_token",
    "user": {
      "name": "John Doe",
      "email": "john@example.com",
      "role": "user",
      "isVerified": true,
      "avatar": "avatar_url"
    }
  }
  ```

### Email Verification
- **POST** `/users/email-verification`
- **Description**: Verify user email
- **Body Validation**: Required
- **Auth**: Not required
- **Request Body Example**:
  ```json
  {
    "email": "john@example.com",
    "verificationCode": "123456"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Email verified successfully"
  }
  ```

### Resend Verification Code
- **POST** `/users/resend-email-verification`
- **Description**: Resend email verification code
- **Body Validation**: Required
- **Auth**: Not required
- **Request Body Example**:
  ```json
  {
    "email": "john@example.com"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Verification code sent successfully"
  }
  ```

### Refresh Token
- **GET** `/users/refresh-token`
- **Description**: Get new access token
- **Auth**: Not required

### Password Reset Request
- **POST** `/users/request-forget-password`
- **Description**: Request password reset
- **Body Validation**: Required
- **Auth**: Not required
- **Request Body Example**:
  ```json
  {
    "email": "john@example.com"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Password reset link sent to your email"
  }
  ```

### Reset Password
- **POST** `/users/forget-password`
- **Description**: Reset user password
- **Body Validation**: Required
- **Auth**: Not required
- **Request Body Example**:
  ```json
  {
    "resetToken": "valid_reset_token",
    "newPassword": "newpassword123"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Password reset successful"
  }
  ```

### Logout
- **POST** `/users/logout`
- **Description**: Logout user
- **Auth**: Required

### Get User Profile
- **GET** `/users/profile`
- **Description**: Get logged in user profile
- **Auth**: Required

### Update User Profile
- **PATCH** `/users/profile`
- **Description**: Update user details
- **Body Validation**: Required
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "name": "Updated Name",
    "avatar": "new_avatar_url"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "user": {
      "name": "Updated Name",
      "email": "john@example.com",
      "avatar": "new_avatar_url"
    }
  }
  ```

### Update Password
- **PATCH** `/users/update-password`
- **Description**: Update user password
- **Body Validation**: Required
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "currentPassword": "oldpassword123",
    "newPassword": "newpassword123"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Password updated successfully"
  }
  ```

### Get All Users (Admin)
- **GET** `/users/all-users`
- **Description**: Get all users list
- **Auth**: Required (Admin only)

## Course Routes

### Get Single Course
- **GET** `/course/:course_id`
- **Description**: Get course details
- **Auth**: Not required

### Get All Courses
- **GET** `/courses`
- **Description**: Get all available courses
- **Auth**: Not required

### Get User Course
- **GET** `/users/course/:course_id`
- **Description**: Get course details for authenticated user
- **Auth**: Required

### Add Question to Course
- **PUT** `/course/add-question`
- **Description**: Add question to course
- **Body Validation**: Required
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "courseId": "course_id",
    "question": "How do I implement authentication?",
    "questionReplies": []
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Question added successfully"
  }
  ```

### Add Answer to Question
- **PUT** `/course/add-answer`
- **Description**: Add reply to course question
- **Body Validation**: Required
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "courseId": "course_id",
    "questionId": "question_id",
    "answer": "You can implement authentication using JWT..."
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Answer added successfully"
  }
  ```

### Add Course Review
- **PUT** `/course/:course_id/review`
- **Description**: Add review to course
- **Body Validation**: Required
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "rating": 5,
    "review": "Excellent course content and teaching methodology"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Review added successfully"
  }
  ```

### Reply to Review (Admin)
- **PUT** `/course/:course_id/review-reply`
- **Description**: Add reply to course review
- **Body Validation**: Required
- **Auth**: Required (Admin only)
- **Request Body Example**:
  ```json
  {
    "reviewId": "review_id",
    "reply": "Thank you for your feedback. We're glad you enjoyed the course!"
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Reply added to review successfully"
  }
  ```

### Get All Courses (Admin)
- **GET** `/all-courses`
- **Description**: Get all courses with detailed info
- **Auth**: Required (Admin only)

### Create Course (Admin)
- **POST** `/course`
- **Description**: Create new course
- **Body Validation**: Required
- **Auth**: Required (Admin only)
- **Request Body Example**:
  ```json
  {
    "name": "Complete Web Development",
    "description": "Learn web development from scratch",
    "price": 499,
    "estimatedPrice": 999,
    "thumbnail": "thumbnail_url",
    "tags": ["web development", "programming"],
    "level": "Beginner",
    "demoUrl": "demo_video_url",
    "benefits": [
      {
        "title": "Job ready skills"
      }
    ],
    "prerequisites": [
      {
        "title": "Basic computer knowledge"
      }
    ],
    "courseData": [
      {
        "title": "Introduction",
        "description": "Course overview",
        "videoUrl": "video_url",
        "videoLength": 10,
        "videoPlayer": "youtube",
        "links": [
          {
            "title": "Resources",
            "url": "resource_url"
          }
        ]
      }
    ]
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "course": {
      "name": "Complete Web Development",
      "description": "Learn web development from scratch"
    }
  }
  ```

### Update Course (Admin)
- **PATCH** `/course/:course_id`
- **Description**: Update course details
- **Body Validation**: Required
- **Auth**: Required (Admin only)
- **Request Body Example**:
  ```json
  {
    "name": "Updated Course Name",
    "price": 599,
    "description": "Updated course description",
    "courseData": [
      {
        "title": "New Module",
        "description": "New module content",
        "videoUrl": "updated_video_url",
        "videoLength": 15
      }
    ]
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Course updated successfully"
  }
  ```

### Delete Course (Admin)
- **DELETE** `/courses/:course_id`
- **Description**: Delete course
- **Auth**: Required (Admin only)

## Offline Course Routes

### Create Offline Course
- **POST** `/offline-course`
- **Description**: Create new offline course
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "name": "Advanced JavaScript Workshop",
    "description": "3-day intensive workshop",
    "price": 999,
    "location": "New York",
    "startDate": "2024-06-01",
    "endDate": "2024-06-03",
    "maxStudents": 20
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "course": {
      "name": "Advanced JavaScript Workshop",
      "description": "3-day intensive workshop",
      "price": 999,
      "location": "New York",
      "startDate": "2024-06-01",
      "endDate": "2024-06-03",
      "maxStudents": 20
    }
  }
  ```

### Update Offline Course
- **PUT** `/offline-course/:id`
- **Description**: Update offline course
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "price": 1099,
    "maxStudents": 25
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Offline course updated successfully"
  }
  ```

### Get All Offline Courses
- **GET** `/offline-course/all`
- **Description**: Get all offline courses
- **Auth**: Not required

### Get Offline Course by ID
- **GET** `/offline-course/:id`
- **Description**: Get specific offline course
- **Auth**: Not required

### Delete Offline Course
- **DELETE** `/offline-course/:id`
- **Description**: Delete offline course
- **Auth**: Required

## Order Routes

### Create Order
- **POST** `/create-order`
- **Description**: Create new order
- **Body Validation**: Required
- **Auth**: Required
- **Request Body Example**:
  ```json
  {
    "courseId": "course_id",
    "payment_info": {
      "type": "card",
      "status": "succeeded"
    }
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "order": {
      "courseId": "course_id",
      "userId": "user_id",
      "payment_info": {
        "type": "card",
        "status": "succeeded"
      }
    }
  }
  ```

### Get All Orders (Admin)
- **GET** `/all-orders`
- **Description**: Get all orders
- **Auth**: Required (Admin only)
- **Success Response**:
  ```json
  {
    "success": true,
    "orders": [
      {
        "orderId": "order_123",
        "courseId": "course_456",
        "userId": "user_789",
        "payment_info": {
          "type": "card",
          "status": "succeeded"
        },
        "createdAt": "2024-03-20T10:00:00Z",
        "amount": 499
      }
    ],
    "totalOrders": 50
  }
  ```

## Layout Routes

### Create Layout (Admin)
- **POST** `/layout`
- **Description**: Create new layout
- **Body Validation**: Required
- **Auth**: Required (Admin only)
- **Request Body Example**:
  ```json
  {
    "type": "BANNER",
    "banner": {
      "image": "banner_image_url",
      "title": "Learn to Code",
      "subTitle": "With industry experts"
    }
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "layout": {
      "type": "BANNER",
      "banner": {
        "image": "banner_image_url",
        "title": "Learn to Code",
        "subTitle": "With industry experts"
      },
      "categories": [
        {
          "title": "Programming",
          "courses": 25
        },
        {
          "title": "Web Development",
          "courses": 40
        }
      ]
    }
  }
  ```

### Get Layout (Admin)
- **GET** `/layout`
- **Description**: Get layout details
- **Auth**: Required (Admin only)

### Update Layout (Admin)
- **PATCH** `/layout/:layout_id`
- **Description**: Update layout
- **Body Validation**: Required
- **Auth**: Required (Admin only)
- **Request Body Example**:
  ```json
  {
    "type": "BANNER",
    "banner": {
      "image": "new_banner_image",
      "title": "Updated Title",
      "subTitle": "Updated Subtitle"
    }
  }
  ```
- **Success Response**:
  ```json
  {
    "success": true,
    "message": "Layout updated successfully"
  }
  ```

## Analytics Routes

### User Analytics (Admin)
- **GET** `/users-analysis`
- **Description**: Get user analytics
- **Auth**: Required (Admin only)
- **Success Response**:
  ```json
  {
    "success": true,
    "analytics": {
      "totalUsers": 1500,
      "lastMonthUsers": 150,
      "thisMonthUsers": 180,
      "userGrowthRate": 20,
      "usersByMonth": [
        {
          "month": "January",
          "count": 120
        },
        {
          "month": "February",
          "count": 150
        }
      ]
    }
  }
  ```

### Course Analytics (Admin)
- **GET** `/courses-analysis`
- **Description**: Get course analytics
- **Auth**: Required (Admin only)
- **Success Response**:
  ```json
  {
    "success": true,
    "analytics": {
      "totalCourses": 50,
      "publishedCourses": 45,
      "draftCourses": 5,
      "totalEnrollments": 2500,
      "coursesByCategory": [
        {
          "category": "Web Development",
          "count": 20
        },
        {
          "category": "Mobile Development",
          "count": 15
        }
      ]
    }
  }
  ```

### Order Analytics (Admin)
- **GET** `/orders-analysis`
- **Description**: Get order analytics
- **Auth**: Required (Admin only)
- **Success Response**:
  ```json
  {
    "success": true,
    "analytics": {
      "totalOrders": 1200,
      "totalRevenue": 59900,
      "lastMonthOrders": 150,
      "thisMonthOrders": 180,
      "ordersByMonth": [
        {
          "month": "January",
          "orders": 120,
          "revenue": 6000
        },
        {
          "month": "February",
          "orders": 150,
          "revenue": 7500
        }
      ]
    }
  }
  ```

## Notification Routes

### Get Notifications (Admin)
- **GET** `/notifications`
- **Description**: Get all notifications
- **Auth**: Required (Admin only)

### Update Notification (Admin)
- **PATCH** `/notifications/:notification_id`