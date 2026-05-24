# Methodology

This project uses an iterative development method. I planned, designed, built, tested and improved the Loyal Cafe Rewards PWA in stages instead of trying to complete the whole application at once.

## Stage 1: Investigate the Problem

I began by identifying the original problem with traditional coffee loyalty cards. Physical cards can be lost, forgotten, damaged or manipulated, and they do not give the business useful customer data. This stage helped define the purpose of the project.

## Stage 2: Plan the Solution

The proposed solution is a PWA loyalty card that stores the customer's progress digitally. During this stage I planned the main features, including sign-up, login, dashboard, reward tracking, transaction history and staff/admin management.

## Stage 3: Design the Application

The design stage includes:

- Storyboards for the user journey.
- Data flow diagrams to show how information moves through the system.
- Input-process-output charts for key functions.
- Entity relationship diagrams and data dictionaries for database planning.
- Class diagrams to show the planned application objects.

## Stage 4: Implement the Application

Implementation is being completed in small sections in the Flask application repository. Each section should be committed to GitHub with a meaningful message, such as:

- `Add initial project proposal`
- `Create storyboard for Cafe Card user flow`
- `Add database design for loyalty rewards`
- `Implement secure sign-up and login`
- `Add dashboard reward progress`
- `Add staff customer management`
- `Add PWA service worker and offline page`
- `Document testing evidence`

Regular commits make it easier to prove the development process and return to earlier versions if a problem appears.

## Stage 5: Test and Evaluate

Testing checks whether each main feature works as expected. I recorded test cases, expected results, actual results and fixes for signup, login, role protection, rewards, history and PWA behaviour. Reflection entries explain what went well, what was difficult and what I would improve in the future.
