---
title: Visualize The Code
---
classDiagram
    class UserController {
        <<Class>>
        -ICreateUserService _createUserService 
        +UserController (CreateUserService createUserService)
        +Create(string email, string username) User
    }

    class CreateUserRequest {
        <<Class>>
        +string Email
        +string Username

        +Validate() bool
    }

    class CreateUserService {
        <<Class>>
        -UserModel _userModel
        -SendWelcomeEmailService _sendWelcomeEmailService
        -Kafka _kafka
        +CreateUserService(UserModel um, SendWelcomeEmailService es, Kafka k)
        +Call(CreateUserRequest createUserRequest) User
        -CheckActiveUsers(List-User> users) bool
    }

    class UserModel {
        <<Class>>
        +FindUsersByEmail(string email) List-User>
        +CreateUser(string email, string username) User
    }

    class User {
        <<Class>>
        +int UserId
        +string Username
        +string Email
    }

    class SendWelcomeEmailService {
        <<Class>>
        +Call(User user) bool
    }

    class Kafka {
        <<Class>>
        +PublishUserCreatedEvent(User user) bool
    }

    class ICreateUserService {
        <<Interface>>
        +Call(CreateUserRequest createUserRequest)
    }

    UserController ..> CreateUserRequest: depends on
    UserController ..> ICreateUserService: depends on
    CreateUserService ..|> ICreateUserService: Implements
    CreateUserService ..> UserModel: depends on
    UserModel ..> User: depends on
    CreateUserService ..> SendWelcomeEmailService: depends on
    CreateUserService ..> Kafka: depends on
