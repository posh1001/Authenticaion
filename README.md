# Authenticaion
## 1. Set Up NestJS Project
- First, create a new NestJS project if you haven't already:

$ nest new project-name
$ cd project-name

## 2. Install Required Packages
- Install necessary packages like nestjs/passport, @nestjs/jwt, and passport-jwt for JWT-based authentication, and typeorm for database interactions:

- npm install @nestjs/passport @nestjs/jwt passport passport-jwt typeorm
- npm install @types/passport-jwt --save-dev

## 3. Set Up TypeORM
- Set up TypeORM to connect to your database. Configure the connection in ormconfig.json or directly in app.module.ts using TypeOrmModule.forRoot().

## 4. Create User Entity
- Create a User entity using TypeORM. For example:

user.entity.ts
- import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

- @Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

- @Column()
  username: string;

-  @Column()
  password: string;
}

## 5. Implement Authentication Service
- Create an authentication service that will handle login and registration logic. This service will interact with your User entity and handle password hashing.

## 6. Implement JWT Strategy
- Create a JWT strategy using Passport and passport-jwt to authenticate requests with JWT tokens. Define a strategy that validates the token and retrieves user information from the database.

## 7. Create Auth Module
- Create an authentication module (auth.module.ts) where you import PassportModule, JwtModule, and your authentication service.

## 8. Guard Routes
- Create guards (AuthGuard, JwtAuthGuard) to protect routes that require authentication. For example:

import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';

@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}

## 9. Implement Controllers
- Implement controllers (auth.controller.ts, users.controller.ts) to handle login, registration, and other user-related operations.

## 10. Protect Routes
- Protect your routes by applying guards (@UseGuards(JwtAuthGuard)) to controllers or specific routes where authentication is required.
