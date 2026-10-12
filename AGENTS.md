## About Application
This application is a resume builder that allows users to create and customize their resumes easily with the help of AI. The application is designed to be user-friendly and intuitive, making it easy for users to create professional-looking resumes in no time.

User clones the repository and runs the application on their local machine. Then they set up with their own data and configure the integration with AI that they prefer.

## How this application should work
1. User runs the application on their local machine.
2. User sets up their own data on a structured json file (`userData.json`) and configures the integration with AI API that they prefer.
3. User can create and customize their resumes using the application, with the help of AI for suggestions and improvements.
4. User informs the AI with your own general carreer data and with the data of the job description that they want to apply for.
5. User generates a resume using the AI integration, which will analyze the user's data and the job description to create a tailored resume that highlights the user's skills and experience optimized to ATS format. 

## Architectural Decisions
- At the moment this application run on a local environment.
- Application is built using Next.js, React, Tailwind CSS, and Zod for schema validation.
- Application data is stored in the local file system of the user's machine, ensuring that the data remains private and secure.
- Backend of the application is built usind Next.js API routes, which allows for easy integration with the frontend and provides a seamless user experience.
- User data is stored in json files (`userData.json`), which allows for easy manipulation and retrieval of data.

## Development Warnings
- Always maintain README.md file up to date with the latest changes in the project and with an easy understanding documentation.
- Because this application has IA integration, it is importante that all data in API routes is validated using Zod to ensure that the data is in the correct format and meets the required criteria.
- Is very important maintain a very large test covarage to ensure that the application is working as expected and to catch any potential bugs or issues before they become a problem. Remember that the application has IA integration and IA is a non deterministic system, so it is important to have a robust testing strategy in place to ensure that the application is working as expected.

## API Routes
defing the API routes for the application, which will handle the backend logic and data manipulation. The API routes will be built using Next.js API routes and will be responsible for handling requests from the frontend and returning the appropriate responses. 

Below is a list of the API routes that will be implemented in the application with a brief description of their functionality:

```
```

## First Steps to development
see the [implementation plan](docs/IMPLEMENTATION_PLAN.md) for the proposed architecture, data schemas, API routes, delivery phases, and testing strategy.

<!-- BEGIN:nextjs-agent-rules -->

## This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->
